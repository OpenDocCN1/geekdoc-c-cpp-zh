```
double u, a, t, distance;
int num_intervals;
printf("Enter initial velocity (u) in m/sec: ");
scanf("%lf", &u);
printf("Enter acceleration (a) in m/sec^2: ");
scanf("%lf", &a);
printf("Enter the number of time intervals: ");
scanf("%d", &num_intervals);
for (int i = 1; i <= num_intervals; i++)
{
printf("Enter time interval %d in seconds: ", i);
scanf("%lf", &t);
distance = u * t + 0.5 * a * t * t;
printf("Distance traveled at time %.2lf seconds: %.2lf meters\n", t, distance);
}
return 0;
}
```

+   - Practical 7: Write a C program, which takes two integer operands and one operator from the user, performs the operation and then prints the result. (Consider the operators +, -, /, % and use Switch Statement)

+   - Solution:

```
#include <stdio.h>
int main()
{
int operand1, operand2;
char operator;
printf("Enter two integer operands: ");
scanf("%d %d", &operand1, &operand2);
printf("Enter an operator (+, -, *, /, %%): ");
scanf(" %c", &operator); // Notice the space before %c to consume any
```