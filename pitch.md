# FreeTyle

## Overview
_What's this project about, briefly?_

It's an RPG mapmaker language. The initial implementation will be text-based only, with a GUI added only if time permits.
The language would let users create tile objects by supplying an image source path, specify an optional border, specify a coordinate system and a map size, and then designate rectangular areas to be filled in. Additionally, non-square "tiles" or objects can be placed on the scene by designating an "anchor point" on the input image and then specifying its coordinates on the map. Different images like this can be placed on the scene, so a "tile" may be any image, and the user will also be able to designate layering. Tiles can also be rotated and translated fairly easily. Once a program is run, an output map will be produced.

## The user and a language
This section describes who the project would serve and why a language might be a
good way to meet their needs.

The user would be game developers (or perhaps artists).

### What's the need?
_What need is met by your idea? Who are you helping? What is that person's
experience like now? What would their experience be like if you could help 
them?_

Well, existing map generators that I'm aware of generally have set tile sizes, which limits the ability to quickly design maps that don't look as blocky or aren't constrained by having every piece of the map fill a tile of the same size. But to have complete control over a map would require illustrating it entirely from scratch, which would take too long. This would be a tool that might keep the process quick while allowing for more artistic design decisions. 

### Why a language?
_Why is a DSL appropriate for your user(s)? How does it address the need?_

If existing map makers count as DSLs, then these tools have already proven to address this type of need.
Perhaps a text-based DSL isn't the most ideal way to go, but it wouldn't be a long process to make a map, and it would be easy to make minor changes without having to handle multiple layers in a software like photoshop.

### Why you?
_What excites you about this idea? How did you come up with it?_

_Words cannot express my interest in game design._
Also, map generation is one of the most basic game dev tools, and free-to-use tools can always be improved on.

### Interface (syntax)
_How might the user interact with the language? What does programming look 
like? Why is this the right way to interact with the problem domain? Be careful
to distinguish between, e.g,. a graphical interface and a linguistic interface._ 

This is mostly described above. A program is just lines of code. The specifics haven't been worked out yet, but specifying tile objects might look something like:

```
tile water1 = SRCPATH 
tile ground1 = SRCPATH {
	edge = SRCPATH
}
freeform tile peninsula = SRCPATH {
	anchor = (5,5)
}
```


### Operation (semantics)
_What might happen when a program runs? How does a program interact with the
user? What kinds of semantic (i.e., non-syntax) errors might occur, and how 
might they be communicated to the user?_

When the program runs, it generates an image file.
One possibility, to help communicate with the users, is to also output a map with the outlines of each area/tile and anchors marked.
Additionally, errors would occur if, for instance, a freeform tile didn't have a specified anchor, or if two tiles on the same layer overlapped one another.

### Expressiveness
_What should be easy to do in this language? What should be possible, but
difficult? What should be impossible or very difficult?_

It should be easy to move around and rotate any tiles, so in theory creating and adjusting maps should be fairly easy. It would technically be possible to create other art projects using this language, but it may be more cumbersome than using other software.
Anything outside of this domain would be difficult or impossible.

### Related work
_Are there any other DSLs in this domain? If not, describe how you know there
aren't and conjecture why not. If so, describe them and provide links. How well 
do they address the need? Are there any particularly admirable qualities of the
language? Are there parts of the language you think could be improved?_

There are loads of RPG mapmakers. Most of them have pre-defined tile sizes, but with enough searching it may be possible to find one that has this behavior; however, overall they give game developers enough tools to succeed. 


## The Project
This section examines whether the idea makes for a good CS 111 project.


### Suitability
_What percentage of your time do you think will be spent directly engaging in
the **language** aspects of this project (e.g., making language design
decisions), as opposed to "systems" aspects of the project (e.g., implementing a
complicated semantics that doesn't require a lot of language design)?_

It seems that trying to invent ways for the user to specify how they want to build the map in an intuitive way should involve more language design decisions. There will be semantics decisions, of course, but trying to add in as much implementation as possible should draw out the language aspects of this project.

### Scope
_How big an idea is this? How ambitious is this project?_

Since I'll be focusing first and foremost on the text-based implementation, and the UI may or may not be implemented, this shouldn't be too ambitious.

### Challenges and opportunities
_Why is this a good project? What are some challenges you expect to face? How
might you overcome them? What are some warning signs that the project has gotten
off track, and how will you get the project back on track if needed?_

The biggest problem to solve is finding the most intuitive way to let the user specify a coordinate system. Perhaps users may also be allowed to specify relative placement, placing certain tiles above, below, to the right of, and to the left of other tiles.
Another possibility is to allow for ambiguity; the user could specify a general area to place things, or somewhere to fill in with a pattern tile even if they don't fit perfectly (for example, tiling a 17x24 area with 5x5 tiles).
