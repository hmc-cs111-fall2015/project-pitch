# Code Vis (potentially [Flowgen])

## Overview
_What's this project about, briefly?_

_Code Vis_&mdash;short for "Code Visualizer"&mdash;makes it easier for programmers
to create flowcharts that visually represent the control flow of their code.
Code documentation is important, so _Code Vis_ strives to make (at least) one method
of documentation as simple and convenient as possible in an effort to
reduce the number of barriers keeping people from producing documentation.

## The user and a language
This section describes who the project would serve and why a language might be a
good way to meet their needs.


### What's the need?
_What need is met by your idea? Who are you helping? What is that person's
experience like now? What would their experience be like if you could help 
them?_

Trying to understand someone else's code&mdash;especially at a large scale&mdash;can be
an intimidating, difficult, and overwhelming task, even if the person trying to digest the code
is an experienced programmer: having to distinguish keywords and follow control flow
in raw source code can be tiring, even if the code is well-commented.
Documentation can help this process, but text alone isn't always the best
or most accessible way to express an idea. To address this problem,
I propose designing a language/tool that translates code into flowcharts,
which would offer a more visually-appealing representation of code&mdash;but
would not replace the need for more traditional text-based documentation.
Not only would this solution help anyone (i.e., programmers and non-programmers alike)
in understanding code, but it could also reduce the effort necessary
to produce 'good' documentation since, ideally, programmers
wouldn't have to venture too far from the code itself to generate the flowcharts.
Perhap optimistically, the language could also compel programmers
to write more high level, commented, and documented code
because doing so would be a sort of requirement of the language.
Another really cool potential result would be that programmers could use skeleton code
in the language in which they intend to work
to generate complete flowcharts that express the entirety of the intended algorithm.

### Why a language?
_Why is a DSL appropriate for your user(s)? How does it address the need?_

1. The programmer might not want every implementation detail
to leak into the flowcharts, so there should be some way to indicate
what _should_ appear on the flowcharts.

2. There should be as few barriers as possible to using this tool,
so I think allowing users to simply add code or annotations
to the code they're already writing would be ideal.

### Why you?
_What excites you about this idea? How did you come up with it?_

I really like the idea of making algorithms represented in code more accessible.
I myself tend to favor and think in visualizations,
and I think it would be a lot easier for me to explain code to someone
if I could easily transform my code into a flowchart.
During my internship over the summer, I wrote a document that details
the design of my project, and in that document, I employed a flowchart
to demonstrate how I decided to handle one of the more complex parts of the project
because a flowchart seemed fitting for the task.
Creating the flowchart was more time consuming than I would have liked,
and it would have been nice if there was a language sort of hiding in the code
that generated the flowchart. I also think documentation is _super_ important,
so it's very appealing to me to develop tools that simplify the documentation process
and compel others to put more effort toward it.

### Interface (syntax)
_How might the user interact with the language? What does programming look 
like? Why is this the right way to interact with the problem domain? Be careful
to distinguish between, e.g,. a graphical interface and a linguistic interface._ 

I'd like the code to feel as much like the underlying language (e.g., a GPL) as possible
so that there's not too much of a learning curve and to minimize the barriers
that might cause one to avoid using the tool. To that end,
my initial thoughts went to [Javadoc] annotations and [Doxygen] comments,
which use minimal indicators in the code to denote something.
I think comments are the way to go for the syntax because
I expect the syntax to be more descriptive and more frequently used than Javadoc annotations,
making them more akin to comments. Annotations also describe functions and classes,
whereas comments are (at least more conventionally) used to outline control flow,
which is appropriate for describing flowcharts.

### Operation (semantics)
_What might happen when a program runs? How does a program interact with the
user? What kinds of semantic (i.e., non-syntax) errors might occur, and how 
might they be communicated to the user?_

The runtime for the language compiles a file, parsing both the flowchart generator's syntax
and control flow keywords in the underlying language, and generates one or more flowcharts.
Additionally, I think it would be pretty cool if users could interact
with the generated flowcharts: for instance, one of the components of the flowchart
could represent a fairly complex helper function that could be clicked
to reveal another flowchart that represents the helper function's algorithm.

