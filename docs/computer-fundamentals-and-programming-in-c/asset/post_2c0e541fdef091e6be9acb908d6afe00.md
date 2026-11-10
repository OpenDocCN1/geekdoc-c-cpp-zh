
```c
{
    int i;
    float *ptr, a[5];
    ptr = a;
    for(i = 0; i < 5; i++)
    {
        *ptr = 0.0; /* *ptr accesses a[i] */
        ptr++;
    }
    return 0;
}
```

Observe that the pointer variable, ptr, is type float *, because the array is of type float. It is initialized to the value of the fixed pointer, a (i.e., the initial value of ptr is set to the same as that of a, namely &a[0]), and may subsequently be modified in the loop to traverse the array. The first time through the loop, *ptr which points to (a[0]) is set to zero and ptr is incremented by one so that it points to the next element in the array. The process repeats and each element of the array is set to 0.0.

Following the same concept, an array cannot be assigned to another. The following code

```c
int a[5]={1,2,3,4,5};
int b[5];
b = a;      /* WRONG */
```

is incorrect. To copy a into b, something like the following has to be entered.

```c
for(i=0; i<5; i++)
    b[i]=a[i];
```

Or, to put it more succinctly,

```c
for(i=0; i<5; i++) b[i]=a[i];
```

But two pointer variables can be assigned.

```c
int *p1, *p2;
int a[5]={1,2,3,4,5};
p1 = &a[0];
p2 = p1;
```

Pointer assignment is straightforward; the pointer on the left is simply made to point wherever the pointer on the right does. The statement p1=p2 does not copy the data pointed to (there is still just one copy in the same place); it just makes two pointers point to the same location.

- The & (address of) operator normally returns the address of the operand. However, arrays are an exception. When applied to an array (which is an address), it has the same value as the array reference without the operator. This is not true of the equivalent pointers, which have an independent address. The following example shows this.

### EXAMPLE

5. (a)

```c
#include <stdio.h>
int main()
{
    int a[]={10, 20, 30, 40, 50};
    printf("%u %u %u", a, &a[0], &a);
    return 0;
}
```

Output

```
65506 65506 65506
```

(b)

```c
#include <stdio.h>
int main()
{
    int a[]={10, 20, 30, 40, 50};
    int *ptr;
    ptr=a;
    printf("%u %u %u", &a[0],ptr,&ptr);
    return 0;
}
```

Output

```
65506 65506 65526
```

- The sizeof operator returns the size of the allocated space for arrays. In case of a pointer, the sizeof operator returns two or four or more bytes of storage (machine dependent).

### EXAMPLE

6. (a)

```c
#include <stdio.h>
int main()
{
    int a[]={10, 20, 30, 40, 50};
    printf("%d", sizeof (a));
    return 0;
}
```

Output

```
In Turbo C
    10

In GCC
    20
```

(b)

```c
#include <stdio.h>
int main()
{
    int a[]={10, 20, 30, 40, 50};
    int *ptr;
    ptr=a;
    printf("%d", sizeof (ptr));
    return 0;
}
```

Output

```
In Turbo C
```

Table 13.3 lists the differences between pointers and arrays.

**Table 13.3** Differences between pointers and arrays

| Arrays | Pointers |
|---|---|
| It is a variable that can hold a set of homogeneous values. | It is a variable which holds an address of another variable. |
| It cannot be resized. | It can be resized using `realloc()`. |
| It cannot be reassigned. | It can be reassigned. |
| `sizeof(arrayname)` gives the number of bytes occupied by the array. | `sizeof(p)` returns the number of bytes used to store the pointer variable p. |

## 13.9 POINTERS AND STRINGS

Strings are one-dimensional arrays of type char. By convention, a string in C is terminated by the end-of-string sentinel `\0`, or null character. The null character is a byte with all bits off; hence, its decimal value is zero. It is useful to think of strings as having a variable length, delimited by `\0`, but with the maximum length determined by the size of the string. The size of a string must include the storage needed for the end-of-string sentinel. As with all arrays, it is the job of the programmer to make sure that string bounds are not overrun.

String constants are written between double quotes. For example, “abc” is a character array of size 4, with the last element being the null character `\0`. Note that string constants are different from character constants. For example, “a” and ‘a’ are not the same. The array “a” has two elements, the first with value ‘a’ and the second with value `\0`.

A string constant, like an array name by itself, is treated by the compiler as a pointer. Its value is the base address of the string. Like the numeric array, individual characters contained in a string can be printed.

```c
#include <stdio.h>
int main()
{
    char s[]="Oxford";
    for(i=0;s[i]!='\0';++i)
        putchar(s[i]);
    return 0;
}
```

A string in C is a pointer itself. The following program proves the fact.

```c
#include <stdio.h>
int main()
{
    for(i=0; *("I am a pointer" + i)!='\0';++i)
        printf("%c", *("I am a pointer" + i));
    return 0;
}
```

