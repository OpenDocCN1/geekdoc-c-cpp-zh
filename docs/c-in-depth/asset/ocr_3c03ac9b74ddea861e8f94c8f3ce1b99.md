to it. If we use return statement then we will have to make three different functions with one return statement in each. The following program shows how we can return all these values from a single function.

```
/*P8.18 Program to show how to return more than one value from a function using call by reference*/
#include<stdio.h>
main()
{
int a,b,sum,diff,prod;
a=6;
b=4;
func(a,b,&sum,&diff,&prod);
printf("Sum = %d, Difference = %d, Product = %d\n",sum,diff,prod);
}
func(int x,int y,int *ps,int *pd,int *pp)
{
*ps=x+y;
*pd=x-y;
*pp=x*y;
}
```

Sum = 10, Difference = 2 , Product = 24

In func() variables a and b are passed by value while variables sum, diff, prod are passed by reference. The function func() knows the addresses of variables sum, diff and prod, so it accesses these variables indirectly using pointers and changes their values.

# 8.16 Function Returning Pointer

We can have a function that returns a pointer. The syntax of declaration of such type of function is - type *func(type1, type 2, ...);

```
float *fun(int , char); /* This function returns a pointer to float. */
int *func(int , int ); /* This function returns a pointer to int. */
```

While returning a pointer, make sure that the memory address returned by the pointer will exist even after the termination of function. For example a function of this form is invalid-

```
main()
{
int *ptr;
ptr=func();
........
}
```

```
int *func()
{
int x=5;
int *p=&x;
........
}
```