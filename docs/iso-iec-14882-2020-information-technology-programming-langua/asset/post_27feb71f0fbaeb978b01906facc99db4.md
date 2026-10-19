
```
auto bind = [](auto m) {
    return [=](auto fvm) { return fvm(m()); };
};
```
// OK to capture objects with automatic storage duration created during constant expression evaluation.

```
static_assert(bind(monad(2))(monad() == monad(2()));
```
— end example]

— end note]

-   (5.14) — a conversion from type cv void* to a pointer-to-object type;
-   (5.15) — a reinterpret_cast (7.6.1.10);
-   (5.16) — a modification of an object (7.6.19, 7.6.1.6, 7.6.2.3) unless it is applied to a non-volatile lvalue of literal type that refers to a non-volatile object whose lifetime began within the evaluation of E;
-   (5.17) — a new-expression (7.6.2.8), unless the selected allocation function is a replaceable global allocation function (17.6.3.2, 17.6.3.3) and the allocated storage is deallocated within the evaluation of E;
-   (5.18) — a delete-expression (7.6.2.9), unless it deallocates a region of storage allocated within the evaluation of E;
-   (5.19) — a call to an instance of std::allocator<T>::allocate (20.10.10.2), unless the allocated storage is deallocated within the evaluation of E;
-   (5.20) — a call to an instance of std::allocator<T>::deallocate (20.10.10.2), unless it deallocates a region of storage allocated within the evaluation of E;
-   (5.21) — an await-expression (7.6.2.4);
-   (5.22) — a yield-expression (7.6.17);
-   (5.23) — a three-way comparison (7.6.8), relational (7.6.9), or equality (7.6.10) operator where the result is unspecified;
-   (5.24) — a throw-expression (7.6.18) or a dynamic cast (7.6.1.7) or typeid (7.6.1.8) expression that would throw an exception;
-   (5.25) — an asm-declaration (9.10); or
-   (5.26) — an invocation of the va_arg macro (17.13.2).

If E satisfies the constraints of a core constant expression, but evaluation of E would evaluate an operation that has undefined behavior as specified in Clause 16 through Clause 32, or an invocation of the va_start macro (17.13.2), it is unspecified whether E is a core constant expression.

[Example 3:

```
int x;                         // not constant
struct A {
    constexpr A(bool b) : m(b?42:x) { }
    int m;
};
constexpr int v = A(true).m;       // OK: constructor call initializes m with the value 42

constexpr int w = A(false).m;      // error: initializer for m is x, which is non-constant

constexpr int f1(int k) {
    constexpr int x = k;           // error: x is not initialized by a constant expression
                                 // because lifetime of k began outside the initializer of x
    return x;
}
constexpr int f2(int k) {
    int x = k;                     // OK: not required to be a constant expression
                                 // because x is not constexpr
    return x;
}

constexpr int incr(int &n) {
    return ++n;
}
```

```
constexpr int g(int k) {
    constexpr int x = incr(k);    // error: incr(k) is not a core constant expression
                               // because lifetime of k began outside the expression incr(k)
    return x;
}
constexpr int h(int k) {
    int x = incr(k);             // OK: incr(k) is not required to be a core constant expression
    return x;
}
constexpr int y = h(1);          // OK: initializes y with the value 2
                               // h(1) is a core constant expression because
                               // the lifetime of k begins inside h(1)
```
— end example]

6 For the purposes of determining whether an expression E is a core constant expression, the evaluation of a call to a member function of std::allocator<T> as defined in 20.10.10.2, where T is a literal type, does not disqualify E from being a core constant expression, even if the actual evaluation of such a call would otherwise fail the requirements for a core constant expression. Similarly, the evaluation of a call to std::destroy_at, std::ranges::destroy_at, std::construct_at, or std::ranges::construct_at does not disqualify E from being a core constant expression unless:

-   (6.1) — for a call to std::construct_at or std::ranges::construct_at, the first argument, of type T*, does not point to storage allocated with std::allocator<T> or to an object whose lifetime began within the evaluation of E, or the evaluation of the underlying constructor call disqualifies E from being a core constant expression, or

