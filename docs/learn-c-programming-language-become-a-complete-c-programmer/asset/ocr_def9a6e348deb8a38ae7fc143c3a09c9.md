# 11

# Select Operations

> When someone says “I want a programming language in which I need only say what I wish done,” give him a lollipop.
> — Alan Perlis

+   - Etc. Operators
+   Logical Operators; Bitwise Logical Operators; Conditional Expressions; Increment and Decrement
+   - Free Store
+   Memory Management; Arrays; Getting Memory Space; Overloading new
+   - Lists
+   Implementation Model; Qualified Lists; Unqualified Lists
+   - Lambda Expressions
+   Implementation Model; Alternatives to Lambdas; Capture; Call and Return; The Type of a Lambda
+   - Explicit Type Conversion
+   Construction; Named Casts; C-Style Cast; Function-Style Cast
+   - Advice

# 11.1 Etc. Operators

This section examines a mixed bag of simple operators: logical operators ( &&, ||, and !), bitwise logical operators (&, |, ^, <<, and >>), conditional expressions (?:), and increment and decrement operators (++ and --). They have little in common beyond their details not fitting elsewhere in the discussions of operators.

# 11.1.1 Logical Operators

The logical operators && (and), || (or), and ! (not) take operands of arithmetic and pointer types, convert them to bool, and return a bool result. The && and || operators evaluate their second argument only if necessary, so they can be used to control evaluation order (§10.3.2). For example:

```
while (p && !whitespace(*p)) ++p;
```

Here, p is not dereferenced if it is the nullptr.

# 11.1.2 Bitwise Logical Operators

The bitwise logical operators & (and), | (or), ^ (exclusive or, xor), ~ (complement), >> (right shift), and << (left shift) are applied to objects of integral types – that is, char, short, int, long, long long and their unsigned counterparts, and bool, wchar_t, char16_t, and char32_t. A plain enum (but not an enum class) can be implicitly converted to an