
| `isupper()` | 检查是否为大写 |
| `isxdigit()` | 检查字符是否为十六进制 |
| `isncntrl()` | 检查字符是否为控制字符 |
| `isprint()` | 检查字符是否为可打印字符 |
| `ispunct()` | 检查字符是否为标点符号 |
| `isgraph()` | 检查字符是否为图形字符 |
| `tolower()` | 检查是否为字母并转换为小写 |
| `toupper()` | 检查是否为字母并转换为大写 |

### 函数、数组和字符串

- C 语言中的 `isalpha()` 函数检查给定字符是否为字母。`isalpha()` 函数的语法所示：

`int isalpha(int x);`

- C 语言中的 `isdigit()` 函数检查给定字符是否为数字。`isdigit()` 函数的语法所示：

`int isdigit(int x);`

- C 语言中的 `isalnum()` 函数检查给定字符是否为字母数字。`isalnum()` 函数的语法所示：

`int isalnum(int x);`

- C 语言中的 `isspace()` 函数检查给定字符是否为空格。`isspace()` 函数的语法所示：

`int isspace(int x);`

- C 语言中的 `islower()` 函数检查给定字符是否为小写。`islower()` 函数的语法所示：

`int islower(int x);`

- C 语言中的 `isupper()` 函数检查给定字符是否为大写。`isupper()` 函数的语法所示：

`int isupper(int x);`

- C 语言中的 `isxdigit()` 函数检查给定字符是否为十六进制。`isxdigit()` 函数的语法所示：

`int isxdigit(int x);`

- C 语言中的 `isncntrl()` 函数检查给定字符是否为控制字符。`isncntrl()` 函数的语法所示：

`int isncntrl(int x);`

- C 语言中的 `isprint()` 函数检查给定字符是否为可打印。`isprint()` 函数的语法所示：

`int isprint(int x);`

- C 语言中的 `ispunct()` 函数检查给定字符是否为标点符号。`ispunct()` 函数的语法所示：

`int ispunct(int x);`

- C 语言中的 `isgraph()` 函数检查给定字符是否为图形字符。`isgraph()` 函数的语法所示：

`int isgraph(int x);`

- C 语言中的 `tolower()` 函数检查给定字符是否为字母并转换为小写。`tolower()` 函数的语法所示：

`int tolower(int x);`

- C 语言中的 `toupper()` 函数检查给定字符是否为字母并转换为大写。`toupper()` 函数的语法所示：

`int toupper(int x);`

### 自定义函数的需要：

- 有时，某些类型的操作或计算会在整个程序中的多处重复。
- 在这种情况下，我们可能在每次需要的地方重复程序语句。
- 另一种方法是设计一个可以在需要时被调用和使用的函数。
- 既节省时间又节省空间。

### 自定义函数是如何工作的？

```c
#include <stdio.h>
void functionName()
{
    ... ... ...
    ... ... ...
}

int main()
{
    ... ... ...
    ... ... ...

    functionName();

    ... ... ...
    ... ... ...
}
```

### 自定义函数的优点

- 1. 程序将更易理解、维护和调试。
- 2. 可以在其他程序使用的可复用代码。
- 3. 大程序可以被分成较小的模块。因此，一个大型项目可以分配给许多程序员完成。

### 示例：自定义函数

这是一个将两个整数相加的示例。为了完成这项任务，我们创建了一个自定义函数 `addNumbers()`。

```c
#include<stdio.h>

addNumbers(int a,int b);// 函数原型

int main()
{
    int n1,n2,sum;

    printf("Enters two numbers: ");
    scanf("%d %d",&n1,&n2);

    sum =addNumbers(n1, n2);// 函数调用
    printf("sum = %d",sum);

    return 0;
}

int addNumbers(int a,int b)// 函数定义
{
    int result;
    result =a+b;
    return result;// 返回语句
}
```

### 函数的组成元素

每个函数都包含以下元素：

- 1. 函数声明（函数原型）
- 2. 函数定义
- 3. 函数调用

#### 函数声明（函数原型）

- 类似于变量，在 C 语言中，每个函数在在使用之前都需要进行声明。
- 函数可以是全局声明，也可以是局部声明（在 `main()` 内部），取决于程序需求。**C 程序的结构** 语法：

```c
return_type function_name(argument list );
```

- 函数原型具有三个部分：

##### 返回类型：

- 它指定了函数的返回类型，如 `int`、`float`、`char` 等。函数如果不返回任何值，返回类型为 `void`。

##### 函数名：

