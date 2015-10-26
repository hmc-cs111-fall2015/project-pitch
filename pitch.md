# Shared Spaces

## Overview
_What's this project about, briefly?_

This project serves a group of people who share a set of spaces and need to use the spaces at various times. Examples include kitchens, lab spaces, and study room. This language would ideally be good for any user to reserve a space or designate the space as 'occupied'.

## The user and a language
This section describes who the project would serve and why a language might be a
good way to meet their needs.

### What's the need?
_What need is met by your idea? Who are you helping? What is that person's experience like now? What would their experience be like if you could help them?_

Shared spaces are often managed by some form of scheduler but the interfaces we use for them are nonintuitive and rather poor. This could help anyone who shares a resource with others, such as MuddVans, conference rooms, and study rooms. One example is a HMC student trying to reserve the Green Room. The student has to submit reservation details before being able to see the schedule. Then, they can only see 12 hours intervals of the schedule and cannot alter their original reservation without creating an entirely new query. This makes deciding on dates and times for meetings more difficult than it should be. If I could help them, the user would be able to query schedules in different ways (e.g. "Show me the schedule on November 28th for rooms that can hold 20 people"; "Reserve the Green room from 8PM to 9PM on November 28th"). There would also be ways to describe a new space that can also be reserved ("New Blue Room in Platt").

### Why a language?
_Why is a DSL appropriate for your user(s)? How does it address the need?_

I think that similar to SQL, this task is better suited as a query system. Although, the most intuitive reservation system may be a visual, a query system can be the internal DSL for a future GUI project. For calendar users, it will provide a smoother experience than the one currently found on EMS.


### Why you?
_What excites you about this idea? How did you come up with it?_

When I try to organize events, it is fairly frustrating to check multiple dates and times or try to do multiple reservations. When I was trying to reserve a MuddVan, I came up with the idea to try something similar and it also aligned with my proposal in free-1.

### Interface (syntax)
_How might the user interact with the language? What does programming look 
like? Why is this the right way to interact with the problem domain? Be careful
to distinguish between, e.g,. a graphical interface and a linguistic interface._ 

The user would be able to do three basic tasks.
* Create spaces that can be reserved
* Reserve spaces for periods of times
* Query for space availability

The user interacts through text queries. The programming will look similar to other query languages like SQL. 

* Create spaces

This would ideally return a confirmation or an error.

"""
CREATE ROOM "Blue Room" IN "Platt"
"""

* Reserve spaces

This would ideally return either a confirmation or an error.

"""
RESERVE ROOM "Blue Room" FROM "1600" TO "2030" ON "11/28/2015"
"""

* Query for availability

This would ideally return a list of reservations on that day, or a list of available times.

"""
CHECK ROOMS IN "Platt" ON "11/28/2015"
"""

### Operation (semantics)
_What might happen when a program runs? How does a program interact with the
user? What kinds of semantic (i.e., non-syntax) errors might occur, and how 
might they be communicated to the user?_

When a query is made, the program parses the query and then returns the appropriate data. It may use a database service like Parse to handle holding information. The data can also be stored locally.

Some errors include querying for names that don't appear. Ideally, the query would return some suggestions but it can also just respond with an error. Another error is that multiple users may attempt to book at the same time, in this case the program should choose one user to give precedence to.

### Expressiveness
_What should be easy to do in this language? What should be possible, but
difficult? What should be impossible or very difficult?_

It should be very easy to create new spaces, reserve spaces, and check the schedule. It should be possible but difficult to write a series of queries that checks which rooms are empty and then books the rooms at the desired time. (On second thought this might be an interesting addition to the language). It should be impossible to do programs such as "hello world" or recursion.

### Related work
_Are there any other DSLs in this domain? If not, describe how you know there
aren't and conjecture why not. If so, describe them and provide links. How well 
do they address the need? Are there any particularly admirable qualities of the
language? Are there parts of the language you think could be improved?_

Yes, the exising Event Management System on campus handles space reservations for us now.
[HMC EMS](https://emsweb.claremont.edu/HMC/)
Also, some use Google Calendar, and doodle poll as their reservation system.

The EMS system is _functional_ but is clunky and difficult to figure out when spaces are actually open. EMS expects your event to already have a set date, so it is easier to find spaces given a time. However, if the date is undetermined, it is harder to decide which would be ideal given the space situation for different dates. 

## The Project
This section examines whether the idea makes for a good CS 111 project.


### Suitability
_What percentage of your time do you think will be spent directly engaging in
the **language** aspects of this project (e.g., making language design
decisions), as opposed to "systems" aspects of the project (e.g., implementing a
complicated semantics that doesn't require a lot of language design)?_

About 60% of the time will be spent thinking about the langauge aspects. There are keywords and syntax that need to be decided, though the implementation of each of the language features should not be _too_ complex. A large part of the time will be spend building out the right mechanisms to ensure that user queries are parsed appropriately. (And that user queries are intuitive to read and write!)

### Scope
_How big an idea is this? How ambitious is this project?_

This project is a small idea (at least for an MVP). The project can easily grow further by creating more ways to let users write in new spaces (like defining different types of spaces in their program).

### Challenges and opportunities
_Why is this a good project? What are some challenges you expect to face? How
might you overcome them? What are some warning signs that the project has gotten
off track, and how will you get the project back on track if needed?_

I think this will be a good project because it is solving a problem I am dealing with on a weekly basis. I expect that the hardest part of this project is creating an intuitive grammar. I presented an example grammar under the syntax question, but I think there is much to improve on.

