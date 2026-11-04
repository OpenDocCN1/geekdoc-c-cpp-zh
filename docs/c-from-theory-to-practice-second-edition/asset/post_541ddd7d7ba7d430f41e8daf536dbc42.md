
## Pointer Arithmetic

Pointer arithmetic refers to the application of some arithmetic operations on pointers. The standard says that pointer arithmetic is guaranteed to produce reliable results when applied to elements of the same array; otherwise, the behavior is undefined. An exception to that rule is the address of the first element past the end of the array; the standard guarantees that it is valid to use that place in pointer arithmetic. The allowed operations are adding or subtracting a pointer and an integer and subtracting and comparing pointers provided that they point to the same array. As discussed, assignment or comparison with 0 is also allowed.

## Pointers and Integers

Suppose that a pointer variable ptr points to an element of an array. The addition of a positive integer n in an assignment such as:

```
ptr = ptr + n;
```

increases the pointer's value by n * size of the pointer's data type and makes the pointer point to the address of the nth element after the one it points to. For example, if ptr points to the array element arr[i] and n is 3, ptr will point to arr[i+3]. If the resulting element is out of the array, with the exception of the first element past the end, the result is undefined. For example, given the assumptions we've made for the data types in Chapter 2, if ptr is declared as a pointer to an array of:

- **char**, its value is increased by n*1=n, because the size of the `char` type is one byte.
- **int or float**, its value is increased by n*4, because the size of both types is four bytes.
- **double**, its value is increased by n*8, because the size of `double` is eight bytes.

Consider the following program:

```c
#include <stdio.h>
int main(void)
{
    int *ptr, arr[] = {10, 20, 30};

    ptr = &arr[0];
    printf("Addr:%d\n", ptr);
    ptr = ptr+2;
    printf("Addr:%d Val:%d\n", ptr, *ptr);
    return 0;
}
```

ptr is increased by 8, not by 2, because ptr is declared as a pointer to int. The program displays two addresses and the second one is 8 places higher than the first one. Since ptr points to arr[2], the program outputs 30, as well.

```c
scanf("%f%f%f", ptr1, ptr2, ptr3);
if((*ptr1 >= 5) && (*ptr2 >= 5) && (*ptr3 >= 5))
{
    if(*ptr1 <= *ptr2 && *ptr1 <= *ptr3)
    {
        printf("%f ", *ptr1);
        if(*ptr2 < *ptr3)
            printf("%f %f\n", *ptr2, *ptr3);
        else
            printf("%f %f\n", *ptr3, *ptr2);
    }
    else if(*ptr2 <= *ptr1 && *ptr2 <= *ptr3)
    {
        printf("%f ", *ptr2);
        if(*ptr1 < *ptr3)
            printf("%f %f\n", *ptr1, *ptr3);
        else
            printf("%f %f\n", *ptr3, *ptr1);
    }
    else
    {
        printf("%f ", *ptr3);
        if(*ptr2 < *ptr1)
            printf("%f %f\n", *ptr2, *ptr1);
        else
            printf("%f %f\n", *ptr1, *ptr2);
    }
}
else
    printf("Avg = %.2f\n", (*ptr1 + *ptr2 + *ptr3)/3);
return 0;
```

## C.8.14 Use the p1 and p2 pointers and complete the following program to display the product of even numbers from 10 up to 20.

```c
#include <stdio.h>
int main(void)
{
    int *p1, *p2, i, mul;
    ...
}
```

Answer:

```c
#include <stdio.h>
int main(void)
{
    int *p1, *p2, i, mul;
    p1 = &i;
    p2 = &mul;
    for(*p1=10, *p2=1; *p1 <= 20; (*p1)+=2)
        *p2 = *p2 * *p1;
}
```

elements in memory. For example, in a char array, the distance is one byte, while in an int array, it is four bytes.

> Tip
> The close relationship between pointers and arrays is based on the fact that the name of an array can be used as a pointer to its first element.

In a similar way, arr+1 can be used as a pointer to the second element, arr+2 as a pointer to the third one, and so on. In general, the following expressions are equivalent:

- arr == &arr[0]
- arr + 1 == &arr[1]
- arr + 2 == &arr[2]
- ...
- arr + n == &arr[n]

As a result, the following program outputs four times the same value:

```c
#include <stdio.h>
int main(void)
{
    int *ptr, arr[5];
    ptr = arr;
    printf("%p %p %p %p\n", ptr, &arr[0], arr, &arr);
    return 0;
}
```

Notice that although the expression &arr outputs the same value, it is different from the others. This expression evaluates to a pointer to the whole array, whereas the others evaluate to a pointer to its first element. In particular, the type of &arr is "pointer to an array of five integers," while the type of the others is "pointer to integer." Tough!

And to make it even harder, if we write arr+1 instead of &arr, what would be the difference with the other values (would be one, four, or something else, ...)? To answer it, use the type of the expression and pointer arithmetic. We won’t tell you the answer; give it some thought, run the program, check the output, and try to figure out why is that. If you need an explanation, don’t get in contact with us, we are out ...

