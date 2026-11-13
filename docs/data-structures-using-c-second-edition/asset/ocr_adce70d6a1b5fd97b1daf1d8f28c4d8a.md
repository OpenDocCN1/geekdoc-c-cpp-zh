+   • Pointers are used for the dynamic memory allocation of a variable (refer Appendix A on memory allocation in C programs).

# 1.11.1 Declaring Pointer Variables

The general syntax of declaring pointer variables can be given as below.

```
data_type *ptr_name;
```

Here, data_type is the data type of the value that the pointer will point to. For example,

```
int *pnum;
char *pch;
float *pfnum;
```

In each of the above statements, a pointer variable is declared to point to a variable of the specified data type. Although all these pointers (pnum, pch, and pfnum) point to different data types, they will occupy the same amount of space in the memory. But how much space they will occupy will depend on the platform where the code is going to run. Now let us declare an integer pointer variable and start using it in our program code.

```
int x = 10;
int *ptr;
ptr = &x;
```

In the above statement, ptr is the name of the pointer variable. The * informs the compiler that ptr is a pointer variable and the int specifies that it will store the address of an integer variable. An integer pointer variable, therefore, “points to” an integer variable. In the last statement, ptr is assigned the address of x. The & operator retrieves the lvalue (address) of x, and copies that to the contents of the pointer ptr. Consider the memory cells given in Fig. 1.11.

![](bbox=[0.258, 0.514, 0.811, 0.558])

Figure 1.11 Memory representation

Now, since x is an integer variable, it will be allocated 2 bytes. Assuming that the compiler assigns it memory locations 1003 and 1004, the address of x (written as &x) is equal to 1003, that is the starting address of x in the memory. When we write, ptr = &x, then ptr = 1003.

We can ‘dereference’ a pointer, i.e., we can refer to the value of the variable to which it points by using the unary * operator as in *ptr. That is, *ptr = 10, since 10 is the value of x. Look at the following code which shows the use of a pointer variable:

```
#include <stdio.h>
int main()
{
    int num, *pnum;
    pnum = &num;
    printf("\n Enter the number : ");
    scanf("%d", &num);
    printf("\n The number that was entered is : %d", *pnum);
    return 0;
}
```

# Output

Enter the number : 10
The number that was entered is : 10

What will be the value of *(&num)? It is equivalent to simply writing num.