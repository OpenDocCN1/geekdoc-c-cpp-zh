
![](img/57c0d966bb33c67a5a188e6bf39e4e02_400_0.png)

## 8.4.2 Call by address

When a function is called by passing the address of the actual parameters instead of values, the mechanism is named as **call by address**.

Consider the given code to understand working of call by address. The function `main()` has a local variable a and its address is passed to `f1()` at the time when function call is made. Note that, formal argument of function `f1()` is declared as a pointer, as it needs to store the address that is passed by `main()`.

```c
#include<stdio.h>
void f1(int*);
void main()
{
int a=10;
printf("Before call a=%d\n",a);

f1(&a);
printf("After call a=%d\n",a);
}
void f1(int *p)
{
(*p)++;
}
```

### Output

```text
Before call a=10
After call a=11
```

To understand the working of ‘call by address’ in detail, let us go through the given code line by line.

The execution of the code will start from the `main()` function. The following table explains the execution of each line in `main()` function.

| Statement | Description |
|---|---|
| `int a=10;` | This statement creates a local variable initialized to value 10. Remember it is local variable of `main()` and cannot be directly accessed by function `f1()`. |
| `printf("Before call a=%d\n",a);` | The statement prints the value of variable `a` which is 10. Hence the following message is printed on the computer screen:<br>`Before call a=10` |
| `f1(&a);` | This statement is a function call to `f1()` by passing the address of variable `a` as an argument. Let us assume the address of variable `a` as 1000 as shown in Figure 8.10. The control will now be transferred to the function definition by storing the address of the actual argument `a` in the formal argument `p` which is a pointer. Hence it will be correct to say that the pointer `p` stores the address of variable `a`. Therefore the value stored in the pointer `p` is 1000 as shown in Figure 8.10. The statement inside function `f1()`,<br><br>`(*p)++;`<br><br>applies an indirection operator to pointer `p`, hence increment (`++`) is applied to the contents of the variable whose address is contained in the pointer. This changes the value of variable `a` to 11. It is important to understand that because pointer `p` points to variable `a`, both `a` and `*p` will operate on the same memory location, hence adding 1 to `*p` is same as adding 1 to variable `a` as shown in the Figure 8.10.<br><br>Also note the presence of parentheses in the statement `(*p)++;` which first applies the indirection operator to the pointer and then increments the value of the variable. This is necessary because in the normal course the priority of `++` is greater than the priority of `*` which we have to alter in this case.<br><br>After the `f1()` completes its execution, the control is transferred back to the `main()` function. |
| `printf("After call a=%d\n",a);` | The statement prints the value of variable `a` after returning from the function `f1()`. Note that the function `f1()` has already changed the value of variable `a` by using a pointer. Hence, when the control returns to `main()` function the value of variable `a` is already changed to 11.<br><br>Following message is printed on the computer screen as a result of this statement:<br>`After call a=11` |

> **NOTES**
>
> When a function is called by passing address of actual argument, the **called** function creates an additional link (using pointer) to the variable defined in the **calling** function. This way we can access the actual value of the variable in the **called** function using an **indirection operator**. This mechanism is named as **call by address**.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_402_0.png)

Figure 8.10: Call by address

### NOTES

Clearly, call by address gives additional access to the called function to modify the variable declared in the calling function by using the principle of indirection. Though this is required in some cases but it also creates a possibility of genuine programmers to accidentally modify the memory location of the calling function. In this example, we have intentionally modified the memory location of the main() from f1(). This is ok, but in some cases, we may not want to do so. Under such circumstances you can declare the pointer argument as a const. For example, if we make pointer p as a constant argument of function f1() as shown in the following statement:

```c
void f1(const int *p)
{
(*p)++; /*ERROR: Value pointed by p cannot be changed*/
}
```

then, we will not be able to modify the value which is pointed by pointer p. Hence the statement (*p)++; will give an error. This is because, making the argument as const in this case, conveys the compiler that the value pointed by pointer should not be modified. If this is the requirement, the keyword const must also be added while prototyping the function f1() as shown in the following statement:

```c
void f1(const int*);
```

Further details about const pointers are discussed in Section 8.5. This note just explains one of the possible usage of const pointers. Please refer Section 8.5 to know more about const pointers.

## 8.4.3 To swap the values of two variables by using call by address: An example

In the given main() function, we have created two local variables a and b with values 10 and 20, respectively. The requirement is to write another function swap() such that the values of local variables a and b in main() are exchanged after the swap() function is executed. The function swap() is required to be called from a place in main() function as shown below:

```c
void main()
{
    int a=10,b=20;
    printf("Before swap\n");
    printf("a=%d\nb=%d\n",a,b);
    Call function swap here
    printf("After swap\n");
    printf("a=%d\nb=%d\n",a,b);
}
```

We understand from Chapter 7 that variables declared in a particular function are always local to that function and cannot be directly accessed by any other function.

The requirement here is that, when the execution of function swap() completes the values of a and b should be exchanged (i.e., swap() should store 20 in variable a and 10 in variable b). This means that the function swap() is required to modify the values of variables a and b which is against the concept of ‘local variables’ and ‘call by value’.

Hence, the only option is to call the function swap() by address. Let us create two pointers in swap() function say p and q, so that these pointers can store the addresses of variables a and b, respectively. So, we already understand that the contents of actual arguments in the ‘calling function’ can be modified by using the pointers in the ‘called function’ provided that the pointers store the addresses of the actual variables in ‘calling function’. This means that we can now access the values of variables a and b in function swap() by applying the indirection operator to pointers p and q, respectively. Hence, swapping the values of a and b in main() function is same as swapping of *p and *q in swap() function, because the pointer p points to variable a, pointer q points to variable b.

```c
void swap(int *p, int *q)
{
    int temp;
    temp=*p;
    *p=*q;
    *q=temp;
}
```

As shown below, we call function swap() such that the first argument passed to swap() is address of variable a and the second argument is the address of variable b. This will ensure that p holds address of a and q holds address of b.

```c
swap(&a,&b);
```

### NOTES

In summary, as pointers p and q point to variables a and b respectively, using *p in function swap() we can access the value of variable a of function main() and using *q in function swap() we can access the value of variable b of function main().

Given below is the full source code that performs exchange of variables in main() using swap() function:

```c
#include<stdio.h>
void swap(int*, int*);
void main()
{
int a=10,b=20;
printf("Before swap\n");
printf("a=%d\nb=%d\n",a,b);
swap(&a,&b);
printf("After swap\n");
printf("a=%d\nb=%d\n",a,b);
}
void swap(int *p, int *q)
{
        int temp;
        temp=*p;
        *p=*q;
        *q=temp;
}
```

### Output

```text
Before swap
a=10
b=20
After swap
a=20
b=10
```

Let us go through the above code line-by-line to understand the approach of swapping values by using call by address. The execution will start from the main() function and the first line in the code creates two variables a and b with values 10 and 20 as shown in the Figure 8.11:

```c
int a=10,b=20;
```

The next two printf() statements in the code will print the values of a and b as follows:

```text
Before swap
a=10
b=20
```
