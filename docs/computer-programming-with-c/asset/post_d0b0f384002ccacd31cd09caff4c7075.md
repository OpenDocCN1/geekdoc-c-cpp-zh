
Note that parentheses have a very important role in the expression, and they are used to increase the priority of address calculation. The parentheses are needed because we want the address calculation to happen before an indirection is applied. The result of the expression `*(p+1)` will not be the same as `*p+1` because the latter does not have parentheses. The former is used to read the contents of location `1002` (which is actually the same as reading `a[1]`), whereas the latter is used to increment the value `a[0]` from 10 to 11, because the pointer `p` still points to the first element of the array. The result produced by expressions `*(p+0)` and `*(p+2)` shown in Figure 8.22 can be understood using the same theory as explained for `*(p+1)`.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_417_0.png)

**Figure 8.22:** Accessing array elements using pointer `p`

## NOTES

Figure 8.22 proves that `*(p+0)` gives the same result as `a[0]`, `*(p+1)` gives the same result as `a[1]`, and `*(p+2)` gives the same result as `a[2]`.

In general, `*(p+i)` will always give the same value as that of `a[i]`, provided the pointer `p` stores the starting address of the array. Hence, every element of the array can be accessed using a single pointer, provided that the pointer holds the base address of the array.

For example, the statement

```c
printf("%d", a[i]);
```

is equivalent to

```c
printf("%d", *(p+i));
```

Needless to say, using the expression `(p+i)` [without the indirection operator] will give you the address of `a[i]` (`&a[i]`). The address of `a[i]` is typically needed when we use the `scanf()` statement to accept the *i*th element of an array as input from the user.

For example:

```c
scanf("%d", &a[i]);
```

can be rewritten as

```c
scanf("%d", (p+i));
```

Note that the indirection operator `*` is not present with the expression `(p+i)` because a call to the `scanf()` function is always made by passing the address of the variable as an argument to it.

As pointer arithmetic already takes care of different sizes of data types while performing addition/subtraction operations with addresses, this theory of accessing elements of an array using pointers can be applied to arrays of any type, including arrays of user-defined types. Pointer arithmetic in C/C++ is designed to save programmers' efforts in worrying about the data type of the array while accessing the array elements using a single pointer.

> According to Section 8.5.4, if the name of the array is `a`, it means that `a` is actually the pointer containing the starting address of an array. Here, we have created another pointer `p` in which we are explicitly storing the starting address of an array `a`. Is there any difference between pointers `p` and `a`?
>
> Yes, there is a difference between the two pointers. Pointer `a` is a constant pointer, whereas pointer `p` is not. Pointer `p` is explicitly created by the programmer, and pointer `a` is created by the compiler when an array named `a` is created. Since pointer `p` is owned by us, we can change `p` at runtime to point to any other value or even to any other array, but you cannot change the address inside pointer `a` in any way because it is a constant pointer created by the compiler, and it will continue pointing to the same array throughout the program execution.

## 8.6.1 Program to arrange n-numbers in ascending order using pointers: An example

As we have already implemented the solution for sorting the array of integers in Chapter 6 of this textbook, we will reuse the same solution to arrange numbers in ascending order by using pointers.

> **NOTES**
>
> If the name of the array is `a`, then `&a[0]` gives the starting address of an array. We also know that `a` in itself is a pointer that contains the starting address of an array. This means that you can use `&a[0]` and `a` interchangeably in the code. For example, if `p` is another pointer that is required to hold the starting address of array `a`, you can do this using any one of the following statements:
>
> ```c
> p=a;
> ```
>
> OR
>
> ```c
> p=&a[0];
> ```

To perform sorting of elements in array `a`, the code creates an integer-type pointer `p` such that `p` holds the starting address of the array `a` using the following statements:

```c
int *p;
p=&a[0];
```

The code given below is the same as that of Chapter 6, except that every access to element `a[i]` is now done by using the expression `*(p+i)`.

Following substitutions are required to be applied to the solution discussed in Chapter 6 to solve the same program by using pointers:

- Every occurrence of `a[i]` in the code should be replaced by `*(p+i)`.
- Every occurrence of `&a[i]` in the code should be replaced by `(p+i)`.
- Every occurrence of `a[j]` in the code should be replaced by `*(p+j)`.

```c
#include<stdio.h>
void main()
{
int a[100],temp,n,i,j;
int *p;
p=&a[0];
printf("Enter length of the array:");
scanf("%d",&n);
printf("Enter array elements\n");
    for(i=0;i<=n-1;i++)
    {
    scanf("%d", (p+i) ); /*Input element number i */
    }
    for(i=0;i<=n-2;i++)
    {
    for(j=i+1;j<=n-1;j++)
        {
        if(*(p+i) > *(p+j))
            {
            temp=*(p+i);  /*store value of a[i] in variable temp*/
            *(p+i)=*(p+j);  /* store value of a[j] in a[i]*/
            *(p+j)=temp;    /*store value of temp in a[j]*/
            }
        }
    }
printf("Ascending order is as below\n");
    for(i=0;i<=n-1;i++)
    {
    printf("%d\n",*(p+i)); //print a[i] using pointer p
    }

}
```

