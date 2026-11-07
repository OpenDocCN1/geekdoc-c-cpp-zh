
that makes the loop-continuation condition fail; recursion keeps producing simpler versions of the original problem until the base case is reached.

- Both iteration and recursion can occur infinitely: An infinite loop occurs with iteration if the loop-continuation test never becomes false; infinite recursion occurs if the recursion step does not reduce the problem each time in a manner that converges on the base case. Infinite iteration and recursion typically occur as a result of errors in a program's logic.

## Negatives of Recursion

Recursion has many negatives. It repeatedly invokes the mechanism, and consequently the overhead, of function calls. This can be expensive in both processor time and memory space. Each recursive call causes another copy of the function (actually only the function's variables) to be created; this can consume considerable memory. Iteration normally occurs within a function, so the overhead of repeated function calls and extra memory assignment is omitted. So why choose recursion?

## Recursion Is Not Required

Any problem that can be solved recursively can also be solved iteratively (nonrecursively). A recursive approach is chosen in preference to an iterative approach when the recursive approach more naturally mirrors the problem and results in a program that's easier to understand and debug. Another reason to choose a recursive solution is that an iterative solution may not be apparent.

## Recursion Examples and Exercises Throughout This Book

Most programming textbooks introduce recursion much later than we've done here. We feel that recursion is such a sufficiently rich and complex topic that it's better to introduce it earlier and spread the examples over the remainder of the text. The following table summarizes by chapter the recursion examples and exercises in the text.

| Recursion examples and exercises |  |  |
| --- | --- | --- |
| Chapter 5 | Print an array backward | Chapter 12 |
| Factorial function | Print a string backward | Search a linked list |
| Fibonacci function | Check whether a string is a palindrome | Print a linked list backward |
| Greatest common divisor | Minimum value in an array | Binary tree insert |
| Multiply two integers | Linear search | Preorder traversal of a binary tree |
| Raising an integer to an integer power | Binary search | Inorder traversal of a binary tree |
| Towers of Hanoi | Eight Queens | Postorder traversal of a binary tree |
| Recursive main | Chapter 7 | Printing trees |
| Visualizing recursion | Maze traversal | Chapter 13 |
| Chapter 6 | Chapter 8 | Selection sort |
| Sum of the elements of an array | Printing a string input at the keyboard backward | Quicksort |
| Print an array |  |  |

## Closing Observations

Let’s close this discussion with some observations that we make repeatedly throughout the book. Good software engineering is important, and high performance is important. So, we’ve included extensive software-engineering and performance tips throughout the book. Unfortunately, these goals are often at odds with one another. Good software engineering is key to making more manageable the task of developing the larger and more complex software systems we need. High performance is key to realizing the systems of the future that will place ever greater computing demands on hardware. Where do functions fit in here?

### Software Engineering

Dividing a large program into functions promotes good software engineering. But it has a price. A heavily functionalized program—compared to a monolithic (i.e., one-piece) program without functions—makes potentially large numbers of function calls. These consume execution time on a computer’s processor(s). Although monolithic programs may perform better, they’re more difficult to program, test, debug, maintain and evolve.

![](img/43d318ad505997c339a3ea78d716d162_276_0.png)

### Performance

Today’s hardware architectures are tuned to make function calls efficient. C compilers help optimize your code, and today’s hardware processors and multicore architectures are incredibly fast. For the vast majority of applications and software systems you’ll build, concentrating on good software engineering will be more important than high-performance programming. Nevertheless, in many applications and systems, such as game programming, real-time systems, operating systems and embedded systems, performance is crucial, so we include performance tips throughout the book.

![](img/43d318ad505997c339a3ea78d716d162_276_1.png)

### ✓ Self Check

1. **(True/False)** Dividing a large program into functions promotes good software engineering. But a heavily functionalized program—compared to a monolithic (i.e., one-piece) program without functions—makes a potentially large number of function calls. These consume execution time on a computer’s processor(s). Although monolithic programs may perform better, they’re more difficult to program, test, debug, maintain and evolve.
   
   **Answer:** True.

2. **(Multiple Choice)** Which of the following statements is *false*?
   - a) Recursion repeatedly invokes the mechanism, and consequently the overhead, of function calls. This can be expensive in both processor time and memory space.
   - b) Each recursive call causes another copy of the function’s statements and variables to be created; this can consume considerable memory.
   - c) Iteration normally occurs within a function, so the overhead of repeated function calls and extra memory assignment is omitted.
   - d) A recursive approach is chosen in preference to an iterative approach when the recursive approach more naturally mirrors the problem and results in a program that's easier to understand and debug.
   
   **Answer:** b) is false. Actually, each recursive call causes another copy of only the function's variables to be created.

