
## 定义内联函数

图 15.3 使用内联函数 cube（第 11～14 行）计算边长为 side 的立方体体积。函数 cube 参数列表中的关键字 const 告诉编译器，该函数不会修改变量 side。这确保在执行计算时，side 的值不会被该函数改变。注意，函数 cube 的完整定义出现在程序中使用它之前。这是必需的，以便编译器知道如何将 cube 函数调用展开为其内联代码。因此，可复用的内联函数通常放在头文件中，这样使用它们的每个源文件都可以包含其定义。

![](img/d0d3b7423c2d9e5650be79209ea1885d_589_0.png)

### 软件工程观察 15.5

> 应使用 const 限定符来贯彻最小权限原则。利用最小权限原则正确设计软件，可以大幅减少调试时间和不当副作用，并使程序更易于修改和维护。

第 4～6 行是 using 声明，帮助我们消除重复 std:: 前缀的需要。一旦包含这些 using 声明，在程序余下部分就可以写 cout 而不是 std::cout、写 cin 而不是 std::cin、写 endl 而不是 std::endl。从此以后，每个 C++ 示例都包含一个或多个 using 声明。

```cpp
// Fig. 15.3: fig15_03.cpp
// inline function that calculates the volume of a cube.
#include <iostream>
using std::cout;
using std::cin;
using std::endl;

// Definition of inline function cube. Definition of function appears
// before function is called, so a function prototype is not required.
// First line of function definition acts as the prototype.
inline double cube( const double side )
{
return side * side * side; // calculate the cube of side
}

int main()
{
double sideValue; // stores value entered by user

for ( int i = 1; i <= 3; i++ )
{
cout << "\nEnter the side length of your cube: ";
cin >> sideValue; // read value from user

// calculate cube of sideValue and display result
cout << "Volume of cube with side "
<< sideValue << " is " << cube( sideValue ) << endl;
}
}
```

```text
Enter the side length of your cube: 1.0
Volume of cube with side 1 is 1

Enter the side length of your cube: 2.3
Volume of cube with side 2.3 is 12.167

Enter the side length of your cube: 5.4
Volume of cube with side 5.4 is 157.464
```

**图 15.3** | 计算立方体体积的 `inline` 函数。（第 2 部分，共 2 部分。）

许多程序员更喜欢用以下声明代替第 4～6 行：

```cpp
using namespace std;
```

它使程序能够使用程序可能包含的任何标准 C++ 头文件（例如 `<iostream>`）中的所有名称。在本章接下来的内容中，我们将在程序中使用前面的声明。

for 语句的条件（第 20 行）求值为 0（false）或非零（true）。这与 C 一致。C++ 还提供 bool 类型来表示布尔（true/false）值。bool 的两个可能值是关键字 true 和 false。当 true 和 false 转换为整数时，它们分别成为值 1 和 0。当非布尔值转换为 bool 类型时，非零值变为 true，零或空指针值变为 false。

## 15.7 C++ 关键字

图 15.4 列出了 C 和 C++ 共有的关键字、C++ 独有的关键字，以及 C++11 标准中添加到 C++ 的关键字。

| C++ 关键字 |  |  |  |  |
|---|---|---|---|---|
| *C 和 C++ 编程语言共有的关键字* |  |  |  |  |
| auto | break | case | char | const |
| continue | default | do | double | else |
| enum | extern | float | for | goto |
| if | int | long | register | return |
| short | signed | sizeof | static | struct |
| switch | typedef | union | unsigned | void |
| volatile | while |  |  |  |
| *C++ 独有的关键字* |  |  |  |  |
| and | and_eq | asm | bitand | bitor |
| bool | catch | class | compl | const_cast |
| delete | dynamic_cast | explicit | export | false |

**图 15.4** | C++ 关键字。（第 1 部分，共 2 部分。）

引用参数是函数调用中对应实参的别名。要表明函数参数按引用传递，只需在函数原型和函数定义中参数类型后面加上与号（&）。例如，以下参数声明

