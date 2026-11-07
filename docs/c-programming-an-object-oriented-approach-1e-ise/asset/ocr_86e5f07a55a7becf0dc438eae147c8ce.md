# **Program 3.26** Inputting integers in different bases (Continued)

```
    17 // Input second number in hexadecimal
    18 cout << "Enter the third number in hexadecimal: ";
    19 cin >> hex >> num3;
    20 // Output values
    21 cout << num1 << endl;
    22 cout << num2 << endl;
    23 cout << num3;
    24 return 0;
    25 }
```

```
    Run:
    Enter the first number in decimal: 124
    Enter the second number in octal: 76
    Enter the third number in hexadecimal: 2ab
    124
    62
    683
```

# ## 3.6 STATEMENTS

We have studied expressions, but we also need statements to create a program in the C++ language. A C++ program is made of a sequence of **statements**. Each statement is executed by the computer, in the order dictated by the program, to achieve the goal of the program.

If we compare the C++ language with a natural language such as English, we find that a statement in C++ plays the role of a sentence in a natural language. When reading text in English, for example, a sentence is a unit of information we must interpret and understand before moving to the next sentence. A statement in a C++ program is a command that the C++ running environment must execute before going to the next statement. However, a programming language, like C++, has some statements that change the order of execution to move from one point in the program to another.

C++ provides many different types of statements, each with a predefined task. We discuss only some of them here. We discuss the rest gradually in future chapters.

Some statements need a semicolon to terminate the statement. On the other hand, some statements do not need a semicolon because they have another token at the end that is used as a terminator.

> > Some statements need a semicolon at the end as the terminator,
> > but some already have a built-in terminator.

# ### 3.6.1 Declaration Statement

There are two terms in C++ that must be explained: *declaration* and *definition*. **Declaration** introduces an entity by mentioning its type and giving it a name (an identifier). **Definition**, on the other hand, means to allocate memory for the entity. There are many entities that need to be declared and defined for a complex program, but for now we limit ourselves only to variable and constant declaration.