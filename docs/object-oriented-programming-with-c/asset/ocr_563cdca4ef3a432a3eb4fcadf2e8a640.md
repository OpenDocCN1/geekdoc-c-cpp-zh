# Key Concepts

Errors and exceptions | Throwing mechanism | Multiple catching | Rethrowing exceptions | Exception handling mechanism | Catching mechanism | Catching all exceptions | Restricting exceptions thrown

# 13.1                                             Introduction

We know that it is very rare that a program works correctly first time. It might have bugs. The two most common types of bugs are *logic errors* and *syntactic errors*. The logic errors occur due to poor understanding of the problem and solution procedure. The syntactic errors arise due to poor understanding of the language itself. We can detect these errors by using exhaustive debugging and testing procedures.

We often come across some peculiar problems other than logic or syntax errors. They are known as *exceptions*. Exceptions are run time anomalies or unusual conditions that a program may encounter while executing. Anomalies might include conditions such as division by zero, access to an array outside of its bounds, or running out of memory or disk space. When a program encounters an exceptional condition, it is important that it is identified and dealt with effectively. ANSI C++ provides built-in language features to detect and handle exceptions which are basically run time errors.

Exception handling was not part of the original C++. It is a new feature added to ANSI C++. Today, almost all compilers support this feature. C++ exception handling provides a type-safe, integrated approach, for coping with the unusual predictable problems that arise while executing a program.

# 13.2                                     Basics of Exception Handling