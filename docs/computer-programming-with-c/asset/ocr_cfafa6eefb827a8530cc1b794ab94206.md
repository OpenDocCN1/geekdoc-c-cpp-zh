```
```c
{
    int a=10;
    float b=32.5;
/*Create a void type pointer p*/
    void *p;
/*Create an integer type pointer "pint"*/
    int *pint;
/*Create a float type pointer "pflt"*/
    float *pflt;
/*Store the address of variable a in the pointer p*/
p=&a;
/*Copy the address inside p in pointer "pint"*/
pint=(int*)p;
/*Store the address of variable b in the pointer p*/
p=&b;
/*Copy the address inside p in pointer "pflt"*/
pflt=(float*)p;
printf("Value of variable a is %d\n", *pint);
printf("Value of variable b is %f\n", *pflt);
}
```
```

**Output**

```
```
Value of variable a is 10
value of variable b is 32.5
```
```

# ## 8.13 Pointer to a Function

Pointers in C/C++ can also point to a function which is defined in the program. This facilitates the programmer to call a particular function using a pointer. To make a pointer point to a function, type of the pointer must match with the prototype of the function.

Consider the given program, wherein we have created two functions `add()` and `sub()`. Both the functions take two integer values as an argument and return an integer as a result of execution. Since both of the function have same prototype, it is possible to create a single pointer which has an ability to point to either of the functions. The statement

```
```c
int (*pfunction)(int,int);
```
```

creates a pointer named pfunction that can point to any function taking two arguments of type int and returning a int value.

As the type of pointer pfunction exactly matches with the type of functions `add()` as well as `sub()`, the pointer can point to any of these functions. The statement,

```
```c
pfunction=add;
```
```