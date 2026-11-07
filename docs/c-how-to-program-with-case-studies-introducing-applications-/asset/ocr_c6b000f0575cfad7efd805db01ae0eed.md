# main’s Return Type

The main function’s int return value indicates whether the program executed correctly. In earlier versions of C, we’d explicitly place

`return 0; // 0 indicates successful program termination`

at the end of main. The C standard indicates that main implicitly returns 0 if you omit the preceding statement—as we do throughout this book. You can explicitly return nonzero values from main to indicate that a problem occurred during your program’s execution. For information on how to report a program failure, see the documentation for your particular operating system.

# 5.3.2 maximum Function

Let’s consider a custom maximum function that returns the largest of three integers (Fig. 5.2). Next, they’re passed to maximum (line 17), which determines the largest integer. This value is returned to main by the return statement in maximum (line 32). The printf statement in line 17 then prints the value returned by maximum.

```
```c
// fig05_02.c
// Finding the maximum of three integers.
#include <stdio.h>

int maximum(int x, int y, int z); // function prototype

int main(void) {
   int number1 = 0; // first integer entered by the user
   int number2 = 0; // second integer entered by the user
   int number3 = 0; // third integer entered by the user

   printf("%s", "Enter three integers: ");
   scanf("%d%d%d", &number1, &number2, &number3);

   // number1, number2 and number3 are arguments
   // to the maximum function call
   printf("Maximum is: %d\n", maximum(number1, number2, number3));
}

// Function maximum definition
int maximum(int x, int y, int z) {
   int max = x; // assume x is largest

   if (y > max) { // if y is larger than max,
      max = y; // assign y to max
   }

   if (z > max) { // if z is larger than max,
      max = z; // assign z to max
   }

   return max; // max is largest value
}
```
```

**Fig. 5.2** | Finding the maximum of three integers. (Part 1 of 2.)