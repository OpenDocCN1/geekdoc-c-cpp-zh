# Chapter 2

# Understanding lvalues and rvalues

An **lvalue** is something that refers to an address in memory and is so called because any expression that results in an lvalue can appear on the left of the equals sign in an assignment statement. Most variables are lvalues, because they specify a place in memory. However, as you’ll see, there are variables that aren’t lvalues and can’t appear on the left of an assignment because their values have been defined as constant.

The variables a and b that appear in the preceding paragraph are lvalues, whereas the result of evaluating the expression a+b would not be, because its result doesn’t determine an address in memory where a value might be stored. The result of an expression that is not an lvalue is referred to as an **rvalue**.

> Lvalues will pop up at various times throughout the book, sometimes where you least expect them, so keep the idea in mind.

# Arithmetic Operations

The basic arithmetic operators you have at your disposal are addition, subtraction, multiplication, and division, represented by the symbols +, −, * and /, respectively. These operate generally as you would expect, with the exception of division which has a slight aberration when working with integer variables or constants, as you’ll see. You can write statements such as the following:

```
netPay = hours * rate - deductions;
```

Here, the product of hours and rate will be calculated and then deductions subtracted from the value produced. The multiply and divide operators are executed before addition and subtraction, as you would expect. I will discuss the order of execution of the various operators in expressions more fully later in this chapter. The overall result of evaluating the expression hours * rate − deductions will be stored in the variable netPay.

The minus sign used in the last statement has two operands — it subtracts the value of its right operand from the value of its left operand. This is called a **binary operation** because two values are involved. The minus sign can also be used with one operand to change the sign of the value to which it is applied, in which case it is called a **unary minus**. You could write this:

```
int a = 0;
int b = -5;
a = -b;                         // Changes the sign of the operand
```

Here, a will be assigned the value +5 because the unary minus changes the sign of the value of the operand b.

Note that an assignment is not the equivalent of the equations you saw in high school algebra. It specifies an action to be carried out rather than a statement of fact. The expression to the right of the assignment operator is evaluated and the result is stored in the lvalue — typically a variable — that appears on the left.

Look at this statement:

```
number = number + 1;
```