![](bbox=[0.121, 0.109, 0.813, 0.356])

**Figure 4.19:** Execution of the code to print the ‘day of the week’

```
#include<stdio.h>
void main()
{
    int day;
    printf("Enter the day number\n");
    scanf("%d",&day);
    /*switch over the value of variable "day"*/
        switch(day)
        {
        case 1: printf("Sunday\n");
            break;
        case 2: printf("Monday\n");
            break;
        case 3: printf("Tuesday\n");
            break;
        case 4: printf("Wednesday\n");
            break;
        case 5: printf("Thursday\n");
            break;
        case 6: printf("Friday\n");
            break;
        case 7: printf("Saturday\n");
            break;
        default: printf("Invalid Day Number\n");
        }
}
```