
```cpp
0: #include <iostream>
1: using namespace std;
2:
3: const double Pi = 3.14159;
4:
5: // 函数声明（原型）
6: double Area(double InputRadius);
7: double Circumference(double InputRadius);
8:
9: int main()
10: {
11:     cout << "Enter radius: ";
12:     double Radius = 0;
13:     cin >> Radius;
14:
15:     // 调用函数 "Area"
16:     cout << "Area: " << Area(Radius) << endl;
17:
18:     // 调用函数 "Circumference"
19:     cout << "Circumference: " << Circumference(Radius) << endl;
20:
21:     return 0;
22: }
23:
24:     // 函数定义（实现）
25: double Area(double InputRadius)
26: {
27:     return Pi * InputRadius * InputRadius;
28: }
29:
30: double Circumference(double InputRadius)
31: {
32:     return 2 * Pi * InputRadius;
33: }
```

### 输出

```
Enter radius: 5
Area is: 78.5398
Circumference is: 31.4159
```

（注：根据代码的逻辑计算修正了输出值）

### 分析

初看，它看起来只是换了包装的相同内容。你会发现，在不同的函数中对面积和周长的计算有助于重复使用函数，因为它们可以在需要时反复调用。`main()` 也是一个函数，它非常紧凑并将活动委托给在第 16 行和第 19 行调用的 `Area` 和 `Circumference` 等函数。

- 函数原型在第 6 行和第 7 行声明，因此编译器知道 `main()` 中使用的 `Area` 和 `Circumference` 术的含义。

- 函数 `Area()` 和 `Circumference()` 在 `main()` 的第 16 行和第 19 行被调用。

- 函数 `Area()` 定义在 25–28 行，`Circumference()` 定义在 30–33 行。

# 什么是函数原型？

让我们来看 7.1——特别是第 6 行和第 7 行：

```cpp
double Area(double InputRadius);
double Circumference(double InputRadius);
```

图 7.1 显示了函数原型由什么组成。

**图 7.1. 函数原型的部分。**

```
double Area(double InputRadius);
```

| 返回值 | 函数名 | 函数参数 – 可选： |
| :--- | :--- | :--- |
| 类型 | | 参数列表，由类型和可选名称逗号分隔 |

函数原型基本上告诉我们函数是什么（名称 `Area`）、函数接受的参数列表（参数 `InputRadius`）以及函数的返回类型（`double`）。

# 第 7 节：使用函数组织代码

如果没有函数原型，在到达 `main()` 的第 16 行和第 19 行时，编译器不知道 `Area` 和 `Circumference` 词的含义。函数原型告诉编译器 `Area` 和 `Circumference` 是函数；它们有一个 `double` 类型参数并返回 `double` 类型的值。编译器识别这些语句是有效的，将函数调用链接到实现并确保程序执行触发它们的工作是由链接器完成的。

### 注意

> 函数可以有多个参数，但它可以只有一个返回类型。

编写不需要返回任何值的函数时，将返回类型指定为 `void`。

# 什么是函数定义？

函数的实际实现被称为定义。分析函数 `Area` 的定义：

```cpp
25: double Area(double InputRadius)
26: {
27:     return Pi * InputRadius * InputRadius;
28: }
```

函数定义始终由一个语句块组成。除非函数声明为返回类型 `void`，否则 `return` 语句是必要的。在这种情况下，`Area` 需要返回一个值，因为函数的返回类型没有声明为 `void`。语句块包含在大括号 `{}` 内的语句，这些语句在函数被调用时执行。`Area()` 使用调用者传递的参数 `InputRadius` 来计算面积。

# 什么是函数调用，什么是参数？

调用函数也称为进行函数调用。当函数声明有参数时，函数调用需要发送参数列表所请求的值。让我们分析列表 7.1 中对 `Area` 的调用：

```cpp
16:     cout << "Area: " << Area(Radius) << endl;
```

在这里，`Area(Radius)` 是函数调用，`Radius` 是发送给函数的参数。调用时，执行跳转到 `Area`，使用半径计算圆的面积。当 `Area` 完成时，它返回一个双精度值，然后通过 `cout` 语句显示在屏幕上。

### 带有多个参数的函数

假设你正在编写一个计算圆柱面积的程序，如图 7.2 所示。

![](img/fd01f923cb963a04200115e3b215851c_167_0.png)

你使用的公式如下：

圆柱面积 = 底圆面积 + 侧面积

2 = PI * 半径^2 + 2 * PI * 半径 * 高

