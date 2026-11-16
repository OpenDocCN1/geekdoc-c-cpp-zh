+   • The swap function's
+   
+   * b = temp;
+   
+   statement assigns the local temp value to main's var2 variable, since swap's b parameter points to main's var2.

+   • Within main, the call
+   
+   swap(&var1, &var2);
+   
+   passes the addresses of its local variables to swap.

In reality, pass by reference with pointers is still using pass by value. Instead of passing copies of values, we are passing copies of addresses. In Listing 10.18 (swapwithpointers.cpp), for example, the values of the addresses of var1 and var2 are copied to the formal parameters a and b. The difference is we are not attempting to reassign a or b; we are reassigning memory to which a and b point. Whether we use the original address or a copy of the address, it is still the same address—the same numeric location in memory.

# ## 10.9.2 Pass by Reference via References

Both C and C++ support pass by reference with pointers (see Section 10.9.1). Since C++ programs often use C libraries, C++ programmers must be familiar with the pointer technique for pass by reference. C++, however, provides a simpler way of implementing pass by reference using _reference parameters_. (See Section 10.8 for an introduction to reference variables.) Listing 10.19 (swapwithreferences.cpp) uses reference parameters in our variable interchange program.

```
Listing 10.19: swapwithreferences.cpp

#include <iostream>

/*
 * swap(a, b)
 *  Interchanges the values of memory
 *  referenced by its parameters a and b.
 *  It effectively interchanges the values
 *  of variables in the caller's context.
 */
void swap(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

/*
 * main
 *  Interchanges the values of two variables
 *  using the swap function.
 */
int main() {
    int var1 = 5, var2 = 19;
    std::cout << "var1 = " << var1 << ", var2 = " << var2 << '\n';
    swap(var1, var2);
    std::cout << "var1 = " << var1 << ", var2 = " << var2 << '\n';
}
```