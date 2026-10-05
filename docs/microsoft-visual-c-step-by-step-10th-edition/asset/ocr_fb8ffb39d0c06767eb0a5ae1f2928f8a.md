The ++ and -- operators are unary operators, meaning they take only a single operand. They share the same precedence and are both left associative.

# Prefix and postfix

The increment (++) and decrement (--) operators are unusual in that you can place either before or after the variable. Placing the operator symbol before the variable is called the *prefix form* of the operator, and using the operator symbol after the variable is called the *postfix form*. Here are some examples:

```
count++; // postfix increment
++count; // prefix increment
count--; // postfix decrement
--count; // prefix decrement
```

Whether you use prefix or postfix form of the ++ or -- operator makes no difference to the variable being incremented or decremented. For example, if you write count++, the value of count increases by 1, and if you write ++count, the value of count also increases by 1. Knowing this, you're probably wondering why there are two ways to write the same thing. To understand the answer, you must remember that ++ and -- are operators, that all operators are used to evaluate an expression that has a value. The value returned by count++ is the value of count before the increment takes places, whereas the value returned by ++count is the value of count after the increment takes places. Here's an example:

Click here to view image

```
int x;
x = 42;
Console.WriteLine(x++); // x is now 43, 42 written out
x = 42;
Console.WriteLine(++x); // x is now 43, 43 written out
```

The way to remember which operand does what is to look at the order of the elements (and the operator) in a prefix or postfix expression. In the expression x++, the variable x occurs first, so its value is the value of the expression before x is incremented. In the expression ++x, the operator occurs first, so its operation is performed before the value of x is evaluated as the result.

These operators are most commonly used in while and do statements, which are presented in Chapter 5, "Using compound assignment and iteration statements." If you're using the increment and decrement operators in isolation, stick to the postfix form and be consistent.