# 11) Write a program for calculating the result of cosine series.

**Algorithm:**

+   - Step 1: Start
+   - Step 2: Initialize N = 20;
+   - Step 3: Read x
+   - Step 4: Convert x values into radian using formula x = x*3.1412/180
+   - Step 5: Term = 1, sum = 1
+   - Step 6: Setup for loop from i = 1 until i <n+1> increment i
+   - Step 7: Term=(Term*pow(double)(1),(double) (2*i-1))*x*x/(2*i*(2*i-1))
+   - Step 8: sum = sum + Term
+   - Step 9: Print sum
+   - Step10: Stop

**Program:**

```
```c
#include<Stdio.h>
#include<conio.h>
#include<math.h>
void main()
{
    float x, a, sum, term;
    int i, no = 20, mul;
    printf("\n Enter the value of x: ");
    scanf("%f", &x);
    a = x;
    x = x*3.1412/180;
    term = 1;
    sum = 1;
    for(i=1; i < no +1; i++)
    {
        term = term *pow((double)(-1), (double)(2 * i -1))* x * x /(2 * i * (2 * i -1));
        sum = sum + term;
    }
    printf("\n the cosine value of %f is %f", a, sum);
    getch();
}
```
```

**Output:**

Enter the value of x: 60
The cosine value of 60.000000 is 0.500113