# BarScript

## Overview
_What's this project about, briefly?_

This project is about creating a language to specify coffee/alcoholic drinks, so they can be made to your taste by an automated machine. We already have some automated coffee machines, but these machines usually have a limited number of adjustable settings and are considered by many to be inferior to an actual barista's work for this reason. Theoretically, if a project like this was wildly successful it'd eliminate the need for bartenders/baristas.

## The user and a language
This section describes who the project would serve and why a language might be a
good way to meet their needs.

### What's the need?
_What need is met by your idea? Who are you helping? What is that person's
experience like now? What would their experience be like if you could help 
them?_

Coffee drinks are difficult to make. In the world of the ever-present hipster, it's getting harder and harder to get it just right. In a world where customers actually order a "split-shot, heavy on decaf, 20 oz, soy, extra dry latte, with half pump vanilla & half-pump hazlenut", keeping track of all the modifications to make for a coffee drink is a difficult experience even for a physical barista. On the other hand, automatic coffee machines have a finite amount of settings that a customer can customize. 

Alcoholic beverages present a similar challenge. The barista I was discussing this project idea with told me about his favourite drink: "Old fashioned, with 2 shots of rye whisky, cane syrup instead of brown sugar, extra bitters, and orange zest instead of an orange slice". 

If there was a standard language by which a customer could specify a drink to an arbitrary level of precision, then you could easily program an automatic coffee machine or autobartender to make exactly the drink you want. 

### Why a language?
_Why is a DSL appropriate for your user(s)? How does it address the need?_

