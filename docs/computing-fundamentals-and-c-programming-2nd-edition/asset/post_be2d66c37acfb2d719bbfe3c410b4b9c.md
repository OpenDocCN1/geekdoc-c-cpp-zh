
```text
    20
    Enter Employees in Group - 5 : 11
    11
               |
    Group-1    |************
               |************** (12)
               |************
               |
    Group-2    |************************
               |************************** (23)
               |************************
               |
    Group-3    |**********************************************
               |************************************************ (35)
               |**********************************************
               |
    Group-4    |************************
               |************************** (20)
               |************************
               |
    Group-5    |************
               |************** (11)
               |************
               |
```

**Fig. 8.17** Program to draw a histogram

## 3. Minimum Cost [LO 8.3, 8.4 M]

**Problem:** The cost of operation of a unit consists of two components C1 and C2 which can be expressed as functions of a parameter p as follows:

C1 = 30 - 8p  
C2 = 10 + p²

The parameter p ranges from 0 to 10. Determine the value of p with an accuracy of ±0.1 where the cost of operation would be minimum.

**Problem Analysis:**

Total cost = C1 + C2 = 40 - 8p + p²

The cost is 40 when p = 0, and 33 when p = 1 and 60 when p = 10. The cost, therefore, decreases first and then increases. The program in Fig. 8.18 evaluates the cost at successive intervals of p (in steps of 0.1) and stops when the cost begins to increase. The program employs **break** and **continue** statements to exit the loop.

Program

```c
main()
{
    float p, cost, p1, cost1;
    for (p = 0; p <= 10; p = p + 0.1)
    {
        cost = 40 - 8 * p + p * p;
        if (p == 0)
        {
            cost1 = cost;
            continue;
        }
        if (cost >= cost1)
            break;
        cost1 = cost;
        p1 = p;
    }
    p = (p + p1) / 2.0;
    cost = 40 - 8 * p + p * p;
    printf("\nMINIMUM COST = %.2f At p = %.1f\n", cost, p);
}
```

Output

```text
MINIMUM COST = 24.00 At p = 4.0
```

**Fig. 8.18** Program of minimum cost problem

## 4. Plotting of Two Functions [LO 8.3, 8.4 H]

**Problem:** We have two functions of the type

y1 = exp (-ax)

y2 = exp (-ax²/2)

Plot the graphs of these functions for x varying from 0 to 5.0.

**Problem Analysis:** Initially when x = 0, y1 = y2 =1 and the graphs start from the same point. The curves cross when they are again equal at x = 2.0. The program should have appropriate branch statements to print the graph points at the following three conditions:

- 1. y1 > y2
- 2. y1 < y2
- 3. y1 = y2

The functions y1 and y2 are normalized and converted to integers as follows:

y1 = 50 exp (-ax) + 0.5

y2 = 50 exp (-ax²/2) + 0.5

