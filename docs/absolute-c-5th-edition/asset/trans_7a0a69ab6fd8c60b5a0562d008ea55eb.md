

# 828 第 18 章 异常处理

显示 18.1 在不使用异常处理的情况下处理特殊情况

```cpp
#include <iostream>
using std::cin;
using std::cout;

int main() {
    int donuts, milk;
    double dpg;
    cout << "Enter number of donuts:\n";
    cin >> donuts;
    cout << "Enter number of glasses of milk:\n";
    cin >> milk;

    if (milk <= 0) {
        cout << donuts << " donuts, and No Milk!\n";
        cout << "Go buy some milk.\n";
    } else {
        dpg = donuts / static_cast<double>(milk);
        cout << donuts << " donuts.\n";
        cout << milk << " glasses of milk.\n";
        cout << "You have " << dpg << " donuts for each glass of milk.\n";
    }
    return 0;
}
```

示例对话

| 输入甜圈数量: 12 |
| 输入牛奶杯数: 0 |
| 12 个甜圈，没有牛奶！ |
| 去买些牛奶吧。 |
| 程序结束。 |

# 异常处理基础

## 18.2 使用异常处理实现相同的功能（2 部分中的第 1 部分）

```cpp
#include <iostream>
using std::cin;
using std::cout;

int main ( ) {
    int donuts, milk;
    double dpg;

    try {
        cout << "Enter number of donuts:\n";
        cin >> donuts;
        cout << "Enter number of milk:\n";
        cin >> milk;

        if (milk <= 0) {
            throw donuts;
        }

        dpg = donuts / static_cast<double>(milk);
        cout << " donuts.\n";
        cout << "You have " << dpg << " donuts for each glass of milk.\n";
    } catch (int e) {
        cout << e << " donuts, and No Milk!\n";
        cout << "Go buy some milk.\n";
    }

    cout << "End of program.\n";
    return 0;
}
```

> 这只是一个学习 C++ 语法的简单示例。请不要将其作为异常处理的典型良好用法示例。

（续）

# 830 第 18 章 异常处理

显示 18.2 使用异常处理实现相同的功能（2 部分中的第 2 部分）

示例对话 1

| 输入甜圈数量: 12 |
| 输入牛奶杯数: 6 |
| 12 个甜圈。 |
| 6 杯牛奶。 |
| 每杯牛奶配有 2 个甜圈。 |
| 程序结束。 |

示例对话 2

| 输入甜圈数量: 12 |
| 输入牛奶杯数: 0 |
| 12 个甜圈，没有牛奶！ |
| 去买些牛奶吧。 |
| 程序结束。 |

与其巨大的 `if-else` 语句（在显示 18.1 中突出显示），这个新程序有了以下较小的 `if` 语句（加上一些简单的非分支语句）：

```cpp
if (milk <= 0)
    throw donuts;
```

该语句的意思是，如果没有牛奶，则执行异常操作。异常操作位于 `catch` 关键字之后。其核心思想是：正常情况由 `try` 之后的代码处理，而异常情况由 `catch` 之后的代码处理。因此，我们将普通情况与异常情况分离开来。这个示例并没有让我们受益太多，但在其他情况下，它将被证明是非常有用的。让我们来看细节。

C++ 中处理异常的基本方法由 `try-throw-catch` 三位一体结构组成。`try` 块具有以下语法：

```cpp
try
{
    Some_Code
}
```

这个 `try` 块包含了基本算法代码，告诉程序在一切顺利进行时应该做什么。它之所以被称为 `try` 块，是因为你并不 100% 确定一切都会万无一地进行，但你想“尝试一下”。

# 异常处理基础

如果确实发生了异常情况，指示这种情况的方法是抛出（throw）一个异常。因此，当我们添加 `throw` 时，基本轮廓如下：

```cpp
try {
  Code_To_Try
  Possibly_Throw_An_Exception
  More_Code
}
```

以下是一个包含 `throw` 语句的 `try` 块示例（拷贝自显示 18.2）：

```cpp
try {
  cout << "Enter number of donuts:\n";
  cin >> donuts;
  cout << "Enter number of glasses of milk:\n";
  cin >> milk;
  if (milk <= 0)
    throw donuts;
}

dpg = donuts / static_cast<double>(milk);
cout << donuts << " \n";
cout << milk << " glasses of milk.\n";
cout << "You have " << dpg << " \n";
cout << donuts << " for each glass of milk.\n";
```

以下语句抛出了 `int` 类型的值 `donuts`：
`throw donuts;`

抛出的值（在本例中为 `donuts`）被称为**异常**；它的执行被称为**抛出异常**。你可以抛出任何类型的值。在这种情况下，抛出一个 `int` 类型的值。

### throw 语句

`throw Expression_for_Value_to_Be_Thrown;`

当执行 `throw` 语句时，`try` 块的执行就会停止。如果 `try` 块后面紧跟着一个合适的 `catch` 块，则会进行处理。

