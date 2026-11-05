
## C# FOR DATA PROCESSING

## Contents
Introduction 5
Welcome...................................................5
Reading the notes..........................................5
Getting a copy of the notes................................5
1 Computers and Programs 6
1.1 Computers...............................................6
1.2 Programs and Programming...............................8
1.3 Programming Languages..................................13
1.4 C#......................................................14
2 Simple Data Processing 18
2.1 A First C# Program.....................................18
2.2 Manipulating Data......................................26
2.3 Writing a Program......................................37
3 Creating Programs 52
3.1 Methods................................................52
3.2 Variables and Scope....................................58
3.3 Arrays..................................................61
3.4 Exceptions and Errors..................................65
3.5 The Switch Construction................................68
3.6 Using Files.............................................71
4 Creating Solutions 76
4.1 Our Case Study: Friendly Bank..........................76
4.2 Enumerated Types........................................76
4.3 Structures..............................................79
4.4 Objects, Structures and References.....................82
4.5 Designing With Objects.................................89
4.6 Static Items............................................94
4.7 The Construction of Objects............................98
4.8 From Object to Component...............................104
4.9 Inheritance.............................................109
4.10 Object Etiquette......................................119
4.11 The power of strings and chars........................124
4.12 Properties.............................................126
4.13 Building a Bank.......................................129
5 Advanced Programming 134
5.1 Generics and Collections...............................134
5.2 Storing Business Objects...............................138
5.3 Business Objects and Editing...........................148
5.4 A Graphical User Interface.............................153
5.5 Using Delegates.........................................162
5.6 Threads and Threading..................................163
- 5.7 Structured Error Handling .................................................. 171
- 5.8 Program Organisation .......................................................... 174
- 5.9 Debugging ........................................................................ 180
- 5.10 The End? ....................................................................... 183

## 6 Glossary of Terms ............................................................. 184
- Abstract ........................................................................ 184
- Accessor ....................................................................... 184
- Base ............................................................................. 184
- Call ............................................................................. 184
- Class ............................................................................ 184
- Code Reuse ...................................................................... 185
- Cohesion ......................................................................... 185
- Collection ........................................................................ 185
- Compiler .......................................................................... 185
- Component ......................................................................... 185
- Constructor ........................................................................ 185
- Coupling .......................................................................... 186
- Creative Laziness .................................................................. 186
- Delegate ........................................................................... 186
- Dependency ......................................................................... 186
- Event .............................................................................. 186
- Exception .......................................................................... 186
- Functional Design Specification ..................................................... 187
- Global Unique Identifier (GUID) ...................................................... 187
- Hierarchy .......................................................................... 187
- Immutable ........................................................................... 187
- Inheritance ........................................................................ 188
- Interface .......................................................................... 188
- Library ............................................................................ 188
- Machine code ....................................................................... 188
- Member ............................................................................. 188
- Metadata ........................................................................... 188
- Method ............................................................................. 188
- Mutator ............................................................................ 188
- Namespace .......................................................................... 189
- Overload ........................................................................... 189
- Override ........................................................................... 189
- Portable ........................................................................... 189
- Private ............................................................................ 189
- Property ........................................................................... 189
- Protected .......................................................................... 190
- Public ............................................................................. 190
- Reference .......................................................................... 190
- Signature .......................................................................... 190
- Source file ........................................................................ 190
- Static ............................................................................. 190
- Stream ............................................................................. 191
- Structure .......................................................................... 191
- Subscript .......................................................................... 191
- Syntax Highlighting ................................................................ 191
- Test harness ....................................................................... 191
- This ............................................................................... 191
- Typesafe ........................................................................... 192
- Unit test ........................................................................... 192
- Value type .......................................................................... 192

## Introduction

### Welcome
Welcome to the Wonderful World of Rob Miles™! This is a world of bad jokes, puns, and programming. In this book I'm going to give you a smattering of the C# programming language. If you have programmed before I'd be grateful if you'd still read the text. It is worth it just for the jokes and you may actually learn something.

If you have not programmed before, do not worry. Programming is not rocket science it is, well, programming. The bad news about learning to program is that you get hit with a lot of ideas and concepts at around the same time when you start, and this can be confusing. The keys to learning programming are:

- **Practice** – do a lot of programming and force yourself to think about things from a problem solving point of view
- **Study** – look at programs written by other people. You can learn a lot from studying code which other folk have created. Figuring out how somebody else did the job is a great starting point for your solution. And remember that in many cases there is no *best* solution, just ones which are better in a particular context, i.e. the fastest, the smallest, the easiest to use etc.
- **Persistence** – writing programs is hard work. And you have to work hard at it. The principle reason why most folks don't make it as programmers is that they give up. Not because they are stupid. However, don't get too persistent. If you haven't solved a programming problem in 30 minutes you should call time out and seek help. Or at least walk away from the problem and come back to it. Staying up all night trying to sort out a problem is not a good plan. It just makes you all irritable in the morning. We will cover what to do when it all goes wrong later in section 5.9.

### Reading the notes
These notes are written to be read straight through, and then referred to afterwards. They contain a number of *Programming Points*. These are based on real programming experience and are to be taken seriously. There are also bits written in a *C# Book*. These are really important and should be learnt by heart.

If you have any comments on how the notes can be made even better (although I of course consider this highly unlikely) then feel free to get in touch

Above all, enjoy programming.

Rob Miles  
rob@robmiles.com  
www.robmiles.com  
www.dcs.hull.ac.uk

### Getting a copy of the notes
These notes are made freely available to Computer Science students at the University of Hull.

The website for the book is at http://www.csharpcourse.com
