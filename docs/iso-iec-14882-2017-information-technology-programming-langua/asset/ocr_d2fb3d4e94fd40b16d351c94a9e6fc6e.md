# ISO/IEC 14882:2017(E)

+   (4.6) — integral promotions (7.6)

+   (4.7) — integral conversions (7.8) other than narrowing conversions (11.6,4),

+   (4.8) — null pointer conversions (7.11) from std::nullptr_t,

+   (4.9) — null member pointer conversions (7.12) from std::nullptr_t, and

+   (4.10) — function pointers (7.13),

and the reference binding (if any) binds. [Note: Such expressions may be used in new expressions (8.3,4), as array initializers (9.4,2), as enumerator initializers if the type is fixed (10.2), as array bounds (11.3,4) and as non-template arguments (17.3) — end note] A contextually constant expression of type bool is an expression, converted to bool (Clause7), where the converted expression is constant and the conversion sequence contains only constants

A constant expression is either a glue constant expression that refers to an entity that is a permitted result of a constant expression (as defined below), or a pure constant expression whose value satisfies the following constraints:

+   (5.1) — if the value is an object of class, each non-static data member refers to an entity that is a permitted result of a constant expression,

+   (5.2) — if the value is of pointer, it contains the address of an object with static storage duration, the address just past the end of such an object (8.7), the address of, or a null pointer value,

+   (5.3) — if the value is an array or array type, each subscript satisfies these constraints for the value.

An entity is a permitted result of a constant expression if it is an object with static storage duration, or if it is not a temporary or an object whose value satisfies the above constraints, or if it is a function.

> Note Since this document imposes restrictions on the calculation of floating-point operations, it is unspecified whether the evaluation of a floating-point expression during translation yields the result as the evaluation of the same expression (or the same operations on the same values) during program execution.^{89}

```
bool f() {
    char array[1 + int(1 + 0.2 - 0.1)]; // Must be evaluated during translation
    int size = 1 + int(1 + 0.2 - 0.1); // May be evaluated at runtime
    return array(array);
}
```

It is unspecified whether the value of f() will be true or false. — end note —

If an expression of literal type is used in a context where an integral constant expression is required, then that expression is contextually converted (Clause 7) to an integral or unspecified enumeration type and the selected conversion function shall be constexpr. [Example:

```
struct A {
    constexpr A(int) : val(i) {}
    constexpr operator int() const { return val; }
    constexpr operator long() const { return 42; }
    private:
        int val;
    };
    template<int>
    constexpr A a = alignof(int);
```

> 89) Nonetheless, implementations should provide consistent results, irrespective of whether the evaluation was performed during translation and/or during execution.

§ 8.20 ©ISO/IEC 2017 - All rights reserved 142