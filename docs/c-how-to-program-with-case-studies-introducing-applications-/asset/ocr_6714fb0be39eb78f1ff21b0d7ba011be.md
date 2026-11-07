# # Outline

+   - 2.1 Introduction
+   - 2.2 A Simple C Program: Printing a Line of Text
+   - 2.3 Another Simple C Program: Adding Two Integers
+   - 2.4 Memory Concepts
+   - 2.5 Arithmetic in C
+   - 2.6 Decision Making: Equality and Relational Operators
+   - 2.7 Secure C Programming
+   
+   *Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises*

# ## 2.1 Introduction

The C language facilitates a structured and disciplined approach to computer-program design. This chapter introduces C programming and presents several examples illustrating many fundamental C features. We analyze each example one statement at a time. In Chapters 3 and 4, we introduce structured programming—a methodology that will help you produce clear, easy-to-maintain programs. We then use the structured approach throughout the remainder of the text. This chapter concludes with the first of our “Secure C Programming” sections.

# ## 2.2 A Simple C Program: Printing a Line of Text

We begin with a simple C program that prints a line of text. The program and its screen output are shown in Fig. 2.1.

```
```c
// fig02_01.c
// A first program in C.
#include <stdio.h>

// function main begins program execution
int main(void) {
    printf("Welcome to C!\n");
} // end function main
```
```

```
```
Welcome to C!
```
```

**Fig. 2.1** | A first program in C.

# ### Comments

Lines 1 and 2

```
```c
// fig02_01.c
// A first program in C.
```
```

begin with `//`, indicating that these two lines are comments. You insert comments to document programs and improve program readability. Comments do not cause the computer to perform actions when you execute programs—they’re simply ignored. It’s our convention in each program to use the line 1 comment to specify the file-