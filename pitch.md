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
@register_reaction(mechanism_name("Diels-Alder"))
@reaction_constraints('acidic', 'temp>70C', ...)
def diels_alder_reaction(products, conditions):
    ...
```

(Note that those constraints aren't at all the real constraints for a Diels-Alder
reaction, but existed merely to exemplify what sort of things could be used here).

The language would provide decorators (here I used Python, but this is by no means
required) and some form of multiple dispath to process arguments given to `react`
and then try to find the best fitting reaction.


### Operation (semantics)
_What might happen when a program runs? How does a program interact with the
user? What kinds of semantic (i.e., non-syntax) errors might occur, and how 
might they be communicated to the user?_


### Expressiveness
_What should be easy to do in this language? What should be possible, but
difficult? What should be impossible or very difficult?_


### Related work
_Are there any other DSLs in this domain? If not, describe how you know there
aren't and conjecture why not. If so, describe them and provide links. How well 
do they address the need? Are there any particularly admirable qualities of the
language? Are there parts of the language you think could be improved?_


## The Project
This section examines whether the idea makes for a good CS 111 project.


### Suitability
_What percentage of your time do you think will be spent directly engaging in
the **language** aspects of this project (e.g., making language design
decisions), as opposed to "systems" aspects of the project (e.g., implementing a
complicated semantics that doesn't require a lot of language design)?_


### Scope
_How big an idea is this? How ambitious is this project?_


### Challenges and opportunities
_Why is this a good project? What are some challenges you expect to face? How
might you overcome them? What are some warning signs that the project has gotten
off track, and how will you get the project back on track if needed?_

