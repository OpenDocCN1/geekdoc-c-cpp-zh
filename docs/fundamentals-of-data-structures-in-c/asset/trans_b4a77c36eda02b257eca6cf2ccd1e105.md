

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_119_0.png)

### Fig. 2.1: Representation of a pointer variable.

### 图 2.1: 指针变量的表示。

For example,

例如，

```c
main()
{
 int *ptr, i = 25;
 ptr = &i;
}
```

where ptr is a pointer variable for storing the address of an integer value, hence ptr is an integer pointer. In the above program segment, ptr is made to point i by storing the address of i (i.e., &i) in ptr.

其中，ptr 是一个用于存储整数值地址的指针变量，因此 ptr 是一个整型指针。在上述程序片段中，通过将 i 的地址（即 &i）存储在 ptr 中，使 ptr 指向 i。

### Program 2.9:

### 程序 2.9：

```c
/* Program for accessing a variable through a pointer. */
/* pointer.c */
#include<stdio.h>
void main()
{
 int a = 5, b = 10, *ptr;
 ptr = &a;
 printf("\n Initial values a = %d & b = %d", a, b);
 b = *ptr;
 printf("\n Changed values a = %d & b = %d", a, b);
 printf("\n Value of ptr is %d", ptr);
 printf("\n Value of the address of a is %d", &a);
 printf("\n Value of *ptr is %d", *ptr);
}
```

The program displays the following output
程序显示以下输出
Initial values a = 5 & b = 10
Changed values a = 5 & b = 5
Value of ptr is 4094
Value of the address of a is 4094
Value of *ptr is 5

In Program 2.9 we are using a pointer variable *ptr. The pointer variable is initialized by assigning the address of the variable a to ptr as (ptr = &a). In the expression b = *ptr, the symbol * is placed before a pointer to access the content of the variable which is assigned to it. One can be surprised when you see the output of the program particularly the value of the address of a, when you execute this program in different computers at different times you will get different values of address which will be allocated to the variable a at different times.

在程序 2.9 中，我们使用了一个指针变量 *ptr。该指针变量通过将变量 a 的地址赋值给 ptr（即 ptr = &a）进行初始化。在表达式 b = *ptr 中，符号 * 放在指针之前，以访问分配给它的变量的内容。当您在不同计算机和不同时间执行此程序时，可能会对程序的输出感到惊讶，特别是变量 a 的地址值，每次分配给变量 a 的地址都会不同。

## 2.6 Initialization of Pointers

## 2.6 指针的初始化

Like ordinary variables, a pointer variable can be initialized. Static and external (global) pointer variables are initialized with NULL by default. Automatic (local) pointer variables can be initialized either with NULL or with the address of some other variable, which is already defined.

与普通变量一样，指针变量也可以初始化。静态和外部（全局）指针变量默认初始化为 NULL。自动（局部）指针变量可以初始化为 NULL，也可以初始化为某个已定义变量的地址。

For example the statement,

例如，语句，

```
ptr = &i;
```

is called as **pointer initialization**, since the address of `i` is initialized to the pointer variable `ptr`. A pointer variable can be also initialized as an ordinary variable in declaration itself. For example,

这称为**指针初始化**，因为 `i` 的地址被初始化到指针变量 `ptr`。指针变量也可以在声明本身中像普通变量一样初始化。例如，

```c
int i, *ptr = &i;
```

is also valid, since `ptr` points to the value stored in the address of `i`.

这也是有效的，因为 `ptr` 指向存储在 `i` 地址中的值。

## 2.7 Pointer Arithmetic

## 2.7 指针运算

An interesting use of pointers is pointer arithmetic. The arithmetic operations that can be performed on pointers are addition and subtraction. You can use the increment (++) and decrement (--) operators on the size of the variable pointed by the pointer. For example if

指针的一个有趣用途是指针运算。可以对指针执行的算术运算是加法和减法。您可以对指针所指向变量的大小使用递增（++）和递减（--）运算符。例如，如果

```
ptr++;
```

is an integer pointer, the increment operation moves the pointer by two bytes (since an integer is two bytes long) from where it is previously pointed. Similarly, if `ptr` is a character pointer, the increment operation moves the pointer by one byte (since a character is one byte long) from where it is previously pointed. If a decrement operation is carried out on a pointer, the pointer moves backwards, depending upon the size of the variable pointed by the pointer.

