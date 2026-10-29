# TIP: (continued)

Check the documentation with your compiler to determine whether any special steps are needed to compile C++11 (or C++14) programs and to determine what language features are supported.

Variable declarations in C++ are similar to what they are in other programming languages. The following line from Display 1.1 declares the variable numberOfLanguages:

```
int numberOfLanguages;
```

The type int is one of the C++ types for whole numbers (integers).

If you have not programmed in C++ before, then the use of cin and cout for console I/O is likely to be new to you. That topic is covered a little later in this chapter, but the general idea can be observed in this sample program. For example, consider the following two lines from Display 1.1:

```
cout << "How many programming languages have you used? ";
 cin >> numberOfLanguages;
```

The first line outputs the text within the quotation marks to the screen. The text inside the quotation marks is called a string, or to be more precise, a C-string. The second line reads in a number that the user enters at the keyboard and sets the value of the variable numberOfLanguages to this number.

The lines

```
cout << "Read the preface. You may prefer\n"
    << "a more elementary book by the same author.\n";
```

output two strings instead of just one string. The details are explained in Section 1.3 later in this chapter, but this brief introduction will be enough to allow you to understand the simple use of cin and cout in the examples that precede Section 1.3. The symbolism \n is the newline character, which instructs the computer to start a new line of output.

Although you may not yet be certain of the exact details of how to write such statements, you can probably guess the meaning of the if-else statement. The details will be explained in the next chapter.

(By the way, if you have not had at least some experience with some programming languages, you should read the preface to see if you might prefer a more elementary book. You need not have had any experience with C++ to read this book, but some minimal programming experience is strongly suggested.)

# 1.2 Variables, Expressions, and Assignment Statements

> Once a person has understood the way variables are used in programming, he has understood the quintessence of programming.

> E. W. DIJKSTRA, Notes on Structured Programming, August 1969

string
C-string