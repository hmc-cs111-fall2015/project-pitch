# Grouper

## Overview
_What's this project about, briefly?_
This project is a DSL for solving constraint problems, specifically creating groups for group projects from a larger pool where each student has demonstrated different interests, strengths, and weaknesses. This, potentially, could be slimmed down even more to computer science groups (such as clinic) that have a need for a PM, head designer, etc.


## The user and a language
This section describes who the project would serve and why a language might be a
good way to meet their needs.


### What's the need?
_What need is met by your idea? Who are you helping? What is that person's
experience like now? What would their experience be like if you could help 
them?_
Very often in school there is group work. In a subset of those times groups will split off, pick something to work on together and delve into a larger, more isolated project. Group make up is very important in these larger projects as a good/bad group could drastically alter the experience for everyone involved. If students that have similar interests and similar goals then a group could potentially create a great project that everyone involed is proud of, but if a group is made of different interests and some members are not as engaged then the project could end up with a fractured result potentially produced by some subsection of the group. The need met by my idea is the need to create groups that can consistently achieve the aforementioned positive result, and I am helping teachers by saving them time and students by protecting them from the aforementioned negative outcome. Currently teachers often will make these groups themselves, allow students to choose their groups, or randomly assign groups. The first possibility often works out, but requires significant work for the teacher and is infeasible for large class sizes. The second option can be fine sometimes but more often groups that are made up of friends (instead of groups chosen by interests and compatibility) can devolve. Finally, random groupings have a tendency to leave some groups in a good spot, some in an ok spot, and some pretty screwed. Thats not great, and i think it can be better. Imagine if every time there was a group project students could fill out a survey of keyword interests, discuss the amount of work they are interested in committing to the project (in my opinion if there is a group that is all ok with doing B work they should work together), and indicate whether they have interest in being a leader of the group and then the teacher could write some simple code in Grouper and out comes groups that are designed to suit every student's goals. Sounds much better to me.


### Why a language?
_Why is a DSL appropriate for your user(s)? How does it address the need?_
A DSL is appropriate for my users because in any given project there may be different keywords, group sizes, leadership positions, etc. that are unique to this project. A language allows the teacher to define what constraints matter and which constraints dont and provide her the flexibility to even input her own personal preferences about who would and would not work together etc. It addresses the need by allowing the teacher to simply input text that makes up the descriptions of each student and have that function as a program to return the groups that she needs.

### Why you?
_What excites you about this idea? How did you come up with it?_
I came up with this idea in discussion with Prof. Ben and since then I have gotten increasingly excited about it. I think that constraint solving is very interesting, but more importantly I think that the language design aspects of this project are intriguing. Additionally, from a user standpoint, I have been in many bad groups and many good ones and can testify first hand what a large difference a good group can make to my learning and the quality of my final product.


### Interface (syntax)
_How might the user interact with the language? What does programming look 
like? Why is this the right way to interact with the problem domain? Be careful
to distinguish between, e.g,. a graphical interface and a linguistic interface._ 

I am imagining a linguistic interface to start off but I also can picture, as my project develops, a GUI that maps directly to the linguistic interface (i dont think it would be too tough and would increase likelihood that it might be adopted by a broader range of teachers). I am imagining a syntax where at the top of the program the teacher specifies certain things such as the weight of different aspects of the constraint matcher (there would be defaults), students she would like to see work together or not work together, etc. This would be followed by a block of code for each student in which the relevant input data would be put in a formatted form something like:
Name:
Interests:
Leadership interests:
Commitment to A-level product:
Desired Group Members:
Undesired Group Members:

In the GUI I imagine a bunch of drop downs or text boxes, dunno yet.


### Operation (semantics)
_What might happen when a program runs? How does a program interact with the
user? What kinds of semantic (i.e., non-syntax) errors might occur, and how 
might they be communicated to the user?_
When a program runs it would be parsed into my constraint solver and then the logic would be run on it. Semantic erros might occur if people ask for contradictory constraints or if people ask for constraints that dont make sense. Those types of semantic errors are pretty relevant to most constraint solvers but not as much to my project because the _types_ of constraints allowed would be limited and since we are dealing with one type of object (students) then it would be pretty hard to get a constraint that didnt make sense. Both would still be possible though. I think I would communicate them to the user through command line errors.


### Expressiveness
_What should be easy to do in this language? What should be possible, but
difficult? What should be impossible or very difficult?_
It should be _really, really easy_ to get groups of students based on their interests and preferences and I think it should be __impossible__ to do anything else. I could imagine that someone might be able to misuse it to solve some other type of constraint problem but I think it would be very difficult. I can't think of anything in the middle category of hard but possible.


### Related work
_Are there any other DSLs in this domain? If not, describe how you know there
aren't and conjecture why not. If so, describe them and provide links. How well 
do they address the need? Are there any particularly admirable qualities of the
language? Are there parts of the language you think could be improved?_
There are plenty of languages to solve constraint problems in general such as [AIMMS](https://en.wikipedia.org/wiki/AIMMS), [Oz](https://en.wikipedia.org/wiki/Oz_(programming_language)), and [Curry](https://en.wikipedia.org/wiki/Curry_(programming_language)) but none that are as specifically targeted as mine. They all are more GPL like for solving problems with constraints, but I think that my idea of a language that solves a particular constraint problem is unique.


## The Project
This section examines whether the idea makes for a good CS 111 project.


### Suitability
_What percentage of your time do you think will be spent directly engaging in
the **language** aspects of this project (e.g., making language design
decisions), as opposed to "systems" aspects of the project (e.g., implementing a
complicated semantics that doesn't require a lot of language design)?_

I think that a significant portion of my time would be spent with language aspects, but I do recognize the pretty significant systems portion of actually building the constraint solver. One thing that I think would push me further into the language design decisions area would be the creation of the GUI which would essentially double the amount of decisions I have to make because, as we all know, GUIs are DSLs also! I think I would shoot for 50/50.


### Scope
_How big an idea is this? How ambitious is this project?_
I think this is a pretty big project, especially if I build the GUI but, as I dont have much experience with constraint solvers, I dont know how much of my time that will take up. I think its ambitious but in a good way ie. it excites me and feels daunting but I also feel ready to dive in.


### Challenges and opportunities
_Why is this a good project? What are some challenges you expect to face? How
might you overcome them? What are some warning signs that the project has gotten
off track, and how will you get the project back on track if needed?_

I think this is a good project because it solves a problem that is relevant to my life but also to the life of almost every student at the 5Cs and colleges everywhere. I expect to face significant problems with building the parser and designing the syntax and I bet that the constraint solver itself will be pretty hard as well. I am thinking a lot about how I will actually weight the constraints. Most of these challenges are challenges that simply require me to work hard and learn in order to overcome them. I think that I will know that the project has gotten off track if I start feeling like i _dont want to work on it_. When I'm doing CS homework I almost always am excited to do it and like to dive in and spend hours and hours on it but I also have gotten to times in assignments that are going badly where I just abandon them in the back of my mind. If this happens I will leverage my advisor at Pomona (prof Chen) as well as Prof. Ben to help figure out what is going wrong and how I can get back on track mentally, as well as with the coding.

