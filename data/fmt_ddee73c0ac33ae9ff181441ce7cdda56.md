
这种分治法将创建具有相当规模的运行程序的复杂性降低到了凡人可以完成的程度。

## 编写和使用函数

通过示例是理解函数的最好方式。本节从`FunctionDemo`示例开始，它通过定义一个函数来包含部分逻辑，简化了我在第 5 章讨论的`NestedDemo`程序。本节将解释函数是如何定义的以及如何被调用的，并以`FunctionDemo`为模式来同时理解问题和解决方案。

第 5 章中的`NestedDemo`程序包含至少三个部分，这些部分在脑中和现实中都可以很容易分离：

- 对操作员说明如何输入数据
- 累加单个数字序列的内循环
- 重复调用内循环的外层循环，直到累加值为 0

沿着这些界限分离程序允许程序员专注于处理程序的每一个部分。接下来的`FunctionDemo`程序展示了如何通过创建`displayExplanation()`和`sumSequence()`函数来拆分`NestedDemo`：

```cpp
// FunctionDemo - 展示函数的用法
// 通过将 NestedDemo 程序的
// 内循环拆分为它自己的
// 函数来实现

#include <cstdio>
#include <cstdlib>
#include <iostream>
using namespace std;

// displayExplanation - 提示用户
// 游戏的数字
void displayExplanation(void)
{
    cout << "此程序累加多个系列\n";
    cout << "数字。通过输入负数\n";
    cout << "终止每个序列。\n";
    cout << "通过输入空\n";
    cout << "序列来终止整个系列。\n";
    cout << endl;
}

// sumSequence - 累加从键盘输入的数字序列，
// 直到用户输入
// 负数为止。
// return - 输入数字的总和
int sumSequence(void)
{
    // 无限循环
    int accumulator = 0;
    for(;;)
    {
        // 获取另一个数字
        int nValue = 0;
        cout << "Enter next number: ";
        cin >> nValue;

        // 如果是负数...
        if (nValue < 0)
        {
            // ...则退出循环
            break;
        }

        // ...否则将数字加到
        // 累加器中
        accumulator += nValue;
    }

    // 返回累加值
    return accumulator;
}

int main(int nNumberOfArgs, char* pszArgs[])
{
    // 向用户显示提示
    displayExplanation();

    // 累加数字序列...
    for(;;)
    {
        // 累加从键盘输入的
        // 数字序列
        cout << "Enter next number: ";
        int accumulatedValue = sumSequence();

        // 检查用户是否完成
        if (accumulatedValue == 0)
        {
            break;
        }

        // 输出结果
        cout << "总计为 " << accumulatedValue << endl;
    }

    return 0;
}
```

## 第二部分：成为一名函数式 C++ 程序员

### 定义函数

第 5 章中的`NestedDemo`程序包含至少三个部分，这些部分在脑中和现实中都可以很容易分离：

- 对操作员说明如何输入数据
- 累加单个数字序列的内循环
- 重复调用内循环的外层循环，直到累加值为 0

沿着这些界限分离程序允许程序员专注于处理程序的每一个部分。接下来的`FunctionDemo`程序展示了如何通过创建`displayExplanation()`和`sumSequence()`函数来拆分`NestedDemo`：

```cpp
// FunctionDemo - 展示函数的用法
// 通过将 NestedDemo 程序的
// 内循环拆分为它自己的
// 函数来实现

#include <cstdio>
#include <cstdlib>
#include <iostream>
using namespace std;

// displayExplanation - 提示用户
// 游戏的数字
void displayExplanation(void)
{
    cout << "此程序累加多个系列\n";
    cout << "数字。通过输入负数\n";
    cout << "终止每个序列。\n";
    cout << "通过输入空\n";
    cout << "序列来终止整个系列。\n";
    cout << endl;
}

// sumSequence - 累加从键盘输入的数字序列，
// 直到用户输入
// 负数为止。
// return - 输入数字的总和
int sumSequence(void)
{
    // 无限循环
    int accumulator = 0;
    for(;;)
    {
        // 获取另一个数字
        int nValue = 0;
        cout << "Enter next number: ";
        cin >> nValue;

        // 如果是负数...
        if (nValue < 0)
        {
            // ...则退出循环
            break;
        }

        // ...否则将数字加到
        // 累加器中
        accumulator += nValue;
    }

    // 返回累加值
    return accumulator;
}

int main(int nNumberOfArgs, char* pszArgs[])
{
    // 向用户显示提示
    displayExplanation();

    // 累加数字序列...
    for(;;)
    {
        // 累加从键盘输入的
        // 数字序列
        cout << "Enter next number: ";
        int accumulatedValue = sumSequence();

        // 检查用户是否完成
        if (accumulatedValue == 0)
        {
            break;
        }

        // 输出结果
        cout << "总计为 " << accumulatedValue << endl;
    }

    return 0;
}
```

