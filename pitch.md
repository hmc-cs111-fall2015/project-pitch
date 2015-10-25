# Construct

## Overview
_What's this project about, briefly?_

The Construct language is a domain specific language for doing geometric
constructions on the fly.

The language aims to
   1. Allow users to define geometric constructions
   1. Allow for reuse of constructions.
   1. Provide an efficient way of determining which constructions may be done
      next.
   1. Allow users to render constructions into images or LaTeX.

## The user and a language
This section describes who the project would serve and why a language might be a
good way to meet their needs.


### What's the need?
_What need is met by your idea? Who are you helping? What is that person's
experience like now? What would their experience be like if you could help 
them?_

From time to time, teachers and students of geometry and associated fields are
interested in creating constructions. While sometimes they understand what they
are creating, often times they are creating the idea as they make the drawing.

It is also worth noting that while frequently users want these constructions
rendered into drawings, the objects they are describing are geometric in
nature - not inherently graphical. This means that sometimes geometrically
distinct ideas may be spatially close. If input is spatial then this can result
in geometric imprecision. For example, consider drawing a line from a triangle
vertex to the midpoint of the opposing side vs bisecting that angle. Often
these two actions are spatially similar (the lines end up close to each other).

Current solutions to the problem fail to be both easy to use and geometrically
precise. `tkz-euclid` is geometrically precise but very cryptic, and there are
various visual construction engines which are easy to use but rely on spatial
input and are thus geometrically imprecise in some cases.

Furthermore, none of the above systems allow the user to see what steps they
might take next.


### Why a language?
_Why is a DSL appropriate for your user(s)? How does it address the need?_

Some parts of this solution are clearly a language. The way the user interacts
with the system clearly must be a language. If they use some sort of textual
system like

```
Line from A to B
Line from A to C
Bisect Angle C A B
```

then there is a language writen there with all of the nouns and verbs we
expect.

But there is also more. Under the hood, the system must have some sort of idea
of how to represent these geometric ideas. A common form from which the
description system, the rendering system, and the extrapolation system can all
be build.

I think that this language - this core representation of geometric ideas is the
real DSL behind this project.

### Why you?
_What excites you about this idea? How did you come up with it?_

I've always been somewhat of a geometry enthusiast, which is probably the
real origin of my interest in this project. I enjoy thinking about geometric
ideas and think that I would have a lot of fun doing that for the next few
weeks.

That's not all though. I also generally have a lot of trouble using computers
to foster creativity. I'm a very paper and pencil sort of guy. I think
designing a system which has to potential to make computers a better platform
for exploring ideas (even in the limited domain of classical constructions)
would be worth putting time into.

### Interface (syntax)
_How might the user interact with the language? What does programming look 
like? Why is this the right way to interact with the problem domain? Be careful
to distinguish between, e.g,. a graphical interface and a linguistic interface._ 

#### User Language

The User Language is the way in which users write constructions.

Taken from my project ideas writeup:

> [Users] would write statements like:
>
> ```
> circle x with center C
> line y tangent to x at point D
> line z through points C and D
> ```
>
> I really like language idea because it mirrors the way that mathematicians
> write about geometry. Who hasn't seen something like:
>
> Let x be a circle centered at C. Let y be a line tangent to x at point D. Let z
> be a line through C and D. ...more proof...
>
> =============================================================================
>
> The more interesting would be interactive mode, where as the users enter each
> line the image is drawn for them to see what they have, as well as to indicate
> potentially interesting thing to do next (IE, highlighting the tangent point
> after drawing a tangent). Using this information the users can issue special
> interactive commands that act on those possibilities.
>
> At the end of the session the user could export the image, LaTeX, or DSL code

#### Geometric Representation

We can also talk about the syntax of the internal geometric representation.

The details of the syntax (actual names and symbols) are hard to pin down at
this point, but we can talk about some of the concepts that we expect to come
out in the syntax. For example, although Python, C++, and Java all have
different surface syntax for constructing new objects, they all share the idea
of the existence of classes and the existence of a function-like constructor
that creates an instance of that class.

The current image I have of the internal representation is that we need to be
able to describe points and various types of point-sets (in particular lines
and circles, maybe more). We need to be able to take intersections of point
sets, choose points from point sets.

I also think it would be cool (maybe even necessary) to be able to describe a
construction as a sub-procedure. Perhaps we can define a construction which
takes two points and gives you the midpoint of the segment between them.
Perhaps the subprocedures can only take and return points? Perhaps they can
also return point-sets? Perhaps point-sets shouldn't be fundamentals in the
language?

There are many questions which remain here.

### Operation (semantics)
_What might happen when a program runs? How does a program interact with the
user? What kinds of semantic (i.e., non-syntax) errors might occur, and how 
might they be communicated to the user?_

The internal representation should do two things during runtime.