Output

I am a pointer

But this is not true for a numeric array. The following program gives an error.

```c
#include <stdio.h>
int main()
{
    for(i=0; *(({1,2,3,4,5} + i))!='\0';++i)
        putchar(*(({1,2,3,4,5} + i)));
    return 0;
}
```

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_359_0.png)

Consider the following code.

```c
char *p = "abc";
printf("%s %s\n", p, p + 1);  /* abc bc is printed */
```

The variable p is assigned the base address of the character array “abc”. When a pointer to char is printed in the format of a string, the pointed-at character and successive characters are printed until the end-of-string sentinel (that is, `\0`) is reached. Thus, in the `printf()` statement, the expression p causes abc to be printed, and the expression p + 1, which points to the letter b in the string “abc”, causes bc to be printed. Because a string constant such as “abc” is treated as a pointer, expressions such as

```c
"abc"[1] and *("abc" + 2)
```

are possible. Such expressions are not used in serious code, but they help to emphasize that string constants are treated as pointers. It should be noted that arrays and pointers have similar uses. They also have differences. Let us consider two declarations

```c
char *p = "abcde";
char s[] = "abcde";
```

In the first declaration, the compiler allocates space in the memory for p, puts the string constant “abcde” in memory somewhere else, and initializes p with the base address of the string constant. Now think of p as pointing to the string. The second declaration is equivalent to

```c
char s[] = {'a', 'b', 'c', 'd', 'e', '\0'};
```

Because the brackets are empty, the compiler allocates six bytes of memory for the array s. The first byte is initialized with ‘a’, the second byte is initialized with ‘b’, and so on. Here is how these objects are stored in memory. (Fig. 13.9)

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_359_1.png)

A char is always stored in one byte, and on most machines a pointer is stored in a word. Thus, on the machine, p is stored in four bytes, and s is stored in six bytes of storage. For technical reasons, it is better not to print null characters. However, the printing of null strings is perfectly acceptable.

One question may arise—when an array is passed, how does the function know how many elements the array has?

For a string, the number of elements it has need not be passed because it has the terminating null character. For other types of arrays, the number of elements must be passed as well.

### Note

- A string constant is treated by the compiler as a pointer.
- For a string, the number of elements it has need not be passed to a function because it has the terminating null character.

## 13.10 POINTER ARITHMETIC

If p is declared as a pointer variable of any type and it has been initialized properly, then, just like a simple variable, any operation can be performed with *p. Because * implies value at address, working with *p means working with the variable whose address is currently held by p. Any expression, whether relational, arithmetic, or logical, can be written, which is valid for a simple value variable. But with only p, operations are restricted as in each case address arithmetic has to be performed. The only valid operations on pointers are as follows.

- Assignment of pointers to the same type of pointers: the assignment of pointers is done symbolically. Hence, no integer constant except 0 can be assigned to a pointer.
- Adding or subtracting a pointer and an integer.
- Subtracting or comparing two pointers (within array limits) that point to the elements of an array.
- Incrementing or decrementing the pointers (within array limits) that point to the elements of an array. When a pointer to an integer is incremented by one, the address is incremented by two (as two bytes are used for int). Such scaling factors necessary for the pointer arithmetic are taken care of automatically by the compiler.
- Assigning the value 0 to the pointer variable and comparing 0 with the pointer. The pointer with address 0 points to nowhere at all.

These valid address arithmetic are discussed below in detail. The following arithmetic operations on pointers are not feasible.

- Addition of two pointers
- Multiplying a pointer with a number
- Dividing a pointer with a number

### 13.10.1 Assignment

Pointers with the assignment operators can be used if the following conditions are met.

- The left-hand operand is a pointer and the right-hand operand is a null pointer constant.
- One operand is a pointer to an object of incompatible type and the other is a pointer to void.
- Both the operands are pointers to compatible types.

Some of the pointer assignment statements were discussed earlier. For the notion of incompatible types, including the use of void*, some complicated cases may be considered.

Pointers to void can be freely converted back and forth with pointers to any object or incomplete type. Converting a pointer to an object or an incomplete type to void* and then back gives a value which is equal to the original one.

### EXAMPLE

7.

```c
#include <stdio.h>
int main()
{
    int i;
    int *ip;
    void *vp;
    ip = &i;
    vp = ip;
    ip = vp;
    if(ip != &i)
        printf("\n Compiler error\n");
    else
        printf("\n No Compiler error\n");
    return 0;
}
```

Output

No Compiler error

Now, consider the revised version of the program in Example 7.

```c
#include <stdio.h>
int main()
{
    int i=5;
    int *ip;
    void *vp;
    ip = &i;
    vp = ip;
    //printf("\n *vp=%d",*vp);
    ip = vp;
    printf("\n *ip=%d",*ip);
    return 0;
}
```
