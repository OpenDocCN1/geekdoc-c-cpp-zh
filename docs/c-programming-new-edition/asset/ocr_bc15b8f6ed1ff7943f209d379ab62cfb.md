```
```c
printf("Please enter a positive integer greater than 1.\n");
return 1; // Exit with an error code
}
printf("Prime numbers between 1 and %d are:\n", n);
// Generate and print prime numbers between 1 and n
for (int i = 2; i <= n; i++)
{
    if (is_prime(i))
    {
        printf("%d ", i);
    }
}
printf("\n");
return 0; // Exit successfully
}
```
```

+   - **Practical 11:** Write a C program to calculate the following Sum:
+     `Sum=1-x^2/2!+x^4/4!-x^6/6!+x^8/8!-x^10/10!.`

+   - **Solution:**

```
```c
#include <stdio.h>
#include <math.h>

int main()
{
    double x;
    int n;
    double sum = 1.0;
    // Input the value of x and the number of terms (n)
    printf("Enter the value of x: ");
    scanf("%lf", &x);
    printf("Enter the number of terms (n): ");
    scanf("%d", &n);
    // Calculate and print the sum
    for (int i = 1; i <= n; i++)
```
```