## SEC 5.17 Secure C Programming—Secure Random-Number Generation

In Section 5.10, we introduced the rand function for generating pseudorandom numbers. This function is sufficient for textbook examples but is not meant for use in industrial-strength applications. According to the C standard document's description of function rand, "There are no guarantees as to the quality of the random sequence produced and some implementations are known to produce sequences with distressingly non-random low-order bits." The CERT guideline MSC30-C indicates that implementation-specific random-number generation functions must be used to ensure that the random numbers produced are not predictable—this is extremely important, for example, in cryptography and other security applications.

The guideline presents several platform-specific random-number generators that are considered to be secure. For more information, see guideline MSC30-C at https://wiki.sei.cmu.edu/. If you're building industrial-strength applications that require random numbers, you should investigate for your platform the recommended function(s) to use. For example:

- Microsoft Windows provides the BCryptGenRandom function, which is part of Microsoft's "Cryptography API: Next Generation:"
  https://docs.microsoft.com/en-us/windows/win32/seccng/cng-portal
- POSIX-based systems (such as Linux) provide a random function, which you can learn more about by executing the following command in a Terminal or shell:
  ```
  man random
  ```
- macOS's stdlib.h header provides the arc4random function, which you can learn more about by executing the following command in a macOS Terminal:
  ```
  man arc4random
  ```

### Self Check

1. **(True/False)** The CERT guideline MSC30-C indicates that implementation-specific random-number generation functions must be used to ensure that the random numbers produced are predictable—this is extremely important, for example, in cryptography and other security applications.
   
   **Answer: False.** Actually, the CERT guideline MSC30-C indicates that implementation-specific random-number generation functions must be used to ensure that the random numbers produced are not predictable.

## Summary

### Section 5.1 Introduction

- The best way to develop and maintain a large program is to divide (p. 180) it into several smaller pieces, each more manageable than the original program.

### Section 5.2 Modularizing Programs in C

- A function (p. 180) is invoked by a **function call** (p. 181), which specifies the function name and provides information (as arguments) that the function needs to perform its task.

### Section 5.3 Math Library Functions

- A function is invoked by writing its name followed by a left parenthesis, the argument (or a comma-separated list of arguments) and a right parenthesis.
- Each argument may be a constant, a variable or an expression.

### Section 5.4 Functions

- There are several motivations for “functionalizing” a program. The divide-and-conquer approach makes program development more manageable. Another is building new programs by using existing functions. Such software reusability is a key concept in object-oriented programming languages derived from C, such as C++, Java, C# (pronounced “C sharp”), Objective-C and Swift.
- With good function naming and definition, you can create programs from standardized functions that accomplish specific tasks, rather than custom code. This is known as abstraction. We use abstraction each time we use standard library functions like `printf`, `scanf` and `pow`. A third motivation is to avoid repeating code in a program. Packaging code as a function allows it to be executed from other program locations by calling that function.

### Section 5.5 Function Definitions

- The arguments passed to a function should match in number, type and order with the parameters (p. 185) in the function definition.
- When a program encounters a function call, control transfers from the point of invocation to the called function, the statements of that function execute, then control returns to the caller.
- A called function can return control to the caller in one of three ways. If the function does not return a value, control is returned when the function-ending right brace is reached, or by executing the statement

  ```c
  return;
  ```

  If the function does return a value, the statement

  ```c
  return expression;
  ```

  returns the value of `expression`.
- A local variable (p. 185) is known only in a function definition. Other functions are not allowed to know the names of a function’s local variables, nor is any function allowed to know the implementation details of any other function.