The first of these is consistency-checking. One could imagine syntactically
correct statements about geometry which are not actually possible.

### Expressiveness
_What should be easy to do in this language? What should be possible, but
difficult? What should be impossible or very difficult?_

I want the following to feel seemless:
   - Choosing points
   - Drawing lines though them
   - Drawing circles about them
   - Finding the intesection of these loci
   - Embedding constructions into other constructions concisely (subroutines)

Fancy concepts should be definable using the above ideas, but not built in.
The subroutines should feel like they we language primitives - true
composability.

I want it to be easy to search through possible actions using the internal
geometric representation.

I want it to be hard to move around individual points or lines. This is not the
concern of someone doing a construction.

I want it to be reasonably (but not super-easy) to change render properties of
the figure as a whole (rotations, scaling, etc). It should also be reasonable
to label things and add chromatic annotations (custom colorization). It seems
reasonable to restrict some of the custom rendering options to be performed
after the geometric construction has been completed.

### Related work
_Are there any other DSLs in this domain? If not, describe how you know there
aren't and conjecture why not. If so, describe them and provide links. How well 
do they address the need? Are there any particularly admirable qualities of the
language? Are there parts of the language you think could be improved?_

I've already mentioned some of the other tools/DSLs hanging out in this domain.
A brief list:
   - [tkz-euclide](https://www.ctan.org/pkg/tkz-euclide?lang=en) is a LaTeX
     package which allows for geometrically precise drawings. It is somewhat
     cryptic and documented only in French :heart: .
   - [sketchometry](http://start.sketchometry.org/) is a tool that allows you
     to skethily draws things and fits your drawing to geometrically
     significant shapes.
   - [geogebra](https://www.geogebra.org/) is another, more conventional
     graphical drawing aide.

As discussed, all of these fail to be both precise and easy to use. I like a
lot of what the LaTeX package does, but I think it is rather clunky to use, and
is not well adapted to building further tooling on top of.

I intend to spent some time exploring how it handles errors (I.E. intersection
of parallel lines) to get some inspiration for how I should.

I also like the way that a lot of the graphical tools snap your lines to
geometrically significant positions. I think that this is generally a good
idea, and would like to implement something similar (I.E. suggestions) in a way
that is more extensible and more geometrically precise.

## The Project
This section examines whether the idea makes for a good CS 111 project.


### Suitability
_What percentage of your time do you think will be spent directly engaging in
the **language** aspects of this project (e.g., making language design
decisions), as opposed to "systems" aspects of the project (e.g., implementing a
complicated semantics that doesn't require a lot of language design)?_

At first I thought that this project wouldn't be especially suitable for a DSLs
project. I recognized that making a geometric engine powerful enough to do
suggestions would take a lot of effort. I felt that this task would end up
dwarfing the task of specifying how users should interact with the system.

However, Prof. Ben made me realize that this engine-building segment of the
project is really just building a DSL. During this segment I would be thinking
about a way of representing geometric objects so that developers could then go
and build a text-based interface, a suggestion system, a rendering system.

The 'systems' work would be actually writing intersection code, but the DSL
work would be choosing what the fundamental object of the representation are,
and how they interact.

### Scope
_How big an idea is this? How ambitious is this project?_

It's reasonably ambitious. I think that if I tried to make a polished user
experience then it might end up being too much, but if I start from the core of
the language (geometric representation) and work outwards from there, then it
should be fairly reasonable.

In particular, I plan to start be developing an idea of the geometric
representation - what are the fundamental object? How do they interact? How can
users use composition?

From there I intend to implement these core features, balancing user needs and
implementation time.

Once the base is build I can work on things like the textual interface, the
suggestion system, and the rendering system.

### Challenges and opportunities
_Why is this a good project? What are some challenges you expect to face? How
might you overcome them? What are some warning signs that the project has gotten
off track, and how will you get the project back on track if needed?_

For me this is a good project because I'm passionate about the domain, and I
naturally am interested in organizing ideas in a DSL-ish way. I think the
project offers thi full-stack potential that I think will give me practice
designing a DSL at many levels.

I expect this project to be technically challenging. A lot of the computation
going on is non-trival and would be challenging to write even if someone else
dictacted the DSL.

I think this project will offer a lot of challenging design choices. Already
I've been poking around at some of the geometry/topology libraries that exist
and they tackle things in many different ways. There will be many ways to
implement and feature I desire and choosing the most appropriate will be
interesting.

I think that if I end up spending too much time trying to make any one of these
decisions, or if I spend too much time implementing any one feature on my own,
then I'm stumbly on dangerous ground. It's important to keep on moving - even
if your decision turns out poorly you can always go back.

I think planning out my weeks' work in advance will help me combat this
stalling. If I'm forced to look back at what I did each week I'm more likely to
notice if I'm not making any progress. If I find myself in such a situation I
just need to make a choice and move on.
