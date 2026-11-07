An increment or decrement operator placed before (prefixed to) a variable is called the prefix increment or prefix decrement operator, respectively. An increment or decrement operator placed after (postfixed to) a variable is called the postfix increment or postfix decrement operator, respectively.

Using the prefix increment (or decrement) operator to add 1 to (or subtract 1 from) a variable preincrements (or predecrements) the variable. The variable is incremented (or decremented) by 1, then its new value is used in the expression in which it appears.

Using the postfix increment (or decrement) operator to add 1 to (or subtract 1 from) a variable postincrements (or postdecrements) the variable. The variable’s value before the increment (or decrement) is used in the expression. Unlike binary operators, the unary increment and decrement operators by convention should be placed next to their operands, with no intervening spaces.

# Prefix Increment vs. Postfix Increment

Figure 3.4 demonstrates the difference between the prefix increment and postfix increment versions of the ++ increment operator. The decrement operator (--) works similarly.

```
```cpp
// fig03_04.cpp
// Prefix increment and postfix increment operators.
#include <iostream>
using namespace std;

int main() {
    // demonstrate postfix increment operator
    int c{5};
    cout << " before postincrement: " << c << "\n"; // prints 5
    cout << "    postincrementing c: " << c++ << "\n"; // prints 5
    cout << " after postincrement: " << c << "\n"; // prints 6

    cout << "\n"; // skip a line

    // demonstrate prefix increment operator
    c = 5;
    cout << " before preincrement: " << c << "\n"; // prints 5
    cout << "    preincrementing c: " << ++c << "\n"; // prints 6
    cout << " after preincrement: " << c << "\n"; // prints 6
}
```

```
```text
c before postincrement: 5
    postincrementing c: 5
c after postincrement: 6

c before preincrement: 5
    preincrementing c: 6
c after preincrement: 6
```
```

**Fig. 3.4** | Prefix increment and postfix increment operators.

Line 8 initializes the variable c to 5, and line 9 outputs c’s initial value. Line 10 outputs the value of the expression c++. This expression postincrements the variable c, so c’s