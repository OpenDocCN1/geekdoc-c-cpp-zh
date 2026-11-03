```
```c
{
    float mark1, mark2, percentage;
    printf("\\n Enter the marks of first subject: \\n\\t");
    scanf("%f", &mark1);
    printf("\\n Enter the marks of second subject: \\n\\t");
    scanf("%f", &mark2);
    percentage=((mark1+mark2)/200)*100;
    if(percentage>40)
        printf("\\n Passed \\n");
    else
        printf("\\n Failed \\n");
}
```
```

# Verify Output

![](bbox=[0.08, 0.373, 0.501, 0.429])

# Program 9

Write a C program for investment problem.

```
```c
#define PERIOD 3
#define PRINCIPLE 5000.00
#include<stdio.h>
void main()
{
    int year;
    float amount, value, inrate;
    amount=PRINCIPLE, inrate=0.11, year=0;
    while(year < PERIOD)
    {
        printf("%2d\\t%8.2f\\n", year, amount);
        value=amount+inrate*amount;
        year=year+1;
        amount=value;
    }
}
```
```

# Verify Output

![](bbox=[0.08, 0.884, 0.501, 0.94])