它是一个整型指针，则递增操作会将指针从之前指向的位置移动两个字节（因为整型占两个字节）。同样，如果 `ptr` 是字符指针，则递增操作会将指针从之前指向的位置移动一个字节（因为字符占一个字节）。如果对指针执行递减操作，指针将向后移动，移动距离取决于指针所指向变量的大小。

For example, if

例如，如果

```
ptr--;
```

is a character pointer. The decrement operation moves the pointer backwards by one byte from where it is previously pointed. The expression,

它是一个字符指针。递减操作会将指针从之前指向的位置向后移动一个字节。表达式，

```
ptr += 6;
```

increments the pointer by 6 elements of its type. Similarly, a pointer can be subtracted from an integer. Besides incrementation and decrementation of a pointer to an integer, you may also subtract one pointer from another pointer in order to find the number of elements of their type which separates the two pointers. Other operations like multiplication and division of pointers are prohibited. You cannot add or subtract `float` or `double` type pointers from each other.

将指针按其类型递增 6 个元素。同样，可以从整数中减去一个指针。除了对整型指针进行递增和递减外，您还可以用一个指针减去另一个指针，以找出分隔两个指针的其类型元素的数量。其他操作（如指针的乘法和除法）是被禁止的。您不能相互添加或减去 `float` 或 `double` 类型的指针。

## 2.8 Structure

## 2.8 结构体

*A structure* is a derived type usually representing a collection of variables of same or different data types grouped together under a single name. The variables or data items in a structure are called as *members* of the structure. A structure may contain one or more integer variables, floating-point variables, character variables, arrays, pointers, and even other structures can also be included as members. Structures help to organize data, particularly in large programs, because they allow a group of related variables to be treated as a single unit.

*结构体* 是一种派生类型，通常表示将相同或不同数据类型的变量集合分组在一个名称下。结构体中的变量或数据项称为结构体的*成员*。结构体可以包含一个或多个整型变量、浮点型变量、字符型变量、数组、指针，甚至还可以将其他结构体作为成员包含。结构体有助于组织数据，尤其是在大型程序中，因为它们允许将一组相关变量视为一个单元。

There are two fundamental differences between an array and a structure. One is, an array demands a homogeneous data type, i.e., the elements of an array must be of the same data type, where as a structure is a heterogeneous data type, since it can have any data type as its member. The second difference is that elements in an array are referred by their positions, where as members in a structure are referred by their unique names.

数组与结构体之间存在两个基本区别。其一，数组要求同质数据类型，即数组的元素必须是相同的数据类型，而结构体是异质数据类型，因为它可以将任何数据类型作为其成员。第二个区别是，数组中的元素通过其位置来引用，而结构体中的成员通过其唯一名称来引用。

### 2.8.1 Declaring a Structure

### 2.8.1 声明结构体

Structure declarations are somewhat more complex than array declarations since a structure must be defined in terms of its individual members. The general form or the syntax of declaring a structure is

结构体声明比数组声明稍微复杂一些，因为结构体必须根据其各个成员来定义。声明结构体的一般形式或语法是

```
struct <structure_name>
{
    data type member1;
    data type member2;
    data type member2;
    ..... .....
    data type memberN;
};
```

In the above declaration, *struct* is a keyword, followed by an optional user-defined structure name usually referred as a tag, which is used to identify the structure, and then the list of members with its data types. The list of member declarations is enclosed in a pair of flower braces. The closing brace of the structure and the semicolon ends the structure declaration. A typical example of declaring a structure is

在上述声明中，*struct* 是一个关键字，后面跟着一个可选的用户定义的结构体名称（通常称为标签），用于标识结构体，然后是带有其数据类型的成员列表。成员声明列表用一对花括号括起来。结构体的右花括号和分号结束结构体声明。声明结构体的典型示例是

```
struct employee
{
    int empno;
    char empname[15];
    float salary;
};
```

where *employee* is the name of the structure (i.e., tag). The structure *employee* contains three members of type *int*, *char* and *float* representing *empno*, *empname* and *salary* respectively.

其中，*employee* 是结构体的名称（即标签）。结构体 *employee* 包含三个成员，类型分别为 *int*、*char* 和 *float*，分别表示 *empno*、*empname* 和 *salary*。

### 2.8.2 Defining a Structure

### 2.8.2 定义结构体