- 它是函数的名称，应该是有意义的名字。它应该遵循命名规则。一些函数示例有 `display`、`show`、`calculate` 等。

##### 参数列表：

- 参数列表指定了执行任务所需的所有参数。参数之间用逗号分隔。通常提供数据类型。以下是两个 float 值的函数原型示例：

**函数声明示例**

`float sum (float, float);` 或 `float sum (float x, float y);`

其中，`float` 是返回类型，`sum` 是函数名，`float, float` 是参数列表。

#### 函数定义

- 函数定义包含执行块。它可以写在 `main()` 之前或之后，通常写在 `main()` 之后。

```c
return_type function_name( argument list )
{
    // 局部变量声明;

    // 执行语句;

    // 返回语句;
}
```

- 函数定义包含以下两个部分：
  1. 函数头
  2. 函数体

1. 函数头：
   - 函数定义的第一行被称为函数头。它由三部分组成：返回类型、函数名和参数列表。

2. 函数体：
   - 它由三部分组成：局部变量声明、执行部分和返回语句。所有需要的变量都在局部变量声明部分声明。执行部分包含执行任务的执行语句。返回语句应该是函数体的最后语句。它是可选的。如果函数的返回类型是 `void` 则可以省略，但返回类型非 `void` 的函数必须包含返回语句。下面是上述函数定义的定义示例。

**函数定义示例：**

```c
float sum ( float x, float y)
{
float result;              // 局部变量
result = x + y;            // 执行语句

return result; // 返回语句
}
```

- 无返回类型的示例如下：

```c
void sum ( float x, float y)
{
float result;              // 局部变量
result = x + y;            // 执行语句

printf("\n Sum is %.2f", result);
{
return;                      // 返回语句。可选的
}
}
```

- 注意：如果函数返回类型为 `void`，我们可以省略返回语句。

#### 函数调用

- 函数只需通过使用函数名后跟实际参数（参数）（如果有的话）来调用。下面的示例调用了我们定义的 `sum()` 函数。

```c
void main ()
{
float result;              // 接收局部变量
result = sum (10.0, 2.0);   // 函数调用
printf("\n Sum is %.2f", result);
}
```

当编译器遇到函数调用时，控制转移到函数定义并逐行执行函数，并通过返回语句返回一个计算值。

返回值被赋值给接收变量。如下所示：

```c
void sum ( )
{
    float result ; // 接收局部变量
    result = sum (10.0, 2.0) ); // 函数调用
    printf("\n sum is %.2f", result);
}
float sum ( float x, float y )
{
    float result ; // 局部变量
    result = x + y ; // 执行语句
    return result ; // 返回语句
}
```

在函数调用中传递的参数与函数定义中接收的参数应具有相同的数据类型。

例如，在上面的函数调用 `sum (10.0, 2.0)` 中，我们传递了 `float` 类型参数，在函数定义内部，这些 `float` 类型参数分别被 `float` 变量 `x` 和 `y` 接收。简而言之，函数调用和函数定义中的参数类型应该是相同的。

函数定义中使用的参数被称为形式参数。

### 函数参数

如果函数要使用参数，它必须声明接收参数值的变量。这些变量被称为函数的形式参数。

形式参数类似于函数内部其他局部变量，在进入函数时创建，在退出时销毁。

调用函数时，有两种方式可以将参数传递：

#### 函数、数组和字符串

| 序号 | 调用类型与描述 |
| :--- | :--- |
| 1 | **按值传递 (Call by value)** <br>这种方法将参数的实际值拷贝到函数的形式参数中。在这种情况下，函数内部对参数的修改对参数没有影响。 |
| 2 | **按引用传递 (Call by reference)** <br>这种方法将参数的地址拷贝到函数的形式参数中。在函数内部，使用该地址访问函数中使用的实际参数。这意味着对参数的修改会影响调用。 |

默认情况下，C 语言使用**按值传递**来传递参数。通常，这意味着函数内部的代码无法修改调用时使用的参数。

**按值传递**

**按值传递** 传递参数的方法是将参数的实际值拷贝到函数的形式参数中。在这种情况下，函数内部对参数的修改对参数没有影响。

考虑下面的 `swap()` 函数定义：

```c
/*交换两个值的定义 */
void swap(int x,int y)
{
    int temp;
    temp=x;/*保存x的值*/
    x=y;
    /*赋值给x*/
    y=temp;/*赋值给y*/
    return;
}
```

```c
#include <stdio.h>

/*function declaration */
void swap(int, int y);

int main()
{
    /*local definition */
    int a = 10;
    int b = 20;

    printf("Before value of a: %d\n", a);
    printf("Before value of b: %d\n", b);

    /*calling */
    swap(a, b);

    printf("After value of a: %d\n", a);
    printf("After value of b: %d\n", b);

    return 0;
}
```

