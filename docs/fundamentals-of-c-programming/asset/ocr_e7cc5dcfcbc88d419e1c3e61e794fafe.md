If you have studied calculus, you can confirm that f's derivative, f', is:

$f'(x) = 6x$

Without a knowledge of calculus, simply just accept this as the correct answer so we can test our derivative function.

Listing 20.17 (derivative.cpp) uses the derivative function on f(x) = 3x^2 + 5 and compares its results with the known solution, f'(x) = 6x.

```
Listing 20.17: derivative.cpp
#include <iostream>
#include <iomanip>
#include <functional>

// Approximates the derivative of function f given an h value.
// The closer h is to zero, the better the estimate.
std::function<double(double)> derivative(std::function<double(double)> f,
                                         double h) {
    // Capture function f and h value
    double h;
    return [f, h] (double x) { return (f(x + h) - f(x)) / h; };
}

double fun(double x) { // The function we wish to differentiate
    return 3*x*x + 5;
}

double ans(double x) { // The known derivative of function fun
    return 6*x;
}

int main() {
    // Difference: Approximation better as h -> 0
    double h = 0.0000001;

    // Compute the function representing an approximation
    // of the derivative of function fun
    auto der = derivative(fun, h);

    // Compare the computed derivative to the exact derivative
    // derived symbolically
    double x = 5.0;
    std::cout << "\n"
              << std::cout << " "
    std::cout << "\n x       f(x)      h       Approx.   Actual \\n";
    std::cout << "\n -----------------------------------------------\\n";
    while (x < 5.1) {
        std::cout << std::fixed << std::showpoint << std::setprecision(5);
        std::cout << x << " " << fun(x) << " " << h << " " << der(x)
                  << " " << ans(x) << "\\n";
        x += 0.01;
    }
}
```

With h = 0.0000001, Listing 20.17 (derivative.cpp) produces good results to the fifth decimal place: