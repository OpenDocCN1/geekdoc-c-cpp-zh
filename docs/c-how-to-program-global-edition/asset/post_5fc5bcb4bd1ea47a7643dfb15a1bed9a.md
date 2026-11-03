
## 12.20 (Recursively Print a List Backward)

Write a function printListBackward that recursively outputs the items in a list in reverse order. Use your function in a test program that creates a sorted list of integers and prints the list in reverse order.

## 12.21 (Recursively Search a List)

Write a function searchList that recursively searches a linked list for a specified value. The function should return a pointer to the value if it's found; otherwise, NULL should be returned. Use your function in a test program that creates a list of integers. The program should prompt the user for a value to locate in the list.

## 12.22 (Binary Tree Search)

Write function binaryTreeSearch that attempts to locate a specified value in a binary search tree. The function should take as arguments a pointer to the root node of the binary tree and a search key to be located. If the node containing the search key is found, the function should return a pointer to that node; otherwise, the function should return a NULL pointer.

## 12.23 (Level Order Binary Tree Traversal)

The program of Fig. 12.19 illustrated three recursive methods of traversing a binary tree—inorder traversal, preorder traversal, and postorder traversal. This exercise presents the level order traversal of a binary tree in which the node values are printed level-by-level starting at the root node level. The nodes on each level are printed from left to right. The level order traversal is not a recursive algorithm. It uses the queue data structure to control the output of the nodes. The algorithm is as follows:

- 1) Insert the root node in the queue
- 2) While there are nodes left in the queue,
   Get the next node in the queue
   Print the node's value
   If the pointer to the left child of the node is not NULL
     Insert the left child node in the queue
   If the pointer to the right child of the node is not NULL
     Insert the right child node in the queue.

