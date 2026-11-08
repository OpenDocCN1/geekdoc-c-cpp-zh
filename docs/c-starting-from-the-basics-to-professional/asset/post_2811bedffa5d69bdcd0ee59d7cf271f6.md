
- The floating-point data types are `float`, `double`, and `long double`.
- Uninitialized variables generally contain garbage values. Variables may be given initial values when they're defined, and it's good programming practice to do so. A braced initializer is the preferred way of specifying initial values.
- A variable of type `char` can store a single character and occupies one byte. Type `char` may be signed or unsigned, depending on your compiler. You can also use variables of the types `signed char` and `unsigned char` to store integers. Types `char`, `signed char`, and `unsigned char` are different types.
- Type `wchar_t` stores a wide character and occupies either two or four bytes, depending on your compiler. Types `char8_t`, `char16_t`, and `char32_t` may be better for handling Unicode characters in a cross-platform manner.
- You can fix the value of a variable by using the `const` modifier. The compiler will check for any attempts within the program source file to modify a variable defined as `const`.
- The four main mathematic operations correspond to the binary `+`, `-`, `*`, and `/` operators. For integers, the modulus operator `%` gives you the remainder after integer division.
- The `++` and `--` operators are special shorthand for adding or subtracting one from a numeric variable. Both exist in postfix and prefix forms.
- You can mix different types of variables and constants in an expression. The compiler will arrange for one operand in a binary operation to be automatically converted to the type of the other operand when they differ.
- The compiler will automatically convert the type of the result of an expression on the right of an assignment to the type of the variable on the left when these are different. This can cause loss of information when the left-side type isn't able to contain the same information as the right-side type—`double` converted to `int`, for example, or `long` converted to `short`.
- You can explicitly convert a value of one type to another using the `static_cast<>()` operator.
- The `std::format()` function of the `<format>` module offers a multitude of options to tune the formatting of textual output.

### EXERCISES

The following exercises enable you to try what you've learned in this chapter. If you get stuck, look back over the chapter for help. If you're still stuck after that, you can download the solutions from the Apress website (www.apress.com/book/download.html), but that really should be a last resort.

- Exercise 2-1. Create a program that converts inches to feet and inches. In case you're unfamiliar with imperial units: 1 foot equals 12 inches. An input of 77 inches, for instance, should thus produce an output of 6 feet and 5 inches. Prompt the user to enter an integer value corresponding to the number of inches and then make the conversion and output the result.
- Exercise 2-2. Write a program that will compute the area of a circle. The program should prompt for the radius of the circle to be entered from the keyboard. Calculate the area using the formula area = pi * radius * radius, and then display the result.
- Exercise 2-3. For your birthday you've been given a long tape measure and an instrument that measures angles (the angle between the horizontal and a line to the top of a tree, for instance). If you know the distance, d, you are from a tree, and the height, h, of your eye when peering into your angle-measuring device, you can calculate the height of the tree with the formula h + d*tan(angle). Create a program to read h in inches, d in feet and inches, and angle in degrees from the keyboard, and output the height of the tree in feet.

  > **Note** There is no need to chop down any trees to verify the accuracy of your program. Just check the solutions on the Apress website!

- Exercise 2-4. Your body mass index (BMI) is your weight, w, in kilograms divided by the square of your height, h, in meters (w/(h*h)). Write a program to calculate the BMI from a weight entered in pounds and a height entered in feet and inches. A kilogram is 2.2 pounds, and a foot is 0.3048 meters.
- Exercise 2-5. Knowing your BMI with a precision higher than one decimal digit after the decimal point is, well, pointless. Adjust the program of Exercise 2-4 accordingly.
- Exercise 2-6. Reproduce Table 2-6 with a program, without hard-coding the numeric values or filling spaces, of course. If your command-line interface does not support Unicode characters (perfectly possible), you can replace π with "pi" and omit φ (the Greek letter "phi," in case you were wondering).
- Exercise 2-7. Add a row to your table of Exercise 2-6 for sin(π/4), showing the result with exponent notation and five digits after the decimal point. Make sure the exponent component begins with a capital E, not a lowercase e.
- Exercise 2-8. Here's an extra exercise for puzzle fans. Write a program that will prompt the user to enter two different positive integers. Identify in the output the value of the larger integer and the value of the smaller integer. Using the decision-making facilities of Chapter 5, this would be like stealing a piece of cake from a baby while walking in the park. What makes this a tough brain teaser, though, is that this can be done solely with the operators you've learned about in this chapter!

