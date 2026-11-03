This program takes an integral input from user using scanf function. If the user enters 0,

then the logical operation in if statement holds true and therefore the body of if

statement is executed. If any other number is entered, the body of if statement is not

executed.

Let us now see another example which involves if else statement:

```
```c
void main(void)
{
printf("Program starts\n");
int x=0;
printf("Enter a number and press enter: ");
scanf("%d", &x);
if(x==0)
{
printf("If executes\n");
}
else
{
printf("Else executes\n");
}
```
```