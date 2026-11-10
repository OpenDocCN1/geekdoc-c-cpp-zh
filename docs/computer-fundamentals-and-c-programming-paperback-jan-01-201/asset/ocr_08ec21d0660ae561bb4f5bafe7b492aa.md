In 1989, the American National Standards Institute (ANSI) formally adopted a C standard called C89. This standard was adopted by the International Standards Organization (ISO) in 1990. C89 introduced a number of features not found in K&R C. These include a different way of declaring functions, the induction of additional keywords, and specific guidelines for setting the minimum size of data types (like `int`, `char`, etc.).

As hardware advanced from 8-bit computers (the original IBM PC) to 32- and 64-bit machines, the language had been continuously undergoing changes by the incorporation of new features. As business and academic institutions adopted these features, the need for a new standard was increasingly felt. In 1999, ANSI adopted the C99 standard, which was approved by ISO in 2000.

Many features found in the C99 standard were already offered by pre-C99 compilers. In fact, commenting using `//`, the `long long` data type and function *inlining* have been available in GCC long before C99 came into being. The C99 committee wisely decided to take into account these enhancements. This made the transition to C99 a lot easier for those organizations who have already been using many of its features. C11 (published in 2011) is the current C standard, which we'll occasionally refer to in this book.

This book is based on C89 because that is the version used by most C programmers today. However, the C99 features are also discussed in separate asides. Before writing programs, you will have to decide whether you want C89- or C99-compliance because only then can you make your programs portable. C was developed as a portable language and we’d better let it remain that way.

# WHAT NEXT?

Before we examine the statements supported by C, we need to thoroughly understand the properties of data that are used with these statements. The next chapter pursues this topic and paves the way for further examination of data in expressions.

# WHAT DID YOU LEARN?

A C program is first passed through a *preprocessor*, which processes lines beginning with a `#`. A *compiler* converts the preprocessed code to machine code but which is not ready to run. The *linker* adds the code of functions to the compiled output to create a standalone executable.

Any program logic can be implemented by using statements that feature *sequence*, *decision making* (like the *if* statement) and *repetition* (like the *while* statement).

The compiler detects *syntax errors* in a program. The executable is created only when the program is free from such errors. *Semantic errors* are detected only at runtime.

*Functions* are used to codify a set of statements that are used repeatedly. A *function declaration* specifies the number and type of arguments and the *definition* contains the implementation. It is necessary to only know how to call a standard function.