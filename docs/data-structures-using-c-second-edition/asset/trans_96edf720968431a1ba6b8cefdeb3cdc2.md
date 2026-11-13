

```c
printf("\n The value of num after calling the function = %d", num);
return 0;
}
void add(int n)
{
    n = n + 10;
    printf("\n The value of num in the called function = %d", n);
}
```

### 输出

The value of num before calling the function = 2
The value of num in the called function = 12
The value of num after calling the function = 2

使用按值传递方式向函数传递参数时，请记住以下几点：

- 当按值传递参数时，被调用函数会创建与传递给它的参数具有相同数据类型的新变量。
- 调用函数传递的参数值会被复制到新创建的变量中。
- 当使用按值传递技术传递参数时，调用函数中变量的值不受影响。

### 优缺点

使用按值传递技术的最大优点是，参数可以作为变量、字面量或表达式传递，而其主要缺点是复制数据会消耗额外的存储空间。此外，复制可能需要花费大量时间，从而导致性能损耗，尤其是当函数被多次调用时。

### 按引用传递

当调用函数使用按值传递方法向被调用函数传递参数时，将参数修改后的值返回给调用者的唯一方法是显式使用 return 语句。更好的选择是使用按引用传递技术传递参数。在此方法中，我们将函数参数声明为引用而非普通变量。完成此操作后，函数对其接收到的参数所做的任何更改在调用函数中也可见。

要指示参数是按引用传递的，在参数列表的类型后放置一个星号（*）。

因此，在按引用传递方法中，函数接收到的是参数的隐式引用，而不是其值的副本。因此，函数可以修改变量的值，该更改也会反映在调用函数中。以下代码说明了这一概念。

```c
#include <stdio.h>
void add(int *);
int main()
{
    int num = 2;
    printf("\n The value of num before calling the function = %d", num);
    add(&num);
    printf("\n The value of num after calling the function = %d", num);
    return 0;
}
void add(int *n)
{
*n = *n + 10;
printf("\n The value of num in the called function = %d", n);
}
```

### 输出

The value of num before calling the function = 2
The value of num in the called function = 12
The value of num after calling the function = 12

### 优点

使用按引用传递技术传递参数的优点包括：

- 由于参数不会被复制到新变量中，因此它提供了更高的时间和空间效率。
- 函数可以更改参数的值，并且该更改会反映在调用函数中。
- 函数只能返回一个值。如果需要返回多个值，可以按引用传递这些参数，以便修改后的值在调用函数中可见。

### 缺点

然而，使用此技术的缺点是，如果在被调用函数中对变量造成了无意的更改，则这些更改会反映在调用函数中，因为原始值已被覆盖。

请考虑下面交换两个整数值的代码。请注意调用函数和被调用函数中整数的值。

```c
//This function swaps the value of two variables
#include <stdio.h>
void swap_call_val(int, int);
void swap_call_ref(int *, int *);
int main()
{
 int a=1, b=2, c=3, d=4;
 printf("\n In Main(), a = %d and b = %d", a, b);
 swap_call_val(a, b);
 printf("\n In main(), a = %d and b = %d", a, b);
 printf("\n\n In main(), c = %d and d = %d", c, d);
 swap_call_ref(&c, &d);
 printf("\n In main(), c = %d and d = %d", c, d);
 return 0;
}
void swap_call_val(int a, int b)
{
 int temp;
 temp = a;
 a = b;
 b = temp;
 printf("\n In Function (Call By Value Method) - a = %d and b = %d", a, b);
}
void swap_call_ref(int *c, int *d)
{
 int temp;
 temp = *c;
 *c = *d;
 *d = temp;
 printf("\n In Function (Call By Reference Method) - c = %d and d = %d", *c, *d);
}
```

### 输出

```
In main(), a = 1 and b = 2
In function (Call By Value Method) - a = 2 and b = 1
In main(), a = 1 and b = 2
In main(), c = 3 and d = 4
In function (Call By Reference Method) - c = 4 and d = 3
In main(), c = 4 and d = 3
```

## 1.11 指针

