
success = true
else
{
    success = goNorth(maze, creature)
    if (success)
    {
        success = goWest(maze, creature)
        if (success)
        {
            success = goEast(maze, creature)
            if (success)
            {
                Mark square visited
                Backtrack south
            }
        }
    }
}
else
success = false
return success

The goWest function will examine all the paths that start at the square to the west of the present square as follows. If the square directly to the west is clear, is inside the maze, and has not been visited before, move into this square and mark it as part of the path. (Note that you are moving from the east.) Check whether you are at the exit. If you are, you're done. Otherwise, try to find a path to the exit from here by trying all paths leaving this square except the one going east (this would put you back in the square from which you just came) (as follows. Call goNorth, if it is not successful, call goWest; and if it is not successful, call goSouth. If goSouth is not successful, mark this square as visited, move back into the square to the east, and return. The functions goEast and goSouth are analogous to goWest and goNorth.

The input data to represent a maze is simple. For example, the previously given maze is represented by the following lines of input, which can be in a text file:

```
20 7      <- width and height of the maze in squares
0 18      <- row and column coordinate of maze exit
6 12      <- row and column coordinate of maze entrance
xxxxxxxxxxxxxxxxxx x
x   x
x xxxxx xxxxx x x
x xxxxx xxxxx x x
x xxxxx xxxxx xx x
x xxxxx xxxxx xx x
x xxxxxxxxxx xx x
xxxxxxxxxxxxxx xxxxxxx
```

After the first three lines of numeric data in the file, each of the next lines corresponds to a row in the maze, and each character in a line corresponds to a column in the maze. An x indicates a blocked square (part of the wall), and a blank indicates a clear square. This notation is convenient, because you can see what the maze looks like as you design it.

- 5. Write a program that will recognize and evaluate prefix expressions. First design and implement a class of prefix expressions. This class should contain methods to recognize and evaluate prefix expressions. This chapter discusses the algorithms you will need to implement these methods.

- 6. Implement a recognition algorithm for the language in Exercise 5.

- 7. Implement the algorithm described in this chapter to convert a prefix expression to postfix form.

- 8. The following is a grammar that allows you to omit parentheses in infix algebraic expressions when the precedence rules remove ambiguity. For example, a + b * c means a + (b * c). However, the grammar requires parentheses when ambiguity would otherwise result. That is, the grammar does not permit left-to-right association when several operators have the same precedence. For example, a / b * c is illegal. Notice that the definitions introduce factors and terms.

```
<expression> = <term>|<term> + <term>| <term> - <term>
<term> = <factor>|<factor>*<factor>| <factor>/<factor>
<factor> = <letter>|(<expression>)
<letter> = a | b | ... | z
```

The recognition algorithm is based on a recursive chain of subtasks: find an expression → find a term → find a factor. What makes this a recursive chain is that find an expression uses find a term, which in turn uses find a factor. Find a factor either detects a base case or uses find an expression, thus forming the recursive chain. The pseudocode for the recognition algorithm follows:

```
FIND AN EXPRESSION
// The grammar specifies that an expression is either a single term
// or a term followed by a + or a -, which then must be followed by a second term.
Find a term
if (the next symbol is + or -)
    Find a term
FIND A TERM
// The grammar specifies that a term is either a single factor or
// a factor followed by a * or a /, which must then be followed by a second factor.
Find a factor
if (the next symbol is * or /)
    Find a factor
FIND A FACTOR
// The grammar specifies that a factor is either a single letter (the base case) or
// an expression enclosed in parentheses.
// if (the first symbol is a letter)
Done
else if (the first symbol is a '(')
    Find an expression starting at the character after '('
    Check for ')'
else
    No factor exists
```

Design and implement a class of infix expressions, as described by the given grammar. Include a method to recognize a legal infix expression.

## Stacks

## Contents

- 6.1 The Abstract Data Type Stack 194
- 6.1.1 Developing an ADT During the Design of a Solution 194
- 6.1.2 Specifications for the ADT Stack 196
- 6.2 Simple Uses of a Stack 201
- 6.2.1 Checking for Balanced Braces 201
- 6.2.2 Recognizing Strings in a Language 203
- 6.3 Using Stacks with Algebraic Expressions 205
- 6.3.1 Evaluating Postfix Expressions 205
- 6.3.2 Converting Infix Expressions to Equivalent Postfix Expressions 206
- 6.4 Using a Stack to Search a Flight Map 210
- 6.5 The Relationship Between Stacks and Recursion 216
- Summary 218
- Exercises 218
- Programming Problems 221

## Prerequisites

- Chapter 1 Data Abstraction: The Walls
- C++ Interlude 1 C++ Classes

So far in this book, we have discussed data abstraction as it relates to the design of a solution, introduced C++ classes as a way to hide a solution’s implementation, introduced resizable arrays and linked nodes as data structures used in many ADT implementations, and developed recursion as a problem-solving technique that is useful in the construction of algorithms. The primary concerns of the remainder of this book are the aspects of problem solving that involve the management of data—that is, the identification and implementation of some of the more common data-management operations.

Our study of data management has three goals. The first is to identify useful sets of operations—that is, to identify abstract data types. The second goal is to examine applications that use these abstract data types. The third goal is to construct implementations for the abstract data types—that is, to develop data structures and classes. As you will discover, the nature of the operations of an abstract data type, along with the application in which you will use it, greatly influences the choice of its implementation.

The ADT bag discussed in Chapter 1 does not organize its data. However, you can organize data either by position or by value. In general, these organizations are appropriate for applications of rather different natures. For example, if an application needs to ask a question about the first person in a line, you should organize the data by position. On the other hand, if an application needs to ask a question about the employee named Smith, you should organize the data by value. Throughout the rest of this book, you will see several ADTs that use these two data organizations.

This chapter introduces a well-known ADT called a stack. You will see how the operations on a stack give it a last-in, first-out behavior. Two of the several applications of a stack that the chapter considers are evaluating algebraic expressions and searching for a path between two points. Finally, the chapter discusses the important relationship between stacks and recursion. We leave the implementations of the stack to the next chapter.

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_220_0.png)

## 6.1 The Abstract Data Type Stack

The specification of an abstract data type that you can use to solve a particular problem can emerge during the design of the problem's solution. The ADT developed in the following example happens to be an important one: the ADT stack.

### 6.1.1 Developing an ADT During the Design of a Solution

When you type a line of text on a keyboard, you are likely to make mistakes. If you use the Backspace key to correct these mistakes, each backspace erases the previous character entered. Consecutive backspaces are applied in sequence and so erase several characters. For instance, if you type the line

```
abcc<--dddd<--<--eg<-fg
```

where <- represents the backspace character, the corrected input would be abcdefg

How can a program read the original line and get the correct input? In designing a solution to this problem, you eventually must decide how to store the input line. In accordance with the ADT approach, you should postpone this decision until you have a better idea of what operations you will need to perform at the data.

A first attempt at a solution leads to the following pseudocode:

```
// Read the line, correcting mistakes along the way
// while (not end of line)
{
    Read a new character ch
    if (ch is not a '<-')
        Add ch to the ADT
    else
        Remove from the ADT (discard) the item that was added most recently
}
```

Initial draft of a solution
