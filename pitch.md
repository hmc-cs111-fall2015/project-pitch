# Compile-Time Programming

## Overview

There are aspects of programming languages that operate during compile time.
Examples are simple constant expressions, type checking, and macros. Less common
are dependent types, correctness proofs (relatedly), and LISP-style abstract syntax tree macros.

However, these are features which are extremely difficult to _add_ to an existing language.
And they are nonetheless so desirable that people will go to extreme lengths to get them
when they aren't available. (See: C++ template programming, or anything Andrei Alexandrescu writes)
Furthermore, the nastiness of C++'s templates are not just inherited from C++'s
general style. In Scala, similar things start to happen when you try to implement
dependent types.

Ultimately, the real problem is that programmers only have incidental control
over compile-time behavior. I want to design a language where there is
direct and encouraged access to compile-time behavior. This is extremely ambitious,
so there are many limits that will be discussed later.

## The user and a language


### What's the need?

The big need I see is that with current languages, extensibility ends at
compile-time features. That is not completely true: again, it is _possible_
to develop a lot of functionality by leveraging what already exists,
especially when you get into the realm of macros.  
And Haskell encourages modifications to the compiler, such that something
like Idris (which has dependent types) can be built off of it, which is also
pretty successful. Even so, these are not particularly friendly.
I want to explore the possibility of extensibility in this region as well.

There is also a second need.
Supposedly, this would be a general-purpose programming language, whose compile-time features
were especially easy to extend. That could mean that it would be extremely useful
for people writing code that needs exotic compile-time features, such as verification:
but, in actuality, if it were to be practically useful, it would probably be as a playground
for working with different variations on compile-time concepts such as dependent types.
So it is also potentially useful as a programming language researcher's aide.

### Why a language?

Well, ultimately, this is a language about features of programming languages.
It needs to be in close reflection to programming languages, so this seems to be a no-brainer.


### Why you?

What first interested me about this kind of idea was learning about D. It's essentially
C++ done right. D offers much closer control over compile-time behavior. In particular,
D has such features as compile-time "if" statements, compile-time arguments to functions,
and a much better system than C++'s templates.

The other thing is that I really want to explore type systems.
First, building a language like this would force me to look at them.
But also, _having_ a language like this, if it was actually sufficiently expressive,
would be helpful in learning-through-implementing those ideas.


### Interface (syntax)

The interface is entirely linguistic. You write some code, and you compile it.
However, what happens during compilation will also be a part of your code. In some sense,
errors would happen in "layers" - perhaps not by design, but by reality - in the way that
there would probably end up being layers to what happens during compilation. (First some mutations,
then basic type checking, then some kind of verification thing, etc.) So, it would be especially
important that errors know their source. Specifically, an error that pops up after an AST mutation
would need to reference the mutation, as well as the original code that was mutated.
After that, it just needs to be straightforward for people who write compile-time behavior to
also write error messages.

(You know, that's another thing that might be good. Depending on how much compile-time behavior
can be coded in, you could have people make variant implementations of things that just had better error
messages... that's a rare kind of extensibility.)

One interesting point is that, as is often the case for languages with powerful compile-time 
capabilities, the errors you inevitably get during compilation are not meant just
to inform you that you've typed something wrong. Rather, they are supposed
to guide you to what you should do next in your coding. So that may
also be a (stretch goal) _characteristic_ of the interface.

### Operation (semantics)

A program, as it is running, would probably be a collection of ASTs, or perhaps something
slightly more general.  Some mutations are run on this collection.
Then calculations such as type or other property checking are run on the ASTs.
A final resulting AST, with a lot of annotated information, is produced at the end.
Theoretically it would either compile to runnable code or transpile to some
similar-enough language, but it would really be fine if it didn't do this step.

### Expressiveness
_What should be easy to do in this language? What should be possible, but
difficult? What should be impossible or very difficult?_

- It should be extremely easy to do simple computations at compile-time.
- It should be easy to implement a trivial type system.
- It should be easy to implement simple AST transformations.
- It should be moderately easy to implement simple property-propagations, as a rudimentary form of dependent types.
- It should be possible to implement natural deduction, actually!
- Arguably, it should be impossible to do compile-time calculations that may not terminate, such as Idris requires, but I will not think about that.


### Related work

C++ has templates, which have evolved tremendously and unfortunately.
D has static arguments, and a lot of control of compile time stuff in some ways.
Idris has dependent types, which are the sort of thing you would want to
build in this language. Those are sort of motivating examples.

Closer to what I'm actually going for are Scala and Lisp's macros,
which allow you to manipulate abstract syntax trees directly,
give errors based on them, etc. In fact, it may be that if Scala's
macros are powerful and expressive enough, that is how this project would be implemented.

## The Project
This section examines whether the idea makes for a good CS 111 project.


### Suitability

In an attempt to create an actual, practically usable programming language with these features,
it would take a huge amount of work just on the implementation side.
But, that is not what I'm interested in. I am only interested in the aspects
that are associated with compile-time checking and such. On the next level,
I am also not interested with actually implementing a good type-checking system
(i.e., one with good inference). The only important thing is that such
a thing _could_ be made. Furthermore, how well it actually runs is far less important than what
happens during compilation, _so much so_ that it would be fine if no actually runnable code
could be made.

Thus, the meat of the project is still in language design. The main question is how to
give direct access to compile-time calculations. There are basically two ways
to do this, and it might be possible to unify them. The first is directly manipulating
abstract syntax trees. The second is a generic form of "property propagation", such
as allows naive type-checking. That can be described as an operation on ASTs, though.
So given a rudimentary underlying abstract syntax, which would probably not be any more
complicated than a very simple subset of Haskell, the main question of the project
becomes how to expressively manipulate and calculate the properties of ASTs.

### Scope

Extremely ambitious, if it were to be of practical use.
It might be the case that the final product of a project like this would be
no more than a language specification, and an outline of an implementation strategy,
rather than something that actually ran. That would mean that nearly all the 
work was in languages! But it would also be a rather unsatisfying conclusion.

(Because of this, I have some reserve projects in mind.)

### Challenges and opportunities

The project can get off-track in several ways.

The first is if it starts to turn into an infinite cycle of reading papers.
If that is the case early-on, then I would say that I should abort the project altogether.
Otherwise, it would just be something to avoid.

The second is if things start to get implementation-heavy. Doing a project like this
requires being OK with a well-defined but unimplemented result, because the details of
implementation are probably just too much. So, in this case, I should just step back
and accept a more theoretical result.

Being on-track looks more like this. I find very rudimentary compile-time feature X.
What is the most expressive way to describe how to _implement_ (not use) X? Does that match up
well with how I want to describe the implementation of feature Y? Merge and iterate to more complex,
but still pretty simple features (rudimentary dependent types, for example). Then, iterate downwards: What base features do I have that could be implemented using others?
Reach a simple core that could be built up to implement the features I've explored. Then, see how far that can
go towards implementing other things.