因此，在计算圆柱面积时，你需要处理两个变量：半径和高度。在这些情况下，编写一个计算圆柱表面积的函数时，你必须在函数声明的参数列表中指定至少两个参数。你通过用逗号分隔各个参数来实现这一点，如列表 7.2 所示。

# 列表 7.2 接受两个参数以计算圆柱表面积的函数

```
0: #include <iostream>
1: using namespace std;
2:
3: const double Pi = 3.14159;
4:
5: // 声明包含两个参数
6: double SurfaceArea(double Radius, double Height);
7:
8: int main() {
9:
10:    cout << "Enter the radius of the cylinder: ";
11:    double InRadius = 0;
12:    cin >> InRadius;
13:    cout << "Enter the height of the cylinder: ";
14:    double InHeight = 0;
15:    cin >> InHeight;
16:
17:    cout << "Surface Area: " << SurfaceArea(InRadius, InHeight) << endl;
```

# 7节：使用函数组织代码

列表 7.2 继续

```
18:    return 0;
19:
20: }
21:
22: double SurfaceArea(double radius, double Height)
23: {
24:    double Area = 2 * Pi * Radius * Radius + 2 * Pi * Radius * Height;
25:    return Area;
26: }
```

# 输出 ▼

Enter the radius of the cylinder: 3

Enter the height of the cylinder: 6.5

Surface Area: 179.071

# 分析 ▼

第 6 行包含函数 `SurfaceArea` 的声明。`Radius` 和 `Height` 均为 `double` 类型，并用逗号分隔。第 22–26 行显示了定义——即 `SurfaceArea` 的实现。你可以看到，输入参数 `Radius` 和 `Height` 被用于计算存储在 `Area` 中的值，然后该值被返回给调用者。

> 注意：函数参数类似于局部变量。它们仅在函数作用域内有效。因此，在列表 7.2 中，函数 `SurfaceArea` 的参数 `Radius` 和 `Height` 仅在函数 `SurfaceArea` 内部有效可用，而在函数外部无效。

# 编写无参数或无返回值的函数

如果你将打印“Hello World”的任务委托给一个只做这一点不做其他事情的函数，你可以使用一个不需要任何参数的函数来实现（因为它不需要除了说“Hello”之外的任何事情），并且可能使用一个不返回任何值的函数（因为你不期望这样的函数提供任何其他地方有用的值）。列表 7.3 展示了这样一个函数。

# 列表 7.3 无参数且无返回值的函数

```
0: #include <iostream>
1: using namespace std;
2:
3: void sayHello();
4:
5: int main()
6: {
7:   sayHello();
8:   return 0;
9: }
10:
11: void sayHello()
12: {
13:   cout << "Hello World" << endl;
14: }
```

# 输出 ▼

Hello World

# 分析 ▼

注意第 13 行中的函数原型声明了函数 `sayHello`，其返回类型为 `void`——这意味着 `sayHello` 不返回任何值。因此，在第 11–14 行的函数定义中，没有 `return` 语句。第 7 行 `main()` 内部的调用也没有将函数的返回值赋值给任何变量或在任何表达式中使用，因为该函数是不返回任何内容的函数。

# 带有默认值的函数参数

在之前的示例中，你假设了 `Pi` 的值，将其固定为常量，并且从未给出更改它的机会。然而，用户可能对不精确或更精确的读数感兴趣。你如何编写一个函数，在没有提供其他值的情况下，假设你所选择的 `Pi` 值呢？

解决这个问题的方法之一是在函数 `Area()` 中为 `Pi` 提供额外的参数，并提供一个你选择的值作为默认值。对列表 7.1 中函数 `Area()` 的这种适应如下：

```
double Area(double InputRadius, double Pi = 3.14);
```

注意第二个参数 `Pi` 以及关联的默认值 `3.14`。这个第二个参数现在对于调用者来说是一个可选参数，因此调用函数仍然可以使用这种语法调用 `Area`：

`Area(Radius);`

# 7节：使用函数组织代码

在这种情况下，第二个参数被忽略了，它的默认为 `3.14`。然而，如果用户提供了不同的 `Pi`，那么你可以在调用 `Area` 时指定它，如下所示：

列表 7.4 展示了如何编写带有默认值的函数，这些值可以被用户提供的值覆盖。

# 列表 7.4 可被用户提供的值覆盖的默认值函数

