
```
10 20 30 40 
50 60 70 80 
90 100 110 120 
```

# 分析

列表 6.15 中的两个嵌套循环访问二维数组。外层循环遍历行 `ROWS`，内部循环遍历列 `COLUMNS`。对于每一行，内部循环都会打印该行中的每个元素。这是处理多维结构数据的常用方法。

## 输出

此程序将一次计算 5 个斐波那契数
0 1 2 3 5 8
你想看更多数字吗 (y/n)? y
13 21 34 55 89
你想看更多数字吗 (y/n)? y
144 233 377 610 987
你想看更多数字吗 (y/n)? y
1597 2584 4181 6765 10946
你想看更多数字吗 (y/n)? n
再见！

## 分析

第 13 行的外部 `do...while` 循环基本上是一个查询循环，如果用户想看更多数字，该循环就会重复。第 15 行的内部 `for` 循环负责计算下一个斐波那契数并一次显示五个数字。在第 19 行，你将值存储在临时变量 `num2Temp` 中，以便在第 21 行复用。注意，如果你没有存储这个值，你将直接把第 20 行修改后的值赋给 `num`，这并不是你想要的。当用户按下 'y' 获取更多数字时，`do...while` 循环会再次执行，从而执行嵌套的 `for` 循环来生成五个斐波那契数。

## 总结

本节教了你如何编写条件语句来创建备执行路径并使代码块在循环中重复。你学习了 `if...else` 结构，以及使用 `switch-case` 语句来处理变量包含不同值时的各种情况。

在理解循环时，你学习了 `goto`——但同时也被警告不要使用它，因为它会创建无法理解的代码。你学习了在 C++ 中使用 `while`、`do...while` 和 `for` 结构来编写编程循环。你学习了如何让循环无限迭代以创建无限循环，以及使用 `continue` 和 `break` 来更好地控制它们。

## 问答

- *问：如果我在 `switch-case` 语句中省略 `break` 会发生什么？*
- `break` 语句允许程序执行退出 `switch` 结构。如果没有它，执行将继续评估后续的 `case` 语句。

# 工作坊 149

问：我如何退出无限循环？

使用 `break` 退出包含它的任何循环。使用 `return` 也可以退出函数。

我的 `while` 循环看起来像 `while(Integer)`。当 `Integer` 求结果为 -1 时，`while` 循环会执行吗？

理想情况下，`while` 表达式应该求值为布尔值 `true` 或 `false`。`false` 是零。不为零的条件被视为 `true`。因为 -1 不是零，所以 `while` 条件求结果为 `true`，循环会被执行。如果你希望循环只对正数执行，请编写表达式 `while(Integer>0)`。此规则适用于所有条件语句和循环。

问：是否存在等于 `for();` 的空循环？

不，`while` 总是需要一个伴随的条件表达式。

问：我通过复制粘贴将 `do...while(exp);` 改为了 `while(exp);`。我应该预见到任何问题吗？

是的，大问题！由于 `while` 后面跟着一个空语句（分号），`while(exp);` 已经是一个有效的空 `while` 循环，即使它后面跟着一个语句块。该语句块会被执行一次，但在循环之外。复制粘贴代码时要格外小心。

## 工作坊

工作坊提供了测验题以帮助巩固你对所涵盖内容的理解，并提供了练习让你获得使用所学知识的。在检查附录 E 中的答案之前，请回答测验和练习题，并确保在继续下一节之前理解了这些答案。

## 测验

- 1. 既然即使没有缩进也能编译，为什么还要费力对语句块、嵌套 `if` 和嵌套循环中的代码进行缩进？
- 2. 你可以使用 `goto` 实现快速修复。为什么你仍然要避免它？
- 3. 是否可以写一个计数器递减的 `for` 循环？它看起来是什么样的？

![](img/ccb6520e9d7dbb1b25f5e4ac7152a7c5_168_0.png)

# 第 6 节：控制程序流

4. 下述循环有什么问题？

```
for (int counter=0; counter==10; ++counter)
cout << counter << " ";
```

## 练习

- 1. 写一个 `for` 循环以反序访问数组中的元素。
- 2. 写一个与列表 6.14 等效的嵌套循环，将两个数组中的元素相加，但采用反序。
- 3. 写一个程序显示斐波那契数，类似于列表 6.16，但询问用户想要计算多少个数字。
- 4. 写一个 `switch-case` 结构，判断颜色是否在彩虹中或其他地方。使用枚举常量。
- 5. 漏洞排查 `BUGBUSTERS`：这段代码哪里错了？

```
for (int counter=0; counter==10; ++counter)
cout << counter << " ";
```
- 6. 漏洞排查 `BUGBUSTERS`：这段代码哪里错了？

