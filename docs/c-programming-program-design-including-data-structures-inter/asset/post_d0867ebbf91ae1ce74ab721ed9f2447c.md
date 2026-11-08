
In these statements, both `p` and `ch` are pointer variables. The content of `p` (when properly assigned) points to a memory location of type `int`, and the content of `ch` points to a memory location of type `char`. Usually, `p` is called a pointer variable of type `int`, and `ch` is called a pointer variable of type `char`.

Before discussing how pointers work, let us make the following observations. The statement:

```cpp
int *p;
```

is equivalent to the statement:

```cpp
int* p;
```

which is equivalent to the statement:

```cpp
int * p;
```

Thus, the character `*` can appear anywhere between the data type name and the variable name.

Now, consider the following statement:

```cpp
int* p, q;
```

In this statement, only `p` is the pointer variable, not `q`. Here, `q` is an `int` variable. To avoid confusion, we prefer to attach the character `*` to the variable name. So the preceding statement is written as:

```cpp
int *p, q;
```

Of course, the statement:

```cpp
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

assigns the address of x to p. That is, x and the value of p refer to the same memory location.

## Dereferencing Operator (*)

Every chapter until now has used the asterisk character, *, as the binary multiplication operator. C++ also uses * as a unary operator. When used as a unary operator, *, commonly referred to as the dereferencing operator or indirection operator, refers to the object to which its operand (that is, the pointer) points. For example, given the statements:

```cpp
int x = 25;
int *p;
p = &x;  //store the address of x in p
```

the statement:

```cpp
cout << *p << endl;
```

prints the value stored in the memory space pointed to by p, which is the value of x. Also, the statement:

```cpp
*p = 55;
```

stores 55 in the memory location pointed to by p—that is, in x.

### EXAMPLE 12-1

Let us consider the following statements:

```cpp
int *p;
int num;
```

In these statements, p is a pointer variable of type int, and num is a variable of type int. Let us assume that memory location 1200 is allocated for p, and memory location 1800 is allocated for num (see Figure 12-1).

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_827_0.png)

Consider the following statements:

- 1. `num = 78;`
- 2. `p = &num;`
- 3. `*p = 24;`

The following shows the values of the variables after the execution of each statement.

| After Statement | Values of the Variables | Explanation |
|---|---|---|
| 1 | Memory diagram showing `p` at 1200 and `num` at 1800. | The statement `num = 78;` stores 78 into `num`. |
| 2 | Memory diagram showing `p` at 1200 and `num` at 1800. | The statement `p = &num;` stores the address of `num`, which is 1800, into `p`. |
| 3 | Memory diagram showing `p` at 1200 and `num` at 1800. | The statement `*p = 24;` stores 24 into the memory location to which `p` points. Because the value of `p` is 1800, statement 3 stores 24 into memory location 1800. Notice that the value of `num` is also changed. |

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_828_0.png)

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_828_1.png)

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_828_2.png)

Let us summarize the preceding discussion.

- 1. A declaration such as `int *p;` allocates memory for `p` only, not for `*p`. Later, you will learn how to allocate memory for `*p`.
- 2. The content of `p` points only to a memory location of type `int`.
- 3. `&p`, `p`, and `*p` all have different meanings.
- 4. `&p` means the address of `p`—that is, 1200 (in Figure 12-1).
- 5. `p` means the content of `p`, which is 1800, after the statement `p = &num;` executes.
- 6. `*p` means the content of the memory location to which `p` points. Note that after the statement `p = &num;` executes, the value of `*p` is 78; after the statement `*p = 24;` executes, the value of `*p` is 24.

### EXAMPLE 12-2

Consider the following statements:

```cpp
int *p;
int x;
```

Suppose that we have the memory allocation for p and x as shown in Figure 12-2.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_829_0.png)

**FIGURE 12-2**  Variables p and x

The values of &p, p, *p, &x, and x are as follows:

| Expression | Value |
|---|---|
| `&p` | 1400 |
| `p` | ? (unknown) |
| `*p` | Does not exist (undefined) |
| `&x` | 1750 |
| `x` | ? (unknown) |

Suppose that the following statements are executed in the order given:

```cpp
x = 50;
p = &x;
*p = 38;
```

The values of &p, p, *p, &x, and x are shown after each of these statements executes.

After the statement `x = 50;` executes, the values of &p, p, *p, &x, and x are as follows:

| Expression | Value |
|---|---|
| `&p` | 1400 |
| `p` | ? (unknown) |
| `*p` | Does not exist (undefined) |
| `&x` | 1750 |
| `x` | 50 |

After the statement `p = &x;` executes, the values of &p, p, *p, &x, and x are as follows:

| Expression | Value |
|---|---|
| `&p` | 1400 |
| `p` | 1750 |
| `*p` | 50 |
| `&x` | 1750 |
| `x` | 50 |

After the statement `*p = 38;` executes, the values of &p, p, *p, &x, and x are as follows. (Because *p and x refer to the same memory space, the value of x is also changed to 38.)

| Expression | Value |
|---|---|
| `&p` | 1400 |
| `p` | 1750 |
| `*p` | 38 |
| `&x` | 1750 |
| `x` | 38 |

Let us note the following:

- 1. p is a pointer variable.
- 2. The content of p points only to a memory location of type `int`.
- 3. Memory location `x` exists and is of type `int`. Therefore, the assignment statement:
    ```cpp
    p = &x;
    ```
    is legal. After this assignment statement executes, `*p` is valid and meaningful.

The program in Example 12-3 further illustrates how a pointer variable works.

### EXAMPLE 12-3

The following program illustrates how pointer variables work:

```cpp
//Chapter 12: Example 12-3
#include <iostream>                              //Line 1
#include <iomanip>                               //Line 2

