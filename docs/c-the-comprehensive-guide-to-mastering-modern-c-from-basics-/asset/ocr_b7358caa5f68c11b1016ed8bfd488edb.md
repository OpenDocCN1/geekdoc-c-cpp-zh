```
cout << year; // infix notation
operator<<(cout, year); // function notation
```

If you use the infix notation, the compiler automatically selects the method or free function, depending on what you have defined for your class. If you use the function or method notation, you choose it yourself. This can be useful in cases of doubt, if you have both.

```
// https://godbolt.org/z/P99563KoP
#include <iostream>
using std::cout; using std::ostream;
struct Widget {
    bool operator<(const Widget&) const { // method notation
        return true; // always true
    }
    bool operator<(const Widget&, const Widget&) { // function notation
        return false; // always false
}
int main() {
    Widget x;
    Widget y;
    cout << operator<(x, y) // calls function notation
    ? "Method1\n": "Function1\n";
    cout << (y.operator<(x)) // calls method notation
    ? "Method2\n": "Function2\n";
    cout << (x << y) // infix notation, allows choice, for function
    ? "Method3\n": "Function3\n";
}
```

**Listing 16.22** Infix, function, and method notation for operators.

For the operator< of Widget, two variants are implemented: the free function and the method. To observe the difference in invocation, the two implementations return different values. The first two