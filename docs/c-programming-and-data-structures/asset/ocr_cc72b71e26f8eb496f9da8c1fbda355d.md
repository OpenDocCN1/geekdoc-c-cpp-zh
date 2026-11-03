![](bbox=[0.12, 0.12, 0.9, 0.26])

Fig. 4.25 Program to print binomial coefficient table

# 2. Histogram

Problem: In an organization, the employees are grouped according to their basic pay for the purpose of certain perks. The pay-range and the number of employees in each group are as follows:

| Group | Pay-Range | Number of Employees |
|---|---|---|
| 1 | 750 – 1500 | 12 |
| 2 | 1501 – 3000 | 23 |
| 3 | 3001 – 4500 | 35 |
| 4 | 4501 – 6000 | 20 |
| 5 | above 6000 | 11 |

Draw a histogram to highlight the group sizes.

Problem Analysis: Given the size of groups, it is required to draw bars representing the sizes of various groups. For each bar, its group number and size are to be written.

Program in Fig. 4.26 reads the number of employees belonging to each group and draws a histogram. The program uses four for loops and two if....else statements.

```
Program
#define N 5
main()
{
    int value[N];
    int i, j, n, x;
    for (n=0; n < N; ++n)
    {
        printf("Enter employees in Group - %d :",n+1);
        scanf("%d",&x);
        value[n] = x;
        printf("%3d\n", value[n]);
    }
    printf("\n");
    printf("\n");
    for (n = 0 ; n < N ; ++n)
    {
        for (i = 1 ; i <= 3 ; i++)
        {
            if ( i == 2 )
                printf("Group-id [%d",n+1);
            else
                printf("*");
            for (j = 1 ; j <= value[n] ; ++j)
                printf("**");
```