C 语言中的每个变量都有一个名称和与之关联的值。当声明变量时，计算机内存中会分配一个特定的内存块来存储该变量的值。分配的内存块大小取决于数据类型。请考虑以下语句。

```c
int x = 10;
```

执行此语句时，编译器会预留 2 字节内存来存储值 10。它还会建立一个符号表，在其中添加符号 x 以及预留这 2 字节内存的内存相对地址。

（注意整数的大小可能因系统而异。在 32 位系统上，整数变量分配 4 字节，而在 16 位系统上，它分配 2 字节。）

因此，C 语言中的每个变量都有一个值和一个与之关联的内存位置（通常称为地址）。我们将分别使用 rvalue 和 lvalue 术语来表示变量的值和地址。

rvalue 出现在赋值语句的右侧（上述语句中的 10），不能用于赋值语句的左侧。因此，编写 10 = k; 是非法的。如果我们写，

```c
int x, y;
x = 10;
y = x;
```

然后，我们有两个整数变量 x 和 y。编译器为整数变量 x 预留内存并将 rvalue 10 存储在其中。当我们说 y = x 时，由于 x 在赋值运算符 = 的右侧，因此 x 被解释为其 rvalue。因此，这里 x 指的是存储在为 x 预留的内存位置中的值，在此例中为 10。执行此语句后，y 的 rvalue 也是 10。

你可能也在好奇，我们为什么要讨论地址和 lvalue。实际上，指针只不过是内存地址。指针是一个包含另一个变量内存位置的变量。因此，指针是一个表示数据项位置的变量，例如变量或数组元素。指针在 C 语言中经常使用，因为它们有许多有用的应用。这些应用包括：

- 指针用于在函数之间来回传递信息。
- 指针使程序员能够通过函数参数从函数返回多个数据项。
- 指针提供了一种访问数组单个元素的替代方法。
- 指针用于将数组和字符串作为函数参数传递。我们将在后续章节中讨论此问题。
- 指针用于创建复杂的数据结构，例如树、链表、链栈、链队列和图。
- 指针用于变量的动态内存分配（有关 C 程序中内存分配，请参阅附录 A）。

### 1.11.1 声明指针变量

声明指针变量的一般语法如下。

```c
data_type *ptr_name;
```

在这里，data_type 是指针将指向的值的数据类型。例如，

```c
int *pnum;
char *pch;
float *pfnum;
```

在上述每条语句中，都会声明一个指针变量来指向指定数据类型的变量。虽然所有这些指针（pnum、pch 和 pfnum）都指向不同的数据类型，但它们在内存中将占用相同的空间。但是它们将占用多少空间取决于代码运行的平台。现在让我们声明一个整数指针变量，并在程序代码中开始使用它。

```c
int x = 10;
int *ptr;
ptr = &x;
```

在上述语句中，ptr 是指针变量的名称。* 告诉编译器 ptr 是一个指针变量，而 int 指定它将存储整数变量的地址。因此，整数指针变量“指向”一个整数变量。在最后一条语句中，ptr 被赋予 x 的地址。& 运算符检索 x 的 lvalue（地址），并将其复制到指针 ptr 的内容中。请考虑图 1.11 中给出的内存单元。

![](img/be6359df08208122bec6fad1103de211_48_0.png)

图 1.11 内存表示

现在，由于 x 是整数变量，它将被分配 2 字节。假设编译器为其分配内存位置 1003 和 1004，则 x 的地址（写作 &x）等于 1003，即 x 在内存中的起始地址。当我们写 ptr = &x 时，则 ptr = 1003。

我们可以“解引用”指针，即，我们可以通过使用一元 * 运算符（如 *ptr）来引用其指向的变量的值。也就是说，*ptr = 10，因为 10 是 x 的值。请查看以下显示指针变量用法的代码：

```c
#include <stdio.h>
int main()
{
    int num, *pnum;
    pnum = &num;
    printf("\n Enter the number : ");
    scanf("%d", &num);
    printf("\n The number that was entered is : %d", *pnum);
    return 0;
}
```

### 输出

Enter the number : 10
The number that was entered is : 10

*(&num) 的值是多少？它等同于简单地写 num。

