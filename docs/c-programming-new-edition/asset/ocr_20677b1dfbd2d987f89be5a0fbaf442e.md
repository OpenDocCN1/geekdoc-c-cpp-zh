```
main()
{
int a,b,ans;
printf("Enter a");
scanf("%d",&a);
printf("enter b");
scanf("%d",&b);
ans=add(a,b);
printf("the addition of two numbers is %d",ans);
}
add(x,y)
int x,y;
{
int z;
z=x+y;
return(z);
}
```

The above program, is similar to the earlier one barring that in this program the result after being computed is returned back to the caller function and it is printed from there.

# 5.7. A SIMPLE PROGRAM USING FUNCTIONS

After acknowledging the different aspects of functions in C namely knowing how to declare a function and pass arguments into the function and also being aware of the process of calling a function it seems fair enough to start writing your first program in functions which will be using all the aspects that have been encompassed in the earlier units of this session.

Below is a program which computes the factorial of any given number.

```
/*program to compute the factorial of a given number*/
2.#include<stdio.h>
main()
{
```