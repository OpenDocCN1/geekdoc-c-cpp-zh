
with negative numbers. The eight moves may be described by two one-dimensional arrays, horizontal and vertical, as follows:

```cpp
horizontal[0] = 2    vertical[0] = -1
horizontal[1] = 1    vertical[1] = -2
horizontal[2] = -1   vertical[2] = -2
horizontal[3] = -2   vertical[3] = -1
horizontal[4] = -2   vertical[4] = 1
horizontal[5] = -1   vertical[5] = 2
horizontal[6] = 1    vertical[6] = 2
horizontal[7] = 2    vertical[7] = 1
```

Let the variables currentRow and currentColumn indicate the row and column of the knight’s current position. To make a move of type moveNumber, where moveNumber is between 0 and 7, your program uses the statements

```cpp
currentRow += vertical[ moveNumber ];
currentColumn += horizontal[ moveNumber ];
```

Keep a counter that varies from 1 to 64. Record the latest count in each square the knight moves to. Remember to test each potential move to see if the knight has already visited that square, and, of course, test every potential move to make sure that the knight does not land off the chessboard. Now write a program to move the knight around the chessboard. How many moves did the knight make?

- c) After attempting to write and run a Knight’s Tour program, you’ve probably developed some valuable insights. We’ll use these to develop a **heuristic** (or strategy) for moving the knight. Heuristics do not guarantee success, but a carefully developed heuristic greatly improves the chance of success. You may have observed that the outer squares are more troublesome than the squares nearer the center of the board. In fact, the most troublesome, or inaccessible, squares are the four corners.

Intuition may suggest that you should attempt to move the knight to the most troublesome squares first and leave open those that are easiest to get to, so when the board gets congested near the end of the tour, there will be a greater chance of success.

We may develop an “accessibility heuristic” by classifying each square according to how accessible it’s then always moving the knight to the square (within the knight’s L-shaped moves, of course) that is most inaccessible. We label a two-dimensional array accessibility with numbers indicating from how many squares each particular square is accessible. On a blank chessboard, each center square is rated as 8, each corner square is rated as 2 and the other squares have accessibility numbers of 3, 4 or 6 as follows:

| 2 | 3 | 4 | 4 | 4 | 4 | 3 | 2 |
|---|---|---|---|---|---|---|---|
| 3 | 4 | 6 | 6 | 6 | 6 | 4 | 3 |
| 4 | 6 | 8 | 8 | 8 | 8 | 6 | 4 |
| 4 | 6 | 8 | 8 | 8 | 8 | 6 | 4 |
| 4 | 6 | 8 | 8 | 8 | 8 | 6 | 4 |
| 4 | 6 | 8 | 8 | 8 | 8 | 6 | 4 |
| 3 | 4 | 6 | 6 | 6 | 6 | 4 | 3 |
| 2 | 3 | 4 | 4 | 4 | 4 | 3 | 2 |

Now write a version of the Knight’s Tour program using the accessibility heuristic.

At any time, the knight should move to the square with the lowest accessibility number. In case of a tie, the knight may move to any of the tied squares. Therefore, the tour may begin in any of the four corners. [*Note:* As the knight moves around the chessboard, your program should reduce the accessibility numbers more and more squares become occupied. In this way, at any given time during the tour, each available square’s accessibility number will remain equal to precisely the number of squares from

![](img/b42ba5cd262b1358d16610173f975e4d_367_0.png)

**Fig. 7.28** The 22 squares eliminated by placing a queen in the upper-left corner.

**7.26** *(Knight’s Tour: Closed-Tour Test)* In the Knight’s Tour, a full tour occurs when the knight makes 64 moves, touching each square of the board once and only once. A closed tour occurs when the 64th move is one move away from the location in which the knight started the tour. Modify the Knight’s Tour program you wrote in Exercise 7.22 to test for a closed tour if a full tour has occurred.

**7.27** *(The Sieve of Eratosthenes)* A prime integer is any integer that is evenly divisible only by itself and 1. The Sieve of Eratosthenes is a method of finding prime numbers. It operates as follows:

- a) Create an array with all elements initialized to 1 (true). array elements with prime subscripts will remain 1. All other array elements will eventually be set to zero. You’ll ignore elements 0 and 1 in this exercise.

- b) Starting with array subscript 2, every time an array element is found whose value is 1, loop through the remainder of the array and set to zero every element whose subscript is a multiple of the subscript for the element with value 1. For array subscript 2, all elements beyond 2 in the array that are multiples of 2 will be set to zero (subscripts 4, 6, 8, 10, etc.); for array subscript 3, all elements beyond 3 in the array that are multiples of 3 will be set to zero (subscripts 6, 9, 12, 15, etc.); and so on.