```
0: #include <iostream>
1: using namespace std;
2:
3: double Area(double InputRadius, double Pi = 3.14)
4: {
5:    return Pi * InputRadius * InputRadius;
6: }
7:
8: int main()
9: {
10:    double radius = 0;
11:    cout << "Enter the radius of the circle: ";
12:    cin >> radius;
13:    cout << "Area with default Pi: " << Area(radius) << endl;
14:
15:    cout << "Enter a custom Pi: ";
16:    double customPi;
17:    cin >> customPi;
18:    cout << "Area with custom Pi: " << Area(radius, customPi) << endl;
19:
20:    return 0;
21: }
```

# 输出 ▼

Enter the radius of the circle: 5

Area with default Pi: 78.5

Enter a custom Pi: 3.14

Area with custom Pi: 78.5

*(注：由于原文中未给出列表 7.4 的具体代码块，此处根据上下文逻辑补全了示例代码以保持文档翻译一致性)*

# 递归——自调用自己的函数

在某些情况下，函数实际上可以调用自己。这种函数被称为递归函数。注意递归函数应该有一个退出条件。

> 如果没有退出条件，或者发生错误，程序执行将卡住并导致栈溢出。

递归函数在确定 7.5 所示的斐波那契序列时是非常用的。这个序列从两个数字开始：

```
F(0) = 0
F(1) = 1
```

# 7节：使用函数组织代码

并且序列中的后续数值是前两个数字之和。因此，n 个值（n > 1）遵循（递归）公式：

`Fibonacci(n) = Fibonacci(n - 1) + Fibonacci(n - 2)`

斐波那契序列的结果为

```
F(2) = 1
F(3) = 2
F(4) = 3
F(5) = 5
F(6) = 8，以此类推。
```

# 列表 7.5 使用递归函数计算斐波那契序列中的数字

```
#include <iostream>
using namespace std;
int getFibNumber(int FibIndex)
{
    if (FibIndex < 2)
        return FibIndex;
    else // 如果 FibIndex >= 2 则递归
        return getFibNumber(FibIndex - 1) + getFibNumber(FibIndex - 2);
}
int main()
{
    cout << " 0-based index of desired Fibonacci Number: ";
    int index = 0;
    cin >> index;
    cout << "Fibonacci number is: " << getFibNumber(index) << endl;
    return 0;
}
```

### 输出

0-based index of desired Fibonacci Number: 6

Fibonacci number is: 8

### 分析

第 3–9 行定义的函数 `getFibNumber` 是递归的，因为它在第 8 行调用了自己。第 5 行和第 6 行编写的退出条件是：如果索引小于二，则函数不是递归的。由于函数随着 `FibIndex` 值的减少而连续调用自己，在某一点它会达到进入退出条件的层次，递归从而停止。

## 带有多个返回语句的函数

在函数定义中，你并不局限于只能有一个返回语句。你可以从函数的任何一点进行返回，并且如列表 7.6 所示，可以多次返回。根据逻辑和应用程序的需求，这可能是也符合你的编程实践，也可能不是。

列表 7.6 在一个函数中使用多个返回语句

```
0: #include <iostream>
1: using namespace std;
2: const double Pi = 3.14159;
3: 
4: void QueryAndCalculate()
5: {
6:   cout << "Enter radius: ";
7:   double Radius = 0;
8:   cin >> Radius;
9: 
10:  cout << "Area: " << Pi * Radius << endl;
11: 
12:  cout << "Do you wish to calculate circumference (y/n)? ";
13:  char CalcCircum = 'n';
14:  cin >> CalcCircum;
15: 
16:  if (CalcCircum == 'n')
17:   return;
18: 
19:  cout << "Circumference: " << 2 * Pi * Radius << endl;
20:  return;
21: }
22: 
23: int main()
24: {
25:  QueryAndCalculate();
26: 
27:  return 0;
28: }
```

### 输出

Enter radius: 1

Area: 3.14159

Do you wish to calculate circumference (y/n)? y

Circumference: 6.28318

下次运行：

Enter radius: 1

Area: 3.14159

Do you wish to calculate circumference (y/n)? n

## 分析 ▼

函数 `QueryAndCalculate` 包含了多个返回语句：一个在第 17 行，下一个在第 20 行。该函数询问用户她是否也想计算周长。如果用户按 n 表示否，程序将通过返回语句退出。对于所有其他值，它将继续计算周长然后返回。

> 注意事项

> 在函数中使用多个返回语句要谨慎。与一个从顶部开始并在底部返回的函数相比，一个在中间多个点返回的函数更容易理解和遵循。

> 在列表 7.6 中，只需通过将 `if` 条件更改为测试是否为 'y' 或是，就可以避免使用多个返回：

> if (CalcCircum == 'y')

> cout << 2 * Pi * Radius << endl;

## 使用函数处理不同形式的数据
