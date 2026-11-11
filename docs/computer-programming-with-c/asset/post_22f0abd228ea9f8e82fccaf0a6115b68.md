
The statement,

```c
int * p, *q;
```

is also valid and will create two pointers p and q. Notice that in any case, to create q as a pointer you must use asterisks just before the pointer name q.

The statement,

```c
int * p, q;
```

creates p as a pointer but q as a normal integer variable. This is because no asterisk symbol is specified for q. Hence C/C++ compiler considers q as a simple variable of type integer. But since there is an asterisk specified before p, it is created as a pointer of type integer.

In this text book, we will generally use asterisk symbol just before the pointer name when we create pointers; with an exception while creating constant pointers where we have to use a notation of asterisk immediately after the data type. **Constant pointers** are described in the later part of the text book.

## What is the size of a pointer?

![](img/57c0d966bb33c67a5a188e6bf39e4e02_395_0.png)

C/C++ has two types of pointers.

- 1. Near Pointer (used for relative addressing within the segment).
- 2. Far Pointer (used for absolute addressing to address a location outside the current segment).

As mentioned in Section 8.1.1, the size of each segment and organization of main memory (RAM) depends upon multiple hardware and software parameters. In a typical x86 environment where 16 bit compilers are used the size of each segment is 64 KB and hence near pointer is of 2 bytes in size whereas a far pointer is of 4 bytes in size. As mentioned in Section 8.1.1, near and far addressing is transparent to the programmer so you don't have to worry about this point from programming perspective. When you store the address of a particular variable in a pointer, C/C++ will internally determine whether a near or far pointer needs to be created to point to the target variable.

In fact, with today's generation of computing, most of the C/C++ compilers are 32 bit and they do not have a concept of near and far pointers at all. A 32 bit compiler makes all the pointers declared in the program as 4 bytes wide. Don't be surprised if you always get the size of a pointer as 4 bytes, it just means that you are working on a 32 bit compiler.

## 8.3 Data Type of Pointers

Although the memory addresses are always of type integer, the data type of pointer may not always be an integer. This is because the data type of the pointer depends upon the data type of the target variable whose address is contained in the pointer. In the absence of polymorphism, the data type of the pointer must be exactly the same as the data type of the variable to which the pointer points. This is because the indirection operator (*) is to be used with pointers to fetch the value of the target variable. As the amount of memory required for a particular variable depends on the data type of that variable, giving a correct data type to the pointer helps the CPU to determine the number of memory locations to be fetched to access the complete data value of the target variable. For example, if the pointer is of type integer, then CPU will access only the first two locations in order to fetch the complete value of the variable from memory by using indirection. This is because every integer value is of 2 bytes in size. Or if the pointer is of type float, then CPU will access the first four locations in order to fetch the complete value of the variable by using indirection, because every float value is of 4 bytes in size. This means that, an integer type pointer can only point to an integer variable whereas a float type pointer can only point to a float variable and so on the concept can be similarly extended to other data types.

> **CONCLUSION**
> 
> The data type of the pointer must be the same as the data type of the variable to which it points.

Following is an example that creates two variables a and c of type int and float, respectively. To store the addresses of each of these variables, we create two pointers p and r of type int and float, respectively.

```c
#include<stdio.h>
void main()
{
/*create variables*/
int a=10;
float c=42.9;
/* create individual pointers*/
int *p;
float *r;
/*store address of each of the variables in a corresponding
    pointer*/
p=&a;
r=&c;
/*print the values of a and c using pointers*/
printf("a=%d\n",*p);
printf("c=%f\n",*r);

/*print the address of a and c*/
printf("Address of a is %u\n",p);
printf("Address of c is %u\n",r);
}
```

**Output**

```text
a=10
c=42.900002

Address of a is 1000
Address of c is 3000
```

The statements,

```c
p=&a;
r=&c;
```

store the address of variable a in a integer pointer p and address of variable c in a floating point pointer r. Note that, the data type of each pointer is same as the data type of target variable which it points to. Figure 8.8 shows memory structure created by the code, assuming the starting addresses of variables a and c as 1000 and 3000, respectively.

As each of the pointers is associated with a particular data type, the indirection operator when applied to a particular pointer will accurately determine the number of locations required to be accessed by CPU in order to fetch the complete value of the target variable.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_397_0.png)

