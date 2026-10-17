
+ 11. `\_\_\_\_\_\_\_\_` 不是 C++ 中的有效运算符。

(a) `::`

(b) `::*`

(c) `endI`

(d) `setw`

+ 12. 作用域解析运算符指的是

(a) 静态变量

(b) 全局变量

(c) 动态变量

(d) 局部变量

+ 13. 运算符 `new` 和 `delete` 也被称为

(a) 免费存储运算符

(b) 二元运算符

+ (c) 运算符

+ (d) 逻辑运算符

14. 以下哪个不是 C++ 中的强制类型转换运算符？

+ (a) `const`

+ (b) `interpret`

+ (c) `static`

+ (d) `dynamic`

15. 选择错误的赋值表达式：

+ (a) `p=(q=r=60)+20`

+ (b) `p=(q+10)`

+ (c) `p=(q=10)`

+ (d) `p+=(-10)`

# 4 C++ 中的函数

## 学习目标

阅读本章后，你将能够

- 描述 C++ 程序中 `main()` 函数的用法
- 解释函数原型
- 区分传引用调用和返回引用机制
- 讨论内联函数
- 确定默认参数如何与函数一起使用
- 通过示例解释递归
- 演示函数重载在 C++ 程序中的使用
- 列出各种匹配库函数

### 4.1 引言

我们知道函数在 C 程序开发中起着重要作用。将程序划分为函数是自顶向下结构化编程的主要原则之一。使用函数的另一个优点是，可以通过在程序的不同位置调用和使用它们来减小程序的大小。

回想一下，我们在开发 C 程序时使用了类似以下的语法。

```
void show();                    /* Function declaration */
main()
{
    show();                      /* Function call */
    ....
}
void show()
{
    /* Function definition */
    ....
    /* Function body */
    ....
}
```

面向对象编程与 C++

当函数被调用时，控制权转移到函数体中的第一条语句。然后执行函数体中的其他语句，并在遇到闭合大括号时控制权返回到主程序。C++ 也不例外。函数仍然是 C++ 程序的构建块。事实上，C++ 增加了许多新特性，使其更可靠、更灵活。像 C++ 运算符一样，C++ 函数可以被重载，使其根据传递给它的参数执行不同的任务。其中大多数修改都是为了满足面向对象设施的要求。

在本章中，我们将简要讨论添加到 C++ 函数的各种新特性和其实现。

### 4.2 主函数

C 并未为 `main()` 函数指定任何返回类型，而 `main()` 函数是程序执行的起点。`main()` 的定义看起来像这样：

```
main()
{
    // main program statements
}
```

这是完全有效的，因为 C 中的 `main()` 不返回任何值。

在 C++ 中，`main()` 向操作系统返回 `int` 值。因此，C++ 明确将 `main()` 定义为匹配以下原型之一：

```
int main()
int main(int argc, char * argv[])
```

具有返回值 的函数应使用 `return` 语句终止。因此，C++ 中的 `main()` 函数定义如下：

```
int main()
{
    ...
    ...
    return 0;
}
```

由于函数的返回类型默认为 `int`，`main()` 头部中的关键字是可选的。大多数 C++ 编译器如果没有 `return` 语句会生成错误或警告。Turbo C++ 会发出警告

Function should return a value

然后继续编译程序。实际从 `main()` 返回一个值是良好的编程实践。

许多操作系统会测试返回值（退出值）以确定是否存在问题。通常的约定是，零的退出值意味着程序成功运行，而非零值意味着存在问题。显式使用 `return(0)` 语句将表明程序已成功执行。

### 4.3 函数原型

函数原型是添加到 C++ 函数的主要改进之一。原型通过给出参数的数量和类型以及返回值的类型等细节，向编译器描述函数接口。有了函数原型，声明和定义函数时始终使用模板。当函数被调用时，编译器使用模板来确保传递了正确的参数，并且返回值得到正确处理。任何参数或返回类型的违规都会在编译时被编译器捕获。这些检查和控制在传统的 C 函数中不存在。

记住，C 也使用原型。但它是由 Stroustrup 在 C++ 中引入的，而该特性的成功促使 ANSI C 委员会采纳了它。然而，C 和 C++ 之间的原型存在一个主要区别。虽然 C++ 使原型成为必需，ANSI C 使其成为可选的，也许是为了保持与经典 C 的兼容性。

函数原型是在调用程序中的声明语句，其形式如下之一：

```
type function-name (argument-list);
```

`argument-list` 包含必须传递给函数的参数的类型和名称。

示例：

```
float volume(int x, float y, float z);
```

请注意，每个参数变量必须在括号内独立声明。也就是说，像这样的组合声明

```
float volume(int x, float y, z);
```

是非法的。

在函数声明中，参数的名称是虚拟变量，因此它们是可选的。也就是说，

```
float volume(int, float, float);
```

