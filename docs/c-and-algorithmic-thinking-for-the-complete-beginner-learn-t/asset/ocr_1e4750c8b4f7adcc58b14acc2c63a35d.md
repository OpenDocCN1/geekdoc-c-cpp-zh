```
}
```

> **Notice:** Please note that `M_PI` is a constant, not a function. This is why no parentheses are used.
> 
> **Notice:** The statement `cout.precision(20)` sets the maximum number of digits that the statement `cout` displays.

# Power

```
pow( number, exp )
```

This returns the result of `number` raised to the power of `exp`. It is defined in the `cmath` library.

# Example

```
```cpp
#include <iostream>
#include <cmath>
using namespace std;
int main() {
  double a, b, c;

  a = 2;
  b = 3;
  cout << pow(a, b) << endl;      //outputs: 8.0

  c = pow(3, 2);
  cout << c << endl;              //outputs: 9.0
  return 0;
}
```
```

> **Notice:** Function `pow()` can be used to calculate the square root of a number as well. It is known from mathematics that `√x = x^(1/2)`. So, you can write `y = pow(x, 1/2)` to calculate the square root of `x`, or you can even write `y = pow(x, 1/3)` to calculate the cube root of `x`, and so on!

# Random

```
rand()
```

This returns a pseudo-random integer in the range between 0 and RAND_MAX, where RAND_MAX is a constant of a value of at least 32767. Function `rand()` is defined in the `cstdlib` library.

# Example

```
```cpp
#include <iostream>
#include <cstdlib>
using namespace std;
```
```