using namespace std;                             //Line 3

const double PI = 3.1416;                        //Line 4

int main()                                        //Line 5
{
    double radius;                                //Line 7
    double *radiusPtr;                            //Line 8

    cout << fixed << showpoint << setprecision(2); //Line 9

    radius = 2.5;                                 //Line 10
    radiusPtr = &radius;                          //Line 11

    cout << "Line 12: Radius = " << radius
         << ", area = " << PI * radius * radius << endl; //Line 12

    cout << "Line 13: Radius = " << *radiusPtr
         << ", area = "
         << PI * (*radiusPtr) * (*radiusPtr) << endl;     //Line 13

    cout << "Line 14: Enter the radius: ";       //Line 14
    cin >> *radiusPtr;                            //Line 15
    cout << endl;                                 //Line 16
```

From the output of the statements in Lines 20 and 21, it follows that radiusPtr stores the address of the variable radius. (Note that the address of radiusPtr, the value of radiusPtr, and the address of radius as shown by the output of Lines 19, 20, and 21, respectively, are machine dependent. When you run this program on your machine, you are likely to get different values. Furthermore, the pointer values, that is, the addresses, are printed in hexadecimal by default.)

## Classes, Structs, and Pointer Variables

In the previous section, you learned how to declare and manipulate pointers of simple data types, such as int and char. You can also declare pointers to other data types, such as classes. You will now learn how to declare and manipulate pointers to classes and structs. (Recall that both classes and structs have the same capabilities. The only difference between classes and structs is that, by default, all members of a class are private, and, by default, all members of a struct are public. Therefore, the following discussion applies to both.)

Consider the following declaration of a struct:

```cpp
struct studentType
{
    char name[26];
    double gpa;
    int sID;
    char grade;
};
```

```cpp
studentType student;
studentType *studentPtr;
```

In the preceding declaration, student is an object of type studentType, and studentPtr is a pointer variable of type studentType. The following statement stores the address of student in studentPtr:

```cpp
studentPtr = &student;
```

The following statement stores 3.9 in the component gpa of the object student:

```cpp
(*studentPtr).gpa = 3.9;
```

The expression (*studentPtr).gpa is a mixture of pointer dereferencing and the class component selection. In C++, the dot operator, ., has a higher precedence than the dereferencing operator.

Let us elaborate on this a bit. In the expression (*studentPtr).gpa, the operator * evaluates first, so the expression *studentPtr evaluates first. Because studentPtr is a
