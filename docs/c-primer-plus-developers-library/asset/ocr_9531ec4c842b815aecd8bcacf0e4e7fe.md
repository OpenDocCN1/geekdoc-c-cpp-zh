Then there are the conversions that take place when you arithmetically combine different types, such as adding an `int` to a `float`. When an operation involves two types, the smaller is converted to the larger. For example, the program in Listing 3.11 divides 9.0 by 5. Because 9.0 is type double, the program converts 5 to type double before it does the division. More generally, the compiler goes through a checklist to determine which conversions to make in an arithmetic expression. C++11 has modified the list slightly. Here’s the C++11 version of the list, which the compiler goes through in order:

+   1. If either operand is type `long double`, the other operand is converted to `long double`.
+   2. Otherwise, if either operand is `double`, the other operand is converted to `double`.
+   3. Otherwise, if either operand is `float`, the other operand is converted to `float`.
+   4. Otherwise, the operands are integer types and the integral promotions are made.
+   5. In that case, if both operands are signed or if both are unsigned, and one is of lower rank than the other, it is converted to the higher rank.
+   6. Otherwise, one operand is signed and one is unsigned. If the unsigned operand is of higher rank than the signed operand, the latter is converted to the type of the unsigned operand.
+   7. Otherwise, if the signed type can represent all values of the unsigned type, the unsigned operand is converted to the type of the signed type.
+   8. Otherwise, both operands are converted to the unsigned version of the signed type.

ANSI C follows the same rules as ISO 2003 C++, which are slightly different from the preceding rules, and classic K&R C has yet slightly different rules. For example, classic C always promotes `float` to `double`, even if both operands are `float`.

This list introduces the concept of ranking the integer types. In brief, as you might expect, the basic ranking for signed integer types from high to low is `long long`, `long`, `int`, `short`, and `signed char`. Unsigned types have the same rank as the corresponding signed type. The three types `char`, `signed char`, and `unsigned char` all have the same rank. The `bool` type has the lowest rank. The `wchar_t`, `char16_t`, and `char32_t` have the same types as their underlying types.

# Conversions in Passing Arguments

Normally, C++ function prototyping controls type conversions for the passing of arguments, as you’ll learn in Chapter 7, “Functions: C++’s Programming Modules.” However, it is possible, although usually unwise, to waive prototype control for argument passing. In that case, C++ applies the integral promotions to the `char` and `short` types (`signed