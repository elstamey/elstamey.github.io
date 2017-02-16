title: Status Change Now Using Event Sourcing
author:
  name: Emily Stamey
  twitter: elstamey
  url: http://elstamey.com
theme: sudoki/reveal-cleaver-theme
style: basic-style.css
output: index.html
controls: true

--

# Status Change: 
## Now Using Event Sourcing

--

Definition Event Sourcing

The fundamental idea of Event Sourcing is that of ensuring **every change to the state** of an application **is captured in an event object**, and that these event objects are themselves stored in the sequence they were applied for the same lifetime as the application state itself.

- Martin Fowler

--

## What's important about Events

- Events
- Details of the Event (attributes)
- Order/Sequence


--

## Forms

A lot of our systems are built to facilitate or replace paper processes

They often closely map to this physical form.

![Paper form](https://c1.staticflickr.com/8/7091/6988157282_e62624f274_b.jpg)

--

## Status

When we stick to this idea, we find ourselves using status flags on an object 
to tell where in the process we are.

But these states carry assumed knowledge of the process without clearly saying what happened.

Status meaning or names can change over time without conveying process changes

--

## Paper Forms in a process

![Paper forms sorted for a process](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6f/Copies_of_documents_at_European_Parliament_in_Strasbourg.jpg/1024px-Copies_of_documents_at_European_Parliament_in_Strasbourg.jpg)



--

### Something happened

In a workflow, usually something happens and then your object's status is
updated to reflect that something happened.

Similar to a stamp on your form or sorting the form into a pile 

--
 
![stamped application](http://previews.123rf.com/images/kabby/kabby0711/kabby071100002/2079196-A-crumpled-up-home-loan-application-stamped-with-the-word-Stock-Photo.jpg)
 
--

But that stamp doesn't indicate why or communicate to the applicant what happened

When our Online Student Registration Request is denied, sometimes the student has 
to do something to resolve the issue.  After the hold is fixed, their request can proceed.  It can even be approved.

--

As our software becomes aware of these events, we can adapt, flex, or
reorient.  

Instead of putting the form in the trash, we can reconsider it.

Instead of reviewing the pile of HOLD forms and manually checking the student's record, we
can register the event that a hold is lifted.

That event that a hold is lifted can trigger the request to be reviewed 
by an administrator.


--

Workflows

--

How workflows become complex

-- code

Sometimes your workflow forks in multiple directions or involved long 
lists to capture the complexity of the business process


<B>Change to Status:</B>
<select name="newStatus">
    <option value="RECEIVED">RECEIVED</option>
    <option value="CANCELLED">CANCELLED</option>
    <option value="COURSE CANCELLED">COURSE CANCELLED</option>
    <option value="COURSE NOT APPROVED">COURSE NOT APPROVED</option>
    <option value="CPC DENIED">CPC DENIED</option>
    <option value="CPC NOT APPROVED">CPC NOT APPROVED</option>
    <option value="CPC PENDING TRANSCRIPT">CPC PENDING TRANSCRIPT</option>
    <option value="CPC PROCESSING">CPC PROCESSING*</option>
    <option value="DENIED">DENIED</option>
    <option value="DROPPED AFTER CENSUS">DROPPED AFTER CENSUS*</option>
    <option value="DROPPED BEFORE CLASSES BEGUN">DROPPED BEFORE CLASSES BEGUN*</option>
    <option value="DROPPED BETWEEN BEGINNING OF CLASS AND CENSUS DATE">DROPPED BETWEEN BEGINNING OF CLASS AND CENSUS DATE*</option>
    <option value="DROPS/WITHDRAWALS AT SITES">DROPS/WITHDRAWALS AT SITES*</option>
    <option value="ECE ON CAMPUS STUDENTS">ECE ON CAMPUS STUDENTS</option>
    <option value="ENROLLMENT CANCELLED">ENROLLMENT CANCELLED</option>
    <option value="EOL APPROVED">EOL APPROVED*</option>
    <option value="EOL MISC">EOL MISC*</option>
    <option value="NEW STUDENT REGISTRATION">NEW STUDENT REGISTRATION</option>
    <option value="PENDING ON CAMPUS REQUEST">PENDING ON CAMPUS REQUEST</option>
    <option value="ON CAMPUS STUDENT NOT APPROVED">ON CAMPUS STUDENT NOT APPROVED</option>
    <option value="PENDING CASHIER HOLD">PENDING CASHIER HOLD</option>
    <option value="PENDING EOL APPROVAL">PENDING EOL APPROVAL*</option>
    <option value="PENDING INSTRUCTOR APPROVAL">PENDING INSTRUCTOR APPROVAL</option>
    <option value="PENDING INTERNATIONAL STUDENT">PENDING INTERNATIONAL STUDENT</option>
    <option value="PENDING NDS OPEN ENROLLMENT">PENDING NDS OPEN ENROLLMENT</option>
    <option value="PENDING OIS VISA STUDENT">PENDING OIS VISA STUDENT</option>
    <option value="PENDING PERMANENT RESIDENT">PENDING PERMANENT RESIDENT</option>
    <option value="PENDING TERM ADVISEMENT HOLD">PENDING TERM ADVISEMENT HOLD</option>
    <option value="PENDING TRANSCRIPT">PENDING TRANSCRIPT</option>
    <option value="PENDING TUITION PREPAYMENT">PENDING TUITION PREPAYMENT</option>
    <option value="PREAPPROVED RETURNING">PREAPPROVED RETURNING</option>
    <option value="PROCESSING NDS">PROCESSING NDS*</option>
    <option value="PROCESSING SITE">PROCESSING SITE*</option>
    <option value="PROCESSING Z">PROCESSING Z*</option>
    <option value="PROJECT MESSAGE - MAE 586">PROJECT MESSAGE - MAE 586</option>
    <option value="PROJECT MESSAGE - NE 693">PROJECT MESSAGE - NE 693</option>
    <option value="REGISTERED">REGISTERED</option>
    <option value="REGISTERED ASHEVILLE">REGISTERED ASHEVILLE</option>
    <option value="REGISTERED HAVELOCK">REGISTERED HAVELOCK</option>
    <option value="REGISTERED WILMINGTON">REGISTERED WILMINGTON</option>
    <option value="SITE APPROVAL: ASHEVILLE">SITE APPROVAL: ASHEVILLE*</option>
    <option value="SITE APPROVAL: HAVELOCK">SITE APPROVAL: HAVELOCK*</option>
    <option value="SITE APPROVAL: WILMINGTON">SITE APPROVAL: WILMINGTON*</option>
    <option value="SITE NOT APPROVED">SITE NOT APPROVED</option>
    <option value="SWAPPED OUT">SWAPPED OUT</option>
    <option value="TRANSCRIPT APPROVED">TRANSCRIPT APPROVED*</option>
    <option value="WITHDRAWN">WITHDRAWN*</option>
</select>
      

--


###Event Sourcing 

ensures that every change to the state of an application is captured in an event object, and that these event objects are themselves stored in the sequence they were applied for the same lifetime as the application state itself.



--

Events are usually named as past-tense verbs

Should store values, never an aggregate root or model/collection/object 

--

### Events vs. Status

The fact that an event happened in your system in the past doesn't ever 
change even though the behavior around what that event  

--



--



Event can be wrapped by Domain message

This contains a version, timestamp, id, and the event itself



--

Event Store

Event Store is a domain specific database for people who use the Event Sourcing pattern in their apps. It is a functional database which based on a publish-subscribe messages pattern.



--



--

### A textual example

Content can be written in **Markdown!** New lines no longer need two angle brackets.

This will be in a separate paragraph

--

### Links for further reading

* [Greg Young CQRS and Event Sourcing](https://www.youtube.com/watch?v=JHGkaShoyNs)
* [Greg Young - long class](https://www.youtube.com/watch?v=whCk1Q87_ZI)
* [Greg Young - A Decade of DDD, CQRS, Event Sourcing](https://www.youtube.com/watch?v=LDW0QWie21s)
