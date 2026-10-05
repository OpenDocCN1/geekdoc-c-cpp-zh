```
void f() {
{
    throw SomeErr();
}
```

As we know, to handle the exception from the derived class, we can still use the same catch block with the base reference. If we want to handle them differently, we just add before a catch block of the SomeErr type.

The standard library provides many exception types, we only mention some of them. The exception class logic_error and runtime_error classes are derived. These classes, as well as classes derived from them, are defined in the stdexcept file. From the logic_error class the domain_error, invalid_argument, length_error, and the out_of_range classes are derived, which deal with logical errors. Briefly, the domain_error is used to indicate the violation of the domain of a function (e.g., attempt to calculate the square root of a negative number), the invalid_argument is used to indicate unexpected arguments, the length_error is used to indicate that there is no enough space and the out_of_range is used to indicate out of range values (e.g., it is thrown if you use a vector object out of bounds index). For example, suppose that we have a Rectangle class. If a wrong dimension fails in the constructor we can an out_of_range exception, like this:

```
Rectangle::Rectangle(double w, double h) {
    if (w <= 0 || h <= 0) {
        throw out_of_range("Wrong dimension");
    }

}
```

From the runtime_error class the range_error, overflow_error, and underflow_error classes are derived, which deal with errors related to the value of valid range or the inability to represent values (e.g., due to overflow) in arithmetic calculations. For more information about the exception types consult a standard library reference.

Let's see the bad_alloc exception, which is thrown when the memory allocation with the new new[] operator fails, such because of unavailable memory. The bad_alloc class is defined in the new file and is derived from the exception. For example:

```
#include <iostream> // Example 22.8
#include <cstdlib>
#include <new>
```

```
int main() {
    int num;
    double *p;

    try {
        std::cout << "Enter number: ";
        std::cin >> num;
        p = new double[num];
    }
}
```