**Figure 8.8:** Pointers pointing to variables a and c

The following table will help in understanding the outputs of each of the `printf()` statements.

| Pointer usage | Description |
|---|---|
| `*p;` | The pointer p contains the address of variable a, hence *p will give the value of variable a, that is 10.<br><br>As pointer p contains the address 1000, when an indirection operator is applied to a pointer p, CPU will read the two consecutive locations with addresses 1000 and 1001, to get the value of the variable which is pointed by p. The value stored at these locations in memory is 10, hence the operation *p gives the value 10.<br><br>In this case, the CPU reads two locations in memory because the data type of pointer p is integer and every integer requires 2 bytes in memory. Hence the statement,<br><br>`printf("a=%d\n",*p);`<br><br>will generate the following output:<br><br>`a=10` |
| `*r;` | Similar to how *p works, *r will give the value 42.9, which is the value of variable c. The only point to mention is that the CPU this time reads four locations in memory with addresses 3000, 3001, 3002, and 3003 to get the value by using indirection because this pointer is of type float. |

Hence the statement,

```c
printf("c=%f\n",*r);
```

will generate the following output:

```text
c=42.9
```

Writing p in the code, will give the value stored inside the pointer p. We know that pointer p contains address of variable a, that is 1000. Hence, the result of this token will be 1000.

Hence the statement,

```c
printf("Address of a is %u\n",p);
```

will generate the following output:

```text
Address of a is 1000
```

Writing token r in the code, will give the address stored inside r that is 3000. Hence the statement,

```c
printf("Address of c is %u\n",r);
```

will generate the following output:

```text
Address of c is 3000
```

## 8.4 Types of Function Calls

### 8.4.1 Call by value

Consider the given code which consists of two functions main() and f1(). The function f1() takes one integer type argument and increments the integer value passed to it. The function main() calls a function f1() by passing the value of its local variable a which is created in main().

Due to the function call, value of variable a in main() is passed to variable p which is the formal argument of f1(). Since value of the variable is passed from calling function to the called function, the mechanism is named as ‘call by value’.

```c
#include<stdio.h>
void f1(int);
void main()
{
int a=10;
printf("Before call a=%d\n",a);
f1(a);
printf("After call a=%d\n",a);
}
void f1(int p)
{
p++;
}
```

**Output**

```text
Before call a=10
After call a=10
```

To understand the working of ‘call by value’ in detail, let us go through the above code line by line. The execution of code will start from the `main()` function. The following table explains the execution of each line in `main()`.

| Statement | Description |
|---|---|
| `int a=10;` | This statement creates a local variable `a` initialized to value 10. Note that, this is a local variable of `main()` and cannot be directly accessed by function `f1()`. |
| `printf("Before call a=%d\n",a);` | The statement prints the value of variable `a` which is 10. Hence, the following message is printed on the computer screen:<br><br>`Before call a=10` |
| `f1(a);` | This statement is a function call to `f1()` by passing a value of variable `a` as an argument to the function. On executing this statement, the control is transferred to the function definition of `f1()`, triggering its execution.<br><br>The value 10 is assigned to the formal argument `p` which is the local variable of `f1()` as shown in Figure 8.9. It is important to understand that, there are two variables being created in the memory, first is the variable `a` which is the local variable of `main()` function and the second is the variable `p` which is the local variable of function `f1()`.<br><br>Initially both the variables have same value which is 10 as shown in Figure 8.9. Inside the body of function `f1()`, the statement `p++` changes the value of `p` to 11. After the function completes its execution, the control is transferred back to the `main()` function. |
| `printf("After call a=%d\n",a);` | The statement prints the value of variable `a` after execution of the `f1()` is completed. Note that the function `f1()` never changed the value of variable `a` but it had just changed the value of variable `p`. As shown in Figure 8.9 the variables `a` and `p` are two different variables in memory and changing the value of variable `p` will not change the value of variable `a` in any way. When the control returns to the `main()` function the value of variable `a` is still 10. Hence, this statement prints the following message on the computer screen:<br><br>`After call a=10` |

> **NOTES**
> 
> **Call by value** creates two different variables one in the **calling** function, and the other in the **called** function. Updating the value of variable in **called** function will never update the corresponding variable in the **calling** function. This is because the two variables reside at different physical locations in memory.