## Output

```text
Enter Length of the array:
5
Enter Array elements
30
10
20
6
50
Ascending order is as below
6
10
20
30
50
```

## 8.6.2 Program to check if the string is palindrome or not using pointers: An example

As we have already implemented the solution to check palindromes in Chapter 6 of this textbook, we will reuse the same solution to write a code to check palindromes using pointers.

As discussed in Example 6.5.3, we create two character arrays `a` and `b` such that the array `a` contains the original string and the array `b` contains its reverse. We then need to check if the original string is the same as its reverse. Because there are two character-type arrays, we will now need two character pointers, say `p` and `q`, such that the pointer `p` points to array `a` and pointer `q` points to array `b` as shown below:

```c
/* Pointer p to point to array - a */
char *p;
p=&a[0];

/* Pointer q to point to array - b */
char *q;
q=&b[0];
```

The code given below is the same as that of Chapter 6, with the following substitutions applied to solve the same program using pointers:

- Every occurrence of `a[i]` in the code should be replaced by `*(p+i)`.
- Every occurrence of `b[i]` in the code should be replaced by `*(q+i)`.
- Every occurrence of `b[j]` in the code should be replaced by `*(q+j)`.
- Every occurrence of `b[k]` in the code should be replaced by `*(q+k)`.

```c
#include<stdio.h>
void main()
{
char a[100],b[100];
int i, len=0,last,k,flag=0;
char *p,*q;
p=&a[0];
q=&b[0];
printf("Enter a word:");
scanf("%s",a);
/*calculate the length of word in array -a*/
for(i=0;*(p+i)!='\0';i++)  /*Execute the loop till a[i] is not null*/
{
    len++;
}
/*set the position of last character in array -a*/
last=len-1;
/*copy reverse of array -a in array -b*/
k=0;
for(i=last;i>=0;i--)
{
    *(q+k)=*(p+i); /* Initialize b[k] to the value of a[i] */
    k++;
}
/* Set the end of string marker for array -b*/
*(q+k)='\0';
/*check if the array-a is same as the reverse -b and set the flag
                                  if otherwise*/
for(i=0; i<=last;i++)
{
    if(*(p+i)!=*(q+i))  /*check if a[i] is same as b[i]*/
    {
                         flag=i;
                         break;
    }
}
if(flag==0)
{
    printf("Word is a Palindrome");
}
else
{
    printf("Word is not a Palindrome");
}
}
```

## Output

```text
Enter a word: MOM
Word is a Palindrome
```

## 8.7 Initialization of an Array: Revisited

Recall from Chapter 6, Section 6.2.1, that we can directly initialize all the elements of an array at the time of creation using the following syntax:

```c
DataType arrayname={comma separated list of values};
```

An array name is actually a pointer that holds the starting address of an array. Hence, when the compiler comes across such a statement, it allocates array space of the same size as the number of elements specified in the curly brackets and stores the starting address in a constant pointer named after the “array name” provided by the programmer. For example, the statement

```c
int a[]={10,20,30,40,50};
```

will allocate array space to store 5 integer values and store the starting address of the array in a constant pointer named `a`, as shown in Figure 8.23. Specifying the size of the array in this case is optional because the right-hand side `{10,20,30,40,50}` itself instructs the compiler to create an array of size 5 to store the values specified in the curly brackets. Figure 8.23 assumes the base address of this array as 1000, which is stored inside the constant pointer `a`.

As `a` is a constant pointer, there is no way to change the address stored in `a` later in the program. This means that you will not be able to make `a` point to any other array. This also justifies why you cannot initialize an array after its creation. For example, the following statements will give an error:

```c
int a[5];
a={10,20,30,40,50}; /*ERROR: Cannot reinitialize a constant
                 pointer */
```

because `a` is created as a constant pointer pointing to an array of 5 elements due to the first statement `int a[5];`. At this stage, the array contains junk values as shown in Figure 8.24, and the constant pointer `a` holds the starting address of this array. Figure 8.24 assumes the base address of an array as 1000, which is stored inside the constant pointer `a`.

When you attempt to reinitialize an array with `{10,20,30,40,50}`, the compiler attempts to create another array with values specified in the curly brackets, obviously at some other location in memory. Remember, `{10,20,30,40,50}` instructs the compiler to
![](img/57c0d966bb33c67a5a188e6bf39e4e02_422_0.png)

![](img/57c0d966bb33c67a5a188e6bf39e4e02_422_1.png)
