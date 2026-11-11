```
```c
int i,j,r;
printf("Enter the number of rows\n");
scanf("%d",&r);
    for(i=0; i<=r-1; i++)
    {
        /*Loop for printing spaces */
        for(j=1;j<=r-i; j++)
        {
            printf(" ");
        }
        /*Loop for printing stars */
        for(j=1;j<=2*i+1; j++)
        {
            printf("*");
        }
        printf("\n");
    }
}
```
```

# SCRATCH PAD

In order to print the given pyramid we need to print spaces followed by a stars in each row. It is not required to print any spaces to the right of stars, this is because, the screen to the right of starts will be left blank any which ways when the control is transferred to the new line. Hence we can solve the problem, by designing two loops for each now:

+   - **Inner Loop 1:** To print spaces that appear to the left of starts in each row.
+   - **Inner Loop 2:** To print stars in each row.

The above two loops will now have an ability to print 1 full row as required on the screen. This means that, the execution of these loops must be repeated r times, if we need to print r rows at the output. Therefore, the limits of the outer most loop are from i = 0 to r − 1 as seen in the code. Note that, the outermost loop is responsible to increment row numbers hence it repeats the execution of two inner loops for each row. To understand how the limits of inner loops are decided, let us assume the value of r (no. of rows) is 4. Hence the pattern would be imagined as follows:

| space | space | space | * |   |   |   |
|---|---|---|---|---|---|---|
| space | space | * | * | * |   |   |
| space | * | * | * | * | * |   |
| * | * | * | * | * | * | * |

When the value of the outer loop variable i is 0, we are required to print the first row which has 3 spaces followed by 1 star. After which the control is transferred to new line by execution of statement printf("\n"); When outer loop increments the value of variable i to 1, we are ready to print the second row which has 2 spaces followed by 3 starts. Hence, in general, if number of rows are r, for any row number i, we require to print r-i spaces followed by 2*i+1 starts.

Hence, the first inner loop (Inner Loop 1) is responsible to print r-i spaces and the second inner loop is responsible to print 2*i+1 starts as shown below

```
for(i=0; i<=r-1; i++)
```

> This is a for loop for incrementing **row numbers**. The value of variable i represents the current row number at each iteration of the loop.