让我们将上述代码放在单个文件中，编译并执行，它将产生以下结果：

Before value of a: 10

Before value of b: 20

After value of a: 10

After value of b: 20

这显示尽管值在函数内部被修改过，但它们并没有发生变化。

### 引用传递 (Call by reference):

向函数传递参数的**引用**方法是将参数的地址复制到形式参数中。在函数内部，使用该地址来访问实际使用的参数。

```c
/*function definition*/
void swap(int *x, int *y)
{
    int temp;
    temp = *x;
    *x = *y;
    *y = temp;
}
```

要通过引用传递值，像传递其他值一样将参数传递给函数。因此，你需要将函数参数声明为指针类型。如下示例：

```c
#include <stdio.h>

/*function declaration*/
void swap(int *x, int *y);

int main()
{
    /*local definition*/
    int a = 10;
    int b = 20;

    printf("Before value of a: %d\n", a);
    printf("Before value of b: %d\n", b);

    /*calling*/
    swap(&a, &b);

    printf("After value of a: %d\n", a);
    printf("After value of b: %d\n", b);

    return 0;
}
```

让我们将上述代码放在单个文件中，编译并执行以产生以下结果：

Before value of a: 10

Before value of b: 20

After value of a: 20

After value of b: 10

这显示更改也反映在了函数外部，这与值传递不同。

### 值传递与引用传递的区别

函数可以通过两种方式调用：**值传递 (Call by Value)** 或**引用传递 (Call Reference)**。这两种方式通常通过传递给它们的参数的值的类型来区分，作为函数参数传递的参数被称为*实际参数*，而函数接收到的参数称为*形式参数*。

**值传递：** 在这种参数传递方法中，实际参数的值被复制到函数的形式参数中，两者存储在不同的内存位置。因此，在函数内部内部的任何更改都不会反映在调用者的实际参数中。

**引用传递：** 实际参数和形式参数都指向同一个位置。因此，在函数内部进行的任何更改实际上都会反映在调用者的实际参数中。

### 函数、数组与字符串

| 值传递 (CALL BY VALUE) | 引用传递 (CALL BY REFERENCE) |
| :--- | :--- |
| 在调用函数时，我们把变量的值传递给它。此类函数被称为“值传递”。 | 在调用函数时，我们不是传递变量的值，而是将变量的地址（变量的位置）传递给函数，被称为“引用传递”。 |
| 在这种方法中，调用函数中每个变量的值被复制到被调用函数的形变量中。 | 在这种方法中，调用函数中实际变量的地址被复制到被调用函数的形变量中。 |
| 通过这种方法，对被调用函数中的形变量所做的更改对调用函数中的实际变量没有影响。 | 通过这种方法，使用地址访问实际变量，因此能够对它们进行操作。 |

### 变量的作用域 (SCOPE OF A VARIABLE)

任何编程语言中的作用域都是程序中的一个区域，定义的变量在该区域内存在，而在区域之外无法被访问。在编程语言中，可以在三个地方声明变量：

- 在函数或块内部，称为局部变量。
- 在所有函数外部，称为全局变量。
- 在函数参数的定义中，称为形式参数。

让我们理解一下什么是局部变量、全局变量以及形式参数。

#### 局部变量

在函数或块内部声明的变量称为局部变量。它们只能由该函数或代码块内部的语句使用。局部变量对于外部的函数是不可见的。下面的示例显示了局部变量的使用。在这里，所有变量 `a`、`b` 和 `c` 都是 `main()` 的局部变量。

```c
#include <stdio.h>
int main() {
    /* local variable declaration */
    int a, b;
    int c;
    /* actual initialization */
    a = 10;
    b = 20;
    c = a + b;
    printf("value of a = %d, b = %d and c = %d\n", a, b, c);

    return 0;
}
```

#### 全局变量

全局变量定义在函数外部，通常位于程序的顶部。全局变量在程序的生命周期内保持其值，并可以在程序定义的任何函数内部访问。

全局变量可以被任何函数访问，即全局变量在声明后在整个程序范围内可用。下面的程序显示了全局变量在程序中使用。

```c
#include <stdio.h>

/* global variable declaration */
int g;

int main() {
    /* local variable declaration */
    int a = 10;
    int b = 20;
    g = a + b;
    printf("value of a = %d, b = %d and g = %d\n", a, b, g);

    return 0;
}
```

使用 C 和 C++ 编程
