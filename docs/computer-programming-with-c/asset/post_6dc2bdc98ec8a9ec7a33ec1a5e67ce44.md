
![](img/57c0d966bb33c67a5a188e6bf39e4e02_405_0.png)

**Figure 8.11:** Local variables in `main()` function

The statement,

```c
swap(&a,&b);
```

calls function `swap()` by passing the addresses of actual arguments a and b which will be stored in pointers p and q, respectively.

Hence, pointer p in `swap()` now points to variable a in `main()` and pointer q in `swap()` points to variable b in `main()` as shown in Figure 8.12.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_405_1.png)

**Figure 8.12:** Initialization of formal arguments of `swap()` function

The first line of `swap()` function,

```c
int temp;
```

declares a local variable named as temp as shown in Figure 8.13. The variable temp will give a temporary storage in memory which is required to swap the values of variables a and b.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_406_0.png)

**Figure 8.13:** Variable temp is created in `swap()` function

![](img/57c0d966bb33c67a5a188e6bf39e4e02_406_1.png)

**Figure 8.14:** Execution of `temp=*p`

The next statement in function `swap()`,

```c
temp=*p;
```

stores the value of the variable a in variable temp as shown in the Figure 8.14. Hence, we have accessed the value of variable a in `main()` by the principle of indirection using pointer p in `swap()`.

The next line in function `swap()`,

```c
*p=*q;
```

puts the value of variable b inside variable a as shown in the Figure 8.15. This statement reads the value of variable b by applying the indirection operator to pointer q and writes the value to variable a by applying the indirection to pointer p.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_407_0.png)

![](img/57c0d966bb33c67a5a188e6bf39e4e02_407_1.png)

Similarly, the last line in `swap()` function `*q=temp;` stores the value of local variable `temp` inside the variable `b` as shown in Figure 8.16.

Thus, the values of variables `a` and `b` are exchanged using the pointers created in `swap()` function. Therefore, when control of execution returns back to the `main()` function, the `printf()` statement now prints the value of `a` as 20 and value of `b` as 10 as shown below:

```
After swap
a=20
b=10
```

## CAUTION

If a pointer is used in the program without initializing it to a valid memory location, then such a pointer is called a wild pointer. Wild pointers are dangerous because whenever we use the new memory location they are pointing to, they may corrupt some location in RAM resulting in the program crashing or making the system misbehave.

For example,

```c
int *p; /*The pointer is not initialized and hence it points to some random unknown memory location*/
*p=30; /*changes the contents of some memory location which is not really known and hence it may crash the program or make the system misbehave*/
```

## 8.5 Arithmetic Operations with Pointers

C/C++ supports usage of the following operators for performing operations with the address that is contained in the pointer:

- Unary operators: ++ (increment) and -- (decrement)
- Binary operators: + (addition) and - (subtraction)

Address inside a pointer will be changed as a result of pointer arithmetic; hence it is the responsibility of the programmer to ensure that even after the arithmetic operation completes, the pointer continues to point to a relevant memory location that contains a meaningful data value.

The address inside a pointer is always changed in multiples of the size of its data type. This means that, if we attempt to change the address inside a pointer by a value k, then the address will actually be changed by a factor k*sizeof(d), where d is the 'data type' of the pointer. The factor k*sizeof(d) always ensures that the pointer never contains any address other than the starting address of the data value, in cases when a single data value is spread across multiple locations in RAM.

For example, let us consider an integer type pointer, pointing to a variable a as shown below.

```c
int a=10;
int *p;
p=&a;
```

Let the address of variable a be 1000, which is also contained in the pointer p as shown in the Figure 8.17. Let us now perform an increment operation (++) to change the address inside the pointer. This can be done by the statement below:

```c
p++;
```

![](img/57c0d966bb33c67a5a188e6bf39e4e02_408_0.png)

**Figure 8.17:** Pointer pointing to variable a

