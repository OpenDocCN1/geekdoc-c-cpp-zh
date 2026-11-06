# 8.1.3  Initializing static const data

Static const data members should be initialized like any other static data member: in source files defining these data members.

Usually, if these data members are of integral or built-in primitive data types the compiler accepts in-class initializations of such data members. However, there is no formal rule requiring the compiler to do so. Compilations may or may not succeed depending on the optimizations used by the compiler (e.g., using -O2 may result in a successful compilation, but -O0 (no-optimizations) may fail to compile, but then maybe only when shared libraries are used...).

In-class initializations of integer constant values (e.g., of types `char`, `int`, `long`, etc, maybe unsigned) are nevertheless possible using (e.g., anonymous) enums. The following example illustrates how this can be done:

```
class X
{
    public:
        enum       { s_x = 34 };
        enum: size_t { s_maxWidth = 100 };
};
```

To avoid confusion caused by different compiler options static data members should always explicitly be defined and initialized in a source file, whether or not const.

# 8.1.4  Generalized constant expressions (C++11)

In C macros are often used to let the preprocessor perform simple calculations. These *macro functions* may have arguments, as illustrated in the next example:

```
#define xabs(x)  ((x) < 0 ? -(x) : (x))
```

The disadvantages of macros are well-known. The main reason for avoiding macros is that they are not parsed by the compiler, but are processed by the preprocessor resulting in mere text replacements and thus avoid type-safety or syntactic checks of the macro definition by itself. Furthermore, since macros are processed by the preprocessor their use is unconditional, without acknowledging the context in which they are applied. NULL is an infamous example. Ever tried to define an enum symbol NULL? or EOF? Chances are that, if you did, the compiler threw strange error messages at you.

Generalized const expressions can be used as an alternative.

Generalized const expressions are recognized by the modifier `constexpr` (a keyword), that is applied to the expression's type.

There is a small semantic difference between the use of the `const` modifier and the use of the `constexpr` modifier. While the const modifier can be applied to definitions and declarations alike, the constexpr modifier can only be applied to definitions:

```
extern int const externInt;      // OK: declaration of const int
extern int constexpr error;      // ERROR: not a definition
```

Variables defined with the `constexpr` modifier have constant (immutable) values. But generalized const expressions are not just used to define constant variables; they have other applications as well. The constexpr word is usually applied to functions, turning the function into a *constant-expression function*.

A constant-expression function should not be confused with a function returning a const value (although a constant-expression function *does* return a (const) value). A constant expression function has the following characteristics: