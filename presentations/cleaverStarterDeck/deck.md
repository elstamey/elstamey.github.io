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

The fundamental idea of Event Sourcing is that of ensuring every change to the state of an application is captured in an event object, and that these event objects are themselves stored in the sequence they were applied for the same lifetime as the application state itself.

- Martin Fowler

--

## Forms

A lot of our applications are built to facilitate or replace paper processes

When we stick to this idea, we find ourselves using status flags on an object 
to tell where in the process we are.

But these states can carry knowledge of the process without clearly saying what happened.

Status meaning or names can change over time without conveying process changes

--

### Something happened

In a workflow, usually something happens and then your object's status is
updated to reflect that something happened.

Similar to a stamp on your form

--
 
![stamped application](http://previews.123rf.com/images/kabby/kabby0711/kabby071100002/2079196-A-crumpled-up-home-loan-application-stamped-with-the-word-Stock-Photo.jpg)
 
--

But that stamp doesn't indicate why or communicate to the applicant what happened

When our Online Student Registration Request is denied, sometimes the student has 
to do something to resolve the issue.  After the hold is fixed, their request can proceed.  It can even be approved.

--

As our applications become aware of these events, we can adapt, flex, or
reorient.  

Instead of putting the application in the trash, we can reconsider it.

Instead of looking in the denied pile and manually checking the student's record, we
can register the event that a hold is lifted.

That event can trigger the request to be reviewed by an administrator again.


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




--

Events are usually named as past-tense verbs

Should store values, never an aggregate root or model/collection/object 

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

### A list of things

* Item 1
* Item B
* Item gamma

No need for multiple templates!