Since the name of an array can be used as a pointer to its first element, its content is equal to the value of its first element. Therefore, *arr is equal to arr[0]. In a similar way, since arr+1 is a pointer to the second element, *(arr+1) is equal to arr[1], and so on. In general, the following expressions are equivalent:

- *arr == arr[0]
- *(arr+1) == arr[1]
- *(arr+2) == arr[2]
- ...
- *(arr+n) == arr[n]

The parentheses are necessary because the * operator has higher precedence than the + operator. Therefore, the expressions *(arr+n) and *arr + n are evaluated in a different way. For example, consider the following program:

```c
#include <stdio.h>
int main(void)
{
    int *ptr, arr[] = {10, 20, 30, 40, 50};

    ptr = arr;
    printf("Val1 = %d Val2 = %d\n", *ptr+2, *(ptr+2));
    return 0;
}
```

With the statement ptr = arr; ptr becomes equal to the address of arr[0], so *ptr is equal to arr[0], that is, 10. Since the * operator has higher precedence than +, *ptr+2 is equal to 10+2 = 12.

The expression *(ptr+2) evaluates to the content of the address that ptr points to, incremented by two integers' positions. Therefore, *(ptr+2) is equal to arr[2]. As a result, the program displays: Val1 = 12 Val2 = 30

Notice that we don't write ptr = &arr; because &arr corresponds to a pointer to an array, while ptr is a pointer to an integer.

The following program uses array subscripting and pointer arithmetic to display the addresses and the values of arr elements.

```c
#include <stdio.h>
int main(void)
{
    int i, arr[5] = {10, 20, 30, 40, 50};

    printf("\n***** Using array notation *****\n");
    for(i = 0; i < 5; i++)
        printf("Addr = %p    Val = %d\n", &arr[i], arr[i]);

    printf("\n***** Using pointer notation *****\n");
    for(i = 0; i < 5; i++)
        printf("Addr = %p    Val = %d\n", arr+i, *(arr+i));
    return 0;
}
```

To process an array, our preference is to use array subscripting rather than pointer arithmetic. The reason is to get a clearer and less error-prone code. In other words, we consider that arr[i] is easier to read and safer than *(arr+i). For example, the lack of parentheses introduces a bug, which is not so easy to trace. As far as performance is concerned, the code transformations that to date optimizing compilers make will most probably produce the same efficient code. However, because both ways are quite popular, you must learn and use both of them.

What really matters is to remember that the compiler converts arr[i] to *(arr+i). We could say that arr[i] is an elegant shortcut for *(arr+i). You'll encounter a really weird application of that rule in an exercise later on. Look forward for your answer; the trap is set.

The following program uses another pointer variable to display the values and the addresses of arr elements.

```c
#include <stdio.h>
int main(void)
{
    int *ptr, i, arr[5] = {10, 20, 30, 40, 50};
    ptr = arr;
    for(i = 0; i < 5; i++)
    {
        printf("Addr = %p  Val = %d\n", ptr, *ptr);
        ptr++; /* ptr becomes equal to the memory address of the next array element. Equivalently, we can write ptr = &arr[i]; */
    }
    return 0;
}
```

The statement ptr = arr; makes ptr point to the first element, while each execution of ptr++; makes ptr point to the next element.

When the name of an array is used as a pointer, C treats it as const pointer. Therefore, you are not allowed to change its value and make it point elsewhere. An array is not a modifiable lvalue; its value will always be equal to the memory address of its first element.

Therefore, if we write arr++; or arr = &i; in our last example, the compiler will display an error message for illegal action. Now, you can understand what you were told in Chapter 7, that it is illegal to write b = a; in order to copy the elements of the array a into b. However, you are allowed to copy its value in a pointer variable, as we did with ptr = arr; and use that pointer to access the array elements.

Although arrays and pointers are closely related, it must be clear to you that an array is not a pointer and vice versa. For example, the declarations int a[50]; and int *a; are quite different. With the first declaration, the compiler allocates memory for 50 integers. The array can be filled with different values at different times, but it always refers to the same memory address. As said, it is not possible to assign it a new value, that is, it is illegal to write a = arr. With the second declaration, the compiler allocates memory to store the value of the pointer (e.g., typically 4 bytes). In contrast to an array, you are allowed to assign a new value to a pointer and make it point somewhere else, for example, it is legal to write a = arr.

Just remember that whenever the name of an array is used in an expression, the compiler converts it to a pointer to the address of its first element. Always? Not always, there are a few exceptions:

- a. When it is the operand of the sizeof operator. sizeof calculates the size of the entire array.
- b. As discussed, when the & operator is applied to it. It is the array's address that is retrieved. When discussing complex declarations in Chapter 11, we'll see an example of how to declare and initialize a pointer of that type.
- c. When the array is a literal string initializer.

Although a pointer variable is not an array, it can be indexed like an array.

For example, the following program subscripts the pointer variable ptr as though it were an array to display the values and the addresses of arr elements.
