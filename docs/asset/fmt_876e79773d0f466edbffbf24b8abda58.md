
`int *countPtr, count;`

声明变量 `countPtr` 为类型 `int *`（即指向 `int` 值的指针），读作“`countPtr` 指向 `int`”或“`countPtr` 指向类型为 `int` 的对象”。此外，前述声明中的变量 `count` 被声明为 `int`，而不是指向 `int` 的指针。声明中的 `*` 仅适用于 `countPtr`。每个被声明为指针的变量都必须以星号 (`*`) 为前缀。例如，声明

```cpp
double *xPtr, *yPtr;
```

表示 `xPtr` 和 `yPtr` 都是指向 `double` 值的指针。当 `*` 出现在声明中时，它不是运算符；相反，它表示正在声明的变量是指针。指针可以声明为指向任何数据类型。

### 常见编程错误 8.1

> 假设用于声明指针的 `*` 会传播到声明的以逗号分隔的变量列表中的所有变量名可能会导致错误。每个指针都必须用 `*` 前缀其名称进行声明（名称前有或没有空格都可以——编译器会忽略空格）。每个声明只声明一个变量有助于避免此类错误并提高程序的可读性。

### 良好的编程实践 8.1

> 虽然不是必需的，但在指针变量名中包含字母 `Ptr` 可以清楚地表明这些变量是指针，并且必须相应地处理它们。

指针应在声明时或在赋值时进行初始化。指针可以初始化为 `0`、`NULL` 或相应类型的地址。值为 `0` 或 `NULL` 的指针指向空，称为空指针。符号常量 `NULL` 在头文件 `<iostream>` 中定义（也在其他多个标准库头文件中定义）以表示值 `0`。将指针初始化为 `NULL` 等同于将指针初始化为 `0`，但在 C++ 中按惯例使用 `0`。当 `0` 被赋值时，它会被转换为适当类型的指针。`0` 是唯一可以直接赋给指针变量而不先将整数强制转换为指针类型的整数值。将变量的数字地址赋给指针将在第 8.3 节中讨论。

### 防错提示 8.1

> 初始化指针以防止指向内存中未知或未初始化的区域。

## 8.3 指针运算符

地址运算符 (`&`) 是一个一元运算符，用于获取其操作数的内存地址。例如，假设声明

```cpp
int y = 5; // declare variable y
int *yPtr; // declare pointer variable yPtr
```

语句

```cpp
yPtr = &y; // assign address of y to yPtr
```

将变量 `y` 的地址赋给指针变量 `yPtr`。然后变量 `yPtr` 就被称为“指向”`y`。现在，`yPtr` 间接引用变量 `y` 的值。请注意，前述语句中 `&` 的用法与引用变量声明中 `&` 的用法不同，后者始终位于数据类型名称之前。在声明引用时，`&` 是类型的一部分。在像 `&y` 这样的表达式中，`&` 是一个运算符。

图 8.2 显示了前述赋值后内存的示意表示。“指向关系”是通过从内存中表示指针 `yPtr` 的框画一条箭头到内存中表示变量 `y` 的框来指示的。

图 8.3 显示了指针在内存中的另一种表示，假设整数变量 `y` 存储在内存位置 `600000`，指针变量 `yPtr` 存储在内存位置 `500000`。地址运算符的操作数必须是左值（即可以赋值的东西，例如变量名或引用）；地址运算符不能应用于常量或不产生引用的表达式。

**图 8.2 | 指针指向内存中变量的图形表示。**

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_334_0.png)

**图 8.3 | 内存中 `y` 和 `yPtr` 的表示。**

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_334_1.png)

`*` 运算符通常称为间接运算符或解引用运算符，它返回其指针操作数所指向对象的同义词（即别名或昵称）。例如（再次参考图 8.2），语句

```cpp
cout << *yPtr << endl;
```

打印变量 `y` 的值，即 `5`，就像语句

```cpp
cout << y << endl;
```

一样。以这种方式使用 `*` 称为解引用指针。请注意，解引用的指针也可以用于赋值语句的左侧，如

```cpp
*yPtr = 9;
```

这将在图 8.3 中将 `9` 赋给 `y`。解引用的指针也可以用于接收输入值，如

```cpp
cin >> *yPtr;
```

这会将输入值放入 `y` 中。解引用的指针是一个左值。

### 常见编程错误 8.2

> 解引用未正确初始化或未被赋值为指向内存中特定位置的指针可能会导致致命的执行时错误，或者它可能会意外修改重要数据并允许程序完成运行，可能产生错误的结果。

### 常见编程错误 8.3

> 尝试解引用非指针的变量是编译错误。

### 常见编程错误 8.4

> 解引用空指针通常是致命的执行时错误。

