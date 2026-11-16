# 10.9 Pass by Reference

The default technique for passing parameters to functions is pass by value (see Section 9.3). C++ also supports pass by reference, also known as call by reference, which allows functions to alter the values of formal parameters passed by callers.

Consider Listing 10.17 (faultyswap.cpp), which uses a function that attempts to interchange the values of its two integer parameters.

```
Listing 10.17: faultySwap.cpp

#include <iostream>

/* swap(a, b)
 * Attempts to interchange the values of
 * its parameters a and b. That it does, but
 * unfortunately it only affects the local
 * copies.
 */
void swap(int a, int b) {
    int temp = a;
    a = b;
    b = temp;
}

/* main
 * Attempts to interchange the values of
 * two variables using a faulty swap function.
 */
int main() {
    int var1 = 5, var2 = 19;
    std::cout << "var1 = " << var1 << ", var2 = " << var2 << '\n';
    swap(var1, var2);
    std::cout << "var1 = " << var1 << ", var2 = " << var2 << '\n';
}
```

The output of Listing 10.17 (faultyswap.cpp) is

```
var1 = 5, var2 = 19
var1 = 5, var2 = 19
```

Unfortunately, the swap function simply interchanges copies of the actual parameters, not the actual parameters themselves. We really would like to write a function that interchanges the caller's variables.

Pass by reference is necessary to achieve the desired effect. C++ can do pass by reference in two ways: pointer parameters and reference parameters.

# 10.9.1 Pass by Reference via Pointers

Pointers (see Section 10.7) allow us to access the memory locations of variables. We can use this capability to allow a function to modify the values of variables that are owned by its caller. Listing 10.18 (swapwithpointers.cpp) provides a correct version of our variable interchange program.