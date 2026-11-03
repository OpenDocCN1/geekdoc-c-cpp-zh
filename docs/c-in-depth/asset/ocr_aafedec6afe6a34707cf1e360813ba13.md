# Output

Number = 1
Number = 2
I understand the use of continue
Number = 4
Number = 5
Out of for loop

```
/*P5.29 Program to find the sum and average of 10 positive integers*/
#include<stdio.h>
main()
{
    int i=1,n,sum=0;
    float avg;
    printf("Enter 10 positive numbers : \n");
    while(i<=10)
    {
        printf("Enter number %d : ",i);
        scanf("%d", &n);
        if(n<0)
        {
            printf("Enter only positive numbers\n");
            continue;
        }
        sum+=n;
        i++;
    }
    avg=sum/10.0;
    printf("Sum = %d Avg = %f\n",sum,avg);
}
```

In this program if any negative number is entered then a message is displayed and the control is transferred to the beginning of loop.

# 5.6 goto

This is an unconditional control statement that transfers the flow of control to another part of the program.

The goto statement can be used as-
goto label;
------
------
label:
statement;
------
------
Here label is any valid C identifier and it is followed by a colon.
Whenever the statement goto label; is encountered, the control is transferred to the statement that i