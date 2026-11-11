```
```c
for (i=0; i<=r-1; i++){
printf("\n");
}
```
```

> > Print r-i stars in  
> > each row number i.

The following is the full source code to print the required pattern.

```
```c
#include<stdio.h>
void main()
{
int i,j,r;
/*Take number of rows as input*/
printf("Enter the number of rows:");
scanf("%d",&r);
/*Range row numbers from 0 to r-1*/
    for(i=0; i<=r-1; i++)
    {
/*For each row number i, print r-i stars*/
        for(j=1;j<=r-i; j++)
        {
            printf("*");
        }
/*Transfer the cursor on new line after current row is printed*/
        printf("\n");
    }
}
```
```

```
```text
Output
Enter the number of rows: 4
****
***
**
*
```
```

# 5.3.5  Printing a symmetric pattern: An example

We will now write a program to take number of rows as input and print the following pattern:

```
```text
*   *   *   *   *   *   *   *
*   *   *           *   *   *
*   *               *   *
*                       *
```
```