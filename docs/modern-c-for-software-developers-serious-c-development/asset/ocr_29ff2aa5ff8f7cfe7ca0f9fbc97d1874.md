memory location with a 5 value will not exist after the statement has finished executing.

The following shows examples of manipulating independent reference variables:

```
#include <iostream>
int main() {
    int a = 10;
    // independent reference to a
    int &r = a;

    // a and r have the same values
    std::cout << "a: " << a << " ref: " << r << "\n";

    // changing the value of r changes
    r = 100;
    std::cout << "a: " << a << " ref: " << r << "\n";

    // put variable b's value in r
    int b = 19;
    r = b;
    std::cout << "b: " << b << " a: " << a << " r: " << r << "\n";

    // decrementing r also decrements b
    r--;
    std::cout << "b: " << b << " r: " << r << "\n";

    // output
    a: 10 r: 10
    a: 100 r: 100
    b: 19 r: 19
    a: 18 r: 18
}}
```

# Restrictions On References

A number of restrictions apply to references:

+   * null references are prohibited (the implicit pointer cannot point to null)
* we cannot reference a reference. Put differently, we cannot obtain the address of a reference.
* we cannot create a pointer to a reference