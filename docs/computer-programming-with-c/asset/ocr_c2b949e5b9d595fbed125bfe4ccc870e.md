Given that we need r rows in the output, it means that the process of printing stars and spaces must be executed for each row i, such that the range of i is from 0 to r−1. (Setting the range of i from 0 to r−1 will result in r distinct iterations, thereby printing r rows at the output.)

The following for loop gives different values to variable i starting from 0 to r−1 (from row number 0 to row number 3 when r=4). Note that the presence of printf("\n");, which will move the cursor on the new line after all the stars in the current row are printed and before the row number i is changed to the next value.

```
for (i=0; i<=r-1; i++)
{

```

+   1. Print r-i stars.
+   2. Print 2*i spaces
+   3. Print r-i stars.

```
printf("\n");
}
```

Figure 5.20 gives the full execution plan for the program.
The following is the full source code to print the required pattern.

```
#include<stdio.h>
void main()
{
int i,j,r;
printf("Enter the number of rows\n");
scanf("%d",&r);
    for(i=0; i<=r-1; i++)
    {
        for(j=1;j<=r-i; j++)
        {
        /*printing left star*/
        printf("*");
        }
        for(j=1;j<=2*i; j++)
        {
        /*printing space*/
        printf(" ");
        }
        for(j=1;j<=r-i; j++)
        {
        /*printing right star*/
        printf("*");
        }
```