在声明处是可以接受的。在此阶段，编译器仅在函数被调用时检查参数的类型。

通常，我们可以在函数原型的参数列表中包含或排除变量名。原型中的变量名充当占位符，因此，如果使用名称，它们不必与函数调用或函数定义中使用的名称匹配。

在函数定义中，名称是必需的，因为函数内部必须引用参数。

示例：

```
float volume(int a, float b, float c)
{
  float v = a*b*c;
}
```

面向对象编程与 C++

函数 `volume()` 可以按如下方式调用：

```
float cubel = volume(bl,wl,h1); // Function call
```

变量 `bl`、`wl` 和 `h1` 被称为实际参数，它们指定 `cubel` 的尺寸。它们的类型（已在之前声明）应与原型中声明的类型匹配。记住，调用语句不应在参数列表中包含类型名称。

我们也可以声明一个空参数列表的函数，如以下示例所示：

```
void display( );
```

在 C++ 中，这意味着函数不传递任何参数。它等同于语句

```
void display(void);
```

然而，在 C 中，空括号意味着任意数量的参数。也就是说，我们放弃了原型。C 函数也可以通过在原型中使用省略号来具有“开放”参数列表，如下所示：

```
void do_something ( list_of_arguments, ... );
```

使用省略号的函数在 `list_of_arguments` 中提供一个或多个声明的参数。使用此类支持可变数量参数的函数需要包含头文件 `"cstdarg"`。以下程序演示了使用可变参数列表的函数：

```
#include <iostream>
#include <cstdarg>
using namespace std;
int findmaximum(int count, ...)
{
int max, value;
va_list list;//declare variable argument list
va_start(list, count);//start accessing variable list
max = va_arg(list, int);//extract the first element of list
for (int arg = 1; arg < count; ++arg){
value = va_arg(list, int);//extract each successive element from list
if (max < value)
max = value;
}
va_end(list); //end the access of the variable argument list
return max;
}
int main()
{
cout << findmaximum(5, 14, 15, 12, 13, 10) << endl;
cout << findmaximum(3, 10, 11, 12) << endl;
return max;
}
```

此程序的输出为：

15

12

在此程序中，变量列表中的元素通过 `"va_arg (list, int)"` 访问。它指定了预期参数的类型（在本例中为 `int`）。然而，请注意，编译器无法检查参数列表的类型。让我们考虑以下情况：

```
int main() {
    cout << findmaximum(5, 14.0, "Hello", 13, 10) << endl;
    cout << findmaximum(3, 10, 3.5, 12) << endl;
    return 1;
}
```

上述函数调用通过了编译器的测试，不会产生任何错误。然而，运行时会输出以下内容：

1076625408

1074528256

上述意外输出是由于列表中存在异构类型的参数。`va_arg` 调用从列表中返回一个 4 字节序列，因为我们已指定预期参数的类型为整数。编译器不执行类型检查。因此，此类函数应极其谨慎使用。

### 4.4 传引用调用

在 C 中，函数按值传递参数。被调用函数创建一组新的变量并将参数的值复制到其中。函数无法访问调用程序中的实际变量，只能操作值的副本。调用程序中的原始变量。但可能出现需要更改调用程序中变量值的情况。例如，在冒泡排序中，我们比较列表中相邻的两个元素，如果第一个元素大于第二个元素则交换它们的值。如果使用函数进行冒泡排序，它应该能够更改调用函数中变量的值，而按值调用方法无法实现。

C++ 中引用变量的提供使我们能够按引用向函数传递参数。当我们按引用传递参数时，被调用函数中的“形式”参数成为调用函数中“实际”参数的别名。这意味着当函数操作自己的参数时，它实际上是在操作原始数据。让我们考虑以下情况：

```
void swap(int &a,int &b) // a and b are reference variables
{
    int t = a;
    a = b; // Dynamic initialization
    b = t;
}
```

现在，如果 `m` 和 `n` 是两个整数变量，则函数调用

```
swap(m, n);
```

将使用其别名（引用变量）`a` 和 `b` 交换 `m` 和 `n` 的值。在传统的 C 语言中，这是通过指针和间接寻址实现的，如下所示：

```
void swapl1(int *a, int *b) /* Function definition */
{
    int t;
    t = *a; /* assign the value at address a to t */
    *a = *b; /* put the value at b into a */
    *b = t; /* put the value t into b */
}
```

该函数可以按如下方式调用：

```
swapl(&x, &y); /* call by passing */
             /* addresses of variables */
```

这种方法在 C++ 中也是可以接受的。注意，按引用调用的方法在方法上更简洁。

### 4.5 RETURN BY REFERENCE

函数也可以返回引用。考虑以下函数：

```
int & max(int &x, int &y)
{
    if (x > y)
        return x;
    else
        return y;
}
```

