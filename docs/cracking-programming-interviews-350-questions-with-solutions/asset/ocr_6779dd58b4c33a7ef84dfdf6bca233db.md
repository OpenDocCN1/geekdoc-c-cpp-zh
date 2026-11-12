```
```text
increment_operator.cpp: In function ‘int main()’:
increment_operator.cpp:8:18:
error: lvalue required as increment operand
    int a = one++++++two;
```
```

The expression `one++++++two` is parsed to look like `one ++ ++ two`, which violates a constraint on increment operators, thus leading to incorrect expression.

*one++++++two ⇒ one ++ + + two*

Please note that the expression `one++++++two` is not parsed as `one ++ + ++ two`, which is indeed a correct expression.

*one++++++two ⇒ one ++ + + two*

# **Question 8 — `nullptr`**

What is `nullptr`?

# Solution of Question 8

`nullptr` is the pointer literal designating a prvalue of type `std::nullptr_t`. It is a null pointer constant which can be converted to a null pointer value or a null member pointer value.

Please note that `std::nullptr_t` itself

+   - is not a pointer type
+   - is not a pointer to member type
+   - is a distinct type

# **Question 9 — user defined literal**

What is *user defined literal*?

# Solution of Question 9

A *user defined literal* is a call to a literal operator or literal operator template of the form

+   1. `operator "" identifier`
+   2. `operator "" identifier<'c₁', 'c₂', ..., 'cₖ'>()`

For example:

+   1. `user-defined-integer-literal`