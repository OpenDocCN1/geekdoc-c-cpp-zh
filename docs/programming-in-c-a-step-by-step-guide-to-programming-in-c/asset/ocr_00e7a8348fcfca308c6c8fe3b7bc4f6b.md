false, the loop will be terminated and the control goes to the statement that appears immediately after the while statement.

On using the do loop, the body of the loop is always executed at least once irrespective of the expression.

# Program 4.7: A program to print the multiplication table from 1 x 1 to 10 x 10 as shown below using do-while loop.

1 2 3 4 ........................ 10
2 4 6 8 ........................ 20
3 6 9 12 ........................ 30
4 ........................ 40
..
..
..
10 100

```
// Program to print multiplication table
main()
{
int rowmax=10,colmax=10,row,col,x;
printf(" Multiplication table\n");
printf("................................\n");
row=1;
do
{
col=1;
```