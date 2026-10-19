Following this recommendation entails some risk. If you commonly use ++ and -- as side effects (as part of other statements), you’ll get burned when you use macros that you think are routines. Considering the other problems with side effects, this is yet another reason to avoid using side effects.

# Limitations on the Use of Macro Routines

Modern languages like C++ provide numerous alternatives to the use of macros:

+   - *const* for declaring constant values
+   - *inline* for defining functions that will be compiled as inline code
+   - *template* for defining standard operations like *min*, *max*, and so on in a type-safe way
+   - *enum* for defining enumerated types
+   - *typedef* for defining simple type substitutions

![](bbox=[0.137, 0.402, 0.211, 0.465])

> As Bjarne Stroustrup, designer of C++ points out, “Almost every macro demonstrates a flaw in the programming language, in the program, or in the programmer.... When you use macros, you should expect inferior service from tools such as debuggers, cross-reference tools, and profilers” (Stroustrup 1997). Macros are useful for supporting conditional compilation—see Section 8.6, “Debugging Aids”—but careful programmers generally use a macro as an alternative to a routine only as a last resort.

# Inline Routines

C++ supports an *inline* keyword. An inline routine allows the programmer to treat the code as a routine at code-writing time, but the compiler will generally convert each instance of the routine into inline code at compile time. The theory is that *inline* can help produce highly efficient code that avoids routine-call overhead.

***Use inline routines sparingly***  Inline routines violate encapsulation because C++ requires the programmer to put the code for the implementation of the inline routine in the header file, which exposes it to every programmer who uses the header file.

Inline routines require a routine’s full code to be generated every time the routine is invoked, which for an inline routine of any size will increase code size. That can create problems of its own.