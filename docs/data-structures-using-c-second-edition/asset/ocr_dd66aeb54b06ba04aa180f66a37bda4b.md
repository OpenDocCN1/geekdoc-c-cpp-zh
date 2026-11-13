In C, since you cannot have a variable of type void, the void pointer will therefore not point to any data and, thus, cannot be dereferenced. You need to cast a void pointer to another kind of pointer before using it.

Generic pointers are often used when you want a pointer to point to data of different types at different times. For example, take a look at the following code.

```
#include <stdio.h>
int main()
{
    int x=10;
    char ch = 'A';
    void *gp;
    gp = &x;
    printf("\n Generic pointer points to the integer value = %d", *(int*)gp);
    gp = &ch;
    printf("\n Generic pointer now points to the character= %c", *(char*)gp);
    return 0;
}
```

# Output

Generic pointer points to the integer value = 10
Generic pointer now points to the character = A

It is always recommended to avoid using void pointers unless absolutely necessary, as they effectively allow you to avoid type checking.

# Programming Example

+   9. Write a program to add two integers using pointers and functions.

```
#include <stdio.h>
void sum (int*, int*, int*);
int main()
{
    int num1, num2, total;
    printf("\n Enter the first number : ");
    scanf("%d", &num1);
    printf("\n Enter the second number : ");
    scanf("%d", &num2);
    sum(&num1, &num2, &total);
    printf("\n Total = %d", total);
    return 0;
}
void sum (int *a, int *b, int *t)
{
    *t = *a + *b;
}
```

# Output

Enter the first number : 23
Enter the second number : 34
Total = 57

# 1.11.5 Pointer to Pointers

In C, you can also use pointers that point to pointers. The pointers in turn point to data or even to other pointers. To declare pointers to pointers, just add an asterisk * for each level of reference.