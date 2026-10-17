```
}
else if (discriminant == 0)
{
// One real root (repeated)
root1 = -b / (2 * a);
printf("Root 1 = Root 2 = %.2lf\n", root1);
}
else
{
// Complex roots
double realPart = -b / (2 * a);
double imaginaryPart = sqrt(-discriminant) / (2 * a);
printf("Root 1 = %.2lf + %.2lfi and Root 2 = %.2lf - %.2lfi\n", realPart, imaginaryPart, realPart, imaginaryPart);
}
return 0; // Exit successfully
}
```

+   - **Practical 13:** To find the factorial of a given integer.
+   - **Solution:**

```
#include <stdio.h>
int main()
{
int n;
unsigned long long factorial = 1;
// Input the integer for which you want to find the factorial
printf("Enter a non-negative integer: ");
scanf("%d", &n);
// Check if n is negative
if (n < 0)
{
printf("Factorial is not defined for negative integers.\n");
return 1; // Exit with an error code
```