```cpp
int loopCounter = 0;
while(loopCounter < 5)
{
cout << loopCounter << " ";
loopCounter++;
}
```
- 7. 漏洞排查 `BUGBUSTERS`：这段代码哪里错了？

```cpp
cout << "Enter a number between 0 and 4" << endl;
int input = 0;
cin >> input;
switch (input)
{
case 0:
case 1:
case 2:
case 3:
case 4:
cout << "Valid input" << endl;
default:
}
```

# 第 7 节

## 使用函数组织代码

到目前为止，你在书中看到的简单程序都包含在 `main()` 中。随着你的程序变得越来越复杂，`main()` 的内容也会变得越来越长，除非你使用函数来组织程序。

函数为你提供了一种将程序执行划分并组织成逻辑块的方法。函数因此是一个子程序，可以选择地接收参数并返回值。在本节中你学习了：

- 函数的需求
- 函数原型和定义
- 向函数传递参数以及从函数返回值

## 函数的需求

想象一个让用户输入半径并计算周和面积的应用程序。实现这种目的的方法是将全部放在 `main()` 中。另一种方法是将该应用程序拆分为逻辑块：给定半径计算周和面积。参见列表 7.1。

**列表 7.1 计算圆周长和面积的函数**

```cpp
#include <iostream>
using namespace std;
const double Pi = 3.14159265;
// 函数声明（原型）
double Area(double radius);
double Circumference(double radius);
int main()
{
    cout << "Enter radius: ";
    double radius = 0;
    cin >> radius;
    // 调用函数 "Area"
    cout << "Area is: " << Area(radius) << endl;
    // 调用函数 "Circumference"
    cout << "Circumference is: " << Circumference(radius) << endl;
    return 0;
}
// 函数定义（实现）
double Area(double radius)
{
    return Pi * radius;
}
double Circumference(double radius)
{
    return 2 * Pi * radius;
}
```

## 输出

输入半径: 6.5
面积为: 132.732
周长为: 40.8407

## 分析

`main()` 一个函数，它是紧凑的，并将活动委托给 `Area()` 和 `Circumference()` 函数，这些函数分别在第 16 行和第 19 行被调用。

该程序演示了使用函数编程的相关组件：

- 函数原型在第 6 和 7 行声明，因此编译器知道 `main()` 中使用的 `Area` 和 `Circumference` 术语的含义。
- 函数 `Area()` 和 `Circumference()` 在第 16 和 19 行被调用。
- 函数 `Area()` 在 25–28 行定义，`Circumference()` 在 30–33 行定义。

## 什么是函数原型？

让我们再次查看列表 7.1，特别是第 6 和 7 行：

```
double Area(double radius);
double Circumference(double radius);
```

图 7.1 显示了函数原型的组成部分。

| 图 7.1 double Area(double radius) |
| :--- |
| 函数原型组成部分 |
| 返回类型 | 函数名 | 参数（可选）：由类型和可选名称组成，在有多个参数时用逗号分隔 |

## 第 7 Lesson：使用函数组织代码

函数原型基本上告诉了函数如何命名（名称 `Area`）、函数接受的参数列表（一个名为 `radius` 的 `double` 类型参数）以及函数的返回类型（`double`）。如果没有函数原型，当运行 `main()` 函数中的第 16 行和第 19 行时，编译器不知道 `Area` 和 `Circumference` 实际上是函数；函数原型告诉编译器 `Area` 和 `Circumference` 是函数；它们接受一个 `double` 类型的参数并返回一个 `double` 类型的值。编译器认为这些语句是有效的，它的工作是将函数调用链接到它的实现上，并确保程序的执行实际上触发了链接器的执行工作。

> 注意
> 函数可以有多个由逗号分隔的参数，但它只能有一个返回类型。

在编写一个不需要返回任何值的函数时，请将返回类型指定为 `void`。

## 什么是函数定义？

真正的实质性内容——函数的实现——被称为定义。分析函数 `Area()` 的定义。

```
25: double Area(double radius)
26: {
27:     return Pi * radius * radius;
28: }
```

函数始终由一个语句块组成。除非函数声明的返回类型为 `void`，否则必须有一个 `return` 语句。在这种情况下，`Area()` 需要返回一个值，因为该函数已被声明为返回 `double` 的函数。语句块包含在花括号 `{...}` 内部的语句，这些语句在函数被调用时会被执行。`Area()` 使用调用者传递的输入参数 `radius`（该参数包含半径）来计算圆的面积。

## 什么是函数调用，什么是参数？

调用函数与触发函数是同一回事。当函数声明包含参数时，该函数需要发送参数。参数是其参数列表中的函数请求。让我们分析列表 7.1 中对 `Area()` 的调用：

```
16:     cout << "Area: " << Area(radius) << endl;
```

