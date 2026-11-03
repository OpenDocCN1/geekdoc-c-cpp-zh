
## Thread

A thread is the smallest processing unit in a system. In parallel programming, several different threads are created corresponding to different computational elements and are then executed in parallel.

## OpenMP (Open MultiProcessing)

It is an API that supports directive-based programming. It provides a number of built-in directives and library functions that facilitate the development of parallel computing applications.

In C, an OpenMP directive is specified with the help of **#pragma** directive, as shown below:

```c
#pragma omp directive [clause 1] [clause 2] ...
```

- **#pragma omp** tells the compiler about the specification of an OpenMP directive
- **directive** is a valid OpenMP directive name.
- **clause** list comprises a set of clauses associated with the directive.

## The Parallel Directive

It is the OpenMP directive that helps to specify a block of code to be executed in parallel via multiple threads.

```c
#pragma omp parallel
```

- For parallel programming in C, we make use of a **#pragma omp parallel** expression that is defined in *"omp.h"* header file.
- So when the compiler comes across the **#pragma omp parallel**, the following block of statements will be executed in parallel as separate threads.

## The for Directive

The for directive is specified before a for loop and it specifies that the iterations of the for loop be divided across multiple threads.

```c
#pragma omp parallel for
```

## Algorithm

```text
Start
Step 1: Read the number of elements
Step 2: Read the elements of first array
        for i ← 0 to n − 1
          Read a[i]
Step 3: Read the elements of second array
        for i ← 0 to n − 1
          Read b[i]
```

### Step 4

Print contents of first array

```text
for i ← 0 to n − 1
    print a[i]
```

### Step 5

Print contents of second array

```text
for i ← 0 to n − 1
    print b[i]
```

### Step 6

```text
#pragma omp parallel for
begin
for i ← 0 to n − 1
tid ← omp_get_thread_num()
c[i] ← a[i] + b[i]
print c[i], tid    //Printing the array C
end
```

### Step 7

Print contents of array C

```text
for i ← 0 to n − 1
    print c[i]
```

Stop

## Flowchart

![](img/dad8bddd927fabdab2417ecbf1eb24eb_102_0.png)

## Program

```c
#include<stdio.h>
#include<omp.h>
void main()
{
int a[10],b[10],c[10],i, n;
int tid;
printf("\n Enter the number of elements");
scanf("%d",&n);
printf("\n Enter the elements of 1st array");
for(i=0;i<n;i++)
    scanf("%d",&a[i]);
printf("Enter the elements of 2nd array");
for(i=0;i<n;i++)
    scanf("%d",&b[i]);
printf("\n Array A\n");
for(i=0;i<n;i++)
{
printf("a[%d]=%d\n",i,a[i]);
}
printf("\n Array B\n");
for(i=0;i<n;i++)
{
printf("b[%d]=%d\n",i,b[i]);
}
#pragma omp parallel for
for(i=0;i<n;i++)
{
tid=omp_get_thread_num();
c[i]=a[i]+b[i]; /* addition of array A and array B in parallel */
printf("\nc[%d]=%d,thread id=%d\n",i,c[i],tid);
}
printf("\n===the new Array C is===\n");
for(i=0;i<n;i++)
{
printf("%d",c[i]);  /* print resultant array C */
}
}
```

## Sample Output 1

```text
Enter the number of elements 5
Enter the elements of 1st array 1 2 3 4 5
Enter the elements of 2nd array 5 6 7 8 9

Array A
a[0]=1
a[1]=2
a[2]=3
a[3]=4
a[4]=5

Array B
b[0]=5
b[1]=6
b[2]=7
b[3]=8
b[4]=9

c[0]=6,thread id=0
c[1]=8,thread id=0
c[2]=10,thread id=0
c[3]=12,thread id=1

c[4]=14,thread id=1
====the new Array C is====
6   8   10   12   14

Enter the number of elements 6
Enter the elements of 1st array 10 20 30 40 50 60
Enter the elements of 2nd array 1 2 3 4 5 6

Array A
a[0]=10
a[1]=20
a[2]=30
a[3]=40
a[4]=50
a[5]=60

Array B
b[0]=1
b[1]=2
b[2]=3
b[3]=4
b[4]=5
b[5]=6

c[0]=11,thread id=0
c[1]=22,thread id=0
c[2]=33,thread id=0
c[3]=44,thread id=1
c[4]=55,thread id=1
c[5]=66,thread id=1
=====the new Array C is===
11   22   33   44   55   66   77   88
```

