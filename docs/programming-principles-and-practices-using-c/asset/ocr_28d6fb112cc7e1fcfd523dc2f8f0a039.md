+   26. How do you copy C-style strings?
27. How do you find the length of a C-style string?
28. How would you copy a large array of **ints**?
29. What’s nice about `printf()`? What are its problems/limitations?
30. Why should you never use `gets()`? What can you use instead?
31. How do you open a file for reading in C?
32. What is the difference between **const** in C and **const** in C++?
33. Why don’t we like macros?
34. What are common uses of macros?
35. What is an include guard?

# Terms

`#define` Dennis Ritchie non-intrusive
`#ifdef` **FILE** opaque type
`#ifndef` `fopen()` overloading
Bell Labs format string `printf()`
Brian Kernighan intrusive `strcpy()`
C/C++ K&R structure tag
compatibility lexicographical three-way comparison
conditional compilation linkage **void**
C-style cast macro **void***
C-style string `malloc()`

# Exercises

For these exercises it may be a good idea to compile all programs with both a C and a C++ compiler. If you use only a C++ compiler, you may accidentally use non-C features. If you use only a C compiler, type errors may remain undetected.

+   1. Implement versions of `strlen()`, `strcmp()`, and `strcpy()`.
2. Complete the intrusive **List** example in §27.9 and test it using every function.
3. “Pretty up” the intrusive **List** example in §27.9 as best you can to make it convenient to use. Do catch/handle as many errors as you can. It is fair game to change the details of the **struct** definitions, to use macros, whatever.
4. If you didn’t already, write a C++ version of the intrusive **List** example in §27.9 and test it using every function.
5. Compare the results of exercises 3 and 4.