在这里 `Area(radius)` 是函数调用，其中 `radius` 是发送给函数 `Area()` 的参数。当被调用时，执行流跳转到函数 `Area()`，该函数使用发送的 `radius` 来计算圆的面积。

## 编写带有多个参数的函数

假设你正在编写一个计算圆柱表面积的程序，如图 7.2 所示。

图 7.2
一个圆柱。

![](img/ccb6520e9d7dbb1b25f5e4ac7152a7c5_174_0.png)

你使用的公式如下：

圆柱面积 = 顶圆面积 + 底圆面积 + 侧面积
= Pi * radius^2 + Pi * radius^2 + 2 * Pi * radius * height
= 2 * Pi * radius^2 + 2 * Pi * radius * height

因此，在计算圆柱面积时，你需要处理两个变量：`radius` 和 `height`。在这种情况下，编写计算圆柱表面积的函数时，你需要在函数声明的参数列表中指定至少两个参数。你通过如列表 7.2 所示，用逗号分隔各个参数来实现此。

列表 7.2 接受两个参数以计算圆柱表面积的函数

```
0: #include <iostream>
1: using namespace std;
2:
3: const double Pi = 3.14159265;
4:
5: // 声明包含两个参数
6: double SurfaceArea(double radius, double height);
7:
8: int main()
9: {
10: cout << "Enter the radius of the cylinder: ";
11: double radius = 0;
12: cin >> radius;
13: cout << "Enter the height of the cylinder: ";
14: double height = 0;
15: cin >> height;
16:
17: cout << "Surface area: " << SurfaceArea(radius, height) << endl;
18:
19: return 0;
20: }
21:
22: double SurfaceArea(double radius, double height)
23: {
24: double area = 2 * Pi * radius * radius + 2 * Pi * radius * height;
25: return area;
26: }
```

### 输出

Enter the radius of the cylinder: 3
Enter the height of the cylinder: 6.5
Surface Area: 179.071

### 分析

第 6 行包含函数 `SurfaceArea()` 的声明，带有两个参数：`radius` 和 `height`，类型均为 `double`，并用逗号分隔。第 22–26 行显示了定义——即 `SurfaceArea()` 的实现。如你所示，输入参数 `radius` 和 `height` 用于计算存储在局部变量 `area` 中的值，然后该值被返回给调用者。

> 注意 函数参数类似于局部变量。它们仅在函数的作用范围内有效。因此在列表 7.2 中，函数 `SurfaceArea()` 内部参数 `radius` 和 `height` 是 `main()` 函数中同名变量的副本。

## 编写无参数或无返回值的函数

如果你将打印“Hello World”的任务委托给一个只做这一件事不做其他任何事的函数，你可以使用不需要任何参数的函数来实现（因为它除了说“Hello”之外不需要做任何事情），可能还需要一个不返回任何值的函数。列表 7.3 展示了这样的例子。

列表 7.3 无参数和返回值的函数

```
0: #include <iostream>
1: using namespace std;
2: void SayHello();
3:
4: int main()
5: {
6:   SayHello();
7:   return 0;
8: }
9:
10: void SayHello()
11: {
12:   cout << "Hello World" << endl;
13: }
```

### 输出

Hello World

### 分析

注意函数原型将 `SayHello()` own为 `void` 类型——即 `SayHello()` 不返回值。某些程序员倾向于在结尾插入 `return` 语句：

```
void SayHello()
{
  cout << "Hello World" << endl;
  return;
}
```

之前的示例中，你假设了 `Pi` 的值，将其固定为常量，并且没有给用户更改的机会。然而，用户可能需要更精确的值。如何编写一个使用 `Pi` 默认值的函数？

解决此问题的方法是在函数 `Area()` 中提供一个额外的 `Pi` 参数并指定一个默认值。列表 7.1 中 `Area()` 的适配将如下：

```
double Area(double radius, double pi = 3.14);
```

注意第二个参数 `pi` 被赋值为默认值 `3.14`。因此，这个第二个参数对于调用者来说是可选的。可以在不存在第二个参数的情况下调用 `Area()`：

```
Area(radius);
```

在这种情况下，第二个参数默认为 `3.14`。然而，当需要时。

列表 7.4 展示了如何编写带有参数默认值的函数，这些值可以在需要时被用户提供的值所覆盖。

列表 7.4 使用默认 3.14 的 Pi 计算圆面积的函数

```
0: #include <iostream>
1: using namespace std;
2:
3: 函数声明（原型）
4: double Area(double radius, double pi = 3.14);
5:
6: int main() {
7: {
8:     cout << "Enter radius: ";
9:     double radius = 0;
10:    cin >> radius;
11:
12:    cout << "pi is 3.14, do you wish to change this (y / n)? ";
13:    char changePi = 'n';
14:    cin >> changePi;
15:
16:    double circleArea = 0;
17:    if (changePi == 'y')
```
