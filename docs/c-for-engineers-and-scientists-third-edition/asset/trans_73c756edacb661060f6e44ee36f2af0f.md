

# 第 4 章 185

在这种情况下，用于根据半径是否为负值来选择正确的操作。
这是 if-else 语句的通用语法：

```
if (expression) statement1;
else statement2;
```

首先计算表达式。如果它的值不零，则执行 statement1。
如果它的值 零，则执行 else 关键字之后的语句。因此，根据表达式的值，始终执行两个语句之一（statement1 或 statement2，但不同时都执行）。注意，被测试的表达式必须包含在括号内，每个语句后面都放置一个分号。
为了清晰起见，if-else 语句通常以这种四行形式书写：

```
if (expression) // 这里没有分号
else // 这里没有分号
statement2;
```

if-else 语句的形式通常取决于 statement1 和 statement2 的长度。然而，当使用这种四行形式时，不要在括号后面或 else 关键字后面放置分号。分号只放置在语句的末尾。图 4.2 显示了 if-else 语句的流程图。
作为 if-else 结构的具体示例，来看构造一个计算圆面积的 C++ 程序，测试条件是半径是否小于 0，因此以下是该情况的适当 if-else 语句：

```
if (radius < 0.0)
cout << "A negative radius is invalid" << endl;
else
cout << "The area of this circle is " << 3.1416 * pow(radius,2) << endl;
```

关系运算符用于表示“小于”这一条件。如果 radius 的值小于 0，则条件为真（值为 1），并执行语句 `cout << "A negative radius is invalid";`。如果条件不成立，表达式的值为 0，并执行 else 关键字之后的语句。程序 4.1 显示了在完整程序中使用该语句的方法。

# 选择结构

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_205_0.png)

图 4.2 if-else 流程图

# 程序 4.1

```cpp
#include <iostream>
#include <cmath>
using namespace std;
int main()
{
    double radius;
    cout << "Please type in the radius: ";
    cin >> radius;

    if (radius < 0.0)
        cout << "A negative radius is invalid" << endl;
    else
        cout << "The area of this circle is " << 3.1416 * pow(radius,2) << endl;
    return 0;
}
```

# 第 4 章 187

## if-else 语句

在 if-else 语句之前之后插入一个空行，以便在程序中突出显示它。这种格式贯穿本书，用于强调正在讨论的语句。

为了说明选择的实际作用，使用不同的输入数据运行两次程序 4.1。这里的结果如下：

- Please type in the radius: -2.5
  A negative radius is invalid

以及

- Please type in the radius: 2.5
  The area of this circle is 19.635

在检查此输出时，观察到第一次运行的半径小于 0，if-else 结构中的 if 部分正确执行了 cout 语句，告诉用户负半径无效。在第二次运行中，半径不是负数，使用 if-else 结构中的 else 部分产生正确的面积计算结果：

```
3.1416 * (2.5)^2 = 19.635
```

虽然任何表达式都可以通过 if-else 语句测试，但关系表达式使用最频繁。然而，如下所示语句也是有效的：

```
if (num)
cout << "Bingo!";
else
cout << "You lose!";
```

因为 num 本身是一个有效表达式，如果 num 有任何非零值，则显示消息 *Bingo!*；如果 num 的值为 0，则显示消息 *You lose!*

## 复合语句

虽然 if-else 语句的 if 和 else 部分只允许单个语句，但每个单个语句都可以是一个复合语句。复合语句是大括号之间的一系列单语句，如示例所示：

```
{
statement1;
statement2;
statement3;
.
last statement;
}
```

# 188 选择结构

使用大括号包围一组语句会创建一个单一的语句块，它可以在 C++ 程序中的任何地方代替单个语句。下一个示例展示了在 if-else 语句的通用形式中使用复合语句：

```
if (expression)
{
    statement1; // 根据需要编写任意语句
    statement2; // 可以放在大括号内
    statement3; // 每个语句必须以 ; 结束
}
else
{
    statement4;
    statement5;
    .
    last statement;
}
```

