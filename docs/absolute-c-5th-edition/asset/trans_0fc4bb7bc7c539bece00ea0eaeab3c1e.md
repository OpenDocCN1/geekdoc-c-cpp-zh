

## 第3章 函数基础

如果在某个程序中执行上述语句，它将在屏幕上显示以下内容：

32.5 华氏度等于
0.3 摄氏度。

注意函数调用以分号结束，这告诉编译器该函数调用是一个可执行的语句。

当调用 `void` 函数时，参数将替换为形式参数，并执行函数体中的语句。例如，调用我们在本章稍些时候过的 `void` 函数 `showResults` 将导致输出被写入屏幕。调用 `void` 函数的一种方式是，想象函数定义的体被复制到函数调用的位置。当函数被调用时，参数将替换形式参数，然后就好像程序中的这些行代码被执行了一样（第 4 章将详细描述了用参数替换形式参数的过程）。在此之前，我们将只使用简单的示例，这些示例在没有对替换过程进行正式描述的情况下也应该是足够清晰的。

## 函数声明（函数原型）

函数声明（函数原型）告诉了你编写对该函数的调用时所需要的所有信息。函数声明（或完整的函数定义）必须出现在程序中调用该函数之前的主部分。

> 不要忘记
> 这个分号。

## 语法

```
返回类型_或_void 函数名 (参数列表);
```

其中 `参数列表` 是一个用逗号分隔的参数列表：

```
类型_1 形式参数_1, 类型_2 形式参数_2,...
类型_3 形式参数_最后一个
```

## 示例

```cpp
double totalWeight(int number, double weightToOne);
// 返回 number 个物品的总重量，
// 每个物品重量为 one。
```

```cpp
void showResults(double fDegrees, double cDegrees);
// 显示消息，说明 fDegrees 华氏度
// 等于 cDegrees 摄氏度。
```

拥有没有参数的函数是完全合法的，有时也是有用的。在这种情况下，函数声明中没有列出形式参数，在调用函数时也不使用任何参数。例如，没有参数的 `void` 函数：

## 程序员自定义函数

`initializeScreen` 在下文定义，它只是向屏幕发送一个换行命令：

```cpp
void initializeScreen() {
  cout << endl;
}
```

如果你的程序将该函数的调用作为它的第一个可执行语句，那么之前运行的程序的输出将与你的程序的输出隔离开：

initializeScreen();

请注意，即使函数没有参数，你也必须在函数声明和函数调用中包含括号。

函数声明（函数原型）和函数定义的位置，对于 `void` 函数来说与我们描述的返回值的函数的函数是一样的。

## void 函数中的 return 语句

`void` 函数和返回值的函数都可以包含 `return` 语句。在返回值的函数中，`return` 语句指定了要返回的值。在 `void` 函数中，`return` 语句不包含任何返回值的表达式。`void` 函数中的 `return` 语句只是结束调用。每个返回值的函数都必须通过执行 `return` 语句来结束。然而，`void` 函数不需要包含 `return` 语句。如果它不包含 `return` 语句，将在执行完函数体中的代码后结束。这就像在函数体末尾的大括号 `}` 之前有一个隐式的 `return` 语句一样。

## 前条件和后置条件

编写函数声明的一种良好方法将其分解为两类信息，称为前条件（precondition）和后置条件（postcondition）。前条件说明了调用函数时应该满足什么条件。除非满足前条件，否则不应使用该函数也无法正确执行。后置条件描述了函数调用的效果；即，后置条件告诉了在前条件成立的情况下，执行函数后什么将是真实的。对于返回值的函数，后置条件将描述函数返回的值。对于改变某些参数变量值的函数，后置条件将描述对参数进行的所有更改。

## 122 页 第3章 函数基础

### 示例 3.7 在 void 函数中使用 return

```cpp
#include <iostream>
using namespace std;

void iceCreamDivision(int number, double totalWeight);
// 输出关于在客户之间分配 totalWeight 盎司冰淇淋的
// 指令。如果 number 为 0，则输出错误
// 消息。

int main() {
    int number;
    double totalWeight;

    cout << "输入客户人数: ";
    cin >> number;
    cout << "输入要分配的冰淇淋重量（盎司）: ";
    cin >> totalWeight;

    iceCreamDivision(number, totalWeight);
    return 0;
}

void iceCreamDivision(int number, double totalWeight) {
    double portion;
    if (number == 0) {
        cout << "无法在零客户之间分配。\n";
        return;
    }
    portion = totalWeight/number;
    cout << "每人获得 ";
    cout << portion << " 盎司冰淇淋。" << endl;
}
``` 

| 输入客户人数: 0 |
| :--- |
| 输入要分配的冰淇淋重量（盎司）: 12 |
| 无法在零客户之间分配。 |

