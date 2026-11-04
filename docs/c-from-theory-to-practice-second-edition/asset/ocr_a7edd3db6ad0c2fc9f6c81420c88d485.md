The same happens with all numbers up to 10. When i becomes 10, printf() outputs 10 and then i becomes 11. Now, since two characters are displayed, printf() returns 2, which makes the condition false (2 < 2) and the loop terminates. Therefore, the program outputs:

012345678910
End = 11

# C.6.18 Write a program that reads the number of students in a class and their grades on a test. The program should display the average test grade of the class, the minimum and maximum test grade, and how many students got the same maximum grade. Assume that the grades are integers within [0, 10].

```
```c
#include <stdio.h>
int main(void)
{
    int i, grd, studs_num, times, min_grd, max_grd, sum_grd;

    printf("Enter number of students: ");
    scanf("%d", &studs_num);

    if(studs_num <= 0)
    {
        printf("Wrong number of students\n");
        return 0; /* Program termination. */
    }
    min_grd = 11;
    max_grd = -1;
    sum_grd = 0;
    for(i = 0; i < studs_num; i++)
    {
        printf("Enter grade [0-10]: ");
        scanf("%d", &grd);

        if(grd < min_grd)
            min_grd = grd;
        if(grd > max_grd)
        {
            max_grd = grd;
            times = 1; /* First appearance of the new maximum grade. */
        }
        else if(max_grd == grd)
            times++;

        sum_grd += grd;
    }
    printf("Min:%d, Max:%d (appeared %d times) Avg:%.2f\n", min_grd, max_grd, times, (float)sum_grd/studs_num);
    return 0;
}
```
```