We need a DSL for this because we want to enable users to specify their drinks to arbitrary levels of precision. There are so many factors that go into a caffeinated or alcoholic beverage that we need a language (rather than, for instance, an enumerated type), because there are just so many possibilities. I imagine that there could be a GUI for end users to interact with this system, but compiling to a DSL built specifically for this purpose seems advantageous. For this project in particular, I plan not to build a GUI (because that seems like more trouble than it's worth), but you could certainly imagine building a GUI on top of the basic language.

### Why you?
_What excites you about this idea? How did you come up with it?_

I **love** coffee, so I'd be really excited to actually make this kind of thing. Amusingly (and probably not coincidentally), I came up with it while sitting in a coffee shop. An important project consideration for me is building something that I think could ulimately be useful, and I think this language could fill a currently empty niche in the drinks market. A barista that I discussed the idea with suggested making the language apply to alcoholic drinks as well, because they're (in his opinion) easier to make algorithmically.

### Interface (syntax)
_How might the user interact with the language? What does programming look 
like? Why is this the right way to interact with the problem domain? Be careful
to distinguish between, e.g,. a graphical interface and a linguistic interface._ 

I think the language is almost definitely going to have to be an external DSL - it doesn't really make sense to me to have it as an internal DSL, since its syntax is so different from Scala's (the language I plan to build my project in). In addition, after completing the assignments piconot and piconot-external, I have a feeling that it might be easier for me to implement this language as an external DSL - it felt like Scala's features hindered more than helped when we were implementing Picobot as an internal DSL, and I see no reason why something different would happen for this language. 

For CS111, I'm going to make the language interactable only through a text-based program. Programming would involve typing commands in the syntax of the language. I think this is the right way to create the language as a project for CS111 because creating a GUI (though it may be more user friendly) would be adding an additional level of complication that doesn't have much to do with language design, which is meant to be the focus of this project. If you wanted to make this language more usable for the general public, though, it would probably be advantageous to build a GUI for it eventually.

A program might look something like this:
```
Begin LATTE:
1. 2 shots espresso
2. Add 10 oz 2% milk
3. Add 2 oz foam
4. Add 4 pumps sugar
End LATTE:
```

Or like this:

```
Begin PUMPKIN_SPICE_LATTE:
1. LATTE
2. Add 2 pumps pumpkin
3. Add 1 shake Cinnamon
~~4. Add judgement~~
End PUMPKIN_SPICE_LATTE
```

Note: Here, you can also see a "function call" being executed (PUMPKIN_SPICE_LATTE calls LATTE). This is a feature that I'd like to build into the language. 

### Operation (semantics)
_What might happen when a program runs? How does a program interact with the
user? What kinds of semantic (i.e., non-syntax) errors might occur, and how 
might they be communicated to the user?_

In an ideal world, the result of running a program in this language would be a delicious drink. However, since I don't have the resources to procure an actual automated coffee machine to program using this lanugauge, I will have to come up with some alternative "final product" of the language. I'm currently leaning towards building an API that represents the coffee machine. API calls would result in printed statements like "pulling *n* shots of espresso now". Thus, the final product of a program will just be a bunch of print statements, but the idea is that if you swapped out the print statments for actual implementation of the automated coffee making, you could keep the API the same and the code that the user writes to create the drink wouldn't have to be changed at all.

Each line of code will be run sequentially. For instance, if a user says
```
1. A shot of whiskey
2. A shot of plain vodka
```
the resultant drink will have a darker hue on the top than if the two steps were reversed.

Calling another drink-making function (the way PUMPKIN_SPICE_LATTE calls LATTE above) should cause the entirety of the callee to be executed before control is returned to the calling function.  

Syntax errors are, of course, always possible. I'm not sure what kind of semantics errors might occur. Theoretically, one could just allow any code written in the language to execute, no matter how nonsensical it seems. Alternatively, you could build some semantic analysis into the language - for example, throwing an exception if a coffee drink is being made but no step to add coffee is included. I would probably lean towards building some semantic analysis (if I have time), as this would make error catching more robust in the language.

### Expressiveness
_What should be easy to do in this language? What should be possible, but
difficult? What should be impossible or very difficult?_

I feel like it should be easy to specify a generic drink, like a regular latte. In the formulation of the language I've proposed so far, there isn't really a way to do this easily - you'd still have to specify every step that goes into making a latte, which is unnecessary work since a latte is a pretty well-known drink. I think that this is where existing programs in the language should come in. For instance, there should be a latte template that contains all the steps required to make a regular latte. A user should be able to load in the regular latte template and either run it as is or modify it to create their preferred kind of drink, and then save the result as its own template. 

### Related work
_Are there any other DSLs in this domain? If not, describe how you know there
aren't and conjecture why not. If so, describe them and provide links. How well 
do they address the need? Are there any particularly admirable qualities of the
language? Are there parts of the language you think could be improved?_

There aren't any other DSLs in this domain that I know of. Automated coffee machines already have a GUI that lets you customize your drink in this way but

1. It almost certainly doesn't compile to a DSL (I guess **maybe** it does, but I highly doubt it).
2. The "language" has limited expressiveness. You can choose a base drink, and then modify the amount of coffee, sugar, and milk to add, but that's about it. The language I'm proposing would allow you to create a drink from the bottom up. 

## The Project
This section examines whether the idea makes for a good CS 111 project.

### Suitability
_What percentage of your time do you think will be spent directly engaging in
the **language** aspects of this project (e.g., making language design
decisions), as opposed to "systems" aspects of the project (e.g., implementing a
complicated semantics that doesn't require a lot of language design)?_

I think I'll be spending a lot of time making language design decisions, but also a fair amount of time implementing the language. The free free-form nature of the language (in particular, the fact that you could probably make programs of arbitrary length) means that parsing will be something of a challenge - I'll probably have to get really familiar with parser combinators. Luckily, once I have the intermediate representation of a program, execution should be pretty easy - just make the relevant library calls with the parameters extracted from the program. 

### Scope
_How big an idea is this? How ambitious is this project?_

I'd call this a medium sized idea. Implementing it is going to be difficult (because there will be a lot of language design choices to make), but I think it'll be manageable over the course of the semester. That said, I tend to underestimate the difficulty of things, and debugging can end up a fair amount of one's time, which could turn this medium-sized idea to a pretty big one. Also, I learned in picobot-external that there is usually a **lot** of error handling that you can add to a lanugage, so if I happen to get lucky and finish way ahead of time, I could always sink a bunch of time into that.

### Challenges and opportunities
_Why is this a good project? What are some challenges you expect to face? How
might you overcome them? What are some warning signs that the project has gotten
off track, and how will you get the project back on track if needed?_

This is a good project because I'm really excited about it, and it could be a really useful idea! Also, there are a lot of language design decisions to make (though I feel like I've made some of the major ones already, I'm sure some of those decisions will change as they come in contact with the real world), making it a project well suited for this class. 

I think the greatest challenge will be in figuring out the semantics of the language - what it should actually do when it runs. I think my idea of printing out the actions the machine would take in sequence sounds reasonable, though it does result in a fairly trivial final result. Another challenge will be architecting the code implementing the language well, since it's going to be pretty big for a DSL (or, at least, my initial vision for it is pretty complex). The third main challenge would be figuring out what language to write this DSL in - I'm leaning towards Scala, partly because it'll force me to learn more Scala, and partly because I could imagine its extensive libraries and language features being useful in implementing this language.

The greatest way the project could get "off track" is if I spend too much time trying to add features to the language that I don't have enough time to actually finish the implementation of the language by the end of the semester. I plan to remedy this by completing the project in "passes" - first I'll get just the base features working, then I'll add the next "nice to have" feature, and will continue doing that until the end of the semester as time allows. This will mean that (after the first couple of weeks) I'll always have a finished project, which will be good both for continuously evaluating the quality of the language and for my stress levels.