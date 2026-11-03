```
Program
/***************************************************************/
/*              PROGRAM SHOWING ONE-DIMENSIONAL ARRAY          */
/************************************************************** */
main()
{
    int i;
    float x[10], value, total;
    /* .................... READING VALUES INTO ARRAY .................... */
    printf("ENTER 10 REAL NUMBERS\n");
    for(i = 0; i < 10; i++)
    {
        scanf("%f", &value);
        x[i] = value;
    }
    /* .................... COMPUTATION OF TOTAL .................... */
    total = 0.0;
    for(i = 0; i < 10; i++)
        total = total + x[i] * x[i];
    /* .................... PRINTING OF x[i] VALUES AND TOTAL .......... */
    printf("\n");
    for(i = 0; i < 10; i++)
        printf("x[%2d] = %5.2f\n",i+1, x[i]);
    printf("\nTotal = %.2f\n", total);
}
Output
ENTER 10 REAL NUMBERS
1.1 2.2 3.3 4.4 5.5 6.6 7.7 8.8 9.9 10.10
x[1]  = 1.10
x[2]  = 2.20
x[3]  = 3.30
x[4]  = 4.40
x[5]  = 5.50
x[6]  = 6.60
x[7]  = 7.70
x[8]  = 8.80
x[9]  = 9.90
x[10] = 10.10
Total = 446.86
```

Fig. 8.1 Program to illustrate one-dimensional array

Consider an array of size, say 100. All the 100 elements have to be explicitly initialized. There is no way to specify a repeat count. In such situations, it would be better to use a for loop to initialize the elements. Consider the following segment of a C program:

```
for (i = 0; i < 100; i = i+1)
{
if (i < 50)
    sum[i] = 0.0;
else
```