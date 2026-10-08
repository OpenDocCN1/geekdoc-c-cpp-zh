The outer loop iterates to check up to 100 numbers. The inner loop checks whether a number is prime by checking whether it is divisible by any number between 2 and its square root. If it is not divisible, it is a prime number, and the number is printed.

# 8.6 Loop Control Statements

In C programming, loop control statements are powerful tools that allow one to modify the behavior of loops. Three commonly used loop control statements are break, continue and goto.

# 8.6.1 The break Statement

The break statement (see Fig. 8.4 is used to terminate the loop prematurely. When a break statement is encountered within a loop, the loop is immediately terminated, and program control is transferred to the statement following the loop. This statement is commonly used to exit loops based on certain conditions or to implement early termination logic.

```
while (test expression) {
  statement/s
  if (test expression) {
    break;
  }
  statement/s
}

do {
  statement/s
  if (test expression) {
    break;
  }
  statement/s
} while (test expression);
```

```
for (intial expression; test expression; update expression) {
  statement/s
  if (test expression) {
    break;
  }
  statements/
```

NOTE: The break statement may also be used inside body of else statement.

Figure 8.4: The break keyword

Consider the following example:

```
#include <stdio.h>

int main() {
```