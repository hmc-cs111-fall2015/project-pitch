# CAOS

## Overview
CAOS is a language that (will be) designed to assist (primarily student) organic
chemists.  It will do so by allowing the simple representation of molecules, as
well as loading various common existing representations of molecules and predicting
how they will react.

## The user and a language
This section describes who the project would serve and why a language might be a
good way to meet their needs.


### What's the need?
Currently chemists must do this by hand or use relatively limited commercial 
software.  By developing an open source and free alternative, it allows 
technically minded chemists to more easily predict reactions they need.

### Why a language?
The language of chemical formulas and reactions is already essentially a DSL - 
this would just provide the computational ability to actually run and test a
reaction.

### Why you?
I've been playing around with this sort of idea for a long time, and have taken
a couple of stabs at it in the past.  I took organic chemistry and thought that
it shouldn't have to be as hard as it was to predict reactions.

### Interface (syntax)
Ideally it should be possible to interact with a GUI, an external DSL, and an 
internal DSL (matching the technical needs and abilities of the users), however
I expect that for 111 I'll be implementing either an internal or external DSL.

A typical program would likely look something like:

```
reactants = load_molecules("path/to/file.cml", format="cml")
conditions = make_conditions(pka=-1.7, temperature=-73, scale=TempEnum.Centigrade)
products = react(reactants, conditions)
```

Conceivably you could also hint what type of reaction you think it should do, like this

```
products = react(reactants, conditions, type_hint='E1')
```

Or try to work your way backwards from a product molecule to it's source using recursion

```
starting_material = retro_synthesis(products, final_conditions, max_steps=50)
```

This is the correct way to work with it (in terms of an internal-ish DSL) because the
concepts lend themselves well to existing programming language features such as
imperative programming and recursion. 

Additionally, it should be possible to extend the language relatively easily. Simply
define a new reaction type and then register it with the program (this is all 
theoretical at this point)

```
@register_reaction(mechanism_name="Diels-Alder")
@reaction_constraints('acidic', 'temp>70C', ...)
def diels_alder_reaction(products, conditions):
    ...
```

(Note that those constraints aren't at all the real constraints for a Diels-Alder
reaction, but existed merely to exemplify what sort of things could be used here).

The language would provide decorators (here I used Python, but this is by no means
required) and some form of multiple dispath to process arguments given to `react`
and then try to find the best fitting reaction.

Lastly it should be possible for the user to extend and implement new molecule 
types (for example if their reaction requires an encoding that my implementation
doesn't have).  This should ideally be duck-typed (i.e. not a strict inheritance 
relationship) or use interfaces/traits, and then require registration so the
intermediate representation knows that it can use this kind of object.

```
@register_molecular_type(type_name="NobleGas")
@molecule_requirements('full_valence')
class NobleGas:
    ...
```

Things like `reaction_constraints` and `molecule_requirements` should also be 
user definable.  Ideally all of these user-defined reactions and molecule types 
would exist in some other file away from their actual reactions and then be
importable/loadable in the scripts that need it.


### Operation (semantics)
_What might happen when a program runs? How does a program interact with the
user? What kinds of semantic (i.e., non-syntax) errors might occur, and how 
might they be communicated to the user?_

When the program runs it should take as much information as the user provides 
(more is probably better) and then attempt to determine as much additional
information about the compounds as possible (such as how nucleophilic it is,
or acidic, or whatever).  From there it should use some type of multiple 
dispatch to find the most likely reaction mechanism for these reactants.

There should be two modes - regular and verbose.  Regular would simply run the
program, outputting "normal" warnings and errors (such as not having sufficient
information to conduct a reaction, or that the hinted reaction mechanism is invalid
for the information given, etc).  Verbose would be much more detailed, explaining
what information about the compounds it is deriving and how, how it determines which
mechanism(s) to try, and what does or does not work in each case.  

In verbose mode (with the GUI form) I would expect it to display the actual physical
changes the molecule undergoes throughout the process.

Semantic errors could occur if the suggested reaction is invalid, or if there isn't a 
way to make these things react.  Additionally if an invalid user type or mechanism 
were defined and found to be the best match then they should also raise some sort of
semantic error.  These should be thrown as (uncatchable either by implementation or
convention) exceptions - invalid reaction types are ideally something that could be 
found at "compile" time but is really more of a runtime type of discovery.  They 
shouldn't be handled by the user in code (such as `SystemExit` in Python).


### Expressiveness

It should be very easy to make molecules react. 

It should be possible to chain lots of reactions together to see how very complex
systems interact.

It shouldn't be possible to use this as a GPL.


### Related work

Yes, the one I've been working on [here](https://github.com/Dannnno/Chemistry).
There are some other ones too, that I learned about asking 
[this question](http://chemistry.stackexchange.com/questions/7765/program-that-simulates-basic-reactions-in-organic-chemistry)
on the Chemistry Stack Exchange.  I know little about them; they are of varying
usefulness and popularity:

- [WODCA from the Gasteiger group](http://www2.chemie.uni-erlangen.de/software/wodca/index.html)
- [CHIRON from the Hanessian group](http://osiris.corg.umontreal.ca/chiron.shtml)
- [LHASA from the Corey group](http://cheminf.cmbi.ru.nl/cheminf/lhasa/)
- [SYLVIA](https://www.molecular-networks.com/products/sylvia)
- [ArChem - also called Route Designer](http://www.simbiosys.ca/archem/)
- [Chematica](https://en.wikipedia.org/wiki/Chematica)
- [Some guy's pet project](http://www.dimuthu.org/blog/2008/11/22/organic-chemistry-reaction-simulator/)

None of them appear to have widespread use or support, and have varying levels
of functionality.  I like that people have tried things, but honestly I don't really
like any of them.


## The Project
This section examines whether the idea makes for a good CS 111 project.


### Suitability
I see myself spending a lot of time on both.  I think designing the main
members of the language would be pretty easy (like the builtin functions you can 
use to load molecules from files, react them, etc) and while it would require 
thought, it shouldn't take too much.  I think the brunt of the language design
would blur into the intermediate representation side of things - how to best 
design the system of creating and using user-defined mechanisms and types and 
then ensuring that the program will use them when appropriate. While it will
take a lot of systems-side thought, I'll have to think a lot about how I want
the user to be able to interact with everything (without ripping apart the 
source code).  I think the systems side will also be hefty, however I plan on
focusing on language design and not worrying too much about very complex reactions
that require more system-side effort.  Probably about 65-35.


### Scope
Big and ambitious at its greatest, but I think I'm going to try and narrow the 
focus down to a single, (relatively) simple type of reaction and a single, 
(relatively) simple language (i.e. either internal or external, and certainly not
a GUI).

I plan on limiting this to (most forms of) acid-base reactions.  Additionally, I 
think I'm going to write this as an internal DSL - I think the flavor of my host
language (Python) lends itself well to what I'm trying to implement.  If it 
becomes necessary I'll make the transition to external.


### Challenges and opportunities
This is a good project because it is going to require a lot of thought in making
it easy and enjoyable to extend for the users.  I think that is going to take up
the bulk of my time.  I plan on doing a lot of research on multiple dispatch, as 
well as learning how to predict the best mechanism (algorithm) for the job at
hand.  

Warning signs will be if I find myself down a rabbit hole of some systems aspect
that may be important but is much more of an algorithms question than a language
design one.  In those cases I'll put a pin in it and either (a) require more 
information from the user so as to require less algorithmic challenges or (b)
decide to work on it later and, at worst, mock it for the sake of this class. I
hope to continue this project after this class, so I don't necessarily need to 
solve all of the systems problems now.
