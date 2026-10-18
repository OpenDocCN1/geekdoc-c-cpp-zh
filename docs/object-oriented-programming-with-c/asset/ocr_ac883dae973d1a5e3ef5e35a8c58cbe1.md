ANSI C++ adds the following new cast operators:

+   - const_cast
+   - static_cast
+   - dynamic_cast
+   - reinterpret_cast

Application of these operators is discussed in Chapter 16.

# ### 3.20 Expressions and Their Types

An expression is a combination of operators, constants and variables arranged as per the rules of the language. It may also include function calls which return values. An expression may consist of one or more operands, and zero or more operators to produce a value. Expressions may be of the following seven types:

+   - Constant expressions
+   - Integral expressions
+   - Float expressions
+   - Pointer expressions
+   - Relational expressions
+   - Logical expressions
+   - Bitwise expressions

An expression may also use combinations of the above expressions. Such expressions are known as *compound expressions*.

# ## Constant Expressions

Constant Expressions consist of only constant values. Examples:

```
15
20 + 5 / 2.0
'x'
```