```
else {
    std::cout << y;
    y = 0;
}
```

or, as in Listing 5.5 (betterfeedback.cpp), both the `if` body and the `else` body can be simple statements.

> Remember, if you wish to associate more than one statement with the body of the `if` or `else`, you must use a compound statement. Compound statements are enclosed within curly braces ({}).

If you ever attempt to use an if/else statement and discover that you need to leave the `else` clause empty, as in

```
if (x == 2)
    std::cout << "x = " << x << '\n';
else
    ; // Nothing to do otherwise
```

or, using a slightly different syntax, as

```
if (x == 2)
    std::cout << "x = " << x << '\n';
else // Nothing to do otherwise
}
```

you instead should use a simple `if` statement:

```
if (x == 2)
    std::cout << "x = " << x << '\n';
```

The empty `else` clauses shown above do work, but they complicate the code and make it more difficult for humans to read.

Due to the imprecise representation of floating-point numbers (see Listing 4.17 (imprecise5th.cpp) in Section 4.1), programmers must use caution when using the equality operator (`==`) by itself to compare floating-point expressions. Listing 5.6 (samedifferent.cpp) uses an `if`/`else` statement to demonstrate the perils of using the equality operator with floating-point quantities.

# Listing 5.6: samedifferent.cpp

```
#include <iostream>
#include <iomanip>

int main() {
    double d1 = 1.11 - 1.10,
           d2 = 2.11 - 2.10;
    std::cout << "d1 = " << d1 << '\n';
    std::cout << "d2 = " << d2 << '\n';
    if (d1 == d2)
        std::cout << "Same\n";
```