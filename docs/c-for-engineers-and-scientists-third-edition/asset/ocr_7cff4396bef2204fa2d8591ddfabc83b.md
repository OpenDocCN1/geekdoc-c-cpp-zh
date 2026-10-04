# Chapter 3

# 167

Chapter Summary

# 3.8 Common Programming Errors

When using the material in this chapter, be aware of the following possible errors:

+   1. Forgetting to assign or initialize values for all variables before using them in an expression. Values can be assigned by assignment statements, initialized in a declaration statement, or assigned interactively by entering values with a cin statement.

+   2. Using a mathematical library function without including the preprocessor statement #include <cmath> (and on a UNIX-based system, forgetting to include the -lm argument on the cc command line).

+   3. Using a library function without providing the correct number of arguments of the proper type.

+   4. Applying the increment or decrement operator to an expression. For example, the expression (count + n)++ is incorrect. The increment and decrement operators can be applied only to variables.

+   5. Forgetting to use the extraction operator, >>, to separate variables in a cin statement.

+   6. A more unusual error occurs when increment and decrement operators are used with variables appearing more than once in a statement. This error occurs because C++ doesn't specify the order in which operands are accessed in an expression. For example, the value assigned to result in the statement depends on the compiler:

```
result = i + i++;
```

If your compiler accesses the first operand (i) first, the preceding statement is equivalent to

```
result = 2 * i;
```

i++; However, if your compiler accesses the second operand (i++) first, the value of the first operand is altered before it used the second time, and the value i + 1 is assigned to result. As a general rule, don't use the increment or decrement operator in a variable when it operates more than once in the expression.

+   7. Being unwilling to test a program in depth. Being objective about testing your own software is difficult, but as a programmer, you must remember that just your program is correct doesn't make it so.

# 3.9 Chapter Summary

+   1. An expression is a sequence of one or more operands separated by operators. An operand is a constant, a variable, or another expression. A value is associated with an expression.

+   2. Expressions are evaluated according to the precedence and associativity of the operators used in the expression.