## CHAPTER 3: Working with Fundamental Data Types

In this chapter, we expand on the types that we discussed in the previous chapter and explain how variables of the basic types interact in more complicated situations. We also introduce some new features of C++ and discuss some of the ways that these are used.

In this chapter, you'll learn

- How the execution order in an expression is determined
- What the bitwise operators are and how you use them
- What variable scope is and what its effects are
- What the storage duration of a variable is and what determines it
- How you can define a new type that limits variables to a fixed range of possible values
- How you can define alternative names for existing data types

### Operator Precedence and Associativity

You already know that there is a priority sequence for executing arithmetic operators in an expression. You'll meet many more operators throughout the book, including a few in this chapter. In general, the sequence in which operators in an expression are executed is determined by the *precedence* of the operators. Operator precedence is just a fancy term for the priority of an operator.

Some operators, such as addition and subtraction, have the same precedence. That raises the question of how an expression such as a+b-c+d is evaluated. When several operators from a group with the same precedence appear in an expression, in the absence of parentheses, the execution order is determined by the *associativity* of the group. A group of operators can be *left-associative*, which means operators execute from left to right, or they can be *right-associative*, which means they execute from right to left.

Nearly all operator groups are left-associative, so most expressions involving operators of equal precedence are evaluated from left to right. The only right-associative operators are all unary operators, the various assignment operators, and the conditional operator. Table 3-1 shows the precedence and associativity of all the operators in C++. You haven't met most of these operators yet, but when you need to know the precedence and associativity of any operator, you'll know where to find it.

**Table 3-1. The Precedence and Associativity of C++ Operators**

| Precedence | Operators | Associativity |
|---|---|---|
| 1 | `::` | Left |
| 2 | `()` `[]` `->` `.`<br>Postfix `++` and `--` | Left |
| 3 | `!` `~`<br>Unary `+` and `-`<br>Prefix `++` and `--`<br>Address-of `&` and indirection `*`<br>C-style cast `(type)`<br>`sizeof`<br>`co_await` (related to coroutines, not discussed in this book)<br>`new` `new[]` `delete` `delete[]` | Right |
| 4 | `*` `->*` (pointers-to-members, not discussed in this book) | Left |
| 5 | `*` `/` `%` | Left |
| 6 | Binary `+` and `-` | Left |
| 7 | `<<` `>>` | Left |
| 8 | `<=>` | Left |
| 9 | `<` `<=` `>` `>=` | Left |
| 10 | `==` `!=` | Left |
| 11 | `&` | Left |
| 12 | `^` | Left |
| 13 | `\|` | Left |
| 14 | `&&` | Left |
| 15 | `\|\|` | Left |
| 16 | `?:` (conditional operator)<br>`*=` `/=` `%=` `+=` `-=` `&=` `\|=` `^=` `<<=` `>>=`<br>`throw`<br>`co_yield` (related to coroutines, not discussed in this book) | Right |
| 17 | `,` (comma operator) | Left |

Each row in Table 3-1 is a group of operators of equal precedence, and the rows are in precedence sequence, from highest to lowest. Let’s see a simple example to make sure that it’s clear how all this works. Consider this expression:

`x*y/z - b + c - d`

The `*` and `/` operators are in the same group with precedence that is higher than the group containing `+` and `-`, so the expression `x*y/z` is evaluated first, with a result of, say, `r`. The operators in the group containing `*` and `/` are left-associative, so the expression is evaluated as though it was `(x*y)/z`. The next step is the evaluation of `r - b + c - d`. The group containing the `+` and `-` operators is also left-associative, so this will be evaluated as `((r - b) + c) - d`. Thus, the whole expression is evaluated as though it was written as follows:

`((((x*y)/z) - b) + c) - d`
