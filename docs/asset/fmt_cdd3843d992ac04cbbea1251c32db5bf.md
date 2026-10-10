
如果 `kids` 的值不是零，那么这个语句没有微妙之处。但是，假设 `kids` 的值为零：考虑短路求值是如何处理这种情况的。表达式 `(kids!=0)` 求值为 `false`，没有需要评估第二个表达式。使用短路求值，C++ 说整个表达式为 `false`，而不必去求值第二个表达式。这防止了运行时错误，确保了第二个表达式不会发生除零错误。

### 自测题

1. 假设变量 `count` 的值为 `0`，确定以下每个布尔表达式的值（`true` 或 `false`），并给出答案为 `true` 或 `false` 之一。
   a. `(count == 0) && (limit < 20)`
   b. `count == 0 && limit < 20`
   c. `(limit > 20) || (count < 5)`
   d. `(count == 12)`
   e. `(count == 1) && (x < y)`
   f. `(count < 10) || (x < y)`
   g. `((count < 10) || ((limit / count) > 7) || (limit < 20))`
   h. `((limit / count) > 7) || (limit < 20)`
   i. `(limit / ((limit / count) > 12)`
   j. `((limit / count) > 7) && (limit < 0)`
   k. `(limit < 0) && ((limit / count) > 7)`
   l. `(5 & 7) + (!6)`

2. 你有时会使用给定的数值区间：

`2 < x < 3`

在 C++ 中，这个区间的含义可能与你预期的不同。解释并给出指定 `x` 介于 `2` 和 `3` 之间的 C++ 布尔表达式。

3. 考虑一个二次表达式，例如

`x² - x - 2`

描述该二次表达式何处为正（即大于 `0`）涉及描述一组小于较小根（即 `-1`）或大于较大根（即 `2`）的数字。出一个 C++ 布尔表达式，当该公式具有正值时，该表达式为 `true`。

4. 考虑二次表达式

`x² - 4x + 3`

描述该二次表达式何处为负涉及描述一组同时大于较小根（`1`）且小于较大根（`3`）的数字。出一个 C++ 布尔表达式，当该二次表达式的值为负时，该表达式为 `true`。

## 2.2 分支机制

当你来到路口时，就走过去吧。

> 出自 YOGI BERRA

### if-else 语句

`if-else` 语句根据布尔表达式的值在两个备选语句之间选择。例如，假设你想设计一个程序来计算小时工的周薪。假设公司对于工作的前 `40` 小时后的所有小时支付常规率 `1.5` 倍的加班费。当员工工作 `40` 小时或更多时，工资等于：

```
rate * 40 + 1.5 * (hours - 40)
```

### 控制流

然而，如果员工工作少于 `40` 小时，正确的工资公式简单为

`rate * hours`

下面的 `if-else` 语句无论员工工作少于 `40` 小时还是工作 `40` 小时或更多，都能计算出正确的工资：

```
if (hours > 40)
Pay = rate * 40 + 1.5 * (hours - 40);
else
grossPay = rate * hours;
```

### 复合语句

你可能希望 `if-else` 语句的分支执行多个语句。为了实现这一点，请将每个分支的语句括在一对括号 `{` 和 `}` 之间，如“`if-else` 语句”框中的第二个语法模板所示。包含在一对大括号中的语句列表被称为复合语句。复合语句被 C++ 视为单个语句，并可以用在任何可以使用单个语句的地方。（因此，“`if-else` 语句”框中的第二个语法模板实际上只是第一个的一种特例。）

在 `if-else` 语句中，有两种常用的缩进和放置括号的方法，如下所示：

```
if (myScore > yourScore)
{
    cout << "I win!\n";
    wager = wager + 100;
}
else
{
    cout << "I wish these were golf scores.\n";
    wager = 0;
}
```

`if-else` 语句的语法在附附框中给出。如果括号中的布尔表达式（`if` 之后）求值为 `true`，则执行 `else` 之前的语句。如果布尔表达式值为 `false`，则执行 `else` 之后的语句。

### 示例

```
if (myScore > yourScore)
{
    cout << "I win!\n";
    wager = wager + 100;
}
else
{
    cout << "I wish these were golf scores.\n";
    wager = 0;
}
```

```
if (myScore > yourScore) {
    cout << "I win!\n";
    wager = wager + 100;
} else {
    cout << "I wish these were golf scores.\n";
    wager = 0;
}
```

唯一的区别在于大括号的位置。我们认为第一种形式更容易读，因此更倾向于使用。第二种形式节省了行数，所以有些程序员更倾向于第二种形式或其某些变体。

### 陷阱：使用 `=` 代替 `==`

