# 5.40 Computer Programming

Numbers of Fibonacci sequence are known as Fibonacci numbers. First few numbers of series are 0, 1, 2, 3, 5, 8, etc. Except first two terms in sequence every other term is the sum of two previous terms. For example, 8 = 3 + 5 (addition of 3, 5). This sequence has many applications in mathematics and computer science.

```
#include <stdio.h>
#include <conio.h>
int fibonacci(int);
main()
{
    int n, i = 0, c;
    scanf("%d",&n);
    printf("Fibonacci Series in C using recursion\n");
    for (c = 1; c <= n; c++)
    {
        printf("%d\n", fibonacci(c));
        i++;
    }
    getch();
    return 0;
}
int fibonacci(int n)
{
    if (n == 0)
    return 0;
    else if (n == 1)
    return 1;
    else
    return ( fibonacci(n-1) + fibonacci(n-2) );
}
```

# 5.21 TOWER OF HANOI

The tower of Hanoi problem is a game, which comprises of three towers with discs stacked around the first tower initially. The game involves shifting the discs across the adjoining towers. There are some conditions that need to be adhered during the shifting:

+   1. A larger disk can not be placed on a smaller disk.
+   2. Only one disc can be shifted at a time.

The end objective is to replicate the initial stack of discs into another tower. Figure 5.18 shows a C program to realize the tower of Hanoi problem.

```
#include <conio.h>
#include <stdio.h>
void tower_hanoi ( int num_disk_f,char tower1, char tower2, char tower3)
```