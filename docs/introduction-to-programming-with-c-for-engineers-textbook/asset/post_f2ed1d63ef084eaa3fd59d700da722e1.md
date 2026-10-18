
1. a. On a sheet of paper, work out an example: for instance, setting a = 255 and b = 221.
   b. Implement Algorithm 2.2. Hint: To implement the loop use the statement `while (b != 0)`, or `for ( ; b != 0 ; ) { loop statements 2-4 }`.
   c. Verify the operation of your program by setting different values of a and b.

2. Analyze the following bisection algorithm for computing an approximation of the square root from an integer value.
   a. Write an implementation of Algorithm 2.3.
   b. Compare the returned values with those produced by the code in Listing 2.1.

3. The bisection algorithm has other applications. It is helpful in search tasks over monotonic values (https://en.wikipedia.org/wiki/Bisection_method). Use the bisection algorithm to find the root of a function (i.e. its zero-crossing point).

4. There can be problems when entering values using the `std::cin` object. For example, on line [14] of Listing 2.2, a numeric value is expected, but the user can enter `abc`. To prevent such errors, the status of the reading operation can be checked as in the following code snippet:

```cpp
if( ! ( cin >> C_0 ) )
{
    cout << "Error entering a value\n" << endl;
    return -1;
}
```

|                      |                                            |                                    |
|----------------------|--------------------------------------------|------------------------------------|
| Input:               | An integer value x                         |                                    |
| Output:              | Approximation of the square root of x      |                                    |
| 1                    | lower_bnd ← 1                              |                                    |
|                      | upper_bnd ← x / 2                          | (for x > 4 sqrt cannot be larger) |
| 2                    | while upper_bnd >= lower_bnd               | (iterate as long as fulfilled)    |
| 3                    | mid_val ← (lower_bnd + upper_bnd) / 2      | (compute a middle value)          |
| 4                    | if mid_val * mid_val > x                   | (check which half)                |
| 5                    | upper_bnd ← mid_val - 1                    | (lower the upper bound)           |
| 6                    | else                                       |                                    |
| 7                    | lower_bnd ← mid_val + 1                    | (advance the lower bound)         |
| 8                    | Return: (lower_bnd + upper_bnd) / 2        | (return a middle value)           |

This works because the `cin >> C_0` expression converts to a bool value of true or false, depending on whether the insertion succeeded or not, respectively. Then, the `!` operator negates this result, so if false was returned, the code inside `if` is executed, and the program terminates.
Using this method, update the value-reading lines of code in Listings 2.2 and 2.3.

5. Refactor the *CharHistogram* source code in Listing 2.3 to print the histogram as vertical bars composed of the `*` symbol, rather than numbers of occurrences.

6. A second-order polynomial can be expressed as follows

$$ax^2 + bx + c = 0$$

where $a$, $b$, and $c$ denote real coefficients. The question is whether there are values of $x$ that fulfill this equation. If they exist, they are called *roots* of the second-order polynomial. Recall that to answer this question, it is sufficient to compute the delta coefficient $d$ as follows:

$$d = b^2 - 4ac$$

If $d \ge 0$, we can compute the solution to Eq. (2.4) (its roots) as follows:

$$x_1 = \frac{-b-\sqrt{d}}{2a}, \quad x_2 = \frac{-b+\sqrt{d}}{2a}$$

Otherwise, there are no roots. Write a C++ program that asks the user for the three coefficients $a$, $b$, and $c$; resolves whether there are roots; and, if possible, computes them. First rewrite the previous equations into equivalent C++ expressions, and then adapt them.

7. Implement the *Secret Chamber* game – its 10×10 grid board looks as follows.

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_53_0.png)

You can move a player ‘P’ up, down, left, or right but only one position at a time (e.g. by pressing the buttons ‘U’, ‘D’, ‘L’ and ‘R’). You win if you step ‘P’ onto the treasure ‘T’. However, you lose if you step onto one of the traps ‘X’. Moreover, at each turn ‘X’ can randomly change its position by one spot. Pay attention not to step outside of the game board range.

