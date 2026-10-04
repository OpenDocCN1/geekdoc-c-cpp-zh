# 85. Write a program that displays the sine and cosine value of all numbers from 0 to 6.3, with a step of 0.1, using Taylor series to calculate the respective sines and cosines.

```
#include <iostream>
#include <cmath>
```

```
int main() {
    const double STEP_SIZE = 0.1;
    const double END_POINT = 6.3;
```

```
for(double x = 0; x <= END_POINT; x += STEP_SIZE) {
    // Calculate sine using Taylor series
    double sine_of_x = x;
    double term = x;
    double power_of_x = x;
    double factorial = 1;
```