程序 4.2 显示了在实际程序中使用复合语句。程序 4.2 检查 tempType 中的值是否为 f。如果是，则执行与 if-else 语句的 if 部分对应的复合语句。tempType 中的任何其他字母都会导致执行与 else 部分对应的复合语句。
程序 4.2 的示例运行如下：

第 4 章 189

## 块

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_205_0.png)

第 4 章 块

## if-else 语句

在 if-else 语句之前之后插入一个空行，以便在程序中突出显示它。这种格式贯穿本书，用于强调正在讨论的语句。

为了说明选择的实际作用，使用不同的输入数据运行两次程序 4.1。这里的结果如下：

- Please type in the radius: -2.5
  A negative radius is invalid

以及

- Please type in the radius: 2.5
  The area of this circle is 19.635

在检查此输出时，观察到第一次运行的半径小于 0，if-else 结构中的 if 部分正确执行了 cout 语句，告诉用户负半径无效。在第二次运行中，半径不是负数，使用 if-else 结构中的 else 部分产生正确的面积计算结果：

```
3.1416 * (2.5)^2 = 19.635
```

虽然任何表达式都可以通过 if-else 语句测试，但关系表达式使用最频繁。然而，如下所示语句也是有效的：

```
if (num)
cout << "Bingo!";
else
cout << "You lose!";
```

因为 num 本身是一个有效表达式，如果 num 有任何非零值，则显示消息 *Bingo!*；如果 num 的值为 0，则显示消息 *You lose!*

## 复合语句

虽然 if-else 语句的 if 和 else 部分只允许单个语句，但每个单个语句都可以是一个复合语句。复合语句是大括号之间的一系列单语句，如示例所示：

```
{
statement1;
statement2;
statement3;
.
last statement;
}
```

# 188 选择结构

使用大括号包围一组语句会创建一个单一的语句块，它可以在 C++ 程序中的任何地方代替单个语句。下一个示例展示了在 if-else 语句的通用形式中使用复合语句：

```
if (expression)
{
    statement1; // 根据需要编写任意语句
    statement2; // 可以放在大括号内
    statement3; // 每个语句必须以 ; 结束
}
else
{
    statement4;
    statement5;
    .
    last statement;
}
```

程序 4.2 显示了在实际程序中使用复合语句。程序 4.2 检查 tempType 中的值是否为 f。如果是，则执行与 if-else 语句的 if 部分对应的复合语句。tempType 中的任何其他字母都会导致执行与 else 部分对应的复合语句。
程序 4.2 的示例运行如下：

第 4 章 210

## 知识点

### 复合语句的括号放置

一些 C++ 程序员的常见做法是将复合语句的起始括号与 if 和 else 语句同一行。使用这种惯例，程序 4.2 中的语句看起来像以下示例（这种放置仅是风格问题——两种风格都是可以的）。

```
if (tempType == 'f') {
    celsius = (5.0 / 9.0) * (temp - 32.0);
    cout << "\nthe Celsius temperature is *\n" << celsius << endl;
} else {
    fahr = (9.0 / 5.0) * temp + 32.0;
    cout << "\nthe Fahrenheit temperature is *\n" << fahr << endl;
}
```

内部块中引用的 a 和 c 使用该块中定义的 a 和 c 的 值。因为外部块中没有名为 b 的变量，所以从内部块显示 b 的值是从外部块获取的。最后，最后一个 cout 语句位于内部块之外，显示了外部块中定义的变量 a 的值。如果尝试在外部块的任何地方显示 c，编译器将发出错误信息，说明 c 是未定义符号。

变量在程序中使用的区域正式称为变量的作用域，你将在第 6 章深入研究这个主题。

## 单向选择

if-else 语句的一种有用修改是省略语句的 else 部分，具有这种简化且通常很有形式：

```
if (expression) {
    statement;
```

(expression) 之后的语句只有在表达式具有非零值（真条件）时才执行。与之前一样，该语句可以是复合语句。图 4.3 显示了该语句的流程图。

