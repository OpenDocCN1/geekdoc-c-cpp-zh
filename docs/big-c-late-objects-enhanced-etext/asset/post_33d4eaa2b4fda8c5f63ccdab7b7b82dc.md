
## CHAPTER 2
## FUNDAMENTAL DATA TYPES
## CHAPTER GOALS
- To be able to define and initialize variables and constants
- To understand the properties and limitations of integer and floating-point numbers
- To write arithmetic expressions and assignment statements in C++
- To appreciate the importance of comments and good code layout
- To create programs that read and process input, and display the results
- To process strings, using the standard C++ string type

## CHAPTER CONTENTS
2.1 VARIABLES 26
SYN Variable Definition 27
SYN Assignment 30
CE1 Using Undefined Variables 33
CE2 Using Uninitialized Variables 33
PT1 Choose Descriptive Variable Names 33
PT2 Do Not Use Magic Numbers 34
ST1 Numeric Types in C++ 34
ST2 Numeric Ranges and Precisions 35
ST3 Defining Variables with auto 35

2.2 ARITHMETIC 36
CE3 Unintended Integer Division 39
CE4 Unbalanced Parentheses 40
CE5 Forgetting Header Files 40
CE6 Roundoff Errors 41
PT3 Spaces in Expressions 42
PT4 Casts 42
ST5 Combining Assignment and Arithmetic 42
C&S The Pentium Floating-Point Bug 43

2.3 INPUT AND OUTPUT 44
SYN Input Statement 44

2.4 PROBLEM SOLVING: FIRST DO IT BY HAND 47
WE1 Computing Travel Time 48
HT1 Carrying out Computations 48
WE2 Computing the Cost of Stamps 51

2.5 STRINGS 51
C&S International Alphabets and Unicode 55

![](img/d61019b035dd82beb581604273c0ee6b_64_0.png)

© sammeg/Stockphoto.

![](img/d61019b035dd82beb581604273c0ee6b_65_0.png)

Numbers and character strings (such as the ones on this display board) are important data types in any C++ program. In this chapter, you will learn how to work with numbers and text, and how to write simple programs that perform useful tasks with them.

### 2.1 Variables

When your program carries out computations, you will want to store values so that you can use them later. In a C++ program, you use variables to store values. In this section, you will learn how to define and use variables.

To illustrate the use of variables, we will develop a program that solves the following problem. Soft drinks are sold in cans and bottles. A store offers a six-pack of 12-ounce cans for the same price as a two-liter bottle. Which should you buy? (Twelve fluid ounces equal approximately 0.355 liters.)

In our program, we will define variables for the number of cans per pack and for the volume of each can. Then we will compute the volume of a six-pack in liters and print out the answer.

![](img/d61019b035dd82beb581604273c0ee6b_65_1.png)

cans: © blackred/Stockphoto. bottle: © travismanley/iStockphoto.

What contains more soda? A six-pack of 12-ounce cans or a two-liter bottle?

### 2.1.1 Variable Definitions

The following statement defines a variable named cans_per_pack:

```
int cans_per_pack = 6;
```

A variable is a storage location in a computer program. Each variable has a name and holds a value.

A variable is similar to a parking space in a parking garage. The parking space has an identifier (such as "J053"), and it can hold a vehicle. A variable has a name (such as cans_per_pack), and it can hold a value (such as 6).

> A variable is a storage location with a name.

![](img/d61019b035dd82beb581604273c0ee6b_65_2.png)

Like a variable in a computer program, a parking space has an identifier and contents.

Javier Larrea/Age Fotostock.

When defining a variable, you usually specify an initial value.

When defining a variable, you also specify the type of its values.

When defining a variable, you usually want to **initialize** it. That is, you specify the value that should be stored in the variable. Consider again this variable definition:

```
int cans_per_pack = 6;
```

The variable cans_per_pack is initialized with the value 6.

Like a parking space that is restricted to a certain type of vehicle (such as a compact car, motorcycle, or electric vehicle), a variable in C++ stores data of a specific **type**. C++ supports quite a few data types: numbers, text strings, files, dates, and many others. You must specify the type whenever you define a variable (see Syntax 2.1).

### Syntax 2.1 Variable Definition

Types introduced in this chapter are the number types int and double (see Table 2) and the string type (see Section 2.5).

```
int cans_per_pack = 6;
```

See Table 3 for rules and examples of valid names.

A variable definition ends with a semicolon.

Use a descriptive variable name. See Programming Tip 2.1.

