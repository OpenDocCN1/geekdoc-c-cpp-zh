# 12. The Preprocessor

The preprocessor provides the tools that enable you to develop programs that are easier to develop, read, modify, and port to different systems. You can also use the preprocessor to literally customize the Objective-C language to suit a particular programming application or your own programming style.

The preprocessor is a part of the Objective-C compilation process that recognizes special statements that can be interspersed throughout a program. As its name implies, the preprocessor actually processes these statements before analysis of the Objective-C program itself takes place. Preprocessor statements are identified by the presence of a pound sign (#), which must be the first spacpace character on the line. As you will see, preprocessor statements have a syntax that is slightly different from that of normal Objective-C statements. We begin by examining the #define statement.

# The #define Statement

One of the primary uses of the #define statement is to assign symbolic names to program constants. The preprocessor statement

```
#define  TRUE  1
```

defines the name TRUE and makes it equivalent to the value 1. The name TRUE can subsequently be used anywhere in the program where the constant 1 could be used. Whenever this name appears, the preprocessor automatically substitutes its defined value of 1 into the program. For example, you might have the following Objective-C statement that uses the defined TRUE:

```
gameOver = TRUE;
```