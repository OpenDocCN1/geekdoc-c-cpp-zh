```
// fig05_03.c
// Demonstrating the function-call stack
// and stack frames using a function square.
#include <stdio.h>

int square(int x); // prototype for function square

int main() {
    int a = 10; // value to square (local variable in main)
    printf("%d squared: %d\n", a, square(a)); // display a squared
}

// returns the square of an integer
int square(int x) { // x is a local variable
    return x * x; // calculate square and return result
}
```

10 squared: 100

Fig. 5.3 | Demonstrating the function-call stack and stack frames using a function square.

# Step 1: Operating System Invokes main to Execute Application

First, the operating system calls main—this pushes a stack frame onto the stack (as shown in the following diagram). The stack frame tells main how to return to the operating system (that is, transfer to return address R1) and contains the space for main's local variable a, which is initialized to 10.

![](bbox=[0.15, 0.7, 0.9, 0.9])

# Step 2: main Invokes Function square to Perform Calculation

Function main—before returning to the operating system—now calls function square in line 11 of Fig. 5.3. This causes a stack frame for square (lines 15–17) to be pushed onto the function-call stack, as shown in the following diagram: