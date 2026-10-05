If you have not programmed in C++ before, then the use of cin and cout for console I/O is likely to be new to you. That topic is covered little later in this chapter, but the general idea can be observed in this sample program. For example, consider the two lines from Display 1.1:

```
cout << "How many programming languages have you used? ";
cin >> numberOfLanguages;
```

The first line outputs the text within the quotation marks to the screen. The text inside the quotation marks is called a string, or to more precise, a C-string. The second line reads in a number that the user enters at the keyboard and sets the value of the variable numberOfLanguages to this number.

```
cout << "Read the preface. You may prefer\n"
 << "a more elementary book by the same author.\\n";
```

output strings instead of just one. The details are explained in Section 1.3 later in this chapter, but this brief introduction will enable you to understand the simple use of cin and cout in the examples that precede Section 1.3. The symbolism \n is the newline character, which instructs the computer to start a new line of output.

Although you may not be certain of the exact details of how to write statements, you can probably guess the meaning of the if-else statement. The details you need, you should read the preface to see if you might prefer a more elementary book.

(By the way, if you have not had at least some experience with programming languages, you should read the preface to see if you might prefer a more elementary book. You do not need have had any experience with C++ to read this book, but some minimal programming experience is strongly suggested.)

# 1.2 Variables, Expressions, and Assignment Statements

Once a person has understood the way variables are used in programming, he has understood the quintessence of programming.

> E. W. DIJKSTRA, Notes on Structured Programming

Variables, expressions, and assignments in C++ are similar to those in most other general-purpose languages.