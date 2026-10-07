# The C Preprocessor

The preprocessor is a part of all C compiler packages. When you compile a C program, the preprocessor is the first compiler component that processes your program. In most compilers, the preprocessor is part of the compiler program. When you run the compiler, it automatically runs the preprocessor.

The preprocessor changes your source code based on instructions, or *preprocessor directives*, in the source code. The output of the preprocessor is a modified source-code file that is then used as the input for the next compilation. Normally, you never see this file because the compiler deletes it after it's used. However, later in this lesson, you need to learn about the preprocessor directives, which all begin with the # symbol.

# The #define Preprocessor Directive

The #define preprocessor directive has two uses: creating symbolic constants and creating macros.

# Simple Substitution Macros Using #define

You learned about substitution macros in Lesson 3, "Storing Information: Variables and Constants," although the term used to describe them in that lesson was *symbolic constants*. You create a substitution macro by using `#define` to replace text with other text. For example, to replace `text1` with `text2`, you write

```
#define text1 text2
```

This directive causes the preprocessor to go through the entire source-code file, replacing every occurrence of `text1` with `text2`. The only exception occurs if `text1` is found within double quotation marks, in which case no change is made.

The most frequent use for substitution macros is to create symbolic constants, as explained in Lesson 3. For example, if your program contains the following lines:

```
#define MAX 1000
x = y * MAX;
z = MAX - 12;
```

during preprocessing, the source code is changed to read as follows:

```
x = y * 1000;
z = 1000 - 12;
```