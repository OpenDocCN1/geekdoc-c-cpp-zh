```
```
1 * 4 = 4
1 * 5 = 5
1 * 6 = 6
1 * 7 = 7
1 * 8 = 8
1 * 9 = 9
1 * 10 = 10
Table of 2
----------------
2 * 1 = 2
2 * 2 = 4
2 * 3 = 6
2 * 4 = 8
2 * 5 = 10
2 * 6 = 12
2 * 7 = 14
2 * 8 = 16
2 * 9 = 18
2 * 10 = 20
```
```

It can be observed from the output of Program 9 that for each occurrence of i\_octr, the inner for loop is repeated 10 times. This means that for i\_octr = 1, the inner for loop is repeated 10 times, and for i\_octr = 2 also, the inner for loop is repeated 10 times. Note that the execution of the inner for loop is always completed first, and only then, the control is transferred back to the outer for loop.

Let us take one more example to understand the concept of nested loops better. Program 10 illustrates the use of nested loops to print a pattern on the monitor:

# ▶ Program 10

```
```
/* Program to print pattern using nested loops */
# include <stdio.h>
/* Beginning of main function */
main()
{
	/* Declare variables */
int i_row, i_temp, i_octr, i_ictt;

/* Input data */
/* Beginning of do...while loop */
do
{
	printf("Enter number of rows : ");
	scanf("%d",&i_row);

	/* Validate data */
if(i_row <= 1)
printf("\nEnter positive value greater than 1\n");
}
while(i_row <= 1);
/* End of do...while loop */
i_temp = i_row;

/* Print the top pattern */
for(i_octr=1; i_octr<=i_row; i_octr++)
{
	/* Beginning of action block of outer for loop */
```
```