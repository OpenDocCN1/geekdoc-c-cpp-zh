
# Pitfall UNINITIALIZED VARIABLES

A variable has no meaningful value until a program gives it one. For example, if the variable minimumNumber has not been given a value either as the left-hand side of an assignment statement or by some other means (such as being given an input value with a cin statement), then the following is an error:

```
desiredNumber = minimumNumber + 10;
```

This is because minimumNumber has no meaningful value, and so the entire expression on the right-hand side of the equal sign has no meaningful value. A variable like minimumNumber that has not been given a value is said to be uninitialized. This situation is, in fact, worse than it would be if minimumNumber had no value at all. An uninitialized variable, like minimumNumber, will simply have some garbage value. The value of an uninitialized variable is determined by whatever pattern of zeros and ones was left in its memory location by the last program that used that portion of memory.

One way to avoid an uninitialized variable is to initialize variables at the same time they are declared. This can be done by adding an equal sign and a value, as follows:

```
int minimumNumber = 3;
```

This both declares minimumNumber to be a variable of type int and sets the value of the variable minimumNumber equal to 3. You can use a more complicated expression involving operations such as addition or multiplication when you initialize a variable inside the declaration in this way. As another example, the following declares three variables and initializes two of them:

```
double rate = 0.07, time, balance = 0.00;
```

C++ allows an alternative notation for initializing variables when they are declared. This alternative notation is illustrated by the following, which is equivalent to the preceding declaration:

```
double rate(0.07), time, balance(0.00);
```

## INITIALIZING VARIABLES IN DECLARATIONS

You can initialize a variable (that is, give it a value) at the time that you declare the variable.

## SYNTAX

```
Type_Name Variable_Name_1 = Expression_for_Value_1,
    Variable_Name_2 = Expression_for_Value_2, ...;
```

**EXAMPLES**

```text
int count = 0, limit = 10, fudgeFactor = 2;
double distance = 999.99;
```

## SYNTAX

Alternative syntax for initializing in declarations:

```
Type_Name Variable_Name_1 (Expression_for_Value_1),
             Variable_Name_2 (Expression_for_Value_2), ...;
```

**EXAMPLES**

```text
int count(0), limit(10), fudgeFactor(2);
double distance(999.99);
```

## Tip — USE MEANINGFUL NAMES

Variable names and other names in a program should at least hint at the meaning or use of the thing they are naming. It is much easier to understand a program if the variables have meaningful names. Contrast

```text
x = y * z;
```

with the more suggestive

```text
distance = speed * time;
```

The two statements accomplish the same thing, but the second is easier to understand.

## MORE ASSIGNMENT STATEMENTS

A shorthand notation exists that combines the assignment operator (=) and an arithmetic operator so that a given variable can have its value changed by adding, subtracting, multiplying by, or dividing by a specified value. The general form is

```text
Variable Operator = Expression
```

which is equivalent to

```text
Variable = Variable Operator (Expression)
```

The Expression can be another variable, a constant, or a more complicated arithmetic expression. The following list gives examples.

| EXAMPLE | EQUIVALENT TO |
|---|---|
| count += 2; | count = count + 2; |
| total -= discount; | total = total - discount; |
| bonus *= 2; | bonus = bonus * 2; |
| time /= rushFactor; | time = time/rushFactor; |
| change %= 100; | change = change % 100; |
| amount *= cnt1 + cnt2; | amount = amount * (cnt1 + cnt2); |

# Self-Test Exercises

- 1. Give the declaration for two variables called feet and inches. Both variables are of type int and both are to be initialized to zero in the declaration. Give both initialization alternatives.
- 2. Give the declaration for two variables called count and distance. count is of type int and is initialized to zero. distance is of type double and is initialized to 1.5. Give both initialization alternatives.
- 3. Write a program that contains statements that output the values of five or six variables that have been defined, but not initialized. Compile and run the program. What is the output? Explain.

# ASSIGNMENT COMPATIBILITY

As a general rule, you cannot store a value of one type in a variable of another type. For example, most compilers will object to the following:

int intVariable;
intVariable = 2.99;

The problem is a type mismatch. The constant 2.99 is of type double, and the variable intVariable is of type int. Unfortunately, not all compilers will react the same way to the above assignment statement. Some will issue an error message, some will give only a warning message, and some compilers will not object at all. Even if the compiler does allow you to use the above assignment, it will give intVariable the int value 2, not the value 3. Since you cannot count on your compiler accepting the above assignment, you should not assign a double value to a variable of type int.

Even if the compiler will allow you to mix types in an assignment statement, in most cases you should not. Doing so makes your program less portable, and it can be confusing.

There are some special cases in which it is permitted to assign a value of one type to a variable of another type. It is acceptable to assign a value of an integer type, such as int, to a variable of a floating-point type, such as type double. For example, the following is both legal and acceptable style:

```
double doubleVariable;
doubleVariable = 2;
```

The above will set the value of the variable named doubleVariable equal to 2.0.

Although it is usually a bad idea to do so, you can store an int value such as 65 in a variable of type char and you can store a letter such as 'Z' in a variable of type int. For many purposes, the C language considers characters to be small integers, and perhaps unfortunately, C++ inherited this from C. The reason for allowing this is that variables of type char consume less memory than variables of type int; thus, doing arithmetic with variables of type char can save some memory. However, it is clearer to use the type int when you are dealing with integers and to use the type char when you are dealing with characters.

The general rule is that you cannot place a value of one type in a variable of another type—though it may seem that there are more exceptions to the rule than there are cases that follow the rule. Even if the compiler does not enforce this rule very strictly, it is a good rule to follow. Placing data of one type in a variable of another type can cause problems because the value must be changed to a value of the appropriate type and that value may not be what you would expect.

Values of type bool can be assigned to variables of an integer type (short, int, long), and integers can be assigned to variables of type bool. However, it is poor style to do this. For completeness and to help you read other people's code, here are the details: When assigned to a variable of type bool, any nonzero integer will be stored as the value true. Zero will be stored as the value false. When assigning a bool value to an integer variable, true will be stored as 1, and false will be stored as 0.

# LITERALS

A literal is a name for one specific value. Literals are often called constants in contrast to variables. Literals or constants do not change value; variables can change their values. Integer constants are written in the way you are used to writing numbers. Constants of type int (or any other integer type) must not contain a decimal point. Constants of type double may be written in either of two forms. The simple form for double constants is like the everyday way of writing decimal fractions. When written in this form a double constant must contain a decimal point. No number constant (either integer or floating-point) in C++ may contain a comma.
