

```cpp
// function square for double values
double square( double y )
{
   cout << "square of double " << y << " is ";
   return y * y;
} // end function square with double argument

int main()
{
   cout << square( 7 ); // calls int version
   cout << endl;
   cout << square( 7.5 ); // calls double version
   cout << endl;
} // end main
```

```text
square of integer 7 is 49
square of double 7.5 is 56.25
```

**图 6.23** | 重载的 square 函数（第 2 部分，共 2 部分）。

## 编译器如何区分重载函数

重载函数通过其签名（signature）来区分。签名是函数名称及其参数类型（按顺序）的组合。编译器将每个函数标识符与其参数类型编码（有时称为**名称修饰**或**名称装饰**）以实现**类型安全链接**。类型安全链接确保调用正确的重载函数，并且实参类型与形参类型一致。

图 6.24 是用 GNU C++ 编译的。我们没有像通常那样显示程序的执行输出，而是显示由 GNU C++ 在汇编语言中生成的修饰后的函数名。每个修饰名（main 除外）都以两个下划线（`__`）开头，后跟字母 Z、一个数字和函数名。Z 后面的数字指定函数名中有多少个字符。例如，函数 square 的名称中有 6 个字符，因此其修饰名前缀为 `__Z6`。函数名后面是其参数列表的编码。在函数 nothing2（第 25 行；见第四行输出）的参数列表中，`c` 表示 char，`i` 表示 int，`Rf` 表示 float &（即对 float 的引用），`Rd` 表示 double &（即对 double 的引用）。在函数 nothing1 的参数列表中，`i` 表示 int，`f` 表示 float，`c` 表示 char，`Ri` 表示 int &。两个 square 函数通过其参数列表区分；一个指定 `d` 表示 double，另一个指定 `i` 表示 int。修饰名中不包含函数的返回类型。重载函数可以有不同的返回类型，但如果返回类型不同，则必须具有不同的参数列表。同样，不能有两个具有相同签名但返回类型不同的函数。函数名修饰是编译器特定的。此外，函数 main 不进行修饰，因为它不能被重载。

![](img/b42ba5cd262b1358d16610173f975e4d_279_0.png)

> **常见编程错误 6.10**
> 
> 创建具有相同参数列表但返回类型不同的重载函数是编译错误。

```cpp
// Fig. 6.24: fig06_24.cpp
// Name mangling to enable type-safe linkage.

// function square for int values
int square( int x )
{
    return x * x;
} // end function square

// function square for double values
double square( double y )
{
    return y * y;
} // end function square

// function that receives arguments of types
// int, float, char and int &
void nothing1( int a, float b, char c, int &d )
{
    // empty function body
} // end function nothing1

// function that receives arguments of types
// char, int, float & and double &
int nothing2( char a, int b, float &c, double &d )
{
    return 0;
} // end function nothing2

int main()
{
} // end of main
```

```text
__Z6squarei
__Z6squared
__Z8nothing1ifcRi
__Z8nothing2ciRfRd
main
```

**图 6.24** | 名称修饰实现类型安全链接。

编译器仅使用参数列表来区分重载函数。此类函数*不必*具有相同数量的参数。重载带有默认参数的函数时要小心，因为这可能导致歧义。

![](img/b42ba5cd262b1358d16610173f975e4d_280_0.png)

> **常见编程错误 6.11**
> 
> 省略默认实参的函数可能与另一个重载函数的调用方式相同；这是一个编译错误。例如，如果程序中既有一个显式不接受参数的函数，又有一个同名但包含全部默认实参的函数，那么当尝试在调用中使用该函数名而不传递任何实参时，会导致编译错误。编译器无法确定应选择哪个版本的函数。

参数在特定模板定义的模板参数列表中必须是唯一的。当编译器在程序源代码中检测到 maximum 调用时，传递给 maximum 的数据的*类型*将在整个模板定义中替换 T，C++ 会创建一个完整的函数来确定指定数据类型的三个值中的最大值——由于此示例中只使用了一个类型参数，所以这三个值必须具有相同的类型。然后编译新创建的函数——模板是*代码生成*的一种手段。

图 6.26 使用 maximum 函数模板分别确定三个 int 值、三个 double 值和三个 char 值中的最大值（第 17、27 和 37 行）。由于第 17、27 和 37 行中的调用，分别创建了期望三个 int 值、三个 double 值和三个 char 值的独立函数。

```cpp
// Fig. 6.26: fig06_26.cpp
// Function template maximum test program.
#include <iostream>
#include "maximum.h" // include definition of function template maximum
using namespace std;

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
} // end main
```

**图 6.26** | 函数模板 maximum 测试程序（第 1 部分，共 2 部分）。

```text
Input three integer values: 1 2 3
The maximum integer value is: 3

Input three double values: 3.3 2.2 1.1
The maximum double value is: 3.3

Input three characters: A C B
The maximum character value is: C
```

**图 6.26** | 函数模板 maximum 测试程序（第 2 部分，共 2 部分）。

为类型 int 创建的函数模板特化会将每个 T 替换为 int，如下所示：

```cpp
int maximum( int value1, int value2, int value3 )
{
   int maximumValue = value1;  // assume value1 is maximum

   // determine whether value2 is greater than maximumValue
   if ( value2 > maximumValue )
      maximumValue = value2;

   // determine whether value3 is greater than maximumValue
   if ( value3 > maximumValue )
      maximumValue = value3;

   return maximumValue;
}  // end function template maximum
```

## C++11——函数的尾置返回类型

C++11 引入了函数的**尾置返回类型**。要指定尾置返回类型，请将关键字 auto 放在函数名之前，然后在函数的参数列表后跟 -> 和返回类型。例如，为函数模板 maximum（图 6.25）指定尾置返回类型时，可以这样写：

```cpp
template < typename T >
auto maximum( T x, T y, T z ) -> T
```

在构建更复杂的函数模板时，有些情况只允许使用尾置返回类型。这类复杂的函数模板超出了本书的范围。

## 6.20 递归

对于某些问题，让函数*调用自身*是很有用的。*递归函数*是直接或间接（通过另一个函数）调用自身的函数。[*注：* C++ 标准文档指出，不应在程序内或递归地调用 main。其唯一用途是作为程序执行的起点。] 本节和下一节将介绍简单的递归示例。递归在高年级计算机科学课程中有详细讨论。图 6.32（在 6.22 节末尾）总结了书中大量的递归示例和练习。

### 递归概念

我们首先从概念上考虑递归，然后研究包含递归函数的程序。递归解决问题的方法有许多共同要素。

