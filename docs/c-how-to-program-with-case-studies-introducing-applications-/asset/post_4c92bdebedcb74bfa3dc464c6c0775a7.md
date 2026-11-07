
of the array should be assigned values input from the keyboard. Print the array’s values. Next, reallocate the memory for the array to half of the current number of elements. Print the array’s remaining values to confirm they match the first half of the original array’s values.

**15.7** *(Command-Line Arguments)* Write a program that takes two filenames as command-line arguments, reads the first file’s characters one at a time and writes them to the second file in reverse order.

## Operator Precedence Chart

Operators are shown in decreasing order of precedence from top to bottom.

| Operator | Type | Associativity |
|---|---|---|
| `()` | parentheses (function-call operator) | left to right |
| `[]` | array subscript |  |
| `.` | member selection via object |  |
| `->` | member selection via pointer |  |
| `++` | unary postincrement |  |
| `--` | unary postdecrement |  |
| `++` | unary preincrement | right to left |
| `--` | unary predecrement |  |
| `+` | unary plus |  |
| `-` | unary minus |  |
| `!` | unary logical negation |  |
| `~` | unary bitwise complement |  |
| `(type)` | C-style unary cast |  |
| `*` | dereference |  |
| `&` | address |  |
| `sizeof` | determine size in bytes |  |
| `*` | multiplication | left to right |
| `/` | division |  |
| `%` | modulus |  |
| `+` | addition | left to right |
| `-` | subtraction |  |
| `<<` | bitwise left shift | left to right |
| `>>` | bitwise right shift |  |
| `<` | relational less than | left to right |
| `<=` | relational less than or equal to |  |
| `>` | relational greater than |  |
| `>=` | relational greater than or equal to |  |
| `==` | relational is equal to | left to right |
| `!=` | relational is not equal to |  |
| `&` | bitwise AND | left to right |

| Operator | Type | Associativity |
|---|---|---|
| ^ | bitwise exclusive OR | left to right |
| \| | bitwise inclusive OR | left to right |
| && | logical AND | left to right |
| || | logical OR | left to right |
| ?: | ternary conditional | right to left |
| = | assignment | right to left |
| += | addition assignment |  |
| -= | subtraction assignment |  |
| *= | multiplication assignment |  |
| /= | division assignment |  |
| %= | modulus assignment |  |
| &= | bitwise AND assignment |  |
| ^= | bitwise exclusive-OR assignment |  |
| |= | bitwise inclusive-OR assignment |  |
| <<= | bitwise left-shift assignment |  |
| >>= | bitwise right-shift assignment |  |
| , | comma | left to right |

## ASCII Character Set

In the following table, the digits in the left column are the left digits of the character code's decimal equivalent (0–127), and the digits in the top row are the right digits of the character code's decimal equivalent. For example, the character code for "A" in row number 6 and column number 5 is 65, and the character code for "&" in row number 3 and column number 8 is 38.

