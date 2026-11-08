# Manipulators with Arguments

There are some manipulators with arguments in the `<iomanip>` header file. You can find an overview of them in Table 27.6.

| Manipulator | Meaning |
|---|---|
| `setiosflags(ios::fmtflags m)` | This allows you to combine multiple flags with a bitwise `|` and set them to `m`. |
| `resetiosflags(ios::fmtflags m)` | Clears all flags specified by `m`. |
| `setbase(int base)` | Sets the base for reading and writing integral values to 8, 10, or 16. |
| `setfill(char ch)` | If a fill width is used, the empty space is filled with the character `ch`. |
| `setprecision(int n)` | This allows you to set the number of decimal places for floating-point numbers. |
| `setw(int w)` | This allows you to set a fill width between two values in a stream. |

**Table 27.6** Manipulators with parameters from the `<iomanip>` header file.

```
```cpp
// https://godbolt.org/z/sYK8oT33x
#include <iostream>
#include <ios>       // left, right, internal
#include <iomanip>   // setw

using std::cout; using std::endl;
int main() {
    double dval = 3.14159;
    std::ios_base::fmtflags f(std::ios::scientific|std::ios::uppercase);
    cout << std::setiosflags(f);
    cout << dval << endl;                         // Output: 3.141590E+00
    cout << std::resetiosflags(f) << dval << endl; // Output: 3.14159
    cout << std::setprecision(3) << dval << endl;  // Output: 3.14
    cout << std::setw(10) << dval << endl;
    cout << std::setfill('*') << 1246 << endl;     // Output: ******1246
}
```
```

**Listing 27.8** Number formats in output.

First, I store a few format flags in the bitmask of type `fmtflags`. You can combine multiple flags using the `|` operator. Then I set the flags so that a floating-point number appears in exponent format and the `e` is capitalized. You don't necessarily have to create `ios_base::fmtflags`; you can also write the flags directly into `setiosflags`. Then I