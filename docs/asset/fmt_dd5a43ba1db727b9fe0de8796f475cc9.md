
复合语句中包含的所有语句构成一个单一的代码块，在此块中声明的任何变量仅在其声明和块的结束花括号之间有效。例如，看以下示例，它由两个代码块组成：

```cpp
// 外部块开始
int a = 25;
int b = 17;
cout << "The value of a is " << a << " and b is now " << b << endl;
  // 内部块开始
  double a = 46.25;
  int c = 10;
  cout << "a is now " << a << " and b is now " << b << " and c is " << c << endl;
  // 内部块结束
cout << "a is now " << a << " and b is now " << b << endl;
// 外部块结束
```

这段代码产生了如下：

a is now 25 and b is now 17

a is now 46.25 and b is now 17 and c is 10

a is now 25 and b is now 17

输出如下：第一个代码块定义了两个名为 `a` 和 `b` 的变量，它们可以在声明后的任何地方使用。在内部块中声明了两个新变量 `a` 和 `c`。内部块的 `a` 存储在与外部块的 `a` 不同的内存位置。在此阶段，创建了四个变量，其中两个同名。当声明一个变量时，编译器尝试访问当前作用域内正确的变量。如果引用的变量在当前作用域未声明，编译器将尝试访问下一个块中声明的变量，直到找到有效访问。此外，内部块的 `a` 和 `c` 分别使用了外部块变量 `a` 和 `c` 的值。因为内部块中没有声明变量 `b`，最后一条语句显示了外部块变量 `b` 的值。如果尝试在外部块的任何地方显示 `c`，编译器会报错说 `c` 是未定义的符号。

## 第 4 章

193

### if-else 语句

#### 信息点

复合语句中的大括号放置

某些 C++ 程序员的习惯做法是在 `if` 和 `else` 语句的同一行放置复合语句的左大括号。按照这种约定，程序 4.2 中的 if 语句将如下所示。这种放置是一个风格问题——两种风格都是接受的。

```cpp
if (tempType == 'f') {
  celsius = (5.0 / 9.0) * (temp - 32.0);
  cout << "\nequivalent Celsius temperature is " << endl;
} else {
  fahrenheit = (9.0 / 5.0) * temp + 32.0;
  cout << "\nequivalent Fahrenheit temperature is " << fahr << endl;
}
```

程序中可以使用变量的区域正式称为变量的作用域（scope），我们将在第 6 章深入探讨这一主题。

#### 单向选择

`if-else` 语句的一种有用修改是省略语句的 `else` 部分，具有这种简短且常用的形式：

```cpp
if (expression)
    statement;
```

`(expression)` 之后的语句仅在 `expression` 为非零值（真条件）时执行。在此之前，语句可以是复合语句。图 4.3 显示了该语句的流程图。

选择结构

![](img/d5a225ca53b347501e86d72212077531_215_0.png)

图 4.3 单向 if 语句

这种修改后的 if 形式被称为单向语句。程序 4.3 使用该语句仅对行驶超过 3000 英里的车辆显示消息。为了看到单向选择的作用，程序 4.3 运行了，每次使用不同的数据。只有第一次运行的输入数据会导致显示“Car is over the limit”。

输入编号和里程: 356

Car is over the limit.

输入编号和里程: 23

End of program output.

## 第 4 章

195

### if-else 语句

#### 程序 4.3

```cpp
#include <iostream>
using namespace std;

int main()
{
    const double LIMIT = 3000.0;
    int idNum;
    double miles;

    cout << "Please type in number and mileage: ";
    cin >> idNum >> miles;

    if (miles > LIMIT)
        cout << " Car " << idNum << " is over the limit.\n";
    else
        cout << "End of program output.\n";

    return 0;
}
```

#### 与 if-else 语句相关的问题

在使用 if-else 语句时遇到的最常见的两个问题是：

- 误解表达式的完整含义
- 使用赋值运算符 `=` 代替关系运算符 `==`

记住，表达式是任何产生结果的操作数和运算符的组合。这个定义比看起来的更宽、更全面。例如，以下所有内容都是有效的 C++ 表达式：

- `age + 5`
- `age == 30`
- `age == 28`

假设变量声明正确，上述每个表达式都会产生一个结果。程序 4.4 使用 `cout` 语句在 `age = 18` 时显示这些表达式的值。

## 196 选择结构

![](img/d5a225ca53b347501e86d72212077531_217_0.png)

```cpp
#include <iostream>
using namespace std;

int main()
{
    int age = 18;

    cout << "The value of the first expression is " << (age + 5) << endl;
    cout << "The value of the second expression is " << (age == 30) << endl;
    cout << "The value of the third expression is " << (age == 40) << endl;

    return 0;
}
```

