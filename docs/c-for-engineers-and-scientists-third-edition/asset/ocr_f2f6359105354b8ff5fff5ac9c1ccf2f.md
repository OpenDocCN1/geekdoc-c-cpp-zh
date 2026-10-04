# Problem Solving Using C++

In addition to C++'s identifier rules, a C++ function name must always be followed by parentheses. Also, a good function name should be a mnemonic (pronounced 'knee-mon-ic'), which is a well designed as a memory aid. For example, the function name degToRad() is a mnemonic for a function that converts degrees to radians. The name helps identify what the function does. Functions that aren't mnemonics should not be used because they convey no information about the function. Here are some examples of valid function names that aren't mnemonics:

```
easy() c3po() r2d2() theForce() mike()
```

Function names can also consist of mixed uppercase and lowercase letters, as in theForce(). This convention is increasingly common in C++, although it's not necessary. Identifiers in all uppercase letters are usually reserved for symbolic constants, covered in Section 3.5.

If you mix uppercase and lowercase letters, be aware that C++ is a case-sensitive language, meaning the compiler distinguishes between uppercase and lowercase letters. Therefore, in C++, the names TOTAL, total, TotAL are different identifiers.

# # The main ( )

As mentioned, a distinct advantage of using functions—and, as in Part Two, classes—is that you can plan the program's structure in order. You can also test and verify each function's operation separately to make sure it meets its objectives.

For functions to be placed and executed in order fashion, each C++ program must have one, and only one, function named main(). The main() function is referred to as a driver because it tells the sequence in which they execute (see Figure 2.3).

Figure 2.4 shows the main() function's structure. The first line of the function—in this case, main()—is referred to as a function header. This line is always the first line of a function and contains three pieces of information:

+   * What type of data, if any, is returned from the function
* The name of the function
* What type of data, if any, is sent to the function

The keyword before the function name defines the type of value returns when it has finished execution. When placing the function it returns an integer value. The parentheses following the function name are empty, no data is transmitted to the function when it runs (Data transmitted to a runtime is referred to as arguments of the function). The braces, { }, determine the beginning and end of the function body and enclose the statements. The statements inside the braces between what the function does, each of your statement must end with a semicolon ().

You'll be reading and writing many C++ functions. In fact, the focus of Part One is primarily about statements required to construct useful functions and how to combine data into useful classes and programs. Each program, however, must have one and only one main() function. You will learn how to pass data and return data

> Functions executed from main() can, in turn, execute other functions. Each function, always, returns to the function that initiated its execution. This is true even for main(), which returns to the operating system that was in effect when main() was initiated.