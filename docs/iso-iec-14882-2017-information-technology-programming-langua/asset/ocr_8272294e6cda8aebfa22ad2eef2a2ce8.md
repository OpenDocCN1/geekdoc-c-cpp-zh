# ISO/IEC 14882:2017(E)

```
constexpr int first(int n) {
    static int value = n; // error: variable has static storage duration
    return value;
}
constexpr int unit() {
    int a; // error: variable is uninitialized
    return a;
}
constexpr int prev(int x) {
    return --x;
 // OK
constexpr int g(int x, int n) { // OK
    int r = 1;
    while (-n > 0) r *= x;
    return r;
}
```

The definition of a constexpr constructor shall satisfy the following requirements:

+   - the class shall not have any virtual base classes;
- each of the parameters shall be a literal type;
- its function-body shall not be a function-block.

In addition, its function-body shall be delete, or it shall satisfy the following requirements:
either its function-body shall be default, or the compound-statement of its function-body shall satisfy the requirements for a constexpr data member

+   - non-delegating data member and class object shall be initialized [15.6.2);
- if the class is a union having variant members (12.3), exactly one of them shall be initialized;
- if the class is a union-like, but is not a union, for each of its anonymous union having variant members, exactly one of them shall be initialized;
- for a delegating constructor, the target constructor shall be a constexpr constructor.

Example:

```
struct Length {
    constexpr Length(int i = 0) : val(i) {}
    private:
    int val;
    };
// end example
```

For a constexpr function or constexpr constructor that is neither defaulted nor a template, if no argument exists such that invocation of the function or constructor could be evaluated as subexpression of a constant expression [8.20), or, for a constructor, a constant initializer for some object (6.6.2), the program is ill-formed, no diagnostic required. Example:

```
constexpr int f(bool b)
    { return b ? 0 : 0; } // OK
constexpr int f() { return f(true); } // ill-formed, no diagnostic required
```

©ISO/IEC 2017 – All rights reserved 163