-   (6.2) — for a call to std::destroy_at or std::ranges::destroy_at, the first argument, of type T*, does not point to storage allocated with std::allocator<T> or to an object whose lifetime began within the evaluation of E, or the evaluation of the underlying destructor call disqualifies E from being a core constant expression.

7 An object a is said to have constant destruction if:

-   (7.1) — it is not of class type nor (possibly multi-dimensional) array thereof, or

-   (7.2) — it is of class type or (possibly multi-dimensional) array thereof, that class type has a constexpr destructor, and for a hypothetical expression E whose only effect is to destroy a, E would be a core constant expression if the lifetime of a and its non-mutable subobjects (but not its mutable subobjects) were considered to start within E.

8 An integral constant expression is an expression of integral or unscoped enumeration type, implicitly converted to a prvalue, where the converted expression is a core constant expression.

[Note 4: Such expressions can be used as bit-field lengths (11.4.10), as enumerator initializers if the underlying type is not fixed (9.7.1), and as alignments (9.12.2). — end note]

9 If an expression of literal class type is used in a context where an integral constant expression is required, then that expression is contextually implicitly converted (7.3) to an integral or unscoped enumeration type and the selected conversion function shall be constexpr.

[Example 4:

```
struct A {
    constexpr A(int i) : val(i) { }
    constexpr operator int() const { return val; }
    constexpr operator long() const { return 42; }
private:
    int val;
};
constexpr A a = alignof(int);
alignas(a) int n;            // error: ambiguous conversion
struct B { int n : a; };     // error: ambiguous conversion
```
— end example]

10 A converted constant expression of type T is an expression, implicitly converted to type T, where the converted expression is a constant expression and the implicit conversion sequence contains only

-   (10.1) — user-defined conversions,

## Hunting Open Source Projects

13 An expression or conversion is in an *immediate function context* if it is potentially evaluated and its innermost non-block scope is a function parameter scope of an immediate function. An expression or conversion is an *immediate invocation* if it is a potentially-evaluated explicit or implicit invocation of an immediate function and is not in an immediate function context. An immediate invocation shall be a constant expression.

14 An expression or conversion is *manifestly constant-evaluated* if it is:

-   - a *constant-expression*, or
-   - the condition of a constexpr if statement (8.5.2), or
-   - an immediate invocation, or
-   - the result of substitution into an atomic constraint expression to determine whether it is satisfied (13.5.2.3), or
-   - the initializer of a variable that is usable in constant expressions or has constant initialization (6.9.3.2).

[Example 7:

```
template<bool> struct X {};
X<std::is_constant_evaluated()> x;                // type X<true>
int y;
const int a = std::is_constant_evaluated() ? y : 1;      // dynamic initialization to 1
double z[a];                                            // error: a is not usable
                                                        // in constant expressions
const int b = std::is_constant_evaluated() ? 2 : y;      // static initialization to 2
int c = y + (std::is_constant_evaluated() ? 2 : y);      // dynamic initialization to y+y

constexpr int f() {
    const int n = std::is_constant_evaluated() ? 13 : 17; // n is 13
    int m = std::is_constant_evaluated() ? 13 : 17;       // m can be 13 or 17 (see below)
    char arr[n] = {}; // char[13]
    return m + sizeof(arr);
}
int p = f();                                            // m is 13; initialized to 26
int q = p + f();                                        // m is 17 for this call; initialized to 56
— end example]
```

[Note 7: A manifestly constant-evaluated expression is evaluated even in an unevaluated operand. — end note]

15 An expression or conversion is *potentially constant evaluated* if it is:

-   - a manifestly constant-evaluated expression,
-   - a potentially-evaluated expression (6.3),
-   - an immediate subexpression of a *braced-init-list*,
-   - an expression of the form & *cast-expression* that occurs within a templated entity, or
-   - a subexpression of one of the above that is not a subexpression of a nested unevaluated operand.

A function or variable is *needed for constant evaluation* if it is:

-   - a constexpr function that is named by an expression (6.3) that is potentially constant evaluated, or
-   - a variable whose name appears as a potentially constant evaluated expression that is either a constexpr variable or is of non-volatile const-qualified integral type or of reference type.