When this process is complete, the array elements that are still set to one indicate that the subscript is a prime number. These can then be printed. Write a program that uses an array of 1000 elements to determine and print the prime numbers between 2 and 999. Ignore element 0 of the array.

## Recursion Exercises

**7.28** *(Palindromes)* A palindrome is a string that is spelled the same way forward and backward. Examples of palindromes include “radar” and “able was I ere I saw elba.” Write a recursive function `testPalindrome` that returns true if a string is a palindrome, and false otherwise. Note that like an array, the square brackets (`[]`) operator can be used to iterate through the characters in a string.

**7.29** *(Eight Queens)* Modify the Eight Queens program you created in Exercise 7.24 to solve the problem recursively.

**7.30** *(Print an array)* Write a recursive function `printArray` that takes an array, a starting subscript and an ending subscript as arguments, returns nothing and prints the array. The function should stop processing and return when the starting subscript equals the ending subscript.

**7.31** *(Print a String Backward)* Write a recursive function `stringReverse` that takes a string and a starting subscript as arguments, prints the string backward and returns nothing. The function should stop processing and return when the end of the string is encountered. Note that like an array, the square brackets (`[]`) operator can be used to iterate through the characters in a string.

**7.32** *(Find the Minimum Value in an array)* Write a recursive function `recursiveMinimum` that takes an integer array, a starting subscript and an ending subscript as arguments, and returns the

## 8 Pointers

> Addresses are given to us to conceal our whereabouts.
>
> —Saki (H. H. Munro)

> By indirection find direction out.
>
> —William Shakespeare

> Many things, having full reference
> To one consent, may work contrariously.
>
> —William Shakespeare

> You will find it a very good practice always to verify your references, sir!
>
> —Dr. Routh

### Objectives

In this chapter you'll:

- Learn what pointers are.
- Learn the similarities and differences between pointers and references.
- Use pointers to pass arguments to functions by reference.
- Understand the close relationships between pointers and built-in arrays.
- Use pointer-based strings.
- Use built-in arrays.
- Use C++11 capabilities, including `nullptr` and Standard Library functions `begin` and `end`.

![](img/b42ba5cd262b1358d16610173f975e4d_369_0.png)

![](img/b42ba5cd262b1358d16610173f975e4d_370_0.png)

- **8.1** Introduction
- **8.2** Pointer Variable Declarations and Initialization
- **8.3** Pointer Operators
- **8.4** Pass-by-Reference with Pointers
- **8.5** Built-In Arrays
- **8.6** Using `const` with Pointers
  - 8.6.1 Nonconstant Pointer to Nonconstant Data
  - 8.6.2 Nonconstant Pointer to Constant Data
  - 8.6.3 Constant Pointer to Nonconstant Data
  - 8.6.4 Constant Pointer to Constant Data
- **8.7** `sizeof` Operator
- **8.8** Pointer Expressions and Pointer Arithmetic
- **8.9** Relationship Between Pointers and Built-In Arrays
- **8.10** Pointer-Based Strings
- **8.11** Wrap-Up

*Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises | Special Section: Building Your Own Computer*

### 8.1 Introduction

This chapter discusses *pointers*—one of the most powerful, yet challenging to use, C++ capabilities. Our goals here are to help you determine when it’s appropriate to use pointers, and show how to use them *correctly* and *responsibly*.

In Chapter 6, we saw that references can be used to perform pass-by-reference. Pointers also enable pass-by-reference and can be used to create and manipulate dynamic data structures that can grow and shrink, such as linked lists, queues, stacks and trees. This chapter explains basic pointer concepts. Chapter 19 presents examples of creating and using dynamic data structures that are implemented with pointers.

We also show the intimate relationship among *built-in arrays* and pointers. C++ inherited built-in arrays from the C programming language. As we saw in Chapter 7, the C++ Standard Library classes array and vector provide implementations of arrays as full-fledged objects—in fact, array and vector each store their elements in built-in arrays. *In new software development projects, you should favor array and vector objects to built-in arrays.*

Similarly, C++ actually offers two types of strings—string class objects (which we’ve been using since Chapter 3) and C-style, *pointer-based strings* (C strings). This chapter briefly introduces C strings to deepen your knowledge of pointers and built-in arrays. C strings were widely used in older C and C++ software. We discuss C strings in depth in Appendix F. *In new software development projects, you should favor string class objects.*

We’ll examine the use of pointers with class objects in Chapter 12, where we’ll see that the so-called “polymorphic referencing” associated with object-oriented programming is performed with pointers and references.

### 8.2 Pointer Variable Declarations and Initialization

*Indirection*

Pointer variables contain *memory addresses* as their values. Normally, a variable directly contains a specific value. A pointer contains the *memory address* of a variable that, in turn, contains a specific value. In this sense, a variable name *directly references a value*, and a pointer *indirectly references a value* (Fig. 8.1). Referencing a value through a pointer is
