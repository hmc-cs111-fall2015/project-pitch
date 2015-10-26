# Robot Logic

## Overview
_What's this project about, briefly?_

This project is about providing a simpler way of programming robots. It will
essentially provide ways to have a more complete separation between the logic of
the robot and its specific implementation details, and be able to specify logic
more clearly and succinctly.

## The user and a language
This section describes who the project would serve and why a language might be a
good way to meet their needs.


### What's the need?
_What need is met by your idea? Who are you helping? What is that person's
experience like now? What would their experience be like if you could help 
them?_

Often when writing robot code, quite a bit of work needs to go into writing the
boiler plate for a state machine or interrupts or whatever structure is needed
to get the actual logic implemented. It would be really nice for both
inexperienced robot developers and people trying to write robot code quickly to
be able to just specify the logic, and let someone else take care of the boiler
plate.

I've observed freshmen in E11 (autonomous vehicles) trying to write C++ for
their robots. They neither know C++ very well nor have a great idea about how to
write good robot code. A DSL can help solve both of these issues. The syntax
could be somewhat nicer than C++'s (not a hard task), and the language can help
steer programmers into using good design constructs by making them easy. In the
C++ that E11 students are using, it's very easy to make a busy loop to wait for
a certain amount of time and much more difficult to set up a state machine that
will let their robot actually succeed. If they got to use this DSL, writing such
a busy loop would be very difficult and the state machine would be simple,
shoehorning students into using good robot design practices.

### Why a language?
_Why is a DSL appropriate for your user(s)? How does it address the need?_

A DSL is appropriate because the programmer wants to just specify logic,
something programming languages are very good at. An internal DSL is probably
appropriate so that calling out to the back-end functions is easy and users
aren't constrained in any way by the language. An external DSL may also work,
but in this case it might even compile to something like C++ because I want the
language to be fast and very low overhead so that it can be run on many
different systems (especially arduino).

### Why you?
_What excites you about this idea? How did you come up with it?_

This idea is really exciting to me. I have written such boiler plate several
times and while it does make me feel like a HaXXor (to use Prof. O'Neil's
phrasing) it's not the best use of my time, and it would be great if people who
were good at logic but not so much at low-level programming could program
awesome robots.

### Interface (syntax)
_How might the user interact with the language? What does programming look 
like? Why is this the right way to interact with the problem domain? Be careful
to distinguish between, e.g,. a graphical interface and a linguistic interface._ 

The syntax will be text-based and will look a lot like a standard GPL such as
C++ or python. This is the right way because very complex logic might need to be
implemented and writing a good graphical interface for something like this is
extremely difficult. This language isn't trying to be super new-programmer
friendly, it's just trying to make it easier for people to get to specifying
their logic. This does end up making it easier to use in general, but that's
more of a side effect than a primary design goal. Making a graphical interface
would likely make it easier to use by new programmers but would make it harder
to use by advanced programmers.

### Operation (semantics)
_What might happen when a program runs? How does a program interact with the
user? What kinds of semantic (i.e., non-syntax) errors might occur, and how 
might they be communicated to the user?_

When a program is run, it will make the robot execute the actions specified.
Semantic errors happen when the robot simply does the wrong ting, and the
programmer just observes the robot's behavior to determine this.

### Expressiveness
_What should be easy to do in this language? What should be possible, but
difficult? What should be impossible or very difficult?_

It should be easy to do most things involving robot logic. This includes any
sort of state machine the programmer wants, interrupts and exceptions, and a way
to actually move the robot. The robot movements, however, should be pretty
general, calling out to an API written in another language to actually do the
specific setting of output pins and such. It should be difficult or at least
discouraged to do very low-level things in this language. It should also be
difficult to do things that are generally bad for robots, such as busy waits and
other non-real-time operations. It should also be difficult or impossible do
things that relate to non-robot applications. Some exceptions may be made for
operations such as simulating the behavior of a robot.

### Related work
_Are there any other DSLs in this domain? If not, describe how you know there
aren't and conjecture why not. If so, describe them and provide links. How well 
do they address the need? Are there any particularly admirable qualities of the
language? Are there parts of the language you think could be improved?_

There have been a large number of languages that attempt to do similar things. A
lot are listed on the [https://en.wikipedia.org/wiki/Robot_software](Robot
Software Wikipedia Page). Of those, I only have experience with a few. Some of
the LEGO mindstorms languages do things such as having really easy concurrency
that let you write things like delays while still being able to respond in other
parts of the code. They are not so good, however, in that they are graphical and
thus harder to use for larger programs. They also only target one platform. ROS,
the Robot Operating System, is general-purpose but doesn't really address the
same needs my project does: ROS basically provides a way to pass messages
between programs rather than allowing a single program to have good logic
constructs. ROS is nice in that it allows good concurrency via multiple
processes, but if you want to have a state machine you still have to set it up
yourself.

## The Project
This section examines whether the idea makes for a good CS 111 project.


### Suitability
_What percentage of your time do you think will be spent directly engaging in
the **language** aspects of this project (e.g., making language design
decisions), as opposed to "systems" aspects of the project (e.g., implementing a
complicated semantics that doesn't require a lot of language design)?_

This project is pretty large. I feel like there is a huge amount of work to be
done in language design. Figuring out how to integrate lots of different methods
of robot control and allow users to easily specify logic without limiting them
sounds like a difficult challenge. Implementation will probably also require a
bit of work, but I would hazard that about 80\% of this project is just figuring
out what is good for the users. The language has to be as big as a GPL, but this
is easy if the DSL is internal.

### Scope
_How big an idea is this? How ambitious is this project?_

This is a pretty big project. I'm hoping to make something that will be
personally useful to me and potentially useful to others doing robotics. As I
mentioned before, there are lots of other languages that try to do similar
things to what I'm doing, and it will probably take lots of work to figure out a
solution that I find better than theirs. If this DSL ends up being external,
implementation will probably also require a lot of work since it needs to be as
powerful as a GPL, but if it is internal the implementation will not be too
difficult. Since the language design is so much of the project, I feel that if I
get a design I'm satisfied with, I'm OK with leaving it largely unimplemented or
"faking it" for the final.

### Challenges and opportunities
_Why is this a good project? What are some challenges you expect to face? How
might you overcome them? What are some warning signs that the project has gotten
off track, and how will you get the project back on track if needed?_

This is a good project because it is useful and has a huge language design
component. A warning sign may be if I start implementing too early. If I don't
think hard enough about the design, I could end up implementing something that
is no better than current solutions and have to redesign, wasting the
implementation effort. If I find myself wanting to start implementing, I'll try
writing sample programs and see what I find frustrating about that, and then go
back to design. I expect that the most challenging thing I'll face is how to
design a language that supports all the features I want.
