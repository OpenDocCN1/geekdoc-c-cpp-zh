In other words, since we can access the value of i_num using ptr, we can say that ptr points to i_num. It is possible to assign a NULL value to a pointer variable. The statement int *ptr = NULL; defines a pointer with an initial value NULL. Program 1 illustrates the use of pointers in a C program.

# ▶ Program 1

```
```c
/*Program to illustrate pointer variables*/
#include<stdio.h>
/*Beginning of function main */
main()
{
  /* Declare variables */
  int i_num;
  float f_num;
  int *i_ptr1,*i_ptr2;
  float *f_ptr;
  /* Assign values to variables*/
  i_num=10;
  f_num=40.54;
  /* Assign address of variables to pointer variables */
  i_ptr1=&i_num;
  i_ptr2=&i_num;
  f_ptr=&f_num;
  /* Print details of variables */
  printf("\n\nThe value of i_num is %d", i_num);
  printf("\n\n i_num identifies %u location in memory", &i_num);
  printf("\n\n Pointer variable i_ptr1 contains %u ", i_ptr1);
  printf("\n\n Pointer variable i_ptr2 contains %u ",i_ptr2);
  printf("\n\nthe value of *i_ptr1 is %d", *i_ptr1);
  printf("\n\nthe value of *i_ptr2 is %d", *i_ptr2);
  printf("\n\nthe value of f_num is %f", f_num);
  printf("\n\n f_num identifies %u location in memory", &f_num);
  printf("\n\nPointer variable f_ptr contains %u",f_ptr);
  printf("\n\nthe value of *f_ptr is %f\n", *f_ptr);
  return;
}
/* End of function main */
```
```

Output:

The value of i_num is 10
i_num identifies 65524 location in memory
Pointer variable i_ptr1 contains 65524
Pointer variable i_ptr2 contains 65524
The value of *i_ptr1 is 10