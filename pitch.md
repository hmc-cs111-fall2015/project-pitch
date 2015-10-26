# ComplexCalendar

## Overview
_What's this project about, briefly?_

This project is about making complex calendar's easy to make. For any calendar
software it is easy to make specific events but for most people, their life
heavily revolves around a core calendar that repeats and doesn't change often.
I want to make it easier for users to define their complex calendars in fewer
words. 

## The user and a language
This section describes who the project would serve and why a language might be a
good way to meet their needs.

The user for this project would be someone that has a highly structured calendar
that is too complex to easily define with a simple repeat item button. An example
of one user would be a college student. Their calendar for classes only applies 
when school is in session. It would be much easier for the student to define a 
school section of their calendar and mark the dates of the school year to apply
it. This would eliminate their need to go months forward in the calendar to set 
up new repeated events that were already set up for other times. 

While a UI would probably be the final product of this project, it would be 
nicely represented with a backend language. An expressive language allows
for small changes to have large effects. If a user's calendar is always 
recorded in the language instead of chunked time-slots, making a small change
to the initial design of the calendar would just require a small change in the
language, not having to go event by event to make that small change. 

### What's the need?
_What need is met by your idea? Who are you helping? What is that person's
experience like now? What would their experience be like if you could help 
them?_

The need that is met by my idea is the need for complex calendar design. Current
calendar software makes it too hard and work intensive to automate large 
and complex calendars for most users. Their current experience depends on the 
calendar software they use but most have options to repeat events over a span
of time. If they want multiple spans of time, then they have to create multiple
events. If multiple events have the same span of time, there aren't easy ways
to group those together. So changing all time spans that are the same at the same
time is impossible, they all have to be changed separately. 

Their experience using my project would improve the expressiveness of what
calendars are able to understand. They would be able to group events together
under the same span of time, make them easily repeat, make it easy for certain 
events to have exceptions at certain times and much more. It just allows users
to create calendars the same way they have a calendar arranged in their head, by
groups. 

### Why a language?
_Why is a DSL appropriate for your user(s)? How does it address the need?_

DSLs aim to improve expressiveness over a domain. So since I feel like the domain
of calendar creation and editing has been stagnant for quite a while, a DSL that
aims to improve the ease of making and editing one seems to fit quite well. 

Most of the time spent on a calendar is in it's creation. Basically when you are
adding a set of events that all go together. Imagine you just set up your next 
semester's schedule for classes, they will all have the same time span of existance,
so making a new time-section of the calendar with each class being a different 
repeated events makes intuitive sense. After filling in the dates of breaks and each
classes time slot, not much needs to be changed until you get your homework schedule.

Instead of having to redo these restrictions of the school year calendar, you can just
add a new section to your current school year calendar that is just homework. It doesn't
require repetition or much manual input. By having this calendar designer be a DSL,
it becomes much easier to make drastic changes with less effort. 

### Why you?
_What excites you about this idea? How did you come up with it?_

I have never really used a digital calendar because of the limitations I have listed above.
I haven't ever had enough of a static lifestyle that current calendars available to me 
have allowed me to easily organize my life. If it takes a lot of effort to create and 
edit something that is supposed to remove effort from your life, is it really completing 
its task?

The other thing that excites me about this project is the same thing that I mentioned 
above. The calendar market is so saturated at this point that it would seem ridiculous
to even compete. But if you look closely, nothing has really changed that much in the 
last few years except for facebook event integration. I find it interesting to try and
find new innovation in this stagnant and over saturated market. 

### Interface (syntax)
_How might the user interact with the language? What does programming look 
like? Why is this the right way to interact with the problem domain? Be careful
to distinguish between, e.g,. a graphical interface and a linguistic interface._ 

As mentioned above, in a perfect scenario the user would interact with their calendar
in the most intuitive way for them. If thats with a UI, they should be able to easily
create and edit the DSL with one. If they prefer typing, then the language should be
comprehensible enough for humans to create and understand. Allowing user's access
to the raw DSL also allows for the easy possibility of creating templates. Since
everyone at a school generally has the same school year dates, with the same times
for finals and other things, it would be able to save that as a file and send it to 
others. Another plus for being able to send scheduels around is for members of the 
same teams at their jobs and people taking almost the exact same classes (core). 

First, a text based language will be the focus but if time permits a GUI will be
looked into. 

For the text based language, the verbs and nouns should be similar to how current
calendar programs are designed. I want it to be easy for the user to use and
understand the language whether it be the first or hundreths time they look at it. 

I want a calendar to be sectioned off, so that different events can be grouped 
together. Sections can have an endless number of sub-sections which each 
sub-section following all of the rules of its parent. Each section also has rules
which are very important. Rules can denote times that the events in the group
are active and times that they are inactive. 

