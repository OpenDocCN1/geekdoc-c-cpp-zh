
Now we can use `*p1` and `*p2` anywhere in our program. Let us see some examples:

| Expression | is equivalent to | Equivalent |
|---|---|---|
| `*p1 = 9;` | is equivalent to | `a = 9;` |
| `(*p1)++;` | is equivalent to | `a++;` |
| `x = *p2 + 10;` | is equivalent to | `x = b + 10;` |
| `printf("%d %f", *p1, *p2);` | is equivalent to | `printf("%d %f", a, b);` |
| `scanf("%d%f", p1, p2);` | is equivalent to | `scanf("%d%f", &a, &b);` |

The indirection operator can be read as "value at the address". For example, `*p1` can be read as "value at the address `p1`". This indirection operator (`*`) is different from the asterisk that was used while declaring the pointer variable.

Now we will see what is meant by the term `*(&age)`, where `age` is a variable. Since `&age` is an address, dereferencing it with `*` operator will give the variable at that address, and the variable at that address is `age`. Hence `*(&age)` is the same as writing `age`.

```c
/*P8.2 Program to dereference pointer variables*/
#include<stdio.h>
main()
{
    int a=87;
    float b=4.5;
    int *p1=&a;
    float *p2=&b;
    printf("Value of p1 = Address of a = %u\n",p1);
    printf("Value of p2 = Address of b = %u\n",p2);
    printf("Address of p1 = %u\n",&p1);
    printf("Address of p2 = %u\n",&p2);
    printf("Value of a = %d %d %d \n",a,*p1,*(&a));
    printf("Value of b = %f %f %f \n",b,*p2,*(&b));
}
```

Output:

```text
Value of p1 = Address of a = 65524
Value of p2 = Address of b = 65520
Address of p1 = 65518
Address of p2 = 65516
Value of a = 87 87 87
Value of b = 4.500000 4.500000 4.500000
```

We have already seen that while declaring a pointer variable, we have to mention the data type. The reason is that when we use the indirection operator, the number of bytes retrieved will be different for different data types. The value of the pointer only tells the address of the starting byte. For example, suppose we have a pointer `ptr` which contains the address 2000 and when we write `*ptr`, the compiler knows that it has to access the information starting at address 2000. So the compiler will look at the base type of the pointer and will retrieve the information depending on that base type. For example, if base type is `int`, then 2 bytes of information will be retrieved; if base type is `float`, 4 bytes of information will be retrieved, and so on. The following figures illustrate this fact. The shaded portion shows the number of bytes retrieved.

![](img/a76c706396af8b310f291a5313a27079_215_0.png)

The size of the pointer variable is the same for all types of pointers, but the memory that will be accessed while dereferencing is different.

```c
/*P8.3 Program to print the size of pointer variable and size of value dereferenced by that pointer*/
#include<stdio.h>
main()
{
char a='x',*p1=&a;
int b=12,*p2=&b;
float c=12.4,*p3=&c;
double d=18.3,*p4=&d;
printf("sizeof(p1) = %d , sizeof(*p1) = %d\n",sizeof(p1),sizeof(*p1));
printf("sizeof(p2) = %d , sizeof(*p2) = %d\n",sizeof(p2),sizeof(*p2));
printf("sizeof(p3) = %d , sizeof(*p3) = %d\n",sizeof(p3),sizeof(*p3));
printf("sizeof(p4) = %d , sizeof(*p4) = %d\n",sizeof(p4),sizeof(*p4));
}
```

Output:

```text
sizeof(p1) = 2 , sizeof(*p1) = 1
sizeof(p2) = 2 , sizeof(*p2) = 2
sizeof(p3) = 2 , sizeof(*p3) = 4
sizeof(p4) = 2 , sizeof(*p4) = 8
```

## 8.4 Pointer Arithmetic

Not all types of arithmetic operations are possible with pointers. The only valid operations that can be performed are:

- (1) Addition of an integer to a pointer and increment operation.
- (2) Subtraction of an integer from a pointer and decrement operation.
- (3) Subtraction of a pointer from another pointer of the same type.

Pointer arithmetic is scaled according to the size of the base type of the pointer. For example, if we have an integer pointer `pi` which contains address 1000, then on incrementing we get 1002 instead of 1001. This is because the size of `int` data type is 2. Similarly, on decrementing `pi`, we will get 998 instead of 999. The expression `(pi + 3)` will represent the address 1006. Let us see some pointer arithmetic for `int`, `float` and `char` pointers.

```c
int a = 5, *pi = &a;
float b = 2.2, *pf = &b;
char c = 'x', *pc = &c;
```

Suppose the address of variables `a`, `b` and `c` are 1000, 4000 and 5000 respectively, so initially values of `pi`, `pf`, `pc` will be 1000, 4000 and 5000.

- `pi++;` or `++pi;` → `pi = 1000 + 2 = 1002` (Since `int` is of 2 bytes)
- `pi = pi - 3;` → `pi = 1002 - 3*2 = 996`
- `pi = pi + 5;` → `pi = 996 + 5*2 = 1006`
- `pi--;` or `--pi;` → `pi = 1006 - 2 = 1004`

