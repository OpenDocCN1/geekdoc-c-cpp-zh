# **TABLE 5.2**

Tax Rates

| Income | Tax Rate (%) |
|---|---:|
| 0–12,000 | 0 |
| 12,001–14,000 | 15 |
| 14,001–30,000 | 30 |
| >30,000 | 40 |

For example, if the user enters 18000, the tax due is tax: = (14000−12000)*0.15 + (18000−14000)*0.3.

```
```c
#include <stdio.h>
int main(void)
{
    float income, tax;

    printf("Enter income: ");
    scanf("%f", &income);

    if(income <= 12000)
        tax = 0;
    else if(income <= 14000)
        tax = (income - 12000)*0.15;
    else if(income <= 30000)
        tax = (2000*0.15) + (income - 14000)*0.3; /* 2000 is the
        difference of 14000−12000. */
    else
        tax = (2000*0.15) + (16000*0.3) + (income - 30000)*0.4; /*
        16000 is the difference of 30000−14000. */
    printf("Tax = %.2f\n", tax);
    return 0;
}
```
```

**C.5.11** Write a program that reads the grades of three students and displays them in ascending order.

```
```c
#include <stdio.h>
int main(void)
{
    float i, j, k;

    printf("Enter grades: ");
    scanf("%f%f%f", &i, &j, &k);

    if(i <= j && i <= k)
    {
        printf("%f ", i);
        if(j < k)
            printf("%f %f\n", j, k);
        else
            printf("%f %f\n", k, j);
    }
}
```
```