Thinking of Java/C++ syntax, I might use `//?` to indicate a condition check
(i.e., in an `if` statement); therefore, it would probably be a _semantic_ error
if one uses `//?` before any statement that is not an `if` statement.
It would also be nice to have warnings if indicators are expected.
For instance, if someone indicates that an `if`-`else` block should be
represented in the flowchart, but only adds annotations for code
within the `if` portion of the block, then the user should be notified that
one would _typically_ expect the `else` portion to also contain code annotations;
however, it's completely appropriate for the `else` portion to not contain code annotations,
so the flowchart would still be generated, and the user should be able to dismiss
the warning so that it does not reappear. I think these errors/warnings can appear
at compile time on the command line.

### Expressiveness
_What should be easy to do in this language? What should be possible, but
difficult? What should be impossible or very difficult?_

It should be easy to generate flowcharts that illustrate the control flow of some code,
ideally possible to generate the flowcharts without the actual code being written
and further to add comments to the flowcharts,
but pretty much impossible to do any sort of conventional computation.
I haven't thought too much about what syntax would be required to support
the ability to generate a full-featured flowchart without actual code being written,
but I'm pretty sure users would have to be more verbose than they otherwise would be.

It might be useful to allow users to 'program' in more than one mode.
One mode wouldn't rely at all on control flow structures
in the underlying language, but would still use the underlying language's
comment syntax; this mode would be used to describe an algorithm
before it's implemented, and the flowchart description would serve
as a sort of template for the actual implementation,
which could make the implementation process more efficient.
And another mode would rely more on control flow structures,
but users would still have to be explicit about what should be in the flowchart.

### Related work
_Are there any other DSLs in this domain? If not, describe how you know there
aren't and conjecture why not. If so, describe them and provide links. How well 
do they address the need? Are there any particularly admirable qualities of the
language? Are there parts of the language you think could be improved?_

The first DSL in the domain that I found goes by [code2flow]
and is designed to make flowchart creation easy;
however, the language doesn't suit my ideal well
because it's not embedded in an established language&mdash;though
the syntax resembles Java/C++. Another language that is actually
very on par with my idea is [Flowgen]&mdash;it's on GitHub,
and it's even associated with a [paper][Flowgen Paper]!
Flowgen works for C++ and addresses the need pretty well.
For the most part, I appreciate the syntax (It uses comments!),
but, it's not finished (perhaps an opportunity),
the flowcharts aren't very pretty, I don't like how it does subroutine-linking
(expansion in place as opposed to opening a separte flowchart),
and I'm currently of the opinion that the language should be opt-in oriented,
but Flowgen includes _every_ `if` statement (and `for` loop) in flowcharts,
which causes the underling language's syntax to leak into the flowchart
if users do not provide a more human-readable description for the condition.

## The Project
This section examines whether the idea makes for a good CS 111 project.


### Suitability
_What percentage of your time do you think will be spent directly engaging in
the **language** aspects of this project (e.g., making language design
decisions), as opposed to "systems" aspects of the project (e.g., implementing a
complicated semantics that doesn't require a lot of language design)?_

If you include the time I've already spent considering language aspects,
I'd say about 20-30% of my time will be spent engaging in these aspects.
There still remains syntax and philosophy to solidify,
and I don't expect the implementation to be terribly difficult.

### Scope
_How big an idea is this? How ambitious is this project?_

I think the idea is a healthy size and still has potential to grow.
Most importantly, I don't think it will be tough to successfully see
multiple meaningful iterations of the language before the semester's end.

### Challenges and opportunities
_Why is this a good project? What are some challenges you expect to face? How
might you overcome them? What are some warning signs that the project has gotten
off track, and how will you get the project back on track if needed?_

This project is good because I'm invested in the product,
and I think it could cover a range of topics, including meta-programming
and cross-file parsing. The most difficult thing I can currently think of
is cross-file parsing, but that seems common enough that there's probably
plenty of supporting materials for performing it. As far as the project
getting off track, I think it's most likely that the project will get off track
in terms of my consideration for language aspects. I think it will be easy
for me to focus on style, efficiency, and flowchart aesthetic,
so if I notice that I'm spending a lot of time on these things,
I should instead get to a place where the language is stable,
and continue thinking about how I can extend the language for the user,
which will probably result in a greater return on utility for the user.

[code2flow]: http://code2flow.com/
[Doxygen]: https://en.wikipedia.org/wiki/Doxygen
[Flowgen]: http://jlopezvi.github.io/Flowgen/index.html
[Flowgen Paper]: http://arxiv.org/pdf/1405.3240.pdf
[Javadoc]: https://en.wikipedia.org/wiki/Javadoc