- `pf++;` or `++pf;` → `pf = 4000 + 4 = 4004` (Since `float` is of 4 bytes)
- `pf = pf - 3;` → `pf = 4004 - 3*4 = 3992`
- `pf = pf + 5;` → `pf = 3992 + 5*4 = 4012`
- `pf--;` or `--pf;` → `pf = 4012 - 4 = 4008`

- `pc++;` or `++pc;` → `pc = 5000 + 1 = 5001` (Since `char` is of 1 byte)
- `pc = pc - 3;` → `pc = 5001 - 3 = 4998`
- `pc = pc + 5;` → `pc = 4998 + 5 = 5003`
- `pc--;` or `--pc;` → `pc = 5003 - 1 = 5002`

The compiler scales all this arithmetic automatically since it knows the base type of the pointer. The arithmetic in the case of `char` pointer seems to be like ordinary arithmetic because the size of a `char` is 1 byte. The addresses of variables `a`, `b` and `c` are not affected by these operations; only the pointer moves ahead or backwards.

Suppose `pi` is an integer pointer that contains address 1000 initially.

![](img/a76c706396af8b310f291a5313a27079_216_0.png)

(a) `pi++;`

After incrementing, pointer `pi` points to address 1002 and if dereferenced (`*pi`), then it will return the information stored at bytes 1002 and 1003.

![](img/a76c706396af8b310f291a5313a27079_216_1.png)

(b) `pi = pi + 2;`

Now `pi` contains address 1006, and if dereferenced it will return information stored at bytes 1006 and 1007.

![](img/a76c706396af8b310f291a5313a27079_217_0.png)

(c) `pi = pi - 3;`

Now `pi` contains address 1000, and if dereferenced it will return information stored at bytes 1000 and 1001.

![](img/a76c706396af8b310f291a5313a27079_217_1.png)

(d) `printf("%d", *(pi + 2));`

Here the pointer will not move to address 1004 since we have not assigned any new value to it. The integer stored at bytes 1004 and 1005 will be printed.

![](img/a76c706396af8b310f291a5313a27079_217_2.png)

It is important to note that when we move a pointer somewhere else in memory by incrementing/decrementing or adding/subtracting integers, then it is not necessary that the pointer still points to a variable of the same data type or a valid memory location. The task of allocating memory locations to variables is done by the compiler. We don't know where and in what order it has stored them. We should take care that we move the pointers in such a way that they always point to valid memory locations. In the case of arrays, elements are stored in consecutive order. So this arithmetic is generally applied in arrays.

```c
/*P8.4 Program to show pointer arithmetic*/
#include<stdio.h>
main()
{
 int a=5,*pi=&a;
 char b='x',*pc=&b;
 float c=5.5,*pf=&c;
 printf("Value of pi = Address of a = %u\n",pi);
 printf("Value of pc = Address of b = %u\n",pc);
 printf("Value of pf = Address of c = %u\n",pf);
 pi++;
 pc++;
 pf++;
 printf("Now value of pi = %u\n",pi);
 printf("Now value of pc = %u\n",pc);
 printf("Now value of pf = %u\n",pf);
}
```

Output:

```text
Value of pi = Address of a = 1000
Value of pc = Address of b = 4000
Value of pf = Address of c = 8000
Now value of pi = 1002
Now value of pc = 4001
Now value of pf = 8004
```

```c
/*P8.5 Program to understand the postfix/prefix increment/decrement in a pointer variable of base type int */
#include<stdio.h>
main ()
{
	int a=5;
	int *p;
	p=&a;
	printf("Value of p = Address of a = %u\n",p);
	printf("Value of p = %u\n",++p);
	printf("Value of p = %u\n",p++);
	printf("Value of p = %u\n",--p);
	printf("Value of p = %u\n",p--);
}
```

Output:

```text
Value of p = Address of a = 1000
Value of p = 1002
Value of p = 1002
Value of p = 1002
Value of p = 1000
```

In the first `printf`, the address of `a = 1000` is printed. Since in the second `printf`, first the pointer is incremented, then its value is printed. Since the base type of the pointer is `int`, it is incremented by 2. Similarly, other `printf` statements are executed.

Subtraction of a pointer from another pointer of the same base type returns an integer, which denotes the number of elements between the two pointers. If we have two `int` pointers `ptr1` and `ptr2`, containing addresses 3000 and 3010 respectively, then `ptr2 - ptr1` will give 5 (since size of `int` is 2). This operation is generally performed when both pointer variables point to the elements of the same array.

The arithmetic operations that can never be performed on pointers are:

- Addition, multiplication, division of two pointers.
- Multiplication of a pointer by any number.
- Division of a pointer by any number.
- Addition of `float` or `double` values to pointers.

The precedence level of `*` operator and increment/decrement operators is the same, and their associativity is from right to left. There can be confusion while combining these operators in pointer expressions.
