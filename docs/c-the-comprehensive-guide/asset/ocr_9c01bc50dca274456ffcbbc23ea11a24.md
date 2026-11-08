```
```cpp
void pr(string_view s) { cout << s << endl; }
double pi = 3.14159265359;

int main() {
    pr(format("Hello, {}!", "Reader"));             // simple C-string
    pr(format("Hello, {}!", "Author"));             // simple string
    pr(format("You are {} years old", 30));           // integers
    pr(format("That makes {:.2f} euros.", 19.993));  // 2 decimal places
    pr(format("Scientific: {:.4e}", -44.876));       // results in "-4.487600e+01"
    pr(format("Binary of {} is {:b}.", 42, 42));      // binary without base
    pr(format("Hex of {} is {:x}.", 73, 73));        // hexadecimal with base
    pr(format("Zero-padded: {:03}", 7));              // results in "007"
    pr(format("{10:<10}{1:^10}{2:>10}", "le", "mi", "ri"));
    // Alignment and index
    pr(format("{:>9}", "Boa", "Constructor"));      // without index, truncate string
    using namespace std::chrono;                       // neat time specifications:
    pr(format("{}, {}", 2023y/11/5, minutes{20}));   // Output: 2023-11-05, 20min
}
```
```

In the last example, you see that you can also format your own types. Here the `<chrono>` header brings in its own formatter.

By the way, did you notice the new C++20 notation for date literals in 2023y/11/5?

In general, the standard formatting attributes are structured as follows; these are the possible elements in a compact form:

*fill align sign # 0 width .precision L type*

All elements are optional, but the order must be maintained. The elements are partially dependent on each other and only make sense in certain combinations and for certain types. There are combinations that are frequently seen, such as .2f for a floating-point number with two decimal places.

The individual elements mean the following:

+   - *fill*
+     Specifies the character to be used for filling. The default is the space character. Requires *align*.
+   - *align*
+     Can be `<` (left), `>` (right), or `^` (centered). The default is left.
+   - *sign*
+     - includes the sign only for negative numbers (default), `+` always includes the sign, and space means that a minus sign is used for negative numbers and a space for positive numbers.