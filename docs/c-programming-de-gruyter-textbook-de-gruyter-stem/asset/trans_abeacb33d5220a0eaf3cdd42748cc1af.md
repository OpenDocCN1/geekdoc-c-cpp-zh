

## 102 — 3 函数

```cpp
int main()
{ add();
}
int add(int x,int y)
{ return x+y;
}
```

在同一作用域内，形式参数默认值的声明应该保持一致；但在不同的作用域内，形式参数默认值的声明可以不同。这里的作用域指的是由体现函数原型的大括号包围的区域。关于作用域的更多细节将在第 5 章中讨论。例如：

```cpp
int add(int x=1,int y=2);
int main()
{ add(int x=3, y=4);
add(); //使用局部默认参数（计算 3+4）
}
void fun(void)
{
add(); //使用全局默认参数（计算 1+2）
}
```

**示例 3.15：** 使用默认参数的函数示例。
程序的功能是计算长方体的体积。子函数 `get_volume` 用于计算体积，它有三个参数：长度、宽度和高度。参数 `width` 和 `height` 有默认值。`main` 函数使用不同的参数调用 `get_volume`。分析程序的运行结果。

```cpp
//3_15.cpp
#include <iostream>
#include <iomanip>
using namespace std;
get_volume(int length, int width = 2, int height = 3);
int main()
{
int x = 10, y = 12, z = 15;
cout << "Some box data is ";
cout << get_volume(x, y, z) << endl;
cout << "Some box data is ";
cout << get_volume(x, y) << endl;
```

## 3.3 函数中的默认形式参数

```cpp
cout << "Some box data is ";cout << get_volume(x) << endl;
cout << "Some box data is ";cout << get_volume(x, 7) << endl;
cout << "Some box data is ";cout << get_volume(5, 5, 5) << endl;
```

```cpp
int get_volume(int length, int width, int height) {
    cout<<setw(5)<<length<<setw(width)<<setw(5)<<height<<' ';
    return length * width * height;
}
```

运行结果：

| Some box data is 10 12 15 1800 |
| Some box data is 10 12 3 360 |
| Some box data is 10 2 3 60 |
| Some box data is 10 7 210 |
| Some box data is 5 5 5 125 |

由于函数 `get_volume` 的第一个参数没有默认值，因此对 `get_volume` 的每次调用必须提供第一个实际参数来初始化形式参数 `length`。参数 `width` 和 `height` 有默认值。因此，三个形式参数都将由实际参数初始化；如果函数调用两个实际参数，最后一个形式参数 `height` 将使用默认值；如果函数调用只提供一个实际参数，最后两个形式参数 `width` 和 `height` 将使用默认值。

在对具有默认值的函数进行重载时，我们应该避免歧义。例如，以下两个原型会导致歧义，使得编译器无法将它们识别为不同的重载形式：

```cpp
void fun(int length, int width = 2, int height = 3);
void fun(int length);
```

换句话说，当以以下形式调用函数 `fun` 时，编译器无法决定应该执行哪一个重载函数：

```cpp
fun(1);
```

编译器会将此视为编译错误。

## 3.4 函数重载

在程序中，函数名本质上是操作的名称。通过借助类似于自然语言的名称，我们可以编写易于理解和修改的程序。这里出现了一个问题：如何用编程语言反映自然语言中的细微差别？通常，自然语言在不同的语文中有不同的含义。这被称为多义性，在编程语言中被称为“重载”。例如：在自然语言中，“play the piano”、“play chess”和“play basketball”都使用动词“play”，但“play”在这三个语境下所指示的动作是完全不同的。我们可以理解这些短语，因为我们已经学习了在生活中如何对待不同的对象。所以，没有人会说“像下象棋一样弹钢琴，或者像打篮球一样下象棋”。计算机是否也可能具有这种能力？这取决于我们编写程序。C++ 提供了函数重载的支持，使我们能够赋予不同函数相同的名称。编译器将根据语境（参数的数量和类型）选择合适的函数来执行。

函数重载意味着两个或多个函数共享相同的名称，尽管它们的形式参数数量或类型存在差异。编译器将根据形式参数的数量和类型，自动选择符合调用语境的函数。

如果没有重载，针对不同数据类型的相同操作，我们需要定义多个不同名称的函数。例如，在定义相加函数时，我们需要为整数相加和浮点数相加定义不同的函数名：

```cpp
int add(int x, int y);
float ladd(float x, float y);
```

C++ 允许在相同作用域内对相似的功能使用相同的名称，这允许重载，这非常便于使用和记忆。例如：

- 1. add(int x, int y);
- 2. ladd(float x, float y);

- 3. fun(int length, int width = 2, int height = 3);
- 4. fun(int length)

换句话说，当以以下形式调用函数 `fun` 时，编译器无法决定应该执行哪一个重载函数：

```cpp
fun(1);
```

编译器会将此视为编译错误。注意：在对具有默认值的函数进行重载时，我们应该避免歧义。例如，以下两个原型会导致歧义，使得编译器无法将它们识别为不同的重载形式：（如上）。由于函数 `get_volume` 的第一个参数没有默认值，因此对 `get_volume` 的每次调用必须提供第一个实际参数来初始化形式参数 `length`。参数 `width` 和 `height` 有默认值。因此，三个形式参数都将由实际参数初始化；如果函数调用两个实际参数，最后一个形式参数 `height` 将使用默认值；如果函数调用只提供一个实际参数，最后两个形式参数 `width` 和 `height` 将使用默认值。

## 3.5 使用系统函数

C++ 不仅允许我们自己设计函数，还提供了许多函数供我们使用。我们知道在调用函数之前必须声明函数。系统函数的原型已由 C++ 库提供，并存储在几个头文件中。程序员只需要使用 `include` 指令将头文件包含到代码中，就可以使用系统函数。例如，如果你想使用数学函数，应该使用头文件 `cmath`。

**示例 3.7：** 使用系统函数的示例。

从键盘输入一个角度，并计算它的正弦、余弦和正切值。分析：C++ 库提供了计算角度正弦、余弦和正角的函数：`sin()`、`cos()` 和 `tan()`，这些函数的原型包含在头文件 `cmath` 中。

源代码：

```cpp
//3_18.cpp
#include<iostream>
#include<cmath>
using namespace std;
const double pi(3.14159265);
int main()
{
    double a,b;
    cin>>a;
    b=a*pi/180;
    cout<<"sin(\<<a<<")="<<sin(b)<<endl;
    cout<<"cos(\<<a<<")="<<cos(b)<<endl;
    cout<<"tan(\<<a<<")="<<tan(b)<<endl;
}
```

