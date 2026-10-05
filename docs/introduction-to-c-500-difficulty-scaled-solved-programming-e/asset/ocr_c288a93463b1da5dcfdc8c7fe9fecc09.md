# 486 Introduction to C++

The restriction to many functions with the same name is that each function must have a different. The signature of a function is determined by the number of parameters and their types; the names of the parameters don't matter. When an overloaded function is called, the compiler checks the name and the type of the arguments passed to it and determines which version to call. As a consequence, the polymorphism is achieved during the compilation of the program (static binding).

Although we can overload functions that perform entirely different tasks, overloading makes sense when used to overload functions that perform similar operations. Thus, there is no need to search for different function names and give the false impression to the reader that they perform different tasks. The same name indicates to that their operation is similar but with different types of data. For example, in the following program the abs_v() function is overloaded three times and the compiler selects the appropriate:

```
#include <iostream> // Example 16.10

int abs_v(int a);
double abs_v(double a);
void abs_v(int a, int b); // Display the absolute value of the sum.

int main() {
    int i = -100;
    double j = 1.2345;

    std::cout << abs_v(i) << ' ';
    std::cout << abs_v(j) << ' ';
    abs_v(i, 30);
    return 0;
}

int abs_v(int a) {
    if (a < 0)
        return -a;
    else
        return a;
}

double abs_v(double a) {
    if (a < 0)
        return -a;
    else
        return a;
}

void abs_v(int a, int b) {
    int sum;
    sum = a+b;
    if (sum < 0)
        std::cout << -sum << '\n';
    else
        std::cout << sum << '\n';
}
```