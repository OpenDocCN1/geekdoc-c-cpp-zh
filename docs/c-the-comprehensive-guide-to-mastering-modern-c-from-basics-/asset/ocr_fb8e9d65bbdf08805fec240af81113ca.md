cout << endl;
}

# Listing 4.5 A custom C++ function.

In the function itself, compared to Listing 4.1, from /* Output divisors */ everything is almost identical. You will actually find only an alternative notation to divider = divider + 1 in the increment part of the for loop with ++divider. So far, you have used the assignment. Here, ++divider is used as a side effect operator to change the value of divider.

# 4.2.4 Side Effect Operators

This is the prefix operator ++, which normally increases a variable by one (“increments”). This results in an expression whose value is the value of the variable increased by one. The result of the expression is unimportant in the update part of the for loop, but you can use the value within a more complex expression, as in the next example.

```
// https://godbolt.org/z/4Mr6fnaEr
#include <iostream> // cout
int main() {
    int basis = 2;
    int index = 10;
    int number = 3 * (basis ++index) - 1; // index is incremented first
    std::cout << number << '\n';    // Output: 38
}
```

# Listing 4.6 Prefix operators are executed before the calculation.