## 第 6 章：创建函数

### 本章

- 编写函数
- 向函数传递数据
- 为不同参数的函数命名
- 创建函数原型
- 按值传递与按引用传递
- 为参数提供默认值

在之前的章节中开发的程序足够小，可以很容易地作为一个整体来阅读。而现实世界中的大型程序往往有数千甚至数百万行。开发者需要将这些“巨兽级”程序拆分成更易于理解、描述和维护的小块结构。

C++ 允许程序员将代码划分为这些被称为“函数”的块。函数是一个可以作为单一实体执行的小代码块。这允许程序员将其程序划分为多个实体，每个实体实现整个程序中某个定义的子集。函数本身又被拆分为更小、更详细的函数，形成一个由不断缩小的更详细解决方案组成的金字塔，最终构成了完整的程序。

这种分治法将创建具有相当规模的运行程序的复杂性降低到了凡人可以完成的程度。

## 编写和使用函数

通过示例是理解函数的最好方式。本节从`FunctionDemo`示例开始，它通过定义一个函数来包含部分逻辑，简化了我在第 5 章讨论的`NestedDemo`程序。本节将解释函数是如何定义的以及如何被调用的，并以`FunctionDemo`为模式来同时理解问题和解决方案。

第 5 章中的`NestedDemo`程序包含至少三个部分，这些部分在脑中和现实中都可以很容易分离：

- 对操作员说明如何输入数据
- 累加单个数字序列的内循环
- 重复调用内循环的外层循环，直到累加值为 0

沿着这些界限分离程序允许程序员专注于处理程序的每一个部分。接下来的`FunctionDemo`程序展示了如何通过创建`displayExplanation()`和`sumSequence()`函数来拆分`NestedDemo`：

```cpp
// FunctionDemo - 展示函数的用法
// 通过将 NestedDemo 程序的
// 内循环拆分为它自己的
// 函数来实现

#include <cstdio>
#include <cstdlib>
#include <iostream>
using namespace std;

// displayExplanation - 提示用户
// 游戏的数字
void displayExplanation(void)
{
    cout << "此程序累加多个系列\n";
    cout << "数字。通过输入负数\n";
    cout << "终止每个序列。\n";
    cout << "通过输入空\n";
    cout << "序列来终止整个系列。\n";
    cout << endl;
}

// sumSequence - 累加从键盘输入的数字序列，
// 直到用户输入
// 负数为止。
// return - 输入数字的总和
int sumSequence(void)
{
    // 无限循环
    int accumulator = 0;
    for(;;)
    {
        // 获取另一个数字
        int nValue = 0;
        cout << "Enter next number: ";
        cin >> nValue;

        // 如果是负数...
        if (nValue < 0)
        {
            // ...则退出循环
            break;
        }

        // ...否则将数字加到
        // 累加器中
        accumulator += nValue;
    }

    // 返回累加值
    return accumulator;
}

int main(int nNumberOfArgs, char* pszArgs[])
{
    // 向用户显示提示
    displayExplanation();

    // 累加数字序列...
    for(;;)
    {
        // 累加从键盘输入的
        // 数字序列
        cout << "Enter next number: ";
        int accumulatedValue = sumSequence();

        // 检查用户是否完成
        if (accumulatedValue == 0)
        {
            break;
        }

        // 输出结果
        cout << "总计为 " << accumulatedValue << endl;
    }

    return 0;
}
```

## 第二部分：成为一名功能性的 C++ 程序员

参数和返回值都是可选的。如果其中任一缺失，则使用关键字`void`代替。也就是说，如果一个函数有一个`void`参数列表，则在调用时该函数不接受任何参数（`FunctionDemo`程序就是此类情况）。如果返回值为`void`，则函数不向调用者返回值。

![](img/c6a7aed193f785f4098546695e53f585_109_0.png)

函数的默认参数类型是`void`，这意味着它不接受任何参数。一个函数`int fn(void)`可以声明为`int()`。

