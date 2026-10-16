2.6 Choose a feature that you think should be added to a programming language of your choice. Why should the feature be added? What needs to be stated about the feature to specify completely its behavior and interaction with other features?

2.7 In Ada, the end reserved word must be qualified by the kind of block that it ends: if . . . then . . . end if, loop . . . end loop, and so on. In Python, begin/end blocks of code are marked by indentation. Discuss the effect these conventions have on readability, writability, and security.

2.8 Should a language require the declaration of variables? Languages such as Lisp and Python allow variable names to be used without declarations, while C, Java, and Ada require all variables to be declared. Discuss the requirement that variables should be declared from the point of view of readability, writability, efficiency, and security.

2.9 Languages such as Lisp and Python are dynamically typed, whereas languages such as C++ and Java are statically typed. Discuss the costs and benefits of each kind of typing.

2.10 The semicolon was used as an example of a nonuniformity in C++. Discuss the use of the semicolon in C. Is its use entirely uniform?

2.11 Two opposing views on comments in programs could be stated as follows:

+   (a) A program should always contain elaborate comments to make it readable and maintainable.
+   (b) A program should be as much as possible self-documenting, with comments added sparingly only where the code itself might be unclear.

Discuss these two viewpoints from the point of view of language design. What design features might aid one viewpoint but not the other? What might aid both?

2.12 Here are two more opposing statements:

+   (a) A program should never run with error checking turned off. Turning off error checking after a program has been tested is like throwing away the life preserver when graduating from the pool to the ocean.
+   (b) A program should always have error checking turned off after the testing stage. Keeping error checking on is like keeping training wheels on a bike after you’ve entered a race.

Discuss (a) and (b) from the point of view of language design.

2.13 Discuss the following two views of language design:

+   (a) Language design is compiler construction.
+   (b) Language design is software engineering.

2.14 Two contrasting viewpoints on the declaration of comments in a programming language are represented by Ada and C: In Ada, comments begin with adjacent hyphens and end with the end of a line:

```
-- this is an Ada comment
```

In C, comments begin with /* and proceed to a matching */:

```
/* this is a C comment */
```

Compare these two comment features with respect to readability, writability, and reliability. C++ added a comment convention (two forward slashes) similar to that of Ada. Why didn’t C++ use exactly the Ada convention?