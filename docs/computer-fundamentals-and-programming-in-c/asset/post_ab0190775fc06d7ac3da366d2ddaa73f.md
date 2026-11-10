
address of the array, that is, the base address of an array is the address of the zero element of the array. The array name is referred to as an *address constant*. Mentioning the name of the array fetches its base address. Consider the following program.

### EXAMPLE

2. (a)

```c
#include <stdio.h>
int main()
{
    int array[]={10, 20, 30, 40, 50};
    printf("%u %u", array, &array[0]);
    return 0;
}
```

**Output**

2147487270 2147487270

Again, consider the following program.

(b)

```c
#include <stdio.h>
int main()
{
    int array[]={10, 20, 30, 40, 50};
    printf("%u %u", array, &array);
    return 0;
}
```

**Output**

2147487270 2147487270

Both array and &array would give the base address of the array. Though both array and &array give the same address, there is a small difference between them. Under ANSI/ISO Standard C, &array yields a pointer, of type pointer-to-array-of-T, where T is the data type to the entire array. Under pre-ANSI C, the & in &array generally elicited a warning, and was generally ignored. Under all C compilers, an unadorned reference to an array yields a pointer, of type pointer-to-T, to the array’s first element.

### Note

- Array name is a pointer constant. It cannot be used as *lvalue*, that is, array names cannot be used as variables on the left of an assignment operator.
- Both array and &array would give the base address of the array, but the only difference is under ANSI/ISO Standard C, &array yields a pointer, of type pointer-to-array-of-the data type to the entire array.

An array can be subscripted to get to individual cells of data. With the name of the array actually being a constant that represents a memory address, the name of the array can be used as a pointer and an integer value can be used to represent an offset from the base address. This alternate method can be used to get to individual cells of an array. An element of the array is addressed as a[i] and the address of the ith element of the array is given by &a[i] = a + i * size of the type pointed to by a.

The expression a + i (with integer i) means the address of the ith element beyond the one a points to. This is not measured in number of bytes, but in number of sizeof(type) bytes. This is known as *scaling*.

The compiler automatically scales a subscript to the size of the object pointed at. The compiler takes care of scaling before adding to the base address. This is the reason why pointers are always type-constrained to point to objects for only one type, so that the compiler knows how many bytes to retrieve on pointer dereference and it knows by how much to scale a subscript.

As indirection operator ‘*’ implies value at address, a[i] is equivalent to *(a+i). Consider the following two versions of the same program.

### EXAMPLE

3. (a)

```c
#include <stdio.h>
int main()
{
    int a[]={10, 20, 30, 40, 50};
    int i;
    for(i=0;i<5;++i)
        printf("\n%d", a[i]);
    return 0;
}
```

**Output**

10
20
30
40
50

(b)

```c
#include <stdio.h>
int main()
{
    int a[]={10, 20, 30, 40, 50};
    int i;
    for(i=0;i<5;++i)
        printf("\n%d", *(a+i));
    return 0;
}
```

**Output**

10
20
30
40
50

The integer identifier i is added to the base address of the array. The C compiler computes the resulting address that will be accessed by taking the value held in i multiplied by the size in bytes of the type of array a and adds the proper offset to a to give the correct memory address. Subscript notation is converted by the compiler into the pointer notation. Hence, pointer notation would work faster since conversion time can be saved by using it.

All the following four expressions are the same when their addresses are considered.

```
a[1]
*(a + 1)
*(1 + a)
1[a]
```

In the expression a[i], i must be an integer. The other may either be an array name or a pointer. For any one-dimensional array a and integer i, the following relationships are always true.

- 1. `&a[0] == a`

  The address of the first element of the array a is the value of a itself. In other words, a is a pointer; it points to the first element in the array.

- 2. `&a[i] == a + i`

  The address of the ith element of a is the value of a + i. This is one of the great truths (and a defining characteristic) of C. The first relationship is a special case of this more general relationship.

- 3. `a[i] == *(a + i)`

  This is basically the same as the previous relationship but this relationship still holds if both sides of the equality operator are dereferenced.

- 4. `(&a[i] - &a[j]) == (i - j)`

  This relationship defines the subtraction of pointers. The subtraction of two pointers of type t is the number of elements of type t that would fit between them.

A pointer variable (of the appropriate type) can also be used to initialize or point to the first element of the array. Then it can also be used as above.

```c
#include <stdio.h>
int main()
{
    int a[]={10, 20, 30, 40, 50};
    int i, *p;
    p=a; /* it can also be written as p=&a[0]; */
    for(i=0;i<5;++i)
        printf("%d\n", p[i]);

    return 0;
}
```

**Output**
10
20
30
40
50

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_355_0.png)