Declaring a structure merely describes the template of the structure. Declaration does not reserve any memory space but it creates a new data type. Defining a structure means creating variables to access the members in the structure. Creating a structure variable allocates sufficient memory space to hold all the members of the structure. Structure variables can be created during structure declaration or by explicitly using the structure name. The general syntax for defining the structure is,

声明结构体仅描述结构体的模板。声明不保留任何内存空间，但它创建一个新数据类型。定义结构体意味着创建变量以访问结构体中的成员。创建结构体变量会分配足够的内存空间来容纳结构体的所有成员。结构体变量可以在结构体声明期间创建，也可以通过显式使用结构体名称来创建。定义结构体的一般语法是，

```
struct <structure_name>
{
    data type member1;
    data type member2;
    data type member2;
    ......
    ......
    data type memberN;
}structure_variable(s);
```

The structure can be defined declaration itself and an example for defining the structure during declaration is,

结构体可以在声明本身中定义，在声明期间定义结构体的示例是，

```c
struct employee
{
    int empno;
    char empname[15];
    float salary;
}emp1;
```

where the structure variable emp1 declares a variable emp1 of its type. The structure_variable(s) can be declared like ordinary variables and used to access the members of the structure. More than one structure_variable can also be declared by placing a comma in between the variables. Fig. 2.2 shows the memory allocation for the structure employee.

其中，结构体变量 emp1 声明了其类型的变量 emp1。结构体变量可以像普通变量一样声明，并用于访问结构体的成员。通过在变量之间放置逗号，也可以声明多个结构体变量。图 2.2 显示了结构体 employee 的内存分配。

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_122_0.png)

The syntax for defining the structure using the structure name is,

使用结构体名称定义结构体的语法是，

```
struct structure_name structure_variable(s)

or

structure_name structure_variable(s);
```

Note that the keyword struct is optional when defining the structure using the structure name.

注意，使用结构体名称定义结构体时，关键字 struct 是可选的。

A typical example for declaring a structure using the structure name is

使用结构体名称声明结构体的典型示例是

```c
struct employee emp1; or employee emp1;
```

If you need only one structure variable, the structure name or the tag is not necessary.

如果只需要一个结构体变量，则不需要结构体名称或标签。

For example,

例如，

```c
struct
{
    int empno;
    char empname[15];
    float salary;
}emp1;
```

where the structure declares and defines a variable named emp1. Note that the structure name or the structure variables may be omitted, but both, should not be omitted.

其中，该结构体声明并定义了一个名为 emp1 的变量。请注意，可以省略结构体名称或结构体变量，但两者不能同时省略。

The member names within a particular structure must be distinct from one another though a member name can be same as the name of the variable, which is defined outside the structure.

特定结构体中的成员名称必须彼此不同，尽管成员名称可以与结构体外部定义的变量名称相同。

For example,

例如，

```c
struct employee
{
    int empno;
    char empname[15];
    float salary;
}emp;
char empname[15];
```

where character variable empname inside the structure shares the same name with the variable empname declare outside the structure. Note that a structure declaration that is not followed by a list of variables reserves no storage space, it merely describes the template (i.e., the structure is only defined not declared).

其中，结构体内部的字符变量 empname 与结构体外部声明的变量 empname 共享相同的名称。请注意，后面没有跟变量列表的结构体声明不保留任何存储空间，它仅描述模板（即，结构体仅被定义而未被声明）。

### 2.8.3 Accessing Structure Members

### 2.8.3 访问结构体成员

We have declared and defined the structure and now let us see how the elements of the structure can be accessed. A member of a structure is always referred and accessed by the structure variable. In arrays, we use subscripts for accessing individual elements of an array. In structures we use the member access operator also referred as the dot operator “.” to access the members independently. The general form or the syntax for accessing a member of the structure is

我们已经声明并定义了结构体，现在让我们看看如何访问结构体的元素。结构体的成员始终通过结构体变量来引用和访问。在数组中，我们使用下标来访问数组的单个元素。在结构体中，我们使用成员访问运算符（也称为点运算符“.”）来独立访问成员。访问结构体成员的一般形式或语法是

```c
structure_variable.member_name
```

The structure variable followed by a period operator and the member name refers an individual member. For example, for accessing the structure elements, you can use

结构体变量后跟点运算符和成员名称引用一个单独的成员。例如，访问结构体元素时，可以使用

```c
emp1.empname similarly emp1.empno
```

In the above example, emp1 is the structure variable, which is used to access the

在上述示例中，emp1 是结构体变量，用于访问

