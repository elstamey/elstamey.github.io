title: Hey Boss, Event Sourcing Can Fix That!
author:
  name: Emily Stamey
  twitter: elstamey
  url: http://elstamey.com
theme: elstamey/reveal-cleaver-theme
style: basic-style.css
output: hey_boss.html
controls: true

--

# Event Sourcing Can Fix That!

--

![Me](img/me.png)

--

![family](img/family.png)

--

# Scholarships

- replaced in pieces
- added DDD & ES & CQRS beside complex framework spaghetti
- separation of concerns
- cleaner history and reports of what had been done

--

## code structure to replace in pieces

How did we add new, modern code within the framework?  What did we use?

--

# Student Enrollment Process

- rewrote
- ES to follow the process
- status drop-down versus events

--

# Session Threats Report

- multiple daemons running parts of code and the UI consumes the results of the analysis
  - complex DB queries
  - reports are slow to generate on-demand




--

## What we'll cover:

- What does an Event look like?
- The Event Store
- How do we create events?
- We have events, now what?
- A short example of how it could work

--

## What Does an Event Look Like?

- An Event is a Class named for the thing that happened
- The event contains attributes that are relevant to that event

--

## Event: SessionDiscovered

- after validation to determine whether we have a valid session, we log a new event

### new SessionDiscovered( attributes we need to know )

--

## Event: SessionDiscovered

- session id
- start time
- protocol
- source ip
- destination ip
- source port
- destination port 

--

## Event: SessionScored

- session id
- threat contributor
- score

--

## Event: FileScored

- after validation that a file has matched a signature, we log a new event

### new FileScored( attributes we need to know )

--

## Event: FileScored

- file id
- session id
- integration
- score
- signature that found it

--

## Event: FileRescored

- after validation that a file has matched a signature and that it has been scored before\n- we log a new event

### new FileRescored( attributes we need to know )

--

## Event: FileRescored

- file id
- session id
- integration
- new score
- signature that found it 

--

## Event Store holds *all* events

- a DB with each row being a Domain Message
- Each Event is the payload of the Domain Message
- The Domain Message has a uuid, timestamp, type, payload (the event itself), and version (if needed)
- this means we can store all events in the same place regardless of the program that logs the event or handles them

--

## Listeners

- we write listeners for each of the events we care about in a given context
- the listeners view the whole event store but cull the events by their type
- the types of structures that have listeners are projections and aggregate roots 

--

## Projector

- a class 
- its apply methods contain the logic of what an event means
- writes information to the table that we will need later

--

![Projectors](../img/status_change/projector.png)

--

## Projection: Session

- listens for SessionDiscovered events
  - creates a new row in a table with the session details and a null score
- listens for SessionScored events
  - finds the session in the table and updates the score and score contributor

-- 

## Projection: Report for Top Threats by Hash

- listens for FileScored and FileRescored Events
  - looks up details of file by the file id
  - adds a row to table with 
    - file id
    - file md5 hash
    - the filename
    - file type
    - the score
    - signature that scored it
    - source ip
    - destination ip
    - protocol

--

## Read Model

- a class
- it contains methods for looking up information from the projection
- ex: look up the history for a certain file, all of its scores

--

## Read Model: Top Threats

methods: 

- top 10 threats by the file hash
  - this excludes hits I'm not allowed to see by the signature that did the scoring
  - gets a current hit count of only the records I can see

- top threats by file type
- top threats by source/destination ip pairs
- top threats by protocol

--

## Good Stuff!

- works well in our environment where we have multiple applications doing different things
- full audit log of what has happened in our environment
- the results of those events can be optimized for read to shorten the time to retrieve data
- separate the logic of what an event means based on context and purpose
- only display results that a user is allowed to see
- flexible to change, our interpretation of events can change, and we can rebuild projections without losing the full history