8. Compute a sum of two positive integer values. However, the sum to compute is given as a string, e.g. “123 + 37”, “78 + 99”, etc. Write a program that performs the following steps:
   a. Prompt a user to enter a string;
   b. Eliminate extra spaces from the string;
   c. Extract the two substrings representing the two arguments, such as “123” and “37”;
   d. Compute integer values of these two substrings, so “123” is transformed to the value 123, etc.
   e. Print the sum of the two values;
   f. Extend your solution to handle potential errors.

9. There are many ways to compare texts. A simple one is to compare the two histograms of their letter occurrences. Two histograms of the same length can be compared by summing up squares of differences of the corresponding bin values.
   a. Extend the program from Listing 2.3 to compute and compare histograms of two texts.
   b. Test your procedure comparing few paragraphs.
   c. Better results will be obtained if the histograms are normalized before the comparison. After normalization, the sum of all bins in a histogram is 1.0. To normalize the histogram, divide each of its bin values by the total sum of all bins in that histogram. Hint: make the histogram vector to store floating-point values, e.g. in line [14] of Listing 2.3 change the initialization value from 0 to 0.0.

This chapter presents the basics of the C++ programming language. The top-level programming topics we will learn about are as follows:

- Constants, variables, `auto`, and built-in data types
- Common containers and algorithms from the Standard Library
- Basics of data structures and their initialization
- Introduction to classes
- Indirect object access with references
- Indirect object access with pointers
- C++ statements
- Functions, passing objects from and to functions, and lambda functions
- C++ operators

We will analyze and present detailed implementations of several projects that we hope will be interesting. Our goal is to show some programming techniques and, in particular, C++ features in action.

To perform computations, we need to represent data and define operations on it. Data is stored in the dedicated computer’s memory regions as what we will call *objects*, although we will extend this concept soon. All computer languages have ways to reserve sufficient memory, initialize such objects, and read from and/or write to them. However, all of them require a means of access. This can be

- *Direct*, by providing a direct name for an object, or
- *Indirect*, by providing a *link* to an object (a reference or a pointer)

Objects can be further divided into the following two groups:

- *Mutable* – After creation and initialization, the objects can be further changed. These are also all variables
- *Immutable* – Such objects can be created and initialized, but they cannot be changed. These are called constants

Soon we will see that objects can contain operations, which is one of the paradigms of the object-oriented programming. However, in this section we will focus on aspects related to representing data.

Figure 3.1 depicts three stages of variable creation and initialization and their imprint in the computer’s memory. In raw memory, each byte has an undefined value. Defining a variable by instructing the computer to perform `char c` reserves a byte of memory in the computer’s address space, as shown in Figure 3.1b. As a result, instead of writing a numeric address, we use the identifier of an object, such as `c` in this example. However, `c` still contains a garbage value, so it has to be initialized. Initializing writes a known value (state) to a variable. In our case, this is `'Z'` – that is, code for the letter Z.

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_56_0.png)

**Figure 3.1** Stages of variable (object) creation and initialization and their imprint in the computer’s memory. In raw memory, each byte has an undefined value (a). Defining a variable by instructing the computer to perform `char c` reserves a byte of memory in the computer’s address space. Instead of writing addresses, we use its identifier, `c` (b). However, `c` is not initialized, so it can contain any value. Initializing sets a known value to the variable. In our case this is code of the letter ‘Z’, i.e. `0x5A` in the hexadecimal representation (c).

We stress here that although it is possible to write and compile an uninitialized variable, such as

```cpp
char c;   // Avoid uninitialized objects!
```

the object can then have *any value* that happened to be in memory! This can lead to serious errors that are difficult to spot. Therefore, *always initialize all the objects you create*! In C++, it is sufficient to add `{}`, as follows:

```cpp
char c {};   // Ok :)
```

When creating an object, consider the following aspects:

- Choose a name for the object¹ that reflects important information about the object’s role in the code. In C++, a name for an object, such as a variable, constant, function, structure, or class,

¹ The notion of an object is a broad concept in computer science. It is a construct placed in a memory, such as a variable or a constant of a given type. In object-oriented programming, a structure or a class denotes a type, which is an abstract concept, whereas instantiations of these types that reside in memory are objects. However, in some interpretations, a function is also considered an object. Objects in the object-oriented context will be discussed further in Section 3.9.