不幸的是，在 C++ 中你可以写出很多内容，你可能认为它们是不符合规范的 C 语言语句，但它们实际上被证明具有某些晦涩的含义。这意味着，如果你错误地写了某些你预期的会产生错误消息的语句，你可能会发现程序可以编译并运行而没有任何错误信息，但输出的结果却是错误的。当你意识到自己使用了错误的方法时，这会导致严重的问题。例如，考虑如下所示的 `if-else` 语句：

```
if (x = 12)
    Do_Something
else
    Do_Something_Else
```

假设你想检查 `x` 的值是否等于 `12`，所以你真的想使用 `==` 而不是 `=`。你可能认为编译器会捕获到你的错误。表达式

```
x = 12
```

并不是一个满足或不满足的状态。它是一个赋值语句，所以事实如此。在 C++ 中，表达式 `x = 12` 是一个返回值的表达式，就像 `x + 12` 或 `2 + 3` 一样。赋值的值是传递给左侧变量的值。例如，`x = 12` 的值是 `12`。我们在关于布尔值兼容性的讨论中看到，非零整型值会被转换为 `true`。如果你在 `if-else` 语句中使用 `x = 12`，该布尔表达式将始终求值为为 `true`。

这个错误很难发现，因为看起来看起来是正确的。如果你将 `12` 放在比较的左侧，编译器不需要任何特殊指令就能找到错误：`12 = x` 不产生错误消息，但 `x = 12` 会生成错误消息。

### 自测练习题

5. 以下序列会产生除零错误吗？

```
j = -1;
if ((j > 0) && (1/(j + 1) > 10))
    cout << i << endl;
```

6. 写一个 `if-else` 语句：如果变量 `score` 的值大于 `100`，输出单词 `High`；如果 `score` 的值最多为 `100`，则输出 `Low`。变量 `score` 的类型为 `int`。

7. 假设 `savings`（储蓄）和 `expenses`（支出）是已经赋值的 `double` 类型变量。写一个 `if-else` 语句：如果 `savings` 至少等于 `expenses`，输出单词 `Solvent`，将 `savings` 的值减去 `expenses` 的值，并将 `expenses` 的值置零。然而如果 `savings` 小于 `expenses`，`if-else` 语句仅输出单词 `Bankruptcy` 而改变任何值。

8. 写一个 `if-else` 语句：如果变量的值大于等于 `60` 且变量 `programsDone` 的值大于等于 `10`，输出单词 `Passed`；否则，`if-else` 语句输出单词 `Failed`。变量 `exam` 和 `programsDone` 的类型为 `int`。

9. 写一个 `if-else` 语句：如果变量 `temperature` 的值大于等于 `100`，或者变量 `pressure` 的值大于等于 `200`，或者两者均是，输出单词 `Warning`；否则，`if-else` 语句输出单词 `OK`。变量 `temperature` 和 `pressure` 的类型为 `int`。

10. 以下内容的输出是什么？解释你的答案。

- a. `if(0)`
    `cout << "0 is true";`
    `else`
    `cout << "0 is false";`
    `cout << endl;`

- b. `if(1)`
    `cout << "1 is true";`
    `else`
    `cout << "1 is false";`
    `cout << endl;`

- c. `if(-1)`
    `cout << "-1 is true";`
    `else`
    `cout << "-1 is false";`
    `cout << endl;`

注意：上述内容仅用于练习。

### 省略 else

有时你想让 `if-else` 语句中的某些情况都不执行操作。在 C++ 中，可以通过省略 `else` 部分来实现。这种 `if-else` 语句被称为“省略 else”。例如，这种省略 else 的 `if-else` 语句如下：

```
if (sales >= minimum)
    salary = sales + bonus;
```

### 嵌套语句

正如你所见，`if-else` 语句可以包含语句。到目前为止，我们使用了赋值语句和简单语句作为嵌套语句。在嵌套语句时，通常会对每个嵌套层进行缩进，但在某些特殊情况下（如多路分支），这种规则并不被遵守。

### 多路 if-else 语句

多路 `if-else` 语句并不是真正不同的 C++ 语句。它只是嵌套在 `if-else` 语句中的，但为了反映这种逻辑，它与普通的 `if-else` 语句在缩进上区分开来。

多路 `if-else` 语句的语法

```
if (Boolean_Expression_1)
    Statement_1
else if (Boolean_Expression_2)
    Statement_2
    ...
else if (Boolean_Expression_n)
    Statement_n
else
    Statement_For_Other_Possibilities
```

示例