图 8.4 中的程序演示了 `&` 和 `*` 指针运算符。在此示例中，内存位置由 `<<` 输出为十六进制（即基数-16）整数。请注意，此程序输出的十六进制内存地址取决于编译器和操作系统，因此您运行程序时可能会得到不同的结果。

### 可移植性提示 8.1

> 指针的输出格式取决于编译器。有些编译器将指针值输出为十六进制整数，有些使用十进制整数，有些使用其他格式。

请注意，`a` 的地址（第 15 行）和 `aPtr` 的值（第 16 行）在输出中是相同的，这证实了 `a` 的地址确实被赋给了指针变量 `aPtr`。`&` 和 `*` 运算符互为逆运算——当它们按任一顺序连续应用于 `aPtr` 时，它们会“相互抵消”，并且打印出相同的结果（`aPtr` 中的值）。

```cpp
// Fig. 8.4: fig08_04.cpp
// Pointer operators & and *.
#include <iostream>
using std::cout;
using std::endl;
int main()
{
    int a; // a is an integer
    int *aPtr; // aPtr is an int * -- pointer to an integer
    a = 7; // assign 7 to a
    aPtr = &a; // assign the address of a to aPtr
    cout << "The address of a is " << &a
         << "\nThe value of aPtr is " << aPtr;
    cout << "\n\nThe value of a is " << a
         << "\nThe value of *aPtr is " << *aPtr;
    cout << "\n\nShowing that * and & are inverses of "
         << "each other.\n&*aPtr = " << &*aPtr
         << "\n*&aPtr = " << *&aPtr << endl;
    return 0; // indicates successful termination
} // end main
```

```
The address of a is 0012F580
The value of aPtr is 0012F580

The value of a is 7
The value of *aPtr is 7

Showing that * and & are inverses of each other.
&*aPtr = 0012F580
*&aPtr = 0012F580
```

**图 8.4 | 指针运算符 & 和 \*。**

图 8.5 列出了到目前为止介绍的运算符的优先级和结合性。请注意，地址运算符 (`&`) 和解引用运算符 (`*`) 是图表中第三优先级级别的一元运算符。

| Operators | Associativity | Type |
|---|---|---|
| `()` `[]` | left to right | highest |
| `++` `--` `static_cast<type>( operand )` | left to right | unary (postfix) |
| `++` `--` `+` `-` `!` `&` `*` | right to left | unary (prefix) |
| `*` `/` `%` | left to right | multiplicative |
| `+` `-` | left to right | additive |

**图 8.5 | 运算符优先级和结合性。 （第 1 部分，共 2 部分。）**

**图 8.5 | 运算符优先级和结合性。（第 2 部分，共 2 部分。）**

| 运算符 | 结合性 | 类型 |
|---|---|---|
| << >> | 从左到右 | 插入/提取 |
| < <= > >= | 从左到右 | 关系 |
| == != | 从左到右 | 相等 |
| && | 从左到右 | 逻辑与 |
| \|\| | 从左到右 | 逻辑或 |
| ?: | 从右到左 | 条件 |
| = += -= *= /= %= | 从右到左 | 赋值 |
| , | 从左到右 | 逗号 |

## 8.4 使用指针按引用向函数传递参数

在 C++ 中，向函数传递参数有三种方式——按值传递、使用引用参数的按引用传递以及使用指针参数的按引用传递。第 6 章比较并对比了按值传递和使用引用参数的按引用传递。在本节中，我们将解释使用指针参数的按引用传递。

正如我们在第 6 章中所看到的，`return` 可用于从被调用函数向调用者返回一个值（或在不返回值的情況下从被调用函数返回控制权）。我们还看到，可以使用引用参数向函数传递参数。此类参数使被调用函数能够修改调用者中参数的原始值。引用参数还使程序能够向函数传递大型数据对象，并避免按值传递对象所带来的开销（当然，按值传递需要复制对象）。指针与引用类似，也可用于修改调用者中的一个或多个变量，或向函数传递指向大型数据对象的指针以避免按值传递对象的开销。

在 C++ 中，程序员可以使用指针和间接运算符 (`*`) 来实现按引用传递（与 C 程序中按引用传递的方式完全相同——C 没有引用）。调用应被修改参数的函数时，会传递该参数的地址。这通常是通过将地址运算符 (`&`) 应用于将被修改变量的名称来实现的。

正如我们在第 7 章中所看到的，数组不会使用运算符 `&` 传递，因为数组的名称是数组在内存中的起始位置（即，数组名称本身就是一个指针）。数组的名称 `arrayName` 等价于 `&arrayName[ 0 ]`。当变量的地址传递给函数时，可以在函数中使用间接运算符 (`*`) 形成变量名称的同义词——进而可用于修改调用者内存中该位置变量的值。

图 8.6 和图 8.7 展示了对整数进行立方运算的函数的两个版本——`cubeByValue` 和 `cubeByReference`。图 8.6 将变量 `number` 按值传递给函数 `cubeByValue`（第 15 行）。函数 `cubeByValue`（第 21–24 行）对参数进行立方运算并使用 `return` 语句（第 23 行）将新值传回 `main`。

```cpp
// Fig. 8.6: fig08_06.cpp
// Pass-by-value used to cube a variable's value.
#include <iostream>
using std::cout;
using std::endl;
int cubeByValue( int ); // prototype
int main()
{
    int number = 5;
    cout << "The original value of number is " << number;
    number = cubeByValue( number ); // pass number by value to cubeByValue
    cout << "\nThe new value of number is " << number << endl;
    return 0; // indicates successful termination
} // end main
// calculate and return cube of integer argument
int cubeByValue( int n )
{
    return n * n * n; // cube local variable n and return result
} // end function cubeByValue
```

```
The original value of number is 5
The new value of number is 125
```

**图 8.6 | 使用按值传递对变量的值进行立方运算。**

新值被赋给 `main` 中的 `number`（第 15 行）。请注意，调用函数有机会在修改变量 `number` 的值之前检查函数调用的结果。例如，在此程序中，我们可以将 `cubeByValue` 的结果存储在另一个变量中，检查其值，并在确定返回的值合理后才将其赋给 `number`。

图 8.7 使用指针参数的按引用传递将变量 `number` 传递给函数 `cubeByReference`（第 16 行）——`number` 的地址被传递给函数。函数 `cubeByReference`（第 23–26 行）指定参数 `nPtr`（指向 `int` 的指针）以接收其参数。函数对指针进行解引用并对 `nPtr` 所指向的值进行立方运算（第 25 行）。这直接改变了 `main` 中 `number` 的值。

### 常见编程错误 8.5

> 当需要通过指针获取指针所指向的值时，未对指针进行解引用是一个错误。

接收地址作为参数的函数必须定义指针参数以接收该地址。例如，函数 `cubeByReference` 的头（第 23 行）指定 `cubeByReference` 接收 `int` 变量的地址（即指向 `int` 的指针）作为参数，将地址本地存储在 `nPtr` 中且不返回值。

`cubeByReference` 的函数原型（第 8 行）包含括号中的 `int *`。与其他变量类型一样，在函数原型中不必包含指针参数的名称。为文档目的而包含的参数名称会被编译器忽略。

```cpp
// Fig. 8.7: fig08_07.cpp
// Pass-by-reference with a pointer argument used to cube a
// variable's value.
#include <iostream>
using std::cout;
using std::endl;
void cubeByReference( int * ); // prototype
int main()
{
    int number = 5;
    cout << "The original value of number is " << number;
    cubeByReference( &number ); // pass number address to cubeByReference
    cout << "\nThe new value of number is " << number << endl;
    return 0; // indicates successful termination
} // end main
// calculate cube of *nPtr; modifies variable number in main
void cubeByReference( int *nPtr )
{
    *nPtr = *nPtr * *nPtr * *nPtr; // cube *nPtr
} // end function cubeByReference
```

```
The original value of number is 5
The new value of number is 125
```

**图 8.7 | 使用指针参数的按引用传递对变量的值进行立方运算。**

图 8.8–8.9 分别图形化分析了图 8.6 和图 8.7 中程序的执行。

### 软件工程观察 8.1

> 除非调用者明确要求被调用函数直接修改调用者中参数变量的值，否则应使用按值传递向函数传递参数。这是最小权限原则的又一例证。

在期望一维数组作为参数的函数的函数头和原型中，可使用 `cubeByReference` 参数列表中的指针表示法。编译器无法区分接收指针的函数和接收一维数组的函数。当然，这意味着函数必须“知道”它接收的是数组还是仅一个通过引用传递的单个变量。当编译器遇到形如 `int b[]` 的一维数组函数参数时，编译器会将其转换为指针表示法 `int *b`（读作“`b` 是指向整数的指针”）。声明函数参数为一维数组的两种形式可以互换。

**步骤 1：在 `main` 调用 `cubeByValue` 之前：**

```cpp
int main()
{
    int number = 5;
    number = cubeByValue( number );
}
```

```cpp
int cubeByValue( int n )
{
    return n * n * n;
}
```

**步骤 2：`cubeByValue` 接收调用之后：**

```cpp
int main()
{
    int number = 5;
    number = cubeByValue( number );
}
```

```cpp
int cubeByValue( int n )
{
    return n * n * n;
}
```

**步骤 3：`cubeByValue` 对参数 `n` 进行立方运算后且在返回 `main` 之前：**

```cpp
int main()
{
    int number = 5;
    number = cubeByValue( number );
}
```

```cpp
int cubeByValue( int n )
{
```
