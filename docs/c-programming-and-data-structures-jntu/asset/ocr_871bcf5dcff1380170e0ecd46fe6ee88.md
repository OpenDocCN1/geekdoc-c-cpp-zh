# C89 vs. C99: AN OVERVIEW

There are three general categories of changes between C89 and C99:

+   - Features added to C89
+   - Features removed from C89
+   - Features that have been changed or enhanced

Many of the differences between C89 and C99 are quite small, and clarify nuances of the C language.
This book will concentrate on the larger changes that affect the way programs are written.

# Features Added

Perhaps the most important features added by C99 are the new keywords:

+   - inline
+   - restrict
+   - _Bool
+   - _Complex
+   - _Imaginary

Other major additions include

+   - Variable-length arrays
+   - Support for complex arithmetic
+   - The long long int data type
+   - The //comment
+   - The ability to intersperse code and data
+   - Additions to the preprocessor
+   - Variable declarations inside the for statement
+   - Compound literals
+   - Flexible array structure members
+   - Designated initializers
+   - Changes to the printf() and scanf() family of functions
+   - The __func__ predefined identifier
+   - New libraries and headers

Most of the features added by C99 are innovations created by the standardization committee, of which many were based on language extensions offered by a variety of C implementations. In a few cases, however, features were borrowed from C++. The inline keyword and // style comments are examples. It is important to understand that C99 does not add C++-style classes, inheritance, or member functions. The consensus of the committee was to keep C as C.

# Features Removed

The single most important feature removed by C99 is the “implicit int” rule. In C89, in many cases when no explicit type specifier is present, the type int is assumed. This is not allowed by C99. Also removed is implicit function declaration. In C89, if a function was not declared before it is used, an implicit declaration is assumed. This is not supported by C99. Both of these changes may require existing code to be rewritten if compatibility with C99 is desired.