程序 4.4 产生的输出如下：

第一个表达式的值为 23

第二个表达式的值为 30

第三个表达式的值为 0

正如程序输出所示，每个表达式都关联有一个值。第一个表达式的值是变量 `age` 加 5 的和，即 23。第二个表达式的值是 30，这也赋值给了变量 `age`。第三个表达式的值为 0，因为 `age` 不等于 40，假条件在 C++ 中用 0 表示。如果 `age` 的值为 40，则关系表达式 `a == 40` 将为真且值为 1。

现在假设本意是在语句中使用关系表达式 `age == 40`：

```cpp
if (age == 40)
    cout << "Happy Birthday";
```

但不小心写成了 `age = 40`，导致结果如下：

`if (age == 40)`

    `cout << "Happy Birthday";`

由于错误导致了一个有效的 C++ 表达式，而任何 C++ 表达式都可以由 if 语句进行测试，因此结果语句是有效的，无论之前给 `age` 赋值了什么值，都会显示 Happy Birthday 消息。知道为什么吗？

## 第 4 章

197

### if-else 语句

#### 信息点

##### 布尔数据类型

在当前的 ANSI/ISO C++ 标准之前，C++ 并没有内置一个带有其布尔值 `true`（真）和 `false`（假）的布尔数据类型。由于这种数据类型不是该语言的一部分，经过测试的表达式无法求值为一个布尔值。因此，如下语法

```cpp
if (Boolean expression is true)
    execute this statement;
```

也没有被内置到 C 或 C++ 中。相反，C 和 C++ 都使用了一种更具通用性的语法：

```cpp
if (expression)
    execute this statement;
```

其中 `expression` 是任何求值为数值的表达式。如果所考虑的表达式的值是非零，则被视为 `true`，只有零值被视为 `false`。正如 ANSI/ISO C++ 标准所规定的，C++ 具有一个包含 `true` 和 `false` 值的内置布尔数据类型。正如你从第 2 章中学到的，布尔变量用 `bool` 关键字声明。按照目前的实现方式，布尔值 `true` 和 `false` 的实际值代表整数值 1 和 0。例如，查看下面的程序，它声明了两个布尔变量：

```cpp
#include <iostream>
using namespace std;
int main() {
    bool t1, t2;
    t1 = true;
    t2 = false;
    cout << "The value of t1 is " << t1
         << "and the value of t2 is " << t2 << endl;

    return 0;
}
```

该程序产生以下输出：

The value of t1 is 1

and the value of t2 is 0

如该输出所示，布尔值 `true` 和 `false` 由整数值 1 和 0 表示，并具有以下关系：

```cpp
!true is false
!false is true
```

（待续）

## 选择结构

#### 信息点

##### 布尔数据类型（续续）

此外，对 `bool` 类型的变量应用后置或前缀 `++` 运算符会将布尔值设置为 `true`。后置和前缀 `--` 运算符不能应用于布尔变量。布尔值也可以进行比较，如下代码所示：

```cpp
if (t1 == t2)
    cout << "The values are equal" << endl;
else
    cout << "The values are not equal" << endl;
```

最后，将任何非零值赋值给布尔变量会导致该变量被设置为 `true`（值为 1），而向布尔变量赋值零值则导致 `false`（值为 0）。

`if` 语句测试的条件并不是将 `age = 0` 中的值与数字 40 进行比较。它将 40 赋值给 `age`。也就是说，表达式 `age = 40` 根本不是一个关系表达式；它是一个赋值语句。在赋值完成后，该表达式本身的值为 40。由于 C++ 将任何非零值视为 `true`，因此看待它的方法是意识到 `if` 语句等同于以下语句：

```cpp
age = 40; // assign 40 to age
if (age) // test the value of age
    cout << "Happy Birthday!";
```

由于 C++ 编译器没有办法知道该表达式不是你想要的，因此在编写条件时必须小心。

![](img/d5a225ca53b347501e86d72212077531_219_0.png)

## 练习题 4.2

