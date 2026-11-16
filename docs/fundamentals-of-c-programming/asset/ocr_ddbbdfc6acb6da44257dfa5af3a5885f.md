+   1. The function must optionally call itself within its definition; this is the *recursive case*.
+   2. The function must optionally *not* call itself within its definition; this is the *base case*.
+   3. Some sort of conditional execution (such as an *if/else* statement) selects between the recursive case and the base case based on one or more parameters passed to the function.
+   4. Each invocation that does not correspond to the base case must call itself with parameter(s) that move the execution closer to the base case. The function's recursive execution must converge to the base case.

Each recursive invocation must bring the function's execution closer to it base case. The *factorial* function calls itself in the *else* clause of the *if/else* statement. Its base case is executed if the condition of the *if* statement is true. Since the factorial is defined only for nonnegative integers, the initial invocation of *factorial* must be passed a value of zero or greater. A zero parameter (the base case) results in no recursive call. Any other positive parameter results in a recursive call with a parameter that is closer to zero than the one before. The nature of the recursive process progresses towards the base case, upon which the recursion terminates.

We can easily write a non-recursive factorial function, as Listing 10.7 (*nonrecursivefact.cpp*) shows.

```
Listing 10.7: nonrecursivefact.cpp
```cpp
#include <iostream>

/*
 * factorial(n)
 * Computes n!
 * Returns the factorial of n.
 */
int factorial(int n) {
    int product = 1;
    for (int i = n; i > 0; i--)
        product *= i;
    return product;
}

int main() {
    // Try out the factorial function
    std::cout << " 0! = " << factorial(0) << '\n';
    std::cout << " 1! = " << factorial(1) << '\n';
    std::cout << " 6! = " << factorial(6) << '\n';
    std::cout << "10! = " << factorial(10) << '\n';
}
```
```

Which *factorial* function is better, the recursive or non-recursive version? Generally, if the same basic algorithm is being used by both the recursive and non-recursive functions, then the non-recursive function will be more efficient. A function call is a relatively expensive operation compared to a variable assignment or comparison. The body of the non-recursive function invokes no functions, but the recursive version calls a function—it calls itself—during all but the last recursive invocation. The iterative version of *factorial* is therefore more efficient than the recursive version.

Even though the iterative version of the factorial function is technically more efficient than the recursive version, on most systems you could not tell the difference. The execution time difference between the two versions is negligible. The reason is the factorial function “grows” fast, meaning it returns fairly large