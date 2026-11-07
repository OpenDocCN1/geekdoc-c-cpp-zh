
values of length and width, and because these values might be needed in more than one place in a program, we would like to know the locations where these values are stored and how to access those memory locations. C++ makes it easy for a programmer to specify the locations because the programmer can supply an alphabetic name for each of those locations. Of course, we must follow the rules to specify the names. For example, in the program in Figure 2-1, we are telling the system to allocate four memory spaces and name them `length`, `width`, `area`, and `perimeter`, respectively. (We will explain the meaning of the word `double`, shown in blue later in this chapter.) Essentially, a *variable* is a memory location whose contents can be changed. So `length`, `width`, `area`, and `perimeter` are variables. Also during program execution, the system will allocate four memory locations large enough to store decimal numbers and those memory locations will be named `length`, `width`, `area`, and `perimeter`, respectively (see Figure 2-2).

![](img/b217c421655b51e7494cf3b89bb5432d_82_0.png)

**FIGURE 2-2**  Memory allocation

The statement `length = 6.0;` will cause the system to store 6.0 in the memory location associated with the name (or identified by the name) `length`, see Figure 2-3. Examples 2-14 and 2-19 further illustrate how data is manipulated in variables.

![](img/b217c421655b51e7494cf3b89bb5432d_82_1.png)

**FIGURE 2-3**  Memory spaces after the statement `length = 6.0;` executes

As we proceed through this chapter, we will explain the meaning of the remaining parts identified in Figure 2-1.

## The Basics of a C++ Program

In the previous section, we gave an example of a C++ program and also identified certain parts of the program. In general, a C++ program is a collection of one or more subprograms, called functions. Roughly speaking, a **subprogram** or a **function** is a collection of statements, and when it is activated, or executed, it accomplishes something. Some functions, called **predefined** or **standard** functions, are already written and are provided as part of the system. But to accomplish most tasks, programmers must learn to write their own functions.

Every C++ program has a function called `main`. Thus, if a C++ program has only one function, it must be the function `main`. Until Chapter 6, other than using some of the predefined functions, you will mainly deal with the function `main`. By the end of this chapter, you will have learned how to write programs consisting only of the function `main`.

If you have never seen a program written in a programming language, the C++ program in Example 2-1 may look like a foreign language. To make meaningful sentences in a foreign language, you must learn its alphabet, words, and grammar. The same is true of a programming language. To write meaningful programs, you must learn the programming language's special symbols, words, and syntax rules. The **syntax rules** tell you which statements (instructions) are legal or valid, that is, which are accepted by the programming language and which are not. You must also learn **semantic rules**, which determine the meaning of the instructions. The programming language's rules, symbols, and special words enable you to write programs to solve problems.

**Programming language:** A set of rules, symbols, and special words.

In the remainder of this section, you will learn about some of the special symbols of a C++ program. Additional special symbols are introduced as other concepts are encountered in later chapters. Similarly, syntax and semantic rules are introduced and discussed throughout the book.

### Comments

The program that you write should be clear not only to you, but also to the reader of your program. Part of good programming is the inclusion of comments in the program. Typically, comments can be used to identify the authors of the program, give the date when the program is written or modified, give a brief explanation of the program, and explain the meaning of key statements in a program. In the programming examples, for the programs that we write, we will not include the date when the program is written, consistent with the standard convention for writing such books.

Comments are for the reader, not for the compiler. So when a compiler compiles a program to check for the syntax errors, it completely ignores comments. Throughout this book, comments are shown in green.

The program in Example 2-1 contains the following comments:

```cpp
//************************************************************
// Given the length and width of a rectangle, this C++ program
// computes and outputs the perimeter and area of the rectangle.
//************************************************************
```

There are two common types of comments in a C++ program—single-line comments and multiple-line comments.

Single-line comments begin with `//` and can be placed anywhere in the line. Everything encountered in that line after `//` is ignored by the compiler. For example, consider the following statement:

```
cout << "7 + 8 = " << 7 + 8 << endl;
```

You can put comments at the end of this line as follows:

```
cout << "7 + 8 = " << 7 + 8 << endl; //prints: 7 + 8 = 15
```

This comment could be meaningful for a beginning programmer.

Multiple-line comments are enclosed between `/*` and `*/`. The compiler ignores anything that appears between `/*` and `*/`. For example, the following is an example of a multiple-line comment:

```
/*
    You can include comments that can
    occupy several lines.
*/
```

In multiple-line comments, many programmers use single-line comments on every line to make the comments stand out more to the reader (as was done in the program in Example 2-1).

### Special Symbols

The smallest individual unit of a program written in any language is called a **token**. C++’s tokens are divided into special symbols, word symbols, and identifiers. Following are some of the special symbols:

|   |   |   |   |
|---|---|---|---|
| `+` | `-` | `*` | `/` |
| `.` | `;` | `?` | `,` |
| `<=` | `!=` | `==` | `>=` |

The first row includes mathematical symbols for addition, subtraction, multiplication, and division. The second row consists of punctuation marks taken from English grammar. Note that the comma is also a special symbol. In C++, commas are used to separate items in a list. Semicolons are also special symbols and are used to end a C++ statement. Note that a blank, which is not shown above, is also a special symbol. You create a blank symbol by pressing the space bar (only once) on the keyboard. The third row consists of tokens made up of two characters that are regarded as a single symbol. No character can come between the two characters in the token, not even a blank.

### Reserved Words (Keywords)

A second category of tokens is reserved word symbols. Some of the reserved word symbols include the following:

```
int, float, double, char, const, void, return
```

Reserved words are also called **keywords**. The letters that make up a reserved word are always lowercase. Like the special symbols, each is considered to be a single symbol. Furthermore, reserved words cannot be redefined within any program; that is, they cannot be used for anything other than their intended use. For a complete list of reserved words, see Appendix A.

> **NOTE** Throughout this book, reserved words are shown in blue.

### Identifiers

A third category of tokens is identifiers. Identifiers are names of things that appear in programs, such as variables, constants, and functions. All identifiers must obey C++’s rules for identifiers.

**Identifier:** A C++ identifier consists of letters, digits, and the underscore character (_) and must begin with a letter or underscore.

Some identifiers are predefined; others are defined by the user. In the C++ program in Example 2-1, `cout` is a predefined identifier and `length` is a user-defined identifier. Two predefined identifiers that you will encounter frequently are `cout` and `cin`. You have already seen the effect of `cout`. Later in this chapter, you will learn how `cin`, which is used to input data, works. Unlike reserved words, predefined identifiers can be redefined, but it would not be wise to do so.

Identifiers can be made of only letters, digits, and the underscore character; no other symbols are permitted to form an identifier.

> **NOTE** C++ is case sensitive—uppercase and lowercase letters are considered different. Thus, the identifier **NUMBER** is not the same as the identifier `number`. Similarly, the identifiers **X** and **x** are different.

In C++, identifiers can be of any length.

**EXAMPLE 2-2**

The following are legal identifiers in C++:

```
first
conversion
payRate
counter1
```

Table 2-1 shows some illegal identifiers and explains why they are illegal and also gives a correct identifier.
