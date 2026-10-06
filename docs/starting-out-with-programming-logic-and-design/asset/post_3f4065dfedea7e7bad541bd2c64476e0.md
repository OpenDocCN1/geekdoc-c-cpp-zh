
# Variable Initialization

When you declare a variable, you can optionally assign a value to it in the declaration statement. This is known as initialization. For example, the following statement declares a variable price and assigns the value 49.95 to:

```
Declare Real price = 49.95
```

We would say that this statement initializes the price variable with the value 49.95. The following statement shows another example:

```
Declare Integer length = 2, width = 4, height = 8
```

This statement initializes three variables. The length variable is initialized with the value 2, width is initialized with the value 4, and height is initialized with the value 8.

# Uninitialized Variables

An uninitialized variable is a variable that has been declared, but has not been initialized or assigned a value. Uninitialized variables are a common cause of logic errors in programs. Look at the following pseudocode:

```
Declare Real dollars
Display "I have , dollars , in my account."
```

In this pseudocode, we have declared the variable, but we have not initialized or assigned a value to it. Therefore, we do not know what value the variable holds. Nevertheless, we have used the variable in a Display statement.

You're probably wondering what a program would display. An honest answer would be "I don't know." This is because each language has its own way of handling uninitialized variables. Some languages have a default value as 0 to uninitialized variables. In many languages, however, uninitialized variables hold unpredictable values. This is because those languages set a place in memory for the variable, but an uninitialized variable holds the value that happens to be stored in its memory location. Programmers often refer to unpredictable values as "garbage.".

Uninitialized variables can cause logic errors that are hard to find in a program. This is especially true when an uninitialized variable is used in a calculation. For example, look at the following pseudocode, which is a modified version of Program 2-13. Can you spot the error?

```
Declare Real test1
Declare Real test2
Declare Real test3
Declare Real average
Set test1 = 88.0
Set test2 = 92.5
Set average = (test1 + test2 + test3) / 3
Display "Your average test score is " , average

```

> This pseudocode contains an error!

# 2.4 Variable Declarations and Types

This program will not work properly because the test3 variable is never assigned a value. The test3 variable will contain garbage when it is used in the calculation in line 8. This means that the calculation will result in an unpredictable value, which will be assigned to the average variable. A beginner programmer might have finding this error because he would initially assume that something is wrong with the math in line 8.

In the next section, we will discuss a debugging technique that will help uncover errors such as the one in the modified version of Program 2-13. However, as a rule you should always make sure that your variables either (1) are initialized with the correct value when you declare them, or (2) receive the correct value from an assignment statement or input statement before they are used for any other purpose.

# Numeric Literals and Data Type Compatibility

Many of the programs you have seen have numbers written into their pseudocode. For example, the following statement, which appears in Program 2-6, has the number 2.75 written into it.

```
Set dollars = 2.75
```

```
Set price = 100
```

And, the following statement, which appears in Program 2-7, has the number 100 written into it. A that is written into a program's code is called a numeric literal. If a numeric literal is written with a decimal point, such as 2.75, that numeric literal will be stored in the computer's memory as a Real and will be treated as a Real when the program runs. If a numeric literal does not have a decimal point, such as 100, that numeric literal will be stored in the computer's memory as an Integer and it will be treated as an Integer when the program runs.

This is important when you are writing assignment statements or initializing variables. In many languages, an error will occur if you try to store a value of one data type in a variable of another data type. For example, look at the following pseudocode:

```
Declare Integer i
Set i = 3.7 <--- This is an error!
```

The assignment statement will cause an error because it attempts to assign a real number, 3.7, in an Integer variable. The following pseudocode will also cause an error.

```
Declare Integer i
Set i = 3.0 <--- This is an error!
```

> NOTE: Most languages do not allow you to assign real numbers to Integer variables because Integer variables cannot hold fractional amounts. In many languages, however, you are allowed to assign an integer value to a Real variable without causing an error. Here is an example:
Declare Real r
Set r = 77
though the numeric literal 77 is treated as an Integer, it can be assigned to a Real variable without the loss of data.

Even though the numeric literal 3.0 does not have a fractional value (it is mathematically as the integer 3), it is still treated as a real number by the computer because it is written with a decimal point.

# Integer Division

Be careful when dividing an integer by another integer. In many programming languages, when an integer is divided by an integer the result will also be an integer. This behavior is known as integer division. For example, look at the following pseudocode:

```
Set number = 3 / 2
```

This statement divides 3 by 2 and stores the result in the number variable. What will be stored in number? You would probably assume that 1.5 would be stored in number because that's your calculator shows when you divide by 2. However, that is not will happen in many programming languages. Because the numbers 3 and 2 are both treated as integers, the programming language that you use might throw away the fractional part of the answer (Throwing the fractional part of a number is called truncation). As a result, the statement will store 1 in the number variable, not 1.5.

If you are using a language that behaves this way and you want to make sure that at least one of the operands yields a real number, or a Real variable.

> NOTE: In Java, C++, and C, the / operator throws away the fractional part of the result when operands are integers. In these languages the result of the expression 3/2 would be 1. In Visual Basic, the / operator does not throw away the fractional part of the answer. In Visual Basic, the result of the expression 3/2 would be 1.

# Checkpoint

- 25 What items do you usually specify with a declaration?
- 26 Does it matter when you write the variable?
- 27 What is variable initialization?
- 28 Do uninitialized variables pose any danger?
- 29 What is an variable?

# Named Constants

> CONCEPT: A named constant is a name that represents a value that cannot be changed during the execution. Assume that the following statement appears in a banking program that calculates data:

```
Set amount = balance * 0.69
```

# 2.5 Named Constants

In such program, two potential problems arise. First, it is not clear to anyone than 0.69. It appears to be an interest rate, but in some situations there are fees associated with loan payments. The second problem occurs if this number is used in other calculations throughout the program and must be changed. If the rate increases to 7.2 percent (You might change a unintended value in the program, and inadvertently cause a logic error.)

Both of these problems can be addressed using named constants. A named constant is a name that cannot be changed during the program's execution. The following is an example of how we declare named constants in our pseudocode:

```
Constant Real INTEREST_RATE = 0.069
```

This creates a constant named INTEREST_RATE. The constant's value is the Real number 0.069. Note that the declaration looks a variable declaration, except that we use Constant instead of Declare. Also notice that the name of the constant is written in all uppercase letters. This is a standard practice in most programming languages because it makes constants easily distinguishable from variable names. An initialization value must be given when declaring a constant

An advantage of using named constants is that they make programs self-explanatory. The following statement:

```
Set amount = balance * 0.069
```

can be changed to read

```
Set amount = balance * INTEREST_RATE
```

A new programmer can read the second statement and know what is happening. It is evident that balance is multiplied by the interest rate. Another advantage to this approach is that widespread changes can easily be made to the program. Let's say the interest rate changes, the initialization value in the declaration of the named constant is the only value that needs to be modified. If the rate increases to 7.2 percent, the declaration can be changed to the following:

```
Constant Real INTEREST_RATE = 0.072
```

The new value of 0.072 will then be used in each statement that uses the INTEREST_RATE.

> NOTE: A named constant cannot be assigned a value with a set statement. If a statement in a program attempts to change the value of a named constant, an error will occur.