The program in Fig. 8.19 plots these two functions simultaneously. (0 for y1, * for y2, and # for the common point).

Program

```c
#include <math.h>
main()
{
    int i;
    float a, x, y1, y2;
    a = 0.4;
    printf("                 Y ------>                 \n");
    printf("0 ------------------------------->\n");
    for (x = 0; x < 5; x = x + 0.25)
    /* BEGINNING OF FOR LOOP */
    /*......Evaluation of functions .......*/
        y1 = (int)(50 * exp(-a * x) + 0.5);
        y2 = (int)(50 * exp(-a * x / 2) + 0.5);
    /*......Plotting when y1 = y2..........*/
        if (y1 == y2)
        {
            if (x == 2.5)
                printf(" X  |");
            else
                printf("*|");
            for (i = 1; i <= y1 - 1; ++i)
                printf(" ");
            printf("#\n");
            continue;
        }
    /*...... Plotting when y1 > y2 .....*/
        if (y1 > y2)
        {
            if (x == 2.5)
                printf(" X |");
            else
                printf("  |");
            for (i = 1; i <= y2 - 1; ++i)
                printf(" ");
            printf("#");
            for (i = 1; i <= (y1 - y2 - 1); ++i)
                printf("-");
```

- **6.** Explain the operation of each of the following **for** loops.

LO 8.3

```c
for (n = 1; n != 10; n += 2)
    sum = sum + n;
```

```c
for (n = 5; n <= m; n -= 1)
    sum = sum + n;
```

```c
for (n = 1; n <= 5;)
    sum = sum + n;
```

```c
for (n = 1; ; n = n + 1)
    sum = sum + n;
```

```c
for (n = 1; n < 5; n++)
    n = n - 1;
```

- **7.** What would be the output of each of the following code segments?

LO 8.1

```c
count = 5;
while (count-- > 0)
    printf("%d", count);
```

LO 8.1

```c
count = 5;
while (--count > 0)
    printf("%d", count);
```

LO 8.2

```c
count = 5;
do
    printf("%d", count);
while (count > 0);
```

LO 8.3

```c
for (m = 10; m > 7; m -= 2)
    printf("%d", m);
```

- **8.** Compare, in terms of their functions, the following pairs of statements:

    - (a) while and do...while [LO 8.2]
    - (b) while and for [LO 8.3]
    - (c) break and continue [LO 8.4]
    - (d) break and goto [LO 8.4]
    - (e) continue and goto [LO 8.4]

- **9.** Analyse each of the program segments that follow and determine how many times the body of each loop will be executed.

LO 8.1

```c
x = 5;
y = 50;
while (x <= y)
{
    x = y / x;
    ----
    ----
}
```

LO 8.1

```c
int m = 10;
int n = 7;
while (m % n >= 0)
```

```c
continue ;
m = m + 10 ;
} while (m < 50) ;
printf("%d", m);
```

- **15.** What is the output of the following code?

```c
int n = 0, m = 1 ;
do
{
    printf("%d", n) ;
    m++ ;
}
while (m <= n) ;
```

LO 8.2

- **16.** What is the output of the following code?

```c
int n = 0, m ;
for (m = 1; m <= n + 1 ; m++ )
    printf("%d", m);
```

LO 8.3

- **17.** When do we use the following statement?

```c
for ( ; ; )
```

LO 8.3

## DEBUGGING EXERCISES

- **1.** Find errors, if any, in each of the following looping segments. Assume that all the variables have been declared and assigned values.

    - (a)

      ```c
      while (count != 10);
      {
          count = 1;
          sum = sum + x;
          count = count + 1;
      }
      ```

    - (b)

      ```c
      name = 0;
      do {
          name = name + 1;
          printf("My name is John\n");
      } while (name = 1)
      ```

    - (c)

      ```c
      do;
          total = total + value;
          scanf("%f", &value);
      while (value != 999);
      ```

    - (d)

      ```c
      for (x = 1, x > 10; x = x + 1)
      {
          -------
          -------
      }
      ```

LO 8.1

LO 8.2

LO 8.3

LO 8.3

    - (e)

      ```c
      m = 1;
      n = 0;
      for (; m < n < 10; ++n);
          printf("Hello\n");
          m = m + 10
      ```

    - (f)

      ```c
      for (p = 10; p > 0;)
          p = p - 1;
      printf("%f", p);
      ```

## PROGRAMMING EXERCISES

- **1.** Given a number, write a program using while loop to reverse the digits of the number. For example, the number `12345` should be written as `54321`. (**Hint:** Use modulus operator to extract the last digit and the integer division by 10 to get the n-1 digit number from the n digit number.)

- **2.** The factorial of an integer m is the product of consecutive integers from 1 to m. That is, factorial m = m! = m x (m-1) x ... x 1. Write a program that computes and prints a table of factorials for any given m.

- **3.** Write a program to compute the sum of the digits of a given integer number.

- **4.** The numbers in the sequence `1 1 2 3 5 8 13 21 ...` are called Fibonacci numbers. Write a program using a **do...while** loop to calculate and print the first n Fibonacci numbers. (**Hint:** After the first two numbers in the series, each number is the sum of the two preceding numbers.)

- **5.** Rewrite the program of the Example 8.1 using the **for** statement.

- **6.** Write a program to evaluate the following investment equation `V = P(1+r)^n` and print the tables which would give the value of V for various combination of the following values of P, r, and n.

    - P: 1000, 2000, 3000, ..., 10,000
    - r: 0.10, 0.11, 0.12, ..., 0.20
    - n: 1, 2, 3, ..., 10

  (**Hint:** P is the principal amount and V is the value of money at the end of n years. This equation can be recursively written as `V = P(1+r)`, `P = V`. That is, the value of money at the end of first year becomes the principal amount for the next year and so on.)
