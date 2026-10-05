# FUNCTIONS

```
#include<stdio.h>
#include <conio.h>
int factorial(int);
void main() {
    int num, fact;
    printf("...Finding the FACTORIAL value: ...\n\n");
    printf("\nenter the number:\n\n    scanf("%d", &num);
    fact=factorial(num);
    printf("The factorial value is %d", fact);
    getch();
}

int factorial(int num) {
    if(num==1||num==0)
        return 1;
    else
        return num*factorial(num-1);
}
```

![](bbox=[0.475, 0.285, 0.635, 0.335])

Finding the FACTORIAL Value...................
enter the number:6
The factorial value is 720-

# Output 5.9 Factorial using recursion

One example would make recursion clearer. Program 5.8 explains the Fibonacci series using recursion.
A quick glance of Fibonacci series problem goes here.

Given an integer value, a series will be generated as follows. Let the integer number 7, Then the series would be, 0 → 1 → 1 → 2 → 3 → 5 → 8. What is the logic behind the series generation? Every number in the series is the sum of its immediate 2 predecessors from 3rd value. First two numbers are 0, 1 by default.

Refer Program 5.10 Recursive solution to Fibonacci series.

```
#include<stdio.h>
#include<conio.h>
void main() {
    void fibonacci(int, int, int);
    int n, fib;
    int a=1,b=1;
    printf("Enter the number:\n");
    scanf("%d",&n);
    fibonacci(a,b,n);
    getch();
}

void fibonacci(int a, int b, int n) {
    if(n>0) {
        printf("%d\t",a,a+b);
        fibonacci(b,a+b,n-1); //recursive call
    }
}
```

# Program 5.10 Recursive solution to Fibonacci series problem