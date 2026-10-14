more work to do." As long as the expression is true, the body of the loop is executed; presumably, it makes at least some progress at its task. When the expression becomes false, the task is done, and the rest of the program (beyond the loop) can proceed. When we think about a loop in this way, we can see an additional important property: if the expression evaluates to “false" before the very first trip through the loop, we make zero trips through the loop. In other words, if the task is already done (if there's no work to do) the body of the loop is not executed at all. (It's always a good idea to think about the “boundary conditions" in a piece of code, and to make sure that the code will work correctly when there is no work to do, or when there is a trivial task to do, such as sorting an array of one number. Experience has shown that bugs at boundary conditions are quite common.)

# Program 4.5: Program to find largest of n numbers

```
main()
{
int num, large, n, i;

clrscr();
printf("enter number of numbers \n");
scanf("%d",&n);
large=0;
i=0;
while(i<n)
{
printf("\n enter number "); scanf("%d", &num);
if(large<num)
large=num;
i++;

```