- (练习) 为以下条件编写适当的 `if` 语句：

    a. 如果角度为 90 度，打印消息“The angle is a right angle”；否则，打印消息“The angle is not a right angle.”

    b. 如果温度高于 100 度，显示消息“above the boiling point of water”；否则，显示消息“below the boiling point of water.”

    c. 如果数字为正数，将该数字加到变量 `postivum`；否则，从变量 `negativeum` 中减去该数字。

    d. 如果斜率小于 0.5，将变量 `flat` 设置为 0；否则，将 `flat` 设置为 1。

    c. 如果 `volts1` 和 `volts2` 之间的差小于 0.001，将变量 `approx` 设置为 0；否则，计算 `approx` 为 `(volts1 - volts2) / 2.0`。

    f. 如果频率高于 60，显示消息“The frequency is too high.”

    g. 如果 `temp1` 和 `temp2` 之间的差超过 2.3，计算变量 `error` 为 `(temp1 - temp2) * factor`。

    h. 如果 `x` 大于 `y` 且 `z` 小于 20，要求用户输入变量 `p` 的值。

    i. 如果距离大于 20 且小于 35，要求用户输入变量 `time` 的值。

- 2. (练习) 为下方流程图所示的条件编写对应的 `if` 语句：

    - a.

    ![](img/d5a225ca53b347501e86d72212077531_220_0.png)

    - b.

    ![](img/d5a225ca53b347501e86d72212077531_220_0.png)

    - c.

    ![](img/d5a225ca53b347501e86d72212077531_220_0.png)

## 选择结构

- 3. (练习) 为以下条件编写对应的 `if` 语句：

    - a. 如果角度为 90 度，打印消息“The angle is a right angle”；否则，打印消息“The angle is not a right angle.”

    - b. 如果温度高于 100 度，显示消息“above the boiling point of water”；否则，显示消息“below the boiling point of water.”

    - c. 如果数字为正数，将该数字加到变量 `postivum`；否则，从变量 `negativeum` 中减去该数字。

    - d. 如果斜率小于 0.5，将变量 `flat` 设置为 0；否则，将 `flat` 设置为 1。

    - c. 如果 `volts1` 和 `volts2` 之间的差小于 0.001，将变量 `approx` 设置为 0；否则，计算 `approx` 为 `(volts1 - volts2) / 2.0`。

    - f. 如果频率高于 60，显示消息“The frequency is too high.”

    - g. 如果 `temp1` 和 `temp2` 之间的差超过 2.3，计算变量 `error` 为 `(temp1 - temp2) * factor`。

    - h. 如果 `x` 大于 `y` 且 `z` 小于 20，要求用户输入变量 `p` 的值。

    - i. 如果距离大于 20 且小于 35，要求用户输入变量 `time` 的值。

- 2. (练习) 为下方流程图所示的条件编写对应的 `if` 语句：

    - a.

    ![](img/d5a225ca53b347501e86d72212077531_220_0.png)

    - b.

    ![](img/d5a225ca53b347501e86d72212077531_220_0.png)

    - c.

    ![](img/d5a225ca53b347501e86d72212077531_220_0.png)

## 第 4 章

201

### 嵌套 if 语句

代码。编写一个 C++ 程序接受此代码作为输入。如果输入，显示一条引导使用较小生成器的消息；否则，显示一条使用较大生成器的消息。

## 4.3 嵌套 if 语句

正如你所见，`if-else` 语句可以包含任何有效的简单或复合语句，包括另一个 `if-else` 语句。因此，一个或多个 `if-else` 语句可以包含 `if-else` 语句的任何部分。在 `if` 语句内部包含一个或多个语句被称为嵌套 `if` 语句。例如，将单语句语句

```cpp
if (distance > 500)
    cout << "snap";
```

替换到以下语句

```cpp
if (hours < 9)
    statement1;
else
cout << "pop";
```

中，会导致此嵌套 `if` 语句：

```cpp
if (hours < 9)
{
    if (distance > 500)
        cout << "snap";
}
else
    cout << "pop";
```

内部单语句周围的大括号是关重要的，因为在没有括号的情况下，C++ 将 `else` 与最近的未配对的 `if` 关联。

## 20 选择结构

图 4.4a 和 4.4b 显示了嵌套 if-else 语句的通用形式，其中第二个 if-else 语句分别嵌套在 (a) 一个 if-else 语句的 if 部分和 (b) 一个 if-else 语句的 else 部分中。

![](img/d5a225ca53b347501e86d72212077531_223_0.png)

图 4.4a 嵌套在 if 部分

### if-else 链

通常情况下，图 4.4a 所示的嵌套往往会令人困惑，在实践中最好避免使用这种结构。然而，图 4.4b 所示嵌套的一种很有用的构造形式如下：

```
if (expression_1)
    statement1;
else
    if (expression_2)
        statement2;
    else
        statement3;
```

与所有的 C++ 程序一样，由于编译器会忽略空白字符，因此这种缩进并不是必须的。通常，上述构造按以下排列方式编写：

```
if (expression_1)
    statement1;
    else if (expression_2)
        statement2;
    else
        statement3;
```
