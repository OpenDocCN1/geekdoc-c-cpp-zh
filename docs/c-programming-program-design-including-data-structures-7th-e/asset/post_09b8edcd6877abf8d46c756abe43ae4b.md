
## Pointer Data Type and Pointer Variables

In Chapter 2, you learned that C++’s data types are classified into three categories: simple, structured, and pointers. Until now, you have studied only the first two data types. This chapter discusses the third data type called the pointer data type. You will first learn how to declare pointer variables (or pointers, for short) and manipulate the data to which they point. Later, you will use these concepts when you study dynamic arrays and linked lists. Linked lists are discussed in Chapter 14.

Chapter 2 defined a data type as a set of values together with a set of operations. Recall that the set of values is called the domain of the data type. In addition to these two properties, until now, all of the data types you have encountered have one more thing associated with them: the name of the data type. For example, there is a data type called `int`. The set of values belonging to this data type includes integers that range between −2147483648 and 2147483647, and the operations allowed on these values are the arithmetic operators described in Chapter 2. To manipulate numeric integer data in the range −2147483648 to 2147483647, you can declare variables using the word `int`. The name of the data type allows you to declare a variable of that type. Next, we describe the pointer data type.

The values belonging to pointer data types are the memory addresses of your computer. As in many other languages, there is no name associated with the pointer data type in C++. Because the domain—that is, the set of values of a pointer data type—is the addresses (locations) in memory, a pointer variable is a variable whose content is an address, that is, a memory location and the pointer variable is said to point to that memory location.

**Pointer variable:** A variable whose content is an address (that is, a memory address) and is therefore said to point to a memory address.

### Declaring Pointer Variables

As remarked previously, there is no name associated with pointer data types. Moreover, pointer variables store memory addresses. So the obvious question is: If no name is associated with a pointer data type, how do you declare pointer variables?

The value of a pointer variable is an address or memory space that typically contains some data. Therefore, when you declare a pointer variable, you also specify the data type of the value to be stored in the memory location pointed to by the pointer variable. For example, if a pointer variable contains the address of a memory location containing an `int` value, it is said to be an `int` pointer or a pointer (variable) of type `int`. As with regular variables, pointers are bound to a data type and they can only contain the addresses of (or point to) variables of a specific data type they were created to hold.

In C++, you declare a pointer variable by using the asterisk symbol (*) between the data type and the variable name. The general syntax to declare a pointer variable is:

```cpp
dataType *identifier;
```

As an example, consider the following statements:

```c
int *p;
char *ch;
```

In these statements, both `p` and `ch` are pointer variables. The content of `p` (when properly assigned) points to a memory location of type `int`, and the content of `ch` points to a memory location of type `char`. So, `p` is a pointer variable of type `int`, and `ch` is a pointer variable of type `char`.

Before discussing how pointers work, let us make the following observations. The statement:

```c
int *p;
```

is equivalent to the statement:

```c
int* p;
```

which is equivalent to the statement:

```c
int * p;
```

Thus, the character `*` can appear anywhere between the data type name and the variable name.

Now, consider the following statement:

```c
int* p, q;
```

In this statement, only `p` is the pointer variable, not `q`. Here, `q` is an `int` variable. Each variable must have its own `*` character placed to the left of it to make it a pointer variable. To avoid confusion, we prefer to attach the character `*` to the variable name. So the preceding statement is written as:

```c
int *p, q;
```

Of course, the statement:

```c
int *p, *q;
```

declares both `p` and `q` to be pointer variables of type `int`.

Now that you know how to declare pointers, next we will discuss how to make a pointer point to a memory space and how to manipulate the data stored in these memory locations.

Because the value of a pointer is a memory address, a pointer can store the address of a memory space of the designated type. For example, if `p` is a pointer of type `int`, `p` can store the address of any memory space of type `int`. C++ provides two operators—the address of operator (`&`) and the dereferencing operator (`*`)—to work with pointers. The next two sections describe these operators.

## Address of Operator (&)

In C++, the ampersand, `&`, called the **address of operator**, is a unary operator that returns the address of its operand. For example, given the statements:

```cpp
int x;
int *p;
```

the statement:

```cpp
p = &x;
```

assigns the address of `x` to `p`. That is, `x` and the value of `p` refer to the same memory location.

Let’s compare names and pointers. In the following two declarations, `num1` and `num2` are `int` variables and `numptr` is the name of an `int` pointer:

```cpp
int num1, num2;
int *numptr;
```

The name `num1` now stands in place of an `int` memory location and can be assigned the value of any integer between −2147483648 and 2147483647. For example, the following statement stores 100 in `num1`:

```cpp
num1 = 100;
```

The value held at the memory location named `num1` can easily be copied directly to another integer memory location by using the assignment operator. For instance, if we want to copy the integer 100 at the memory location `num1` to the memory location `num2`, we can use this statement:

```cpp
num2 = num1;
```

The name `num1` in a sense means “the value held in the memory location named `num1`.” This value is copied into the memory location named `num2`.

On the other hand, when we use the statement:

```cpp
numptr = &num1;
```

we are asking the program to copy the address of the memory location of `num1` to `numptr`, not the integer value it is holding. The pointer `numptr` will *not* contain 100, but the actual address `num1` has been assigned by the operating system. (In a sense, since the name `num1` stands for the memory address of `num1`’s value, and `numptr` contains the address of `num1`, `numptr` is really holding the name `num1`. This makes `numptr` a *reference* to `num1`.)

Now, if we output both `num1` and `numptr` using the statements

```cpp
cout << num1 << endl;
cout << numptr << endl;
```

the first line will output 100 onto the screen, while the second line will output an address usually displayed in hexadecimal digits.

In the next section, after discussing the dereference operator, we will explain how to output the value of the memory location whose address is stored in `numptr`.

## Dereferencing Operator (*)

Every chapter until now has used the asterisk character, `*`, as the binary multiplication operator. C++ also uses `*` as a unary operator. When used as a unary operator, `*`, commonly referred to as the **dereferencing operator** or **indirection operator**, refers to the object to which its operand (that is, the pointer) points. For example, given the statements:

```cpp
int x = 25;
int *p;
p = &x;    //store the address of x in p
```

the statement:

```cpp
cout << *p << endl;
```

prints the value stored in the memory space pointed to by `p`, which is the value of `x`. Also, the statement:

```cpp
*p = 55;
```

stores 55 in the memory location pointed to by `p`—that is, in `x`.

### EXAMPLE 12-1

Let us consider the following statements:

```cpp
int *p;
int num;
```

In these statements, `p` is a pointer variable of type `int`, and `num` is a variable of type `int`. Let us assume that memory location 1200 is allocated for `p`, and memory location 1800 is allocated for `num`. (See Figure 12-1.)

![](img/d0be7fc6d804b63484835c6c8bc67a07_865_0.png)

**FIGURE 12-1**  Variables `p` and `num`