|   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|
| 0 | nul | soh | stx | etx | eot | enq | ack | bel | bs | ht |
| 1 | lf | vt | ff | cr | so | si | dle | dc1 | dc2 | dc3 |
| 2 | dc4 | nak | syn | etb | can | em | sub | esc | fs | gs |
| 3 | rs | us | sp | ! | " | # | $ | % | & | ' |
| 4 | ( | ) | * | + | , | - | . | / | 0 | 1 |
| 5 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | : | ; |
| 6 | < | = | > | ? | @ | A | B | C | D | E |
| 7 | F | G | H | I | J | K | L | M | N | O |
| 8 | P | Q | R | S | T | U | V | W | X | Y |
| 9 | Z | [ | \ | ] | ^ | _ | ` | a | b | c |
| 10 | d | e | f | g | h | i | j | k | l | m |
| 11 | n | o | p | q | r | s | t | u | v | w |
| 12 | x | y | z | { | | | } | ~ | del |

This page intentionally left blank

## Multithreading/Multicore and Other C18/C11/C99 Topics

![](img/43d318ad505997c339a3ea78d716d162_778_0.png)

### Objectives

In this appendix, you'll:

- Understand the purpose of C18.
- Learn the headers added in C99 and C11/C18.
- Initialize arrays and structs with designated initializers.
- Use data type bool to create boolean variables whose data values can be true or false.
- Perform arithmetic operations on complex variables.
- Learn about preprocessor enhancements.
- Use multithreading to improve performance on today's multicore systems.

### Outline

- C.1 Introduction
- C.2 Headers Added in C99
- C.3 Designated Initializers and Compound Literals
- C.4 Type bool
- C.5 Complex Numbers
- C.6 Macros with Variable-Length Argument Lists
- C.7 Other C99 Features
  - C.7.1 Compiler Minimum Resource Limits
  - C.7.2 The restrict Keyword
  - C.7.3 Reliable Integer Division
  - C.7.4 Flexible Array Members
  - C.7.5 Type-Generic Math
  - C.7.6 Inline Functions
  - C.7.7 __func__ Predefined Identifier
  - C.7.8 va_copy Macro
- C.8 C11/C18 Features
  - C.8.1 C11/C18 Headers
  - C.8.2 quick_exit Function
  - C.8.3 Unicode Support
  - C.8.4 _Noreturn Function Specifier
  - C.8.5 Type-Generic Expressions
  - C.8.6 Annex L: Analyzability and Undefined Behavior
  - C.8.7 Memory Alignment Control
  - C.8.8 Static Assertions
  - C.8.9 Floating-Point Types
- C.9 Case Study: Performance with Multithreading and Multicore Systems
  - C.9.1 Example: Sequential Execution of Two Compute-Intensive Tasks
  - C.9.2 Example: Multithreaded Execution of Two Compute-Intensive Tasks
  - C.9.3 Other Multithreading Features

### C.1 Introduction

The C99 (1999) and C11 (2011) standards refined and expanded C's capabilities. Since C11, there has been only one new version, C18¹ (2018). It "addressed defects in C11 without introducing new language features."² Some features added by the C99 and C11/C18 standards are designated as optional. Before using the features shown in this appendix, check that your compiler supports them. Our goal is to introduce these capabilities and provide resources for further reading.

We explain with complete code examples and code snippets designated initializers, compound literals, type bool and complex numbers. We provide brief explanations of additional features, including restricted pointers, reliable integer division, flexible array members, generic math, inline functions and return without expression.

We discuss C11/C18 capabilities, including improved Unicode® support, the function specifier _Noreturn, type-generic expressions, the quick_exit function, memory alignment control, static assertions, analyzability and floating-point types.

### C11/C18 Multithreading

A key feature of this appendix is Section C.9's introduction to multithreading. In today's multicore systems, the hardware can put multiple processors (cores) to work on different parts of your task. This enables the tasks (and the program) to complete faster. To take advantage of multicore architecture from C programs, you need to write multithreaded applications. When a program splits tasks into separate threads, a multicore system can run those threads in parallel—that is, simultaneously. Section C.9 first demonstrates two long-running calculations performed in sequence. Then we separate those calculations into two threads to demonstrate the significant performance improvement of running the threads in parallel on multiple cores.

1. ISO/IEC 9899:2018, Information technology — Programming languages — C, https://www.iso.org/standard/74528.html
2. https://en.wikipedia.org/wiki/C18_(C_standard_revision). Also http://www.iso-9899.info/wiki/The_Standard.

### C.2 Headers Added in C99

The following table lists the standard-library headers added in C99—these remain available in C11/C18. We’ll discuss the new C11/C18 headers in Section C.8.1.

| Header | Explanation |
|---|---|
| `<complex.h>` | Contains support for complex numbers (see Section C.5). |
| `<fenv.h>` | Provides information about the C implementation’s floating-point environment and capabilities. |
| `<inttypes.h>` | Defines portable integral types and provides format specifiers for them. |
| `<stdbool.h>` | Contains macros defining bool, true and false, used for boolean variables (see Section C.4). |
| `<stdint.h>` | Defines extended integer types and related macros. |
| `<tgmath.h>` | Provides type-generic macros that allow functions from <math.h> to be used with a variety of parameter types (see Section C.7). |

### C.3 Designated Initializers and Compound Literals

[This section can be read after Section 10.3.] Designated initializers allow you to initialize array elements by subscript and union or struct members by name. Figure C.1 shows that we can use designated initializers to initialize specific array elements.

```c
// fig_C01.c
// Initializing specific array elements with designated initializers.
#include <stdio.h>

int main(void) {
    int values[5] = {
        [0] = 123, // initialize element 0
        [4] = 456  // initialize element 4
    }; // semicolon is required

    // output array contents
    printf("values: ");

    for (size_t i = 0; i < 5; ++i) {
        printf("%d ", values[i]);
    }
}
```

Fig. C.1 | Initializing specific array elements with designated initializers. (Part 1 of 2.)
