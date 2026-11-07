# Overloading Restrictions

Most C++ operators (see Table 11.1) can be overloaded in the manner described in the preceding section. Overloaded operators (with some exceptions) don’t necessarily have to be member functions. However, at least one of the operands has to be a user-defined type. Let’s take a closer look at the limits C++ imposes on user-defined operator overloading:

+   - The overloaded operator must have at least one operand that is a user-defined type. This prevents you from overloading operators for the standard types. Thus, you can’t redefine the minus operator (`-`) so that it yields the sum of two double values instead of their difference. This restriction preserves program sanity, although it may hinder creative accounting.
+   - You can’t use an operator in a manner that violates the syntax rules for the original operator. For example, you can’t overload the modulus operator (`%`) so that it can be used with a single operand:

```
int x;
Time shiva;
% x;      // invalid for modulus operator
% shiva;  // invalid for overloaded operator
```

Similarly, you can’t alter operator precedence. So if you overload the addition operator to let you add two classes, the new operator has the same precedence as ordinary addition.

+   - You can’t create new operator symbols. For example, you can’t define an `operator**()` function to denote exponentiation.
+   - You cannot overload the following operators:

| Operator | Description |
|---|---|
| `sizeof` | The sizeof operator |
| `.` | The membership operator |
| `.*` | The pointer-to-member operator |
| `::` | The scope-resolution operator |
| `?:` | The conditional operator |
| `typeid` | An RTTI operator |
| `const_cast` | A type cast operator |
| `dynamic_cast` | A type cast operator |
| `reinterpret_cast` | A type cast operator |
| `static_cast` | A type cast operator |

This still leaves all the operators in Table 11.1 available for overloading.