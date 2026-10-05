# 4.9 Algorithms

An algorithm is a finite sequence of steps, each step taking a finite length of time, that solves a problem or computes a result. A computer program is one example of an algorithm, as is a recipe to make lasagna. In both of these, the order of steps matters. In the case of lasagna, the noodles must be cooked in boiling water before they are layered into the filling to be baked. It would be inappropriate to place the raw noodles into the pan with all the other ingredients, bake it, and then remove the already baked noodles to cook them in boiling water separately. In the same way, the ordering of steps is very important in a computer program. While this point may be obvious, consider the following sound argument:

+   1. The relationship between degrees Celsius and degrees Fahrenheit can be expressed as

$$C = \frac{5}{9}\times(F - 32)$$

+   2. A temperature in degrees Fahrenheit, the corresponding temperature in degrees Celsius be computed.

Armed with this knowledge, Listing 4.14 (faultytempconv.cpp) follows directly.

```
Listing 4.14: faultytempconv.cpp
// File faultytempconv.cpp

#include <iostream>

using namespace std;

int main({
    double degreesF = 0, degreesC = 0;
    // Define the relationship between F and C
    degreesC = 5.0/9*(degreesF - 32);
    // Prompt user for degrees F
    cout << "Enter the temperature in degrees F: ";
    // Read in the user's input
    cin >> degreesF;
    // Report the result
    cout << degreesC << endl;
}
```

Unfortunately, the executing program displays

![](bbox=[0.176, 0.761, 0.842, 0.818])

regardless of the input provided. The English description provided above is correct. No integer division problems occur, as in Listing 4.10 (tempconv.cpp). The problem lies simply in statement ordering. The statement

degreesC = 5.0/9*(degreesF - 32);