## Outcomes

- Able to differentiate between sequential and parallel programming.
- Capable of identifying applications where parallelism can be applied.

## Practice Programs

- 1. Write a C program to create multiple threads in a program and print their thread IDs.
- 2. Write a parallel program to multiply two square matrices.

## Term-Work 12

### Problem Definition

Design and develop a function `rightrot(x, n)` in C that returns the value of the integer x rotated to the right by n bit positions as an unsigned integer. Invoke the function from the main with different values for x and n and print the results with suitable headings.

### Objectives

- To develop a function rightrot to rotate a number toward the right by a given number of bit positions and return the rotated number to main function.
- To understand the concepts of using functions and parameter passing.
- To test the program for all possible input cases.

### Prerequisites for Coding

The basic requirement to write this program is to have the knowledge of bitwise operators.

### Functions in C

The programs we have presented so far have been very simple. They solved problems that could be understood without too much effort. The principles of top-down design and structured programming dictate that a program should be divided into a main module and its related modules. Each module should also be divided into submodules according to software engineering principles.

In C, the idea of top-down design is done using functions. A C program is made of one or more functions, one and only one of which must be named main. In general, the purpose of a function is to receive zero or more pieces of data, operate on them, and return at most one piece of data.

A function in C is an independent module that will be called to do a specific task. When it is called it receives zero or more pieces of data, operates on them and returns at most one piece of data to the calling function.

> **Note:** In C, a program is made of one or more functions, one and only one of which must be called main.

The execution of the program always starts with main, but it can call other functions to do some part of the job.

### User-Defined Functions

Like every other object in C, functions must be both declared and defined. The function declaration gives the whole picture of the function that needs to be defined later. The function definition contains the code for a function.

A function name is used three times: for declaration, in a call, and for definition.

### Function Design Strategies

Basically, there are four function design strategies, namely

- 1. void function without parameters.
- 2. void function with parameters.
- 3. non-void function without parameters.
- 4. non-void function with parameters.

### Sample Program

Program in C to find the GCD of two integers and to output the result, ***using function.***

```c
#include<stdio.h>
#include<process.h>
int GCD(int a, int b)
{
    if (a<0) a = -a;
    if (b<0) b = -b;
    if (b>a)
    {
        printf("\n Invalid Input");
        exit(0);
    }
    else
    {
        if (a==0 || b==1 || a==b) return b;
        if (a==1 || b==0) return a;
        if (a%b) return GCD(b, a%b);
        else return GCD(a, b%a);
    }
}
void main()
{
  int x,y;
  printf("\n Enter 1st number:");
  scanf("%d",&x);
  printf("\n Enter 2nd number:");
  scanf("%d",&y);
  printf("\n GCD is:%d", GCD(x,y));
}
```

### For three numbers

```c
int GCD3 (int x, int y, int z)
{
  return GCD(x, GCD(y, z));
}
```

### Output

```text
Enter 1st number: 10
Enter 2nd number: 5
GCD is: 5

Enter 1st number: 20
Enter 2nd number: 15
GCD is: 5

Enter 1st number: 8
Enter 2nd number: 20
Invalid Input
```

### Related Theory: Logic Used

### What is Rotation?

A rotation is an operation similar to shift except that the bits that fall off at one end are put back to the other end. In C there is no operator for rotation. Instead rotation operation is performed by using bitwise shift operators (`<<` and `>>`) and OR operator (`|`).

### Left shift

In the expression `n << d`, the number n is moved d number of bits toward left. While shifting toward left, the leftmost bits will be lost and 0's will be filled at the right side.