The other main part to the language are of course events. Events have times of the
day and week they are active. These are denoted with rules also. Rules go even
deeper for events though as they allow for repetition, importance levels
and even being conditional on other events occuring at the same time or on the 
same day. 

This all culminates in a tree like system with each terminal node being an 
event and each branching node being a section. 


### Operation (semantics)
_What might happen when a program runs? How does a program interact with the
user? What kinds of semantic (i.e., non-syntax) errors might occur, and how 
might they be communicated to the user?_

This will describe the text based language. Since the possible UI extension 
would just be a visual representation of the text based language, its 
semantics should be basically the same. 

When the program runs, it will take in the file containing the DSL and evauate
it. It will return a static calendar for now, even though allowing dynamic 
changes in an online system could be a stretch goal. It will compute all of 
the sections, events and rules and return a calendar that follows all of them
over a given time span. One obvious error is events that occur at the same
time. For now, I am thinking that it will allow it, showing them just as
overlapping. Maybe later I will realize that we will need to make the user
choose though. That will be decided after user testing. 

The end result of the program should easily be importable by google calendar and
other large calendars, so it will output an icalendar file. 

### Expressiveness
_What should be easy to do in this language? What should be possible, but
difficult? What should be impossible or very difficult?_

It should be easy to make and edit complex but largely repititious calendars 
using this language. It should be possible to make a calendar full of one-off
events but the effort to do that wouldn't necessarily be worth it for the user.
I want it so users only go back to the language to change something when something 
significant in their schedule has changed, and for it to be easy to make 
adjustments to implement that change. I can't think of much that would be 
impossible in this language that is calendar specific. I guess for now it would 
be impossible to easily visualize their text files for the DSL like most calendars
easily show you. 

### Related work
_Are there any other DSLs in this domain? If not, describe how you know there
aren't and conjecture why not. If so, describe them and provide links. How well 
do they address the need? Are there any particularly admirable qualities of the
language? Are there parts of the language you think could be improved?_

The only DSL I could find for caldendars was just an example talked about in a 
DSLs book. Link: https://books.google.com/books?id=7q53NhGHa3MC&pg=PA67&lpg=PA67&dq=calendar+dsl&source=bl&ots=v3Hm5QS6LW&sig=fn2ujHcbLl__JYUWRoFFVLaOduo&hl=en&sa=X&ved=0CE8Q6AEwCGoVChMI0NrFgq7fyAIVCsxjCh0hUgJN#v=onepage&q=calendar%20dsl&f=false

The DSL described in the book is very simple and deals with single events rather
than focusing on reoccuring events. 

## The Project
This section examines whether the idea makes for a good CS 111 project.

I think this would make a great CS 111 project because I think it leads itself 
well to icremental or iterative design. It would be easy to maintain a working
language while adding additional features to it. This means that since we can't 
really know what will be easy or hard about the project, almost any ammount I 
can accomplish after the initial barebones design would result in a fully 
functioning DSL. The farther I get just means it will have more features 
included. I think it would also be easy for the other members of the class 
to give input on this project since they are part of the key demographic. 

### Suitability
_What percentage of your time do you think will be spent directly engaging in
the **language** aspects of this project (e.g., making language design
decisions), as opposed to "systems" aspects of the project (e.g., implementing a
complicated semantics that doesn't require a lot of language design)?_

So I think it will be around 50/50 right now. If it was easy to allow users to 
do these complex calendar designs then other calendar creation tools would
have implemented them by now. It won't be easy to allow them a lot of creativity
with their design without making it also harder to intially understand. 

On the other hand, the output of the program won't be easy either. While it is 
static, I have to compute reptitious events that might overlap with one another
and return it in a general calendar file format. 


### Scope
_How big an idea is this? How ambitious is this project?_

I think this idea is great for scale. It's initial idea of just having repeating 
events over a sectioned time scale seems very simple but adding additional rules
will make the project more complex. The project can become very ambitious but if 
I remain very iterative adding feature after completed feature, I can't really
see the project becoming too ambitious to complete.

The idea of creating a UI for the DSL is most likely too ambitious for the 
project though. 

### Challenges and opportunities
_Why is this a good project? What are some challenges you expect to face? How
might you overcome them? What are some warning signs that the project has gotten
off track, and how will you get the project back on track if needed?_

I think this is a good project because even though it is confined to the small
domain of calendars, the hopeful expressiveness of the language allows for a
lot of creativity in how the language is defined. I think the biggest challenge
will be taking in uses that users want the langauge to achieve and translating
those into actual language features that are intuitive. I think a warning sign
that the project is off track is having calendar files that have so many 
different verbs and nouns that it becomes almost impossible to understand what
each part of the code is doing without referencing the creator. If this happens,
iterative design will allow me to just restrict the scale back down to when 
the language was much more comprehensible, alieviating the problem.