One can define a pointer of the same type as the elements of the array and can assign it the address of any element of the array and use it to access the array elements. In fact, one may add an integer value to it. Such a statement in the program uses the formula given earlier to do the assignment; so it also adjusts the count for the size of the element. Pointers and arrays are so closely related that their notation can be interchanged such that the following terms are identical if p contains the value of a.

```
a[1]
*(a + 1)
*(p + 1)
p[1]
```

where i=0,1,2,...(N-1). N is the size of the array.

The similarities between arrays and pointers end up being quite useful, and in fact C builds on the similarities, leading to what is called ‘the equivalence of arrays and pointers in C’. This equivalence does not mean that arrays and pointers are the same (they are, in fact, quite different) but that they can be used in related ways, and that certain operations may be used between them. These operations are as follows.

- The first such operation is that it is possible to (apparently) assign an array to a pointer.

    ```c
    int a[10];
    int *p;
    p = a;
    ```

    C defines the result of this assignment to be that p receives a pointer to the first element of a. In other words,

    `p = &a[0];`

- The second aspect of the equivalence is that the *array subscripting* notation `[i]` can be applied on pointers, too. `p[3]` can be written as `*(p + 3)`.

So, a pointer that points to an array or a part of an array can be treated ‘as if’ it was an array, using the convenient `[i]` notation. In other words, at the beginning of this discussion, the expressions `p`, `*(p+1)`, `*(p+2)`, and in general `*(p+i)`, could have been written as `p[0]`, `p[1]`, `p[2]`, and `p[i]`. This can be quite useful (or at least convenient).

The pointer to an array does not always point to the first element of the array. It can point to any element of the array. For example,

```c
int a[]={10,20,30,40,50};
int *p;
p = a + 3;
```

can also be written as follows

```c
p = &a[0] + 3;
```

which, in turn, gives the same result as

```c
p = &a[3];
```

```c
printf("\n Enter the array elements one by one\n");
while(i < n)
{
    scanf("%d", &x);
    *(a + i) = x;
    i++;
}
return i;
}
void show(int *a, int n)
{
    int i;
    for(i=0;i<n;++i)
        printf("\n %d", *(a+i));
}
```

Figure 13.8 illustrates the connection between the calling function main(), and the called functions.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_357_0.png)

When an array is passed to a function, the C language allows the programmer to refer the formal parameter as either an array or as a pointer. The compiler knows that whenever a formal parameter is declared as an array, inside the function it will in fact always be dealing with a pointer to the first element of the array of unknown size. That is why the calling function must simply pass an appropriate array pointer and maximum number of elements as arguments.

Parts of an array, called a sub-array, may also be passed to a function. A pointer to a sub-array is also an array pointer; it simply specifies the base of the sub-array. In fact, as far as C is concerned, there is no difference between an entire array and any of its sub-arrays. For example, a function call can be made to print a sub-array by specifying the starting pointer of the sub-array and its size. Suppose we need to print the sub-array starting at arr[3] containing five elements; the expression, &arr[3] is a pointer to an array starting at arr[3]. The function call is.

```c
show(&arr[3], 5);
```

Alternatively, since arr + 3 points to arr[3], the function call can be

```c
show(arr + 3, 5);
```

> **Note**
>
> - When an array is passed to a function, it degenerates to a pointer. All array names that are function parameters are always converted into pointers by the compiler. Because when passing an array to a function, the address of the zero-th element of the array is copied to the pointer variable which is the formal parameter of the function. However, arrays and pointers are processed differently by the compiler, represented differently at run time.

### 13.8.3 Differences between Array Name and Pointer

From the above discussion it seems that array name and pointer which points to the base address of the array, are equivalent. But it is not true. There are several differences between them. They are as follows.

- When memory is allocated for the array, the starting address is fixed, i.e., it cannot be changed during program execution. Therefore, array name is an address constant; the value contained in it should not be changed. To ensure that this pointer is not changed, in C, array names may not be used as variables on the left of an assignment statement, i.e., they may not be used as an lvalue. Instead, if necessary, separate pointer variables of the appropriate type may be declared and used as lvalues. Here is an example of a common error when an attempt to use an array as an lvalue is made.

```c
#include <stdio.h>
int main()
{
    int i;
    float a[5];
    for(i = 0; i < 5; i++)
    {
        *a = 0.0;
        a++; /* BUG: a = a + 1; */
    }
    return 0;
}
```

In this example, a is fixed and cannot be used as an lvalue; the compiler will generate an error stating that an lvalue is required for the ++ operator. However, a pointer variable can be declared, which can point to the same type as the type of the array, and initialize it with the base address of array. This pointer variable can be used as an lvalue and no error message will be displayed. Here is the difference.

```c
#include <stdio.h>
int main()
```