Note that the increment operation will not be applied to the value of variable a, this is because the pointer is not used along with an indirection operator `*`. The statement `p++;` will change the address contained inside the pointer, by a factor `1*sizeof(int)`, as the data type of the pointer is integer. Every integer takes two bytes in the memory, hence the statement will actually change the address by `1*2 = 2`. This means that every change in address by 1 will change the address actually by 2 for integer type pointers. Hence the new address inside a pointer will be 1002 and not 1001. Notice that 1001 is not the starting address of variable a, so it will never be contained in the pointer, this is because pointers should always store the starting address of any object in order to accurately point to the object in memory.

To get a thorough understanding of this concept, let us create four variables a, b, c and d of type integer, char, float, and double, respectively. Let us now create four pointers p, q, r, and s such that they point to the variables a, b, c, and d, respectively as shown in the Figure 8.18.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_409_0.png)

**Figure 8.18:** Pointers p, q, r, and s pointing to variables a, b, c, and d, respectively

```c
/*create variables in memory*/
int a=10;
char b='$';
float c=42.9;
double d=80.2;

/*create individual pointers*/
int *p;
char *q;
float *r;
double *s;

/*store the address of each of the variables in a pointer*/
p=&a;
q=&b;
r=&c;
s=&d;
```

Figure 8.18 assumes the starting address of variables a, b, c, and d as 1000, 2000, 3000, and 4000, respectively as contained in pointers p, q, r, and s, respectively. The table below gives some **examples** of pointer arithmetic.

| Example statement | Description |
|---|---|
| `p+2;` | This statement adds constant 2 to the address contained in the pointer p. Given that the current address contained in the pointer is 1000 and the pointer is of type integer, new address will be calculated as:<br>`=1000 + 2*sizeof(int)`<br>`=1000 + 2*2`<br>`=1004`<br>Hence, the next address generated by the expression is 1004. |
| `q+6;` | This statement adds constant 6 to the address contained in the pointer q. Given that the current address contained in the pointer is 2000 and the pointer is of type char, new address will be calculated as:<br>`=2000 + 6*sizeof(char)`<br>`=2000 + 6*1`<br>`=2006`<br>Hence, the next address generated by the expression is 2006. |
| `r+3;` | This statement adds constant 3 to the address contained in the pointer r. Given that the current address contained in the pointer is 3000 and the pointer is of type float, new address will be calculated as:<br>`=3000 + 3*sizeof(float)`<br>`=3000 + 3*4`<br>`=3012`<br>Hence, the next address generated by the expression is 3012. |
| `s-5;` | This statement subtracts constant 5 to the address contained in the pointer s. Given that the current address contained in the pointer s is 4000 and the pointer is of type double, new address will be calculated as:<br>`=4000 - 5*sizeof(double)`<br>`=4000 - 5*8`<br>`=3960`<br>Hence, the next address generated by the expression is 3960. |

Pointer arithmetic will be heavily used in Section 8.6, which explains the process to access array elements by using pointers.

### 8.5.1 Keyword `const` with pointers

From Chapter 2, we understand that const is a keyword used to create constant variables. For example,

```c
const int a=10;
```

creates a variable a with a constant value 10. As we have used a keyword const in the declaration of a, the value of variable a cannot change throughout the program. Any attempt to change the value of the variable a will raise a compile time error.

Keyword const can also be used with pointer declarations. const can be used to create the following three types of pointers:

- 1. Constant pointer
- 2. Pointer that points to a Constant Data Value
- 3. Constant pointer that points to a constant variable (combination of both 1 and 2)

### 8.5.2 Constant pointer

A pointer which cannot change the address to which it points is called a **constant pointer**. The following is the syntax for creating constant pointers.

```c
DataType* const pointer_name=&Target_Variable;
```

Note the presence of keyword const which creates a constant pointer. The pointer named as pointer_name is initialized to hold the address of Target_Variable.

It is important to note that, when you declare a constant pointer, it must always be initialized. The following declaration of a constant pointer is illegal,

```c
int* const p;
```

because the pointer p is never initialized. The highlighted statement,

```c
int a=10;
int* const p=&a;
```

is legal because it initializes the address of variable a in the constant pointer p. Hence, assuming address of variable a as 1000, pointer p points to variable a as shown in the Figure 8.19.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_411_0.png)

As p is a constant pointer, you cannot change the address stored inside p by any means. This means that you cannot reinitialize p to point to any other variable. For example, if b is another integer type variable, the following statement will give an error,
