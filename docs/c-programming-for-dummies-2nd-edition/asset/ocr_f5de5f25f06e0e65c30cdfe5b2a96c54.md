# Operators

Mixed in with functions and keywords are various symbols collectively known as operators. Most of them are mathematic in origin, including traditional symbols like the plus (+), minus (−), and equal (=) signs.

Operators get thrown in with functions, keywords, and other parts of the C language; for example:

```
result = sqrt(value) + 5;
```

Here, the = and + operators are used to concoct some sort of mathematical mumbo jumbo.

Not all C language operators perform math. Appendix C lists the lot.

![](bbox=[0.12, 0.45, 0.22, 0.6])

# Variables and values

A program works by manipulating information stored in variables. A variable is a container into which you can stuff values, characters, or other forms of information. The program can also work on specific, unchanging values that I call immediate values:

```
result = sqrt(value) + 5;
```

In this example, result and value are variables; their content is unknown by looking at the code, and the content can change as the program runs. The number 5 is an immediate value.

C sports different types of variables, each designed to hold specific values or data types. Chapter 6 explains variables and values in more detail.

# Statements and structure

As with human languages, programming languages feature syntax — it’s the method by which the pieces fit together. Unlike English, where syntax can be determined by rolling dice, the method by which C puts together keywords, functions, operators, variables, and values is quite strict.

The core of the C language is the statement, which is similar to a sentence in English. A statement is an action, a direction that the program gives to the hardware. All statements end with a semicolon, the C language equivalent of a period:

```
beep();
```