```
if ((temperature < -10) && (day == SUNDAY))
    cout << "Stay home."
else if (temperature < -10) // day != SUNDAY
    cout << "Stay home, but call work."
else if (temperature < 0) // temperature >= -10
    cout << "Dress warm."
else // temperature > 0
    cout << "Work hard and play hard.";
```

布尔表达式按顺序检查，直到遇到第一个布尔表达式，然后执行对应的语句。如果没有任何布尔表达式为真，则执行 `Statement_For_Other_Possibilities`。

### switch 语句

`switch` 语句是另一种实现多路分支的 C++ 语句。`switch` 语句的语法和一个简单示例如下所示。

当执行 `switch` 时，会执行多个不同分支之一。执行哪个分支由关键字 `switch` 后括号内的控制表达式决定。`switch` 语句的控制表达式必须始终返回布尔值、枚举常量（在本章稍后讨论）、整型类型之一或字符。当 `switch` 语句执行时，该控制表达式会被求值，计算机会查看各个 `case` 标识符后面的常量值。如果找到一个与控制表达式的值相等的常量，就会执行该分支的代码。你不能让两个 `case` 后面跟着相同的常量值，因为那样会产生歧义指令。

### 分支机制

### switch 语句

语法

```
switch (Controlling_Expression)
{
    case Constant_1:
        Statement_Sequence_1
        break;
    case Constant_2:
        Statement_Sequence_2
        break;
        ...
    case Constant_n:
        Statement_Sequence_n
        break;
    default:
        Default_Statement_Sequence
}
```

> 你不需要在每个 `case` 中放置 `break` 语句。如果你省略了 `break`，该 `case` 将继续执行直到遇到 `break`（或 `switch` 语句的结束）为止。

### 示例

```
int vehicleClass;
double toll;
cout << "Enter vehicle class: ";
cin >> vehicleClass;
switch (vehicleClass)
{
    case 1:
        cout << "Passenger car.";
        toll = 0.50;
        break;
    case 2:
        cout << "Bus.";
        toll = 1.50;
        break;
    case 3:
        cout << "Truck.";
        toll = 2.00;
        break;
    default:
        cout << "Unknown vehicle class!";
}
```

> 如果你忘记了此 `break`，那么轿车将支付 `$1.50`。

# 第 2 章 控制流

`switch` 语句在遇到 `break` 语句或到达 `switch` 语句的结尾时结束。`break` 语句由关键字 `break` 后面跟一个分号组成。当计算机执行 `case` 标签后的语句时，它会持续执行，直到遇到 `break` 语句。当计算机遇到 `break` 语句时，`switch` 语句执行完毕。如果你省略了 `break` 语句，在执行完下一个 `case` 的代码后，计算机将继续执行下一个 `case` 的代码。

注意，你可以为同一段代码设置两个 `case` 标签，如下所示 `switch` 语句的部分所示：

```
case 'A':
case 'a':
    cout << "Excellent. "
    cout << "You need not take the final.\n"
    break;
```

由于第一个 `case` 没有 `break` 语句（实际上，没有任何语句），其效果等同于为一个 `case` 拥有两个标签，而 C++ 语法要求每个标签（如 `'A'` 和 `'a'`）都对应一个 `case`。

如果没有哪个 `case` 的常量与控制表达式的值匹配，则执行 `default` 标签之后的语句。你没有 `default` 部分。如果控制表达式的值没有找到匹配项，则当 `switch` 语句执行时什么都不会发生。然而，最安全的办法始终保留一个 `default` 部分。如果你认为你的 `case` 标签列表涵盖了所有可能的结果，那么你可以在 `default` 部分中放置一条错误信息。

### 自测题

11. 下面代码将产生什么输出？

```
int x = 2;
cout << "Start\n";
if (x <= 3)
    if (x != 0)
        cout << "Hello from the second if.\n";
    else
        cout << "Hello from the else.\n";
cout << "Start again\n";
if (x > 3)
    if (x != 0)
        cout << "Hello from the second if.\n";
    else
        cout << "Hello from the else.\n";
cout << "End again\n";
```

### 自测题（续）

12. 下面代码将产生什么输出？

```
int extra = 2;
if (extra < 0)
    cout << "small";
else if (extra == 0)
    cout << "medium";
else
    cout << "large";
```

13. 如果赋值更改为如下，自测题 `12` 的输出将会是什么？

```
int extra = -37;
```

14. 如果赋值更改为如下，自测题 `12` 的输出将会是什么？

```
int extra = 0;
```

15. 编写一个多分支 `if-else` 语句，将 `int` 变量的值分类为以下类别之一，并输出相应的适当消息。

```
n < 0 或 0 ≤ n ≤ 100 或 n > 100
```
