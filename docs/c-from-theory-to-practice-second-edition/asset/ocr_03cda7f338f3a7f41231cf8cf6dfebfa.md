```
```c
while(1)
{
    printf("\nEnter number: ");
    scanf("%d", &num);
    if(num < 0 || num > 255)
        break;
    for(i = 7; i >= 0; i--) /* Check each bit. */
    {
        if((num >> i) & 1)
            printf("1");
        else
            printf("0");
    }
}
return 0;
```
```

C.6.33 Write a program that reads a positive integer and displays the largest positive integer n for which the sum 1² + 2² + 3² +...+ n² is less than the given number.

```
```c
#include <stdio.h>
int main(void)
{
    int i, num, sum;
    printf("Enter number: ");
    scanf("%d", &num);
    if(num <= 0)
    {
        printf("Error: The number should be positive\n");
        return 0;
    }
    sum = 0;
    i = 1;
    while(1)
    {
        sum += i*i;
        if(sum >= num)
            break;
        i++;
    }
    printf("The last number is = %d\n", i-1); /* The number i-1 is the last number where the value of sum is still less than the given number. */
    return 0;
}
```
```

C.6.34 The final grade in a course is calculated as 30% of the lab grade and as 70% of the exam's grade, only if both grades are greater than or equal to 5; otherwise, the final grade will be the lesser. Write a program that reads continuously pairs of grades (lab and exam grades) and displays the final grade for each student, until the user enters a pair of grades containing the value -1. The program should display the average grade of all students in the course, before it ends. The program should force the user to enter grades within [0, 10].