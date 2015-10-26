# Project Title (replace me)

## Overview
_What's this project about, briefly?_

Compile time and runtime CHECKS are one and the same.

## The user and a language
This section describes who the project would serve and why a language might be a
good way to meet their needs.


This is for people to try out various 



### What's the need?
_What need is met by your idea? Who are you helping? What is that person's
experience like now? What would their experience be like if you could help 
them?_


Templates? Total crap. Macros? Unfortunate. Want dependent types? You have to do template-like crap, even in Scala.
Trying to explore taking extensibility to the next level.
More provable correctness, in more ways than ever before.
Much better errors for DSLs because it is encouraged that you do things at the compile-time level via macros and such.


### Why a language?
_Why is a DSL appropriate for your user(s)? How does it address the need?_


Well, ultimately I'm trying to help out a langauge. Of course it's going to be a language.


### Why you?
_What excites you about this idea? How did you come up with it?_


I have been interested in this kind of thing ever since learning about D.


### Interface (syntax)
_How might the user interact with the language? What does programming look 
like? Why is this the right way to interact with the problem domain? Be careful
to distinguish between, e.g,. a graphical interface and a linguistic interface._ 


You write, you compile. Compilation is especially supposed to help you do the next step,
rather than just succeed or error out, so errors are of paramount importance.
There might even be separate things in the future.
A future version might help talk about an IDE which does the compilation continuously and thus
points you to your problems as they occur, like a real type checker.


### Operation (semantics)
_What might happen when a program runs? How does a program interact with the
user? What kinds of semantic (i.e., non-syntax) errors might occur, and how 
might they be communicated to the user?_


A program runs on several levels. Some things work on ASTs, some things work on compile-time information,
which is just done normally like runtime but it's compile time.
Finally at the end, it compiles normally (Haskell-like?) code.
Some checks have runtime equivalents.



### Expressiveness
_What should be easy to do in this language? What should be possible, but
difficult? What should be impossible or very difficult?_


Very very easy to run certain calculations during compile time.



### Related work
_Are there any other DSLs in this domain? If not, describe how you know there
aren't and conjecture why not. If so, describe them and provide links. How well 
do they address the need? Are there any particularly admirable qualities of the
language? Are there parts of the language you think could be improved?_


C++ has templates, which have evolved tremendously and unfrtunately.
D has static arguments, and a lot of control of compile time stuff in some ways.
Idris has dependent types, which are the sort of thing you would want to
BUILD in this language.


## The Project
This section examines whether the idea makes for a good CS 111 project.


### Suitability
_What percentage of your time do you think will be spent directly engaging in
the **language** aspects of this project (e.g., making language design
decisions), as opposed to "systems" aspects of the project (e.g., implementing a
complicated semantics that doesn't require a lot of language design)?_


I am not too interested in what code does when it runs. That is to say,
all I want to do in the end is produce some code and claim, THIS WILL WORK.
Actually running it? No. In fact, I may just support 


### Scope
_How big an idea is this? How ambitious is this project?_

So ambitious.


### Challenges and opportunities
_Why is this a good project? What are some challenges you expect to face? How
might you overcome them? What are some warning signs that the project has gotten
off track, and how will you get the project back on track if needed?_



