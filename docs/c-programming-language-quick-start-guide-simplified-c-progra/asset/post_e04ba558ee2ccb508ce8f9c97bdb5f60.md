
functions. At the same time, C gives the programmer to choose the scope of a variable by himself. If a programmer wants something to be shared by multiple functions, C provides multiple options to do so. For example, use of pointers or global variables.

The basic rule of scoping is that variables are accessible only within the block of their declaration. They are unknown outside the boundaries of that block unless specified otherwise using special techniques. This is an easy rule to be followed but programmers seem to use same identifiers in different environments. For example, see the second example in Examples section at the end of this chapter. The programmer used the identifier ‘a’ to represent multiple variables in different scope. If there were no rules for Scoping, the compiler could not have differentiated between these identifiers. Let us see another example:

```c
int globalVariable = 10;

void changeValue (int a)
{
    a = a + 10;
    printf ("Inside changeValue function: Value of localVariable = %d\n", a);
    printf ("Inside changeValue function: Value of globalVariable = %d\n", globalVariable);
}

void main(void)
{
    int localVariable=20;
    changeValue(localVariable);
    printf("Inside changeValue function: Value of localVariable = %d\n", localVariable);
    for(int x=1; x<=5; x++)
    {
        printf ("%d,", x);
    }
    printf("\n");
    printf ("%d,", x);
    system ("pause");
}
```

The above program uses four scopes. The first one is global which means it can be accessed anywhere and changes made to it in one place are visible to everyone else. All the others are local scopes which mean they are visible only to their scope. The identifiers “local Variable”, “a” and “x” are all variables defined in local scope. The first two variables follow the general rules of scope but x violates it. This program fails to compile because variable x, declared in the “for” loop is accessed outside its scope. The compiler is unable to identify x as an identifier outside for loop. To make this program work, just delete the second last statement in main program.

### 5.6 Recursion

Recursion is a technique in which a function calls itself in order to achieve a certain goal. Recursion is very important as it provides a way for more efficient and concise code for difficult program.

A function is said to be recursive if it calls itself within its body based on a decision statement usually. Here is an example for better illustration:

```c
void main(void)
{
    printf("This program is never going to end..!\n");
    main ();
    system ("pause");
}
```

Following is another example, which keeps calling itself unless a certain condition (n<=1) is met.

```c
int factorial (int n)
{
    if (n <= 1)
        return 1;
    else
        return (n * factorial(n - 1));
}
```

```c
void main(void)
{
    int f=factorial(5);
    printf("Factorial = %d\n", f);
    system("pause");
}
```

### 5.7 Examples

### 5.7.1 Equalizers

```c
void printTable( int );
void printHeading();
void main(void)
{
    printHeading();
    int x = 1;
    for(x=1;x<=10;x++)
    {
        printTable(x);
    }
    system("pause");
}
void printTable(int a)
{
    for(int x=1; x<=10; x++)
    {
        printf("%d\t",x*a);
    }
    printf("\n");
}
void printHeading()
{
    printf("----------------------------------Table of Tables----------------------------------\n\n");
}
```

### 5.7.2 Multiple Files

In a file header.h:

```c
void func(int a);
void funcSquare(int a);
void funcCube(int a);
```

In a file Implementation1.c:

```c
void func(int a)
{
    printf("I am func. I have to print: a = %d\n", a);
}
```

In a file Implementation2.c:

```c
void funcSquare(int a)
{
    printf("I am funcSquare. I have to print: a = %d\n", a*a);
}
void funcCube(int a)
{
    printf("I am funcCube. I have to print: a = %d\n", a*a*a);
}
```

In a file main.c:

```c
#include "header.h"

void main(void)
{
    printf("This is our main Program. Let's start...\n");
    func(5);
    funcSquare(5);
    funcCube(5);
    printf("This is our main Program. Let's finish...\n");
    system("pause");
}
```

### 5.7.3 Static Variables

```c
void demo()
{
    int normalVariable = 5;
    static int staticVariable = 5;
```

```c
printf("a = %d, b = %d\n", a, b);
swap(&a, &b);
printf("a = %d, b = %d\n", a, b);
system("pause");
}
```

### 5.7.5 BubbleSort

```c
void bubble(int a[], int n)
{
    int i, j;
    for (i = 0; i < n; ++i)
        for (j = n - 1; j > i; --j)
            if (a[j-1] > a[j])
                swap(&a[j-1], &a[j]);
}
```

![](img/6d3b01499498c82f19a5187d6ebfb7f1_142_0.png)

## Chapter 6: Arrays, Pointers and Strings

C provides a data structure that can store multiple values of same type in it by associating each value to a subscript. It is extremely useful in common programming. For example, you need to store marks of 50 students, instead of declaring 50 separate variables, you can simply use an array with size 50. Each element can be accessed by specifying its index or subscript.

An array is a random access data structure, where each element can be accessed directly and in constant time. A typical illustration of random access is a book - each page of the book can be open independently of others.

Arrays in C consist of contiguous memory locations which means that they are placed in memory together. The lowest member of array has the lowest address and last member of array has the highest memory address assigned to it.

In C, arrays and pointers are closely related concepts. Interestingly, an array name itself acts as a pointer, and pointers, like arrays, can be indexed. “Call by reference” mechanism is based on pointers. This mechanism allows the programmer to change the value of a local variable in one scope from another scope. C uses pointers for specifying parameters in function definitions to accomplish this. Strings are also one-dimensional arrays of characters. They will be discussed in the next chapter.

### 6.1 1-D Arrays

1-D arrays refer to one dimensional arrays. Such arrays can be considered as a single row or column containing a fixed number of elements. They have only one index. An array is just like a normal variable except for index. Index always start from 0 and end at (arraySize-1).

A general format for array declaration in C is as follows:

```c
Type arrayName [arraySize];
```

Type refers to the data type of array, followed by identifier and in the end array size enclosed in brackets.

Arrays may be of storage class automatic, static or extern but not register. ANSI C supports the initialization of all three types of arrays using an initializer but traditional C only allowed it for static or extern registers.

The general format for initializing 1-D arrays is as follows:

```c
Type identifier [size] = {list of elements separated by commas}
```

Here is an illustration of using a 1-D array, using initializer:

```c
void main(void)
{
    int table[10] = { 5, 10, 15, 20, 25, 30, 35, 40, 45, 50 };

    //printing elements of array
    for(int i = 0; i < 10 ; i++)
    {
        printf("5 x %d = %d\n",i+1,table[i]);
    }
    system("pause");
}
```

Here is an illustration of using a 1-D array, using a loop for initialization rather than common initializer:

```c
void main(void)
{
    int table[10];

    //initialization of array
    for(int i = 1; i <= 10 ; i++)
    {
        table[i-1] = i * 5;
    }
    //printing elements of array
    for(int i = 0; i < 10 ; i++)
    {
        printf("5 x %d = %d\n",i+1,table[i]);
    }
    system("pause");
}
```

![](img/6d3b01499498c82f19a5187d6ebfb7f1_146_0.png)

Output: Same for both programs

### 6.2 Pointers

A simple variable in a program is stored in a certain number of bytes at a memory location, or address, in the machine. Pointers are basically variables that hold these addresses rather than actual values. These addresses can be accessed and hence the actual values can also be accessed via “reference” of pointers. Pointers are used in programs to