Write function levelOrder to perform a level order traversal of a binary tree. The function should take as an argument a pointer to the root node of the binary tree. Modify the program of Fig. 12.19 to use this function. Compare the output from this function to the outputs of the other traversal algorithms to see that it worked correctly. [Note: You'll also need to modify and incorporate the queue-processing functions of Fig. 12.13 in this program.]

## 12.24 (Printing Trees)

Write a recursive function outputTree to display a binary tree on the screen. The function should output the tree row-by-row with the top of the tree at the left of the screen and the bottom of the tree toward the right of the screen. Each row is output vertically. For example, the binary tree illustrated in Fig. 12.22 is output as follows:

![](img/bf54db922e6fa8319cba11069e785521_542_0.png)

Note that the rightmost leaf node appears at the top of the output in the rightmost column, and the root node appears at the left of the output. Each column of output starts five spaces to the right of the previous column. Function outputTree should receive as arguments a pointer to the root node of the tree and an integer totalSpaces representing the number of spaces preceding the value to be output (this variable should start at zero so that the root node is output at the left of the screen). The function uses a modified inorder traversal to output the tree. The algorithm is as follows:

- While the pointer to the current node is not NULL
- Recursively call outputTree with the current node's right subtree and totalSpaces + 5.
- Use a for statement to count from 1 to totalSpaces and output spaces.
- Output the value in the current node.
- Recursively call outputTree with the current node's left subtree and totalSpaces + 5.

## Special Section: Building Your Own Compiler

In Exercises 7.27–7.29, we introduced Simpletron Machine Language (SML), and you implemented a Simpletron computer simulator to execute SML programs. In Exercises 12.25–12.29, we build a compiler that converts programs written in a high-level programming language to SML. This section “ties” together the entire programming process. You’ll write programs in this new high-level language, compile them on the compiler you build and run them on the simulator you built in Exercise 7.28. [Note: Due to the size of the descriptions for Exercises 12.25–12.29, we’ve posted them in a PDF document located at www.deitel.com/books/chtp8/.]

## 13

## C Preprocessor

## Objectives

In this chapter, you'll:

- Use #include to develop large programs.
- Use #define to create macros with and without arguments.
- Use conditional compilation to specify portions of a program that should not always be compiled (such as code that assists you in debugging).
- Display error messages during conditional compilation.
- Use assertions to test whether the values of expressions are correct.

![](img/bf54db922e6fa8319cba11069e785521_545_0.png)

- **13.1** Introduction
- **13.2** `#include` Preprocessor Directive
- **13.3** `#define` Preprocessor Directive:
  - Symbolic Constants
- **13.4** `#define` Preprocessor Directive: Macros
  - 13.4.1 Macro with One Argument
  - 13.4.2 Macro with Two Arguments
  - 13.4.3 Macro Continuation Character
  - 13.4.4 `#undef` Preprocessor Directive
  - 13.4.5 Standard Library Functions and Macros
  - 13.4.6 Do Not Place Expressions with Side Effects in Macros
- **13.5** Conditional Compilation
  - 13.5.1 `#if...#endif` Preprocessor Directive
  - 13.5.2 Commenting Out Blocks of Code with `#if...#endif`
  - 13.5.3 Conditionally Compiling Debugging Code
- **13.6** `#error` and `#pragma` Preprocessor Directives
- **13.7** `#` and `##` Operators
- **13.8** Line Numbers
- **13.9** Predefined Symbolic Constants
- **13.10** Assertions
- **13.11** Secure C Programming

*Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises*

## 13.1 Introduction

The C preprocessor executes *before* a program is compiled. Some actions it performs are:

- the inclusion of other files into the file being compiled,
- definition of symbolic constants and macros,
- conditional compilation of program code and
- conditional execution of preprocessor directives.

Preprocessor directives begin with #, and only whitespace characters and comments delimited by /* and */ may appear before a preprocessor directive on a line.

C has perhaps the largest installed base of “legacy code” of any modern programming language. It’s been in active use for more than four decades. As a professional C programmer, you’re likely to encounter code written many years ago using older programming techniques. To help you prepare for this, we discuss a number of those techniques in this chapter and recommend some newer techniques that can replace them.

## 13.2 #include Preprocessor Directive

The **#include** preprocessor directive has been used throughout this text. It causes a *copy* of a specified file to be included in place of the directive. The two forms of the **#include** directive are:

```
#include <filename>
#include "filename"
```

The difference between these is the location at which the preprocessor begins searches for the file to be included. If the filename is enclosed in angle brackets (< >)—used for standard library headers—the search is performed in an *implementation-dependent* manner, normally through predesignated compiler and system directories. If the filename is enclosed in *quotes*, the preprocessor starts searches in the *same* directory as the file being

## Good Programming Practice 13.2

By convention, symbolic constants are defined using only uppercase letters and underscores.

## 13.4 #define Preprocessor Directive: Macros

A macro is an identifier defined in a #define preprocessor directive. As with symbolic constants, the macro-identifier is replaced with replacement-text before the program is compiled. Macros may be defined with or without arguments. A macro without arguments is processed like a symbolic constant. In a macro with arguments, the arguments are substituted in the replacement text, then the macro is expanded—the replacement-text replaces the identifier and argument list in the program. A symbolic constant is a type of macro.

### 13.4.1 Macro with One Argument

Consider the following one-argument macro definition that calculates the area of a circle:

```
#define CIRCLE_AREA(x) ((PI) * (x) * (x))
```

#### Expanding a Macro with an Argument

Wherever CIRCLE_AREA(y) appears in the file, the value of y is substituted for x in the replacement-text, the symbolic constant PI is replaced by its value (defined previously) and the macro is expanded in the program. For example, the statement

```
area = CIRCLE_AREA(4);
```

is expanded to

```
area = ((3.14159) * (4) * (4));
```

then, at compile time, the value of the expression is evaluated and assigned to variable area.

#### Importance of Parentheses

The parentheses around each x in the replacement-text force the proper order of evaluation when the macro argument is an expression. For example, the statement

```
area = CIRCLE_AREA(c + 2);
```

is expanded to

```
area = ((3.14159) * (c + 2) * (c + 2));
```

which evaluates correctly because the parentheses force the proper order of evaluation. If the parentheses in the macro definition are omitted, the macro expansion is

```
area = 3.14159 * c + 2 * c + 2;
```

which evaluates incorrectly as

```
area = (3.14159 * c) + (2 * c) + 2;
```

because of the rules of operator precedence.

#### Error-Prevention Tip 13.2

Enclose macro arguments in parentheses in the replacement-text to prevent logic errors.
