(continued)

| CATEGORY | OPERATOR |
|---|---|
| Assignment | = += -= *= /= %= &= |= ^= <<= >>= |
| Member access (for objects and structs) | . |
| Indexing (for arrays and indexers) | [] |
| Cast | () |
| Conditional (the ternary operator) | ?: |
| Delegate concatenation and removal (discussed in Chapter 8, "Delegates, Lambdas, and Events") | + - |
| Object creation | new |
| Type information | sizeof is typeof as |
| Overflow exception control | checked unchecked |
| Indirection and address | [] |
| Namespace alias qualifier (discussed in Chapter 2, "Core C#") | :: |
| Null coalescing operator | ?? |

Note that four specific operators (sizeof, *, ->, and &, listed in the following table), however, are available only in unsafe code (code that bypasses C#'s type-safety checking), which is discussed in Chapter 13, “Memory Management and Pointers.” It is also important to note that the sizeof operator keywords, when used with the very early versions of the .NET Framework 1.0 and 1.1, required the unsafe mode. This is not a requirement since the .NET Framework 2.0 version.

| CATEGORY | OPERATOR |
|---|---|
| Operator keywords | sizeof (for .NET Framework versions 1.0 and 1.1 only) |
| Operators | * -> & |

One of the biggest pitfalls to watch out for when using C# operators is that, as with other C-style languages, C# uses different operators for assignment (=) and comparison (==). For instance, the following statement means let x equal three:

```
x = 3;
```

If you now want to compare x to a value, you need to use the double equals sign ==:

```
if (x == 3)
{
}
```

Fortunately, C#'s strict type-safety rules prevent the very common C error where assignment is performed instead of comparison in logical statements. This means that in C# the following statement will generate a compiler error:

```
if (x = 3)
{
}
```

Visual Basic programmers who are accustomed to using the ampersand (&) character to concatenate strings will have to make an adjustment. In C#, the plus sign (+) is used instead for concatenation, whereas the & symbol denotes a bitwise AND between two different integer values. The symbol | allows you to perform a bitwise OR between two integers. Visual Basic programmers also might not recognize the modulus (%)