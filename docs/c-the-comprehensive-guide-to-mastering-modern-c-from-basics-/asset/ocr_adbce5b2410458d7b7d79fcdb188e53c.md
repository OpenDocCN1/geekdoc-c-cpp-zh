```
// https://godbolt.org/z/4dnTs4vPx
namespace {
    const int MAX_A = 12;    // the same as MAX_B, but no static
    needed
    static const int MAX_B = 10; // in the global namespace
    struct Data {
        static const int SIZE = 14; // as a data field in a class
    };
    void func() {
        static const int LIMIT = 16; // as a local constant
    }
}
```

The distinction mainly arises because static has a different meaning in each of these cases:

+   - const in an anonymous namespace-MAX_A
First without static. The constant MAX_A is only known in this *.cpp file. You cannot access it from another file.

+   - static in the global namespace-MAX_B
Instead of an anonymous namespace, you can use static to define a constant. This has the same effect and is the older syntax. The disadvantage is that you cannot make classes local this way. Prefer an anonymous namespace.

+   - static const as data field-SIZE
The static ensures that all variables of type Data share a single size. The const makes it immutable also.

+   - static const as local variable-LIMIT
For a local variable, static means that it retains its value when the function is exited. The variable is initialized only on the first pass. Together with const, it becomes a constant that is initialized only when needed.