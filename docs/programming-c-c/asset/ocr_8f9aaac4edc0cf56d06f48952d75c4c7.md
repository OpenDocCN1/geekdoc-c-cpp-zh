```
#include<stdio.h>
int main() {
    int marks=83;
    if (marks>75) {
        printf("First class");
    } else if (marks>65) {
        printf("Second class");
    } else if (marks>55) {
        printf("Third class");
    } else {
        printf("Fourth class");
    }
    return 0;
}
```

+   1. We have initialized a variable with marks. In the else-if ladder structure, we have provided various conditions.
2. The value from the variable marks will be compared with the first condition. Since it is true, the statement associated with it will be printed on the output screen.
3. If the first test condition turns out false, then it is compared with the second condition.
4. This process will go on until the all expression is evaluated otherwise control will go out of the else-if ladder, and default statement will be printed.

# Nested if-else Statements

When a series of decision is required, nested if-else is used. Nesting means using one if-else construct within another one.

Let's write a program to illustrate the use of nested if-else.

```
#include<stdio.h>
int main() {
    intnum=1;
```