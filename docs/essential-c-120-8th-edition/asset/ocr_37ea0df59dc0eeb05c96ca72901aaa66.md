# Tuples 103

variable accordingly, just as it would if the programmer had specified the type explicitly.

Although var rather than the explicit data type is allowed, consider avoiding such use when the data type is not obvious—for example, use string for the declaration of text and uppercase. Not only does this make the code understandable, but it also allows the compiler to verify your intent, that the data type returned by the right-hand side expression is the type expected. When using a var-declared variable, the right-hand side data type should be obvious; if it isn’t, use of the var declaration should be avoided.

Guidelines
Avoid using implicitly typed local variables (var) unless the data type of the assigned value is obvious.

Language Contrast: C++/Visual Basic/JavaScript—void*, Variant, and var
An implicitly typed variable is not the equivalent of void+ in C++, Variant in Visual Basic, or var in JavaScript. In each of these cases, the variable declaration is restrictive because the variable may be assigned a value of any type, just as be done in C# with a variable declaration of type object. In contrast, var is definitively typed by the compiler, once established at declaration, the type may not change, and type checks and member calls are verified at compile time.

# Tuples

On occasion, you will find it useful to combine data elements together. For, for example, information about a country such as the poorest country in the world in 2022: Burundi, whose capital is Bujumbura, with a GDP per capita of $263.67. Given the constructs we have established so far, we could store each data element in individual variables, but the result would be no association of the data elements together. That is, $263.67 would have no association with Burundi, except perhaps by a common suffix or prefix in the variable names. Another option would be to