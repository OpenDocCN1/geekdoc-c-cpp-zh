can return a null pointer when it is unable to perform its task.

3.In general, C does not initialize pointers to null for you, and it never tests pointers to see if they are null before using them. (True/False)

# 9.3 Pointers as Function Arguments

Earlier, we learned that functions in C receive copies of their arguments. (This means that C uses *call by value*; it means that a function can modify its arguments without modifying the value in the caller.)

Consider the following function to swap two integers

```
void swap(int x, int y)
{
int temp;
temp=x;
x=y;
y=temp;
return;
}
```

The problem with this function is that since C uses *call by value* technique of parameter passing, the caller can not get the changes done in the function. This can be achieved using pointers as illustrated in the following program.

# Program 9.2: Program to swap two integers using pointers

```
#include<stdio.h>
main()
{
```