Supplying an initial value is optional, but it is usually a good idea. See Common Error 2.2.

The cans_per_pack variable is an **integer**, a whole number without a fractional part. In C++, this type is called int. (See the next section for more information about number types in C++.)

Note that the type comes *before* the variable name:

```
int cans_per_pack = 6;
```

![](img/d61019b035dd82beb581604273c0ee6b_66_0.png)

Each parking space is suitable for a particular type of vehicle, just as each variable holds a value of a particular type.

Table 1 shows variations of variable definitions.

### Table 1 Variable Definitions in C++

| Variable Name | Comment |
|---|---|
| int cans = 6; | Defines an integer variable and initializes it with 6. |
| int total = cans + bottles; | The initial value need not be a constant. (Of course, cans and bottles must have been previously defined.) |
| int bottles = "10"; | Error: You cannot initialize a number with a string. |
| int bottles; | Defines an integer variable without initializing it. This can be a cause for errors—see Common Error 2.2. |
| int cans, bottles; | Defines two integer variables in a single statement. In this book, we will define each variable in a separate statement. |
| bottles = 1; | Caution: The type is missing. This statement is not a definition but an assignment of a new value to an existing variable—see Section 2.1.4. |

### 2.1.2 Number Types

Use the int type for numbers that cannot have a fractional part.

Use the double type for floating-point numbers.

In C++, there are several different types of numbers. You use the integer number type, called int in C++, to denote a whole number without a fractional part. For example, there must be an integer number of cans in any pack of cans—you cannot have a fraction of a can.

When a fractional part is required (such as in the number 0.355), we use floating-point numbers. The most commonly used type for floating-point numbers in C++ is called double. (If you want to know the reason, read Special Topic 2.1.) Here is the definition of a floating-point variable:

```
double can_volume = 0.355;
```

When a value such as 6 or 0.355 occurs in a C++ program, it is called a number literal. Table 2 shows how to write integer and floating-point literals in C++.

### Table 2 Number Literals in C++

| Number | Type | Comment |
|---|---|---|
| 6 | int | An integer has no fractional part. |
| -6 | int | Integers can be negative. |
| 0 | int | Zero is an integer. |
| 0.5 | double | A number with a fractional part has type double. |
| 1.0 | double | An integer with a fractional part .0 has type double. |
| 1E6 or 1e6 | double | A number in exponential notation: 1 x 10^6 or 1000000. Numbers in exponential notation always have type double. |

### 2.1.3 Variable Names

### Table 2 Number Literals in C++
| Number | Type | Comment |
|---|---|---|
| 2.96E-2 | double | Negative exponent: 2.96 x 10⁻² = 2.96 / 100 = 0.0296 |
| 🚫 100,800 |  | Error: Do not use a comma as a decimal separator. |
| 🚫 3 1/2 |  | Error: Do not use fractions; use decimal notation: 3.5. |

By convention, variable names should start with a lowercase letter.

When you define a variable, you should pick a name that explains its purpose. For example, it is better to use a descriptive name, such as can_volume, than a terse name, such as cv.

In C++, there are a few simple rules for variable names:

- 1. Variable names must start with a letter or the underscore (_) character, and the remaining characters must be letters, numbers, or underscores.
- 2. You cannot use other symbols such as $ or %. Spaces are not permitted inside names either. You can use an underscore instead, as in can_volume.
- 3. Variable names are case sensitive, that is, can_volume and Can_volume are different names. For that reason, it is a good idea to use only lowercase letters in variable names. It is also a convention among many C++ programmers that variable names should start with a lowercase letter.
- 4. You cannot use reserved words such as double or return as names; these words are reserved exclusively for their special C++ meanings. (See Appendix A.)

Table 3 shows examples of legal and illegal variable names in C++.

### Table 3 Variable Names in C++
| Variable Name | Comment |
|---|---|
| can_volume1 | Variable names consist of letters, numbers, and the underscore character. |
| x | In mathematics, you use short variable names such as x or y. This is legal in C++, but not very common, because it can make programs harder to understand (see Programming Tip 2.1). |
| ⚠ can_volume | Caution: Variable names are case sensitive. This variable name is different from can_volume. |
| 🚫 6pack | Error: Variable names cannot start with a number. |
| 🚫 can volume | Error: Variable names cannot contain spaces. |
| 🚫 double | Error: You cannot use a reserved word as a variable name. |
| 🚫 ltr/fl.oz | Error: You cannot use symbols such as . or / |
