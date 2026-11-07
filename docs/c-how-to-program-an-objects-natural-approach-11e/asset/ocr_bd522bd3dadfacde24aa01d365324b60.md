The three-argument version adds the **common range**’s elements by default. The four-argument version receives as its last argument a **binary function** that customizes how to perform the calculation. That argument can be supplied as:

+   - a **function pointer to a binary function** that takes two parameters of the **common range**’s element type and returns a result of that type,
+   - a binary function object in which the **operator()** function takes two parameters of the **common range**’s element type and returns a result of that type, or
+   - a **lambda** that takes two parameters of the **common range**’s element type and returns a result of that type.

This example calls **accumulate** with a function pointer, then a function object, then a lambda.

```
```cpp
// fig14_16.cpp
// Demonstrating function objects.
#include <array>
#include <algorithm>
#include <functional>
#include <iostream>
#include <iterator>
#include <numeric>
```
```

**Fig. 14.16**  Demonstrating function objects.

# ## Function sumSquares

Lines 12–14 define a function **sumSquares** that takes two arguments of the same type and returns a value of that type—the requirements for the **binary function** that **accumulate** can receive as an argument. The sumSquares function returns the sum of its first argument total and the square of its second argument value.

```
```cpp
// binary function returns the sum of its first argument total
// and the square of its second argument value
int sumSquares(int total, int value) {
    return total + value * value;
}
```
```

# ## Class SumSquaresClass

Lines 19–25 define class SumSquaresClass.³¹ Its overloaded **operator()** has two int parameters and returns an int. This meets the requirements for the binary function that accumulate can call when processing a **common range** of ints. Function **operator()** returns the sum of its first argument total and the square of its second argument value.

31. This class handles only int values, but could be implemented as a class template that handles many types—we’ll define custom class templates in Chapter 15.