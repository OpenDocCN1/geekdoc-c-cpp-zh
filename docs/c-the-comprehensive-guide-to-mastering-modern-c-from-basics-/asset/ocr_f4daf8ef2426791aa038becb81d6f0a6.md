# 7.5 More about Parameters

C++, the declaration of the parameter in the function header determines how the parameter behaves when called. The most important distinction is whether the parameter is passed as a *value* or as a *reference*.

If you do not take any special precautions, the parameters of a function in C++ are passed as values *(call-by-value)*. This means that if a variable x currently has the value 5 and you pass x to a function, then the 5 ends up in the function—not the x.

```
// https://godbolt.org/8zcvMdM3b
#include <iostream>

void printval8(int n) { // parameter as value
    std::cout << n << " ";
    n = 8; // sets parameter to 8
}

 main() {
    int x = 5;
    printval8(x); // x as value: prints 5, then 8
    std::cout << x << "\"; // x remains unchanged at 5
    printval8(42); // 42 as value: prints 42, then 8
}
```

+   Listing 7.3 Parameters are initially passed as a value.

When *printval8* is called, the compiler copies the value of the arguments to the position n for the function. Therefore, the change at n=8; has no effect on the variable x with which *printval8(x)* was initially called.