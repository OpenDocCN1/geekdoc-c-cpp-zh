According to the C standard committee, the next C standard is likely to be released in 2022.29

Because C is a hardware-independent, widely available language, C applications often can run with little or no modification on a wide range of computer systems.

# Self Check

+   1. *(Fill-In)* C evolved from two previous languages, ________ and ________.
+      **Answer:** BCPL, B.
+   
+   2. *(True/False)* It’s possible to write C programs that are portable to most computers.
+      **Answer:** True.

# 1.7 The C Standard Library and Open-Source Libraries

C programs consist of pieces called functions. You can program all the functions you need to form a C program. However, most C programmers take advantage of the rich collection of existing functions in the C standard library. Thus, there are really two parts to learning C programming:

+   - learning the C language itself, and
+   - learning how to use the functions in the C standard library.

Throughout the book, we discuss many of these functions. P. J. Plauger’s book *The Standard C Library* is must reading for programmers who need a deep understanding of the library functions, how to implement them and how to use them to write portable code. We use and explain many C library functions throughout this text.

*C How to Program, 9/e* encourages a building-block approach to creating programs. When programming in C, you’ll typically use the following building blocks:

+   - C standard library functions,
+   - open-source C library functions,
+   - functions you create yourself, and
+   - functions other people (whom you trust) have created and made available to you.

The advantage of creating your own functions is that you’ll know exactly how they work. The disadvantage is the time-consuming effort that goes into designing, developing, debugging and performance-tuning new functions. Throughout the book, we focus on using the existing C standard library to leverage your program-development efforts and avoid “reinventing the wheel.” This is called software reuse.

Using C standard library functions instead of writing your own versions can improve program performance, because these functions are carefully written to perform efficiently. Using C standard library functions instead of writing your own comparable versions also can improve program portability.

> 29. “Programming Language C—C2x Charter.” Accessed November 4, 2020. http://www.open-std.org/jtc1/sc22/wg14/www/docs/n2086.htm.