```cpp
int &count
```

从右向左读作“count 是对 int 的引用”。在函数调用中，只需按名称提及变量即可按引用传递它。然后，在被调用函数体内用参数名提及该变量，实际上指的就是调用函数中的原始变量，并且被调用函数可以直接修改原始变量。

### 15.8.2 按值传递实参和按引用传递实参

图 15.5 比较了按值传递与使用引用参数的按引用传递。在调用函数 squareByValue（第 15 行）和函数 squareByReference（第 21 行）时，实参的“样式”完全相同——两个变量在函数调用中都只是按名称提及。如果不检查函数原型或函数定义，仅从调用本身无法判断其中任一函数是否能修改其实参。然而，由于函数原型是必需的，编译器可以轻松解决这一歧义。回顾一下，函数原型告诉编译器函数返回的数据类型、函数期望接收的参数个数、参数类型以及参数的期望顺序。编译器使用这些信息来验证函数调用。在 C 中，函数原型不是必需的。在 C++ 中强制要求函数原型可实现类型安全链接，从而确保实参的类型与形参的类型一致。否则，编译器会报告错误。在编译时定位此类错误，有助于防止在 C 中向函数传递错误数据类型的实参时可能发生的运行时错误。

```cpp
// Fig. 15.5: fig15_05.cpp
// Comparing pass-by-value and pass-by-reference with references.
#include <iostream>
using namespace std;

int squareByValue( int ); // function prototype (value pass)
void squareByReference( int & ); // function prototype (reference pass)

int main()
{
   // demonstrate squareByValue
   int x = 2;
   cout << "x = " << x << " before squareByValue\n";
   cout << "Value returned by squareByValue: "
        << squareByValue( x ) << endl;
   cout << "x = " << x << " after squareByValue\n" << endl;

   // demonstrate squareByReference
   int z = 4;
   cout << " z = " << z << " before squareByReference" << endl;
   squareByReference( z );
   cout << " z = " << z << " after squareByReference" << endl;
}

// squareByValue multiplies number by itself, stores the
// result in number and returns the new value of number
int squareByValue( int number )
{
   return number *= number; // caller's argument not modified
}

// squareByReference multiplies numberRef by itself and stores the result
// in the variable to which numberRef refers in the caller
void squareByReference( int &numberRef )
{
   numberRef *= numberRef; // caller's argument modified
}
```

**图 15.5** | 使用引用比较按值传递和按引用传递。（第 1 部分，共 2 部分。）

```text
x = 2 before squareByValue
Value returned by squareByValue: 4
x = 2 after squareByValue

z = 4 before squareByReference
z = 16 after squareByReference
```

**图 15.5** | 使用引用比较按值传递和按引用传递。（第 2 部分，共 2 部分。）

![](img/d0d3b7423c2d9e5650be79209ea1885d_593_0.png)

### 常见编程错误 15.2

由于引用参数在被调用函数体中仅按名称提及，你可能会不经意地把引用参数当作按值传递参数。如果函数改变了变量的原始副本，这可能会导致意外的副作用。

![](img/d0d3b7423c2d9e5650be79209ea1885d_593_1.png)

### 性能提示 15.5

为了高效传递大型对象，可使用常量引用参数来模拟按值传递的外观和安全性，并避免传递大型对象副本的开销。被调用函数将无法修改调用函数中的对象。

![](img/d0d3b7423c2d9e5650be79209ea1885d_593_2.png)

### 软件工程观察 15.7

许多程序员不把按值传递的参数声明为 const，即使被调用函数不应修改传入的实参。在此上下文中，关键字 const 只会保护原始实参的副本，而不会保护原始实参本身；按值传递时，原始实参不会被被调用函数修改。

要指定对常量的引用，请在参数声明中把 const 限定符放在类型说明符之前。注意图 15.5 第 34 行中，& 在函数 squareByReference 参数列表中的位置。一些 C++ 程序员更喜欢写成
