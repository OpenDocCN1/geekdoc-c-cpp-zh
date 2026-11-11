
languages allows the user to create iterators for user-defined data. The **foreach** statement of Perl and C# is a predefined iterator for standard data structures. In the contemporary object-oriented languages, iterators for collections are specified with standard interfaces, which are implemented by the designers of the collections.

Ruby includes iterators that are a special form of methods that are sent to various objects. The language predefines iterators for common uses, but also allows user-defined iterators.

The unconditional branch, or goto, has been part of most imperative languages. Its problems have been widely discussed and debated. The current consensus is that it should remain in most languages but that its dangers should be minimized through programming discipline.

Dijkstra’s guarded commands are alternative control statements with positive theoretical characteristics. Although they have not been adopted as the control statements of a language, part of the semantics appear in the concurrency mechanisms of CSP and the function definitions of Haskell.

## REVIEW QUESTIONS

- 1. What is the definition of *control structure*?
- 2. What did Böhm and Jacopini prove about flowcharts?
- 3. What is the definition of *block*?
- 4. What is/are the design issue(s) for all selection and iteration control statements?
- 5. What are the design issues for selection structures?
- 6. What is unusual about Python’s design of compound statements?
- 7. Under what circumstances must an F# selector have an else clause?
- 8. What are the common solutions to the nesting problem for two-way selectors?
- 9. What are the design issues for multiple-selection statements?
- 10. Between what two language characteristics is a trade-off made when deciding whether more than one selectable segment is executed in one execution of a multiple selection statement?
- 11. What is unusual about C#’s multiple-selection statement?
- 12. On what previous language was C#’s switch statement based?
- 13. Explain how C#’s switch statement is safer than that of C.
- 14. What are the design issues for all iterative control statements?
- 15. What are the design issues for counter-controlled loop statements?
- 16. What is a pretest loop statement? What is a posttest loop statement?
- 17. What is the difference between the *for* statement of C++ and that of Java?

- 8. In his paper on the goto issue, Knuth (1974) suggests a loop control statement that allows multiple exits. Read the paper and write an operational semantics description of the statement.
- 9. What are the arguments both for and against the exclusive use of Boolean expressions in the control statements in Java (as opposed to also allowing arithmetic expressions, as in C++)?
- 10. Describe a programming situation in which the else clause in Python's *for* statement would be convenient.
- 11. Describe three specific programming situations that require a posttest loop.
- 12. Speculate as to the reason control can be transferred into a C loop statement.

## PROGRAMMING EXERCISES

- 1. Rewrite the following pseudocode segment using a loop structure in the specified languages:

```
    k = (j + 13) / 27
    loop:
        if k > 10 then goto out
        k = k + 1
        i = 3 * k - 1
        goto loop
    out: . . .
```

    - a. C, C++, Java, or C#
    - b. Python
    - c. Ruby

Assume all variables are integer type. Discuss which language, for this code, has the best writability, the best readability, and the best combination of the two.

- 2. Redo Programming Exercise 1, except this time make all the variables and constants floating-point type, and change the statement

```
    k = k + 1
```

to

```
    k = k + 1.2
```

- 3. Rewrite the following code segment using a multiple-selection statement in the following languages:

```
    if ((k == 1) || (k == 2)) j = 2 * k - 1
    if ((k == 3) || (k == 5)) j = 3 * k + 1
    if (k == 4) j = 4 * k - 1
    if ((k == 6) || (k == 7) || (k == 8)) j = k - 2
```

    - a. C, C++, Java, or C#
    - b. Python
    - c. Ruby

Assume all variables are integer type. Discuss the relative merits of the use of these languages for this particular code.

- 4. Consider the following C program segment. Rewrite it using no gotos or breaks.

```
j = -3;
for (i = 0; i < 3; i++) {
    switch (j + 2) {
        case 3:
        case 2: j--; break;
        case 0: j += 2; break;
        default: j = 0;
    }
    if (j > 0) break;
    j = 3 - i;
}
```

- 5. In a letter to the editor of CACM, Rubin (1987) uses the following code segment as evidence that the readability of some code with gotos is better than the equivalent code without gotos. This code finds the first row of an n by n integer matrix named x that has nothing but zero values.

```
for (i = 1; i <= n; i++) {
    for (j = 1; j <= n; j++)
        if (x[i][j] != 0)
            goto reject;
    println ('First all-zero row is:', i);
    break;
reject:
}
```

Rewrite this code without gotos in one of the following languages: C, C++, Java, or C#. Compare the readability of your code to that of the example code.

- 6. Consider the following programming problem: The values of three integer variables—first, second, and third—must be placed in the three variables max, mid, and min, with the obvious meanings, without using arrays or user-defined or predefined subprograms. Write two solutions to this problem, one that uses nested selections and one that does not. Compare the complexity and expected reliability of the two.

- 7. Rewrite the C program segment of Programming Exercise 4 using if and goto statements in C.

- 8. Rewrite the C program segment of Programming Exercise 4 in Java without using a switch statement.

- 9. Translate the following call to Scheme's COND to C and set the resulting value to y.

```scheme
(COND
  ((> x 10) x)
  ((< x 5) (* 2 x))
  ((= x 7) (+ x 10))
)
```

## 9 Subprograms

- **9.1** Introduction
- **9.2** Fundamentals of Subprograms
- **9.3** Design Issues for Subprograms
- **9.4** Local Referencing Environments
- **9.5** Parameter-Passing Methods
- **9.6** Parameters That Are Subprograms
- **9.7** Calling Subprograms Indirectly
- **9.8** Design Issues for Functions
- **9.9** Overloaded Subprograms
- **9.10** Generic Subprograms
- **9.11** User-Defined Overloaded Operators
- **9.12** Closures
- **9.13** Coroutines

![](img/e22931b583977bc24a4263ee43d0f0bb_392_0.png)

Subprograms are the fundamental building blocks of programs and are therefore among the most important concepts in programming language design. We now explore the design of subprograms, including parameter-passing methods, local referencing environments, overloaded subprograms, generic subprograms, and the aliasing and problematic side effects that are associated with subprograms. We also include discussions of indirectly called subprograms, closures, and coroutines.

Implementation methods for subprograms are discussed in Chapter 10.

### 9.1 Introduction

Two fundamental abstraction facilities can be included in a programming language: process abstraction and data abstraction. In the early history of high-level programming languages, only process abstraction was included. Process abstraction, in the form of subprograms, has been a central concept in all programming languages. In the 1980s, however, many people began to believe that data abstraction was equally important. Data abstraction is discussed in detail in Chapter 11.

The first programmable computer, Babbage's Analytical Engine, built in the 1840s, had the capability of reusing collections of instruction cards at several different places in a program. In a modern programming language, such a collection of statements is written as a subprogram. This reuse results in savings in memory space and coding time. Such reuse is also an abstraction, for the details of the subprogram's computation are replaced in a program by a statement that calls the subprogram. Instead of describing how some computation is to be done in a program, that description (the collection of statements in the subprogram) is enacted by a call statement, effectively abstracting away the details. This increases the readability of a program by emphasizing its logical structure while hiding its low-level details.

The methods of object-oriented languages are closely related to the subprograms discussed in this chapter. The primary way methods differ from subprograms is the way they are called and their associations with classes and objects. Although these special characteristics of methods are discussed in Chapter 12, the features they share with subprograms, such as parameters and local variables, are discussed in this chapter.

### 9.2 Fundamentals of Subprograms

#### 9.2.1 General Subprogram Characteristics

All subprograms discussed in this chapter, except the coroutines described in Section 9.13, have the following characteristics:

- Each subprogram has a single entry point.
