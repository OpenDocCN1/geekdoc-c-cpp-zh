Here, ptr2, stored at memory location 7645, points to memory address 7676 in which pointer ptr1 is contained. The pointer ptr1 points to the memory address 8687 in which the value of the ‘Name’ variable is stored.

Pointers to pointers are particularly useful while handling arrays or while passing address values as parameters to a function. A pointer to a pointer can be declared in the following way:

data type ** pointername

In the above declaration, data type can be any type, such as char or int and pointername can be any valid name. The ** in the above declaration indicates that the pointer with the name pointername is a pointer to a pointer, which is containing the memory address of a variable of type, data type.

In case of arrays, you can use pointer to a pointer when passing two-dimensional arrays between functions.

As an example, consider the following declarations:

```
int x;
int *ptr1;
ptr1 = &x;
int **ptr2;
ptr2 = &ptr1;
```

In the above declarations, x is an integer type variable and ptr1 is a pointer of integer type holding the address of x. **ptr2 is an integer type pointer to the pointer and contains its address.

The following code is an example of how to use a pointer to pointer in C.

```
#include <stdio.h>
#include <conio.h>

int main(void)
{
clrscr();
int num1, num2, mul, *ptr1,*ptr2,*ptr3,*ptr4;
printf("Enter the first number for multiplication:\n");
scanf("%d",&num1);
printf("Enter the second number for multiplication:\n");
scanf("%d",&num2);
ptr1 = &num1;
ptr2 = &num2;
mul = *ptr1 * *ptr2;
ptr3 = &mul;
ptr4 = &ptr3;
printf("The multiplication of %d and %d is %d", num1, num2,**ptr4);
getch();
return 0;
}
```

Fig. 11.13 C program for pointer to pointer