由于 `max(x)` 的返回类型为 `int&`，函数返回 `x` 或 `y` 的引用（而不是值）。然后像 `max(a,b)` 这样的函数调用将产生对 `a` 或 `b` 的引用，具体取决于它们的值。这意味着此函数调用可以出现在赋值语句的左侧。也就是说，

```
max(a,b) = -1;
```

是合法的，如果 `a` 更大则将 `-1` 赋给 `a`，否则将 `-1` 赋给 `b`。

> 函数不应被制作为返回自动变量（作用域在函数内）的引用。这将导致编译器发出警告。

### 4.6 INLINE FUNCTIONS

使用函数编程的一个目标是节省一些内存空间，当函数可能被多次调用时，这种节省是可观的。然而，每次调用函数时，都需要花费大量额外时间来执行一系列指令，例如跳转到函数、保存寄存器、将参数压入栈以及返回调用函数。当函数很小时，相当一部分执行时间可能花费在这些开销上。

解决此问题的一种方案是使用宏定义，流行地称为宏。预处理器宏在 C 中很流行。宏的主要缺点是它们并不是真正的函数，因此在编译期间通常的错误检查不会发生。

C++ 对此问题有不同的解决方案。为了消除对小型函数的调用成本，C++ 提出了一种称为内联函数的新特性。内联函数是在调用时进行内联展开的函数。编译器用相应的函数代码替换函数调用（类似于宏展开）。内联函数定义如下：

```
inline function-header
{
  function body
}
```

示例：

```
inline double cube(double a)
{
  return(a*a*a);
}
```

上述内联函数可以通过以下语句调用

```
c = cube(3.0);
d = cube(2.5+1.5);
```

执行这些语句后，`c` 和 `d` 的值将分别为 27 和 64。如果参数为 2.5 + 1.5，函数会传递表达式的值。此例中为 4。这使得内联特性优于宏。

使函数内联很容易。我们只需在函数定义前加上 `inline` 关键字即可。所有内联函数必须在被调用前定义。

在使函数内联之前应谨慎行事。随着函数大小的增长，内联函数的速度优势会减弱。到了某个点，函数调用的开销变得小于函数执行的开销，内联函数的优势可能会丧失。在这种情况下，使用普通函数更有意义。通常，当函数足够小，可以在一两行内定义时，才会将其设为内联。

```
inline double cube(double a) {return(a*a*a);}
```

请记住，`inline` 关键字仅向编译器发送请求，而不是命令。如果函数定义过长或过于复杂，编译器可能会忽略此请求并将函数编译为普通函数。

内联展开可能不工作的一些情况是：

- 1. 对于返回值的函数，如果存在循环、`switch` 或 `goto`。
- 2. 对于不返回值 的函数，如果存在 `return` 语句。
- 3. 如果函数包含静态变量。
- 4. 如果内联宏是递归的。

## Object-Oriented Programming with C++

内联展开使程序运行更快，因为消除了函数调用和返回的开销。然而，它使程序占用更多内存，因为定义内联函数的语句会在每次调用函数的地方被复制。因此，需要权衡。

Note

Program 4.1 说明了内联函数的使用。

### Program 4.1 Inline Functions

```
#include <iostream>

using namespace std;

inline float mul(float x, float y)
{
    return(x*y);
}

inline double div(double p, double q)
{
    return(p/q);
}

int main()
{
    float a = 12.345;
    float b = 9.82;

    cout << mul(a,b) << "\n";
    cout << div(a,b) << "\n";

    return 0;
}
```

Program 4.1 的输出为：

121.228

1.2571

> LIMITATION

内联函数可能会使函数大小增加到无法放入缓存的程度。

### 4.7 DEFAULT ARGUMENTS

C++ 允许我们在不指定其所有参数的情况下调用函数。在这种情况下，函数会为在函数调用中没有匹配参数的参数分配默认值。默认值在函数声明时指定。编译器查看原型以查看函数使用多少参数，并提醒程序可能存在默认值。以下是具有默认值的原型的示例：

### 83

Functions in C++

```
float amount(float principal, int period, float rate=0.15);
```

默认值以与变量初始化在语法上相似的方式指定。上述原型为参数 `rate` 声明了默认值 0.15。随后像

```
value = amount(5000, ?); // one argument missing
```

这样的函数调用会将 5000 的值传递给 `principal`，将 7 传递给 `period`，然后函数使用 `rate` 的默认值 0.15。

```
value = amount(5000, 5, 0.12); // no missing argument
```

会将 0.12 的显式值传递给 `rate`。

默认参数在声明时检查，在调用时求值。一个重要点是，只有尾部参数可以有默认值，我们必须从右到左添加默认值。我们不能为参数列表中间的特定参数提供默认值。以下是具有默认值的函数声明的一些示例：

```
int mul(int i, int j=5, int k=10); // legal
int mul(int i=5, int j); // illegal
int mul(int i=0, int j, int k=10); // illegal
int mul(int i=2, int j=5, int k=10); // illegal
```