## 理解简单函数

简单函数`sumSequence()`返回它计算的整数值。函数可以返回第 2 章中描述的任何内置变量类型。例如，函数可以返回`double`或`char`。如果函数不返回任何值，则函数的返回类型为`void`。

![](img/c6a7aed193f785f4098546695e53f585_109_1.png)

函数可以通过其返回类型进行标记——例如，返回`int`的函数通常被称为整数函数。不返回值的函数被称为`void`函数。

例如，以下`void`函数执行了操作但不返回任何值：

```cpp
void echoSquare() {
    int value;
    cout << "Enter a value:";
    cin >> value;
    cout << "\nThe square is: " << (value * value) << "\n";
    return;
}
```

控制从左括号开始，持续到`return`语句。`void`函数中的`return`语句后面没有值。`void`函数中的`return`语句是可选的。如果不存在，当控制遇到右括号时，执行将返回调用函数。

## 理解带参数的函数

没有参数的函数用途有限，因为此类函数的通信是单向的——通过返回值。双向通信通过函数参数实现。

## 第 6 章：创建函数

### 带参数的函数

函数参数是一个变量，其值在调用操作期间传递给调用函数。以下`SquareDemo`示例程序定义并使用了一个函数`square()`，它返回传递给它的双精度浮点数的平方：

```cpp
// SquareDemo - 演示处理参数的
// 函数的使用

#include <stdio>
#include <cstdlib>
#include <iostream>
using namespace std;

// square - 返回其参数的平方
//    doubleVar - 需要平方的值
//    returns - doubleVar 的平方
double square(double doubleVar) {
    return doubleVar * doubleVar;
}

// displayExplanation - 提示用户游戏的
// 规则
void displayExplanation(void) {
    cout << "This program sums the square of multiple\n";
    cout << "series of numbers. Terminate each sequence\n";
    cout << "by entering a negative number.\n";
    cout << "Terminate the series by entering an\n";
    cout << "Empty sequence.\n";
    cout << endl;
}

// sumSquareSequence - 将键盘输入的数字
// 的平方累加到一个序列中，
// 直到用户输入负数
double sumSquareSequence(void) {
    // 无循环
    double accumulator = 0.0;
    for(;;) {
        // 获取下一个数字
        double dValue = 0;
        cout << "Enter next number: ";
        cin >> dValue;

        // 如果是负数...
        if (dValue < 0)
        {
            // ...则退出循环
            break;
        }

        // 否则计算平方
        double value = square(dValue);

        // 现在将平方加到
        // 累加器
        accumulator += value;
    }

    // 返回累加值
    return accumulator;
}

int main(int nNumberOfArgs, char* pszArgs[])
{
    displayExplanation();

    // 继续累加数字...
    for(;;)
    {
        // 键盘输入的序列
        cout << "Enter next sequence" << endl;
        double accumulatedValue = sumSequence();

        // 如果总和为 0，则退出
        if (accumulatedValue <= 0)
        {
            break;
        }

        // 现在输出结果
        cout << "The total is: " << accumulatedValue << endl;
    }

    return 0;
}
```

## 第 6 章：创建函数

### 带参数的函数

简单函数`sumSequence()`返回它计算的整数值。函数可以返回第 2 章中描述的任何内置变量类型。例如，函数可以返回`double`或`char`。如果函数不返回任何值，则函数的返回类型为`void`。

函数可以通过其返回类型进行标记——例如，返回`int`的函数通常被称为整数函数。不返回值的函数被称为`void`函数。

例如，以下`void`函数执行了操作但不返回任何值：

```cpp
void echoSquare() {
    int value;
    cout << "Enter a value:";
    cin >> value;
    cout << "\nThe square is: " << (value * value) << "\n";
    return;
}
```

控制从左括号开始，持续到`return`语句。`void`函数中的`return`语句后面没有值。`void`函数中的`return`语句是可选的。如果不存在，当控制遇到右括号时，执行将返回调用函数。

## 理解带参数的函数

没有参数的函数用途有限，因为此类函数的通信是单向的——通过返回值。双向通信通过函数参数实现。

## 第 6 章：创建函数

### 带参数的函数

函数参数是一个变量，其值在调用操作期间传递给调用函数。以下`SquareDemo`示例程序定义并使用了一个函数`square()`，它返回传递给它的双精度浮点数的平方：
