```
    for(i = 0; i < 100; i++)
    {
        printf("Enter grade: ");
        scanf("%f", &grd);

        if(grd == -1)
            break;
        if(grd > 10 || grd < 0)
        {
            printf("Wrong grade, try again ...\n");
            i--; /* If the input grade is out of [0, 10], the
            grade is ignored and i is decremented to repeat the insertion. */
            continue;
        }
        if(grd >= 5)
        {
            suc++;
            sum_suc += grd;
        }
        else
        {
            fail++;
            sum_fail += grd;
        }
    }
    if(i != 0)
    {
        if(suc)
            printf("Avg(+) = %.2f\n", sum_suc/suc);
        else
            printf("Everybody failed\n");

        if(fail)
            printf("Avg(-) = %.2f\n", sum_fail/fail);
        else
            printf("None failed\n");
    }
    return 0;
}
```

C.6.15 Write a program that reads 8 bits (each bit is 0 or 1) and displays the corresponding unsigned integer, assuming that the bits are entered from left to right. For example, if the user enters 10000000 the program should display 128.

```
    #include <stdio.h>
    int main(void)
    {
        int i, num, dig;

        num = 0;
        for(i = 7; i >= 0; i--)
        {
            printf("Enter digit_%d (0 or 1): ", i+1);
            scanf("%d", &dig);
```