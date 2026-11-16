
[] (int x, int y) { std::cout << x << " " << y << '\n'; } (10, 20);

prints

```
10 20
```

Observe that this statement defines the lambda function and explicitly invokes it.

The following two statements:

```
auto f = [] (int x) { return 5*x; };
std::cout << f(10) << '\n';
```

show how we can assign a lambda function to a variable and invoke it through that variable at a later time.

One interesting aspect of lambda functions is that they can be used to create closures. A closure is a unit of code (in this case a function-like object) that can capture variables from its surrounding context. These captured variables then can be used outside of their original context. In order to demonstrate closure, we first must explore function objects.

A std::function object works like a function pointer (see Section 10.10). The std::function class is a generic class parameterized by a function's type specifications. We can declare a function object representing a function that accepts two integer parameters and returns an integer result as

```
std::function<int(int, int)> f;
```

Note the type parameter int(int, int) inside the angle brackets. The first int represents the function's return type. The two ints inside the parentheses specify the function's parameters. Function objects take the place of function pointers. Function pointers are available in C as well as C++, but C does not provide function objects. Function objects provide capabilities above simple function pointers, including the ability to manage closures.

Listing 20.15 (closurein.cpp) demonstrates a simple closure.

```
Listing 20.15: closurein.cpp
#include <iostream>
#include <functional>
int evaluate2(std::function<int(int, int)> f, int x, int y) {
    return f(x, y);
}
int main() {
    int a;
    std::cout << "Enter an integer: ";
    std::cin >> a;
    std::cout << evaluate2([a](int x, int y) {
        if (x == a)
            x = 0;
        else
            y++;
        return x + y;
    }, 2, 3) << '\n';
}
```

Note that main creates a function via the lambda expression that it passes to evaluate2. The variable a appears within the capture square brackets. This makes a's value available to whatever code invokes the lambda function. In this case the evaluate2 function can see a's value even though a is local to main and is not passed to evaluate2 as an explicit parameter.

We say the lambda function captures the variable a. When evaluate2 invokes the function sent by the caller, evaluate2 has no access to a variable named a. The a involved in the conditional expression is captured from main. This is an example of a closure transporting a captured variable into a function call.

For an example of a closure transporting a captured local variable out of a function, consider Listing 20.16 (makeadder.cpp) which includes a function that returns a lambda function to its caller.

### Listing 20.16: makeadder.cpp

```
#include <iostream>
#include <functional>

std::function<int(int)> make_adder() {
    int loc_val = 2; // Local variable definition
    return [loc_val](int x) { return x + loc_val; }; // Returns a function
}

int main() {
    auto f = make_adder();
    std::cout << f(10) << '\n';
    std::cout << f(2) << '\n';
}
```

Ordinarily when a function returns, all of its local variables disappear. This means that after the following statement in the main function executes:

```
auto f = make_adder();
```

make_adder's loc_val local variable should no longer exist. The function that make_adder returns, however, uses loc_val in its computation. This means the function that make_adder returns forms a closure that captures make_adder's local variable loc_val. In the output of Listing 20.16 (makeadder.cpp) we can see that function f still has knowledge of loc_val's value:

```
12
4
```

C++'s lambda capture mechanism provides capabilities that go beyond the examples shown here; for example, the expression &a within the square brackets would capture variable a by reference, allowing an external context to modify the variable. Note that when a closure captures a variable by reference, that variable must exist in its original context as long as the closure is viable. This means you should not attempt to capture a local non-static variable of a function by reference by a closure to be returned by that function. The local variables disappear when the function returns, and so the references will refer to garbage values.

We can assign a variable to a lambda function; for example, the following code fragment:

```
auto f = [](int x) { return 2*x; };
std::cout << f(10) << '\n';
```

will print 20. This gives the function a name, so the statement

```
auto f = [](int x) { return 2*x; };
```

is roughly equivalent to the function definition

```
int f(int x) {
    return 2*x;
}
```

While not a particularly useful application of lambda functions, to demonstrate the regularity of the C++ language, we can define an anonymous function and invoke it immediately; for example, the statement

```
std::cout << [](int x, int y) { return x * y; }(2, 3);
```

prints 6. In this case the statement

```
std::cout << 2*3 << '\n';
```

or, even better,

```
std::cout << 6 << '\n';
```

produces the same result much more simply.

As a more practical example using a lambda function and a closure, consider the calculation of a derivative. Those familiar with basic calculus will recall the derivative of a function f at a is defined to be

\( f'(a) = \lim_{h \to 0} \frac{f(a+h)-f(a)}{h} \)

If you are unfamiliar with calculus, all you need to know is that the derivative of a function is itself a function; the above formula shows how to transform a function into its derivative. The process of computing a derivative is known as differentiation. The lim_{h->0} notation indicates that the answer becomes more precise as the value h gets closer to zero. Letting h be exactly zero would result in division by zero, which is undefined. The trick is to make h as small as possible, keeping in mind that the computer's floating-point values have limitations.

Based on the mathematical definition we can define a C++ function that computes the derivative of another function, as shown here:

```
std::function<double(double)> derivative(std::function<double(double)> f,
                                         double h) {
    // Capture function f and h value and return the function's derivative
    return [f, h](double x) { return (f(x + h) - f(x)) / h; };
}
```

Note that the derivative function returns a function, as a lambda expression is a simple function definition. The function that derivative returns is a closure because it captures the function parameters f and h.

Our derivative function allows us to compute the derivative of a function at a given value. This is known as numerical differentiation. Another approach (the one emphasized in calculus courses) uses symbolic differentiation. Symbolic differentiation transforms the formula for a function into a different formula. The details of symbolic differentiation are beyond the scope of this text, but we will use one of its results for a particular function to check our computed numerical results.

A particular function f is defined as follows:

\( f(x) = 3x^2 + 5 \)

If you have studied calculus, you can confirm that f's derivative, f', is:

\( f'(x) = 6x \)

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
    std::cout << "\n";
    std::cout << " x       f(x)      h       Approx.   Actual \n";
    std::cout << "\n -----------------------------------------------\n";
    while (x < 5.1) {
        std::cout << std::fixed << std::showpoint << std::setprecision(5);
        std::cout << x << " " << fun(x) << " " << h << " " << der(x)
                  << " " << ans(x) << "\n";
        x += 0.01;
    }
}
```

With h = 0.0000001, Listing 20.17 (derivative.cpp) produces good results to the fifth decimal place:
