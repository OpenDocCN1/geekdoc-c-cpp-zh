
图 15.11 使用 GNU C++ 编译。与通常展示程序的执行输出不同，我们展示了 GNU C++ 在汇编语言中产生的名称修饰函数名。每个名称修饰的名称（main 除外）都以两个下划线（__）开头，后跟字母 Z、一个数字和函数名。Z 之后跟随的数字指定了函数名称中的字符数。例如，函数 square 的名称有 6 个字符，因此其名称修饰的名称以 __Z6 为前缀。

### 常见编程错误 15.9

*使用相同的参数列表但返回类型不同的重载函数是编译错误。*

```cpp
// Fig. 15.11: fig15_11.cpp
// Name mangling to enable type-safe linkage.

// function square for int values
int square( int x )
{
    return x * x;
}

// function square for double values
double square( double y )
{
    return y * y;
}

// function that receives arguments of types
// int, float, char and int &
void nothing1( int a, float b, char c, int &d )
{
    // empty function body
}

// function that receives arguments of types
// char, int, float & and double &
int nothing2( char a, int b, float &c, double &d )
{
    return 0;
}

int main()
{
    return 0; // indicates successful termination
}
```

```
__Z6squarei
__Z6squared
__Z8nothing1ifcRi
__Z8nothing2ciRfRd
_main
```

**图 15.11** | 名称修饰以实现类型安全链接。

函数名随后跟随其参数列表的编码。在函数 nothing2 的参数列表中（第 25 行；参见第四行输出），c 代表一个 char，i 代表一个 int，Rf 代表一个 float &（即对 float 的引用）而 Rd 代表一个 double &（即对 double 的引用）。在函数 nothing1 的参数列表中，i 代表一个 int，f 代表一个 float，c 代表一个 char 而 Ri 代表一个 int &。两个 square 函数通过其参数列表区分；一个指定 d 表示 double，另一个指定 i 表示 int。

函数的返回类型未在名称修饰的名称中指定。重载函数可以具有不同的返回类型，但如果有，则必须同时具有不同的参数列表。同样，你不能有两个具有相同签名但返回类型不同的函数。函数名修饰是编译器特定的。此外，函数 main 未被修饰，因为它不能被重载。

编译器仅使用参数列表来区分同名函数。重载函数不必具有相同数量的参数。程序员在重载带有默认参数的函数时应谨慎，因为这可能导致歧义。

### 常见编程错误 15.10

![](img/bf54db922e6fa8319cba11069e785521_596_0.png)

> 省略默认参数的函数可能与另一个重载函数被以相同方式调用；这是编译错误。例如，在程序中同时存在一个显式不接受参数的函数和一个同名且所有参数都有默认值的函数，在尝试不带参数调用该函数时会产生编译错误。编译器不知道应选择哪个版本的函数。

## 重载运算符

在第 18 章中，我们讨论如何重载运算符以定义它们应如何作用于用户定义数据类型对象的操作。（事实上，我们一直在使用重载运算符，包括流插入运算符 << 和流提取运算符 >>，每个运算符都被重载以能够显示所有基本类型的数据。我们在第 18 章中更详细地说明了如何重载 << 和 >> 以处理用户定义类型对象。）第 15.13 节介绍了函数模板，用于自动生成对不同类型数据执行相同任务的重载函数。

## 15.13 函数模板

重载函数通常用于执行可能涉及对不同数据类型不同程序逻辑的相似操作。如果对每种数据类型程序逻辑和操作都相同，则可以使用函数模板更紧凑、更方便地执行重载。你编写单个函数模板定义。给定对该函数的调用中提供的参数类型，C++ 会自动生成单独的函数模板特化以适当处理每种类型的调用。因此，定义单个函数模板本质上定义了一整个重载函数族。

### 15.13.1 定义函数模板

图 15.12 包含了一个函数模板的定义（第 4–18 行），用于确定三个值的最大值。所有函数模板定义都以 template 关键字（第 4 行）开头，后跟用尖括号（< 和 >）括起的函数模板的模板参数列表。模板参数列表中的每个参数（每个称为形式类型参数）前面都有关键字 typename 或关键字 class（它们是同义词）。形式类型参数是基本类型或用户定义类型的占位符。这些占位符用于指定函数的参数类型（第 5 行）、指定函数的返回类型以及在函数定义体中声明变量（第 7 行）。函数模板像其他函数一样定义，但使用形式类型参数作为实际数据类型的占位符。

```cpp
// Fig. 15.12: maximum.h
// Function template maximum header file.

template < class T >  // or template< typename T >
T maximum( T value1, T value2, T value3 )
{
    T maximumValue = value1; // assume value1 is maximum

    // determine whether value2 is greater than maximumValue
    if ( value2 > maximumValue )
        maximumValue = value2;

    // determine whether value3 is greater than maximumValue
    if ( value3 > maximumValue )
        maximumValue = value3;

    return maximumValue;
}
```

图 15.12 | 函数模板 maximum 头文件。

图 15.12 中的函数模板声明了一个单一的形式类型参数 T（第 4 行），作为函数 maximum 所测试数据的类型的占位符。类型参数的名称必须在特定模板定义的模板参数列表中唯一。当编译器在程序源代码中检测到 maximum 调用时，将把传递给 maximum 的数据的类型替换为模板定义中所有的 T，并创建用于确定指定数据类型三个值的最大值的完整源代码函数。然后编译新创建的函数。因此，模板是为一系列相似函数生成代码的手段。

> **常见编程错误 15.11**
> 未在函数模板的每个形式类型参数前放置关键字 class 或关键字 typename（例如，写成 <class S, T> 而不是 <class S, class T>）是语法错误。

### 15.13.2 使用函数模板

图 15.13 使用 maximum 函数模板（第 18、28 和 38 行）来确定三个 int 值、三个 double 值和三个 char 值的最大值。

```cpp
// Fig. 15.13: fig15_13.cpp
// Demonstrating function template maximum.
#include <iostream>
using namespace std;

#include "maximum.h" // include definition of function template maximum

int main()
{
    // demonstrate maximum with int values
    int int1, int2, int3;

    cout << "Input three integer values: ";
    cin >> int1 >> int2 >> int3;

    // invoke int version of maximum
    cout << "The maximum integer value is: "
         << maximum( int1, int2, int3 );

    // demonstrate maximum with double values
    double double1, double2, double3;

    cout << "\n\nInput three double values: ";
    cin >> double1 >> double2 >> double3;

    // invoke double version of maximum
    cout << "The maximum double value is: "
         << maximum( double1, double2, double3 );

    // demonstrate maximum with char values
    char char1, char2, char3;

    cout << "\n\nInput three characters: ";
    cin >> char1 >> char2 >> char3;

    // invoke char version of maximum
    cout << "The maximum character value is: "
         << maximum( char1, char2, char3 ) << endl;
}
```

输入三个整数值：1 2 3
最大整数值是：3

输入三个双精度值：3.3 2.2 1.1
最大双精度值是：3.3

输入三个字符：A C B
最大字符值是：C

图 15.13 | 演示函数模板 maximum。

在图 15.13 中，由于第 18、28 和 38 行的调用创建了三个函数——分别期望三个 int 值、三个 double 值和三个 char 值。

