
关系运算符有：

- `==` 等于
- `!=` 不等于
- `>` 大于
- `<` 小于
- `>=` 大于或等于
- `<=` 小于或等于

这些运算符是*二元*运算符，因此它们需要在运算符两侧都有操作数。这些操作数可以是任何表达式，包括字面值。关系运算符与两个操作数的组合称为*关系表达式*。

关系表达式总是求值为一个布尔值，要么是 true，要么是 false。以下是一些关系表达式的示例：

```cpp
(2 == 2) // true
(50 >= 50) // true
(34 <= 272) // true
(9 != 9) // false
("Ronald" == "ronald")
// false because "R" is not equal to "r"
("baboon" > "ape")
// true because "b" is greater than "a"
```

当然，变量和字面值一样可以用于关系表达式。注意，在 C++ 中关系表达式必须写在括号内。有些其他语言（例如 Visual Basic）没有这个要求。

## 逻辑运算符

更复杂的比较有时需要程序员组合两个或多个关系表达式。这类比较被称为逻辑表达式，并通过逻辑运算符执行。逻辑运算符有：

- `&&` 与
- `||` 或
- `!` 非

下面是一个示例，说明如何将 `&&` 逻辑运算符与两个关系表达式一起使用（假设我们已经声明了变量 `workerType` 和 `hoursWorked`）：

```cpp
((workerType == "hourly") && (hoursWorked > 40))
```

请注意，两个表达式必须分别用括号括起来，并且整个组合也要用括号括起来。

如果所有关系表达式都为真，`&&` 逻辑表达式返回 true；如果其中任何一个或两个关系表达式为假，则返回 false。我们可以用真值表总结这种行为：

| 关系表达式 1 | 关系表达式 2 | 结果 |
|---|---|---|
| 真 | 真 | 真 |
| 真 | 假 | 假 |
| 假 | 真 | 假 |
| 假 | 假 | 假 |

下面是一个 `||` 逻辑表达式的示例：

```cpp
((hoursWorked < 41) || (workerType == "salary"))
```

在 `||` 逻辑表达式中，如果任一关系表达式为真，则表达式为真；仅当两个关系表达式都为假时，表达式才为假。以下是 `||` 表达式的真值表：

| 关系表达式 1 | 关系表达式 2 | 结果 |
|---|---|---|
| 真 | 真 | 真 |
| 真 | 假 | 真 |
| 假 | 真 | 真 |
| 假 | 假 | 假 |

最后一个逻辑运算符是 `!`（非）运算符。该运算符是单目运算符，对布尔表达式的值取反。例如：

```cpp
! (2 == 2) // false
! (3 < 2) // true
```

在本书中，我们不会经常使用 `!` 运算符。事实上，我们只会在处理文本文件时使用它，你将在本书后面看到。

## 使用 *if* 语句做出决策

在解决涉及决策的编程问题时，仅使用关系表达式和逻辑表达式是不够的；必须有某种方式根据关系和/或逻辑表达式的结果来控制哪些语句被执行。C++ 中用于做出决策的一个工具是 *if* 语句。

### *if-else* 语句

*if* 语句最简单的形式是 *if-else* 语句。该语句用于根据条件（可以是关系表达式或逻辑表达式）的值执行一组语句或另一组语句。

*if-else* 语句的一般形式如下：

```cpp
if (condition)
    statement1
else
    statement2
```

*if-else* 语句的工作方式如下：如果条件为真，则执行 statement₁，否则执行 statement₂。让我们看一个 C++ 示例：

```cpp
int hoursWorked;
cout << "Enter the number of hours worked: ";
cin >> hoursWorked;
```

```cpp
double rate = 25.00;
double pay;
if (hoursWorked > 40)
    pay = (40 * rate) + ((hoursWorked - 40) * (rate
        * 1.5));
else
    pay = (hoursWorked * rate);
```

存储在 `pay` 中的值取决于用户为 `hoursWorked` 变量输入的内容。如果用户输入的数值大于 40，则 `pay` 的值由条件正下方的语句设置。如果用户输入的工作小时数为 40 或更少，则 `pay` 的值由 `else` 下方的语句设置。

你会注意到，在上面的示例中，如果条件为真，只执行一条语句；如果条件为假，也只执行一条语句。如果你使用花括号将多条语句放在一个块中，那么 if-else 语句的每种可能结果并不限于只执行一条语句。此版本 if-else 语句的一般形式如下：

```cpp
if (condition)
{
    statement₁;
    statement₂;
    statementₙ;
}
else
{
    statement₁;
    statement₂;
    statementₙ;
}
```

使用这种 if-else 形式时，当条件为真时执行第一个语句块，当条件为假时执行第二个语句块。让我们看一个示例：

```cpp
int grade, bonus;
bool passFail;
cout << "Enter your grade: ";
cin >> grade;
if (grade >= 70)
{
    passFail = true;
    bonus += 5;
}
else
    passFail = false;
```

在上面的示例中，及格分数（70 分或以上）会将布尔变量设置为 true，并给予 5 分奖励。不及格分数只会将布尔变量设置为 false。

为了节省一点空间，你经常会看到 if-else 语句中的语句块将左花括号与条件写在同一行，例如：

```cpp
if (grade >= 70) {
    passFail = true;
    bonus += 5;
}
```

这样开始一个语句块是一种风格约定，你可以根据需要遵循，但无论选择哪种风格，你都应该保持一致，并始终使用相同的风格。

if 语句可以放在另一个 if 语句内部。这称为嵌套 if 语句。下面是一个示例：

```cpp
int num1, num2, num3;
cout << "Enter three numbers: ";
cin >> num1 >> num2 >> num3;
if (num1 > num2)
    if (num1 > num3)
        cout << "The largest number is " << num1
             << endl;
```

如果第一个条件为真，则执行嵌套在第一个 if 语句内部的第二个 if 语句。

当你想要将 else 语句与嵌套的 if 语句一起使用时，else 语句总是与最近的 if 语句配对。例如：

```cpp
if (guess != number)
    if (guess < number)
        high = guess - 1;
    else
        high = guess + 1;
```

如果你希望 else 与第一个 if 语句结合，可以在嵌套的 if 语句周围使用花括号，如下所示：

```cpp
if (guess != number) {
    if (guess < number)
        low = guess + 1;
    else
        high = guess + 1;
}
else
    if (guess > number)
        high = guess - 1;
```

在编写嵌套 if 语句时，缩进有助于表明你的意图，但使用花括号将确保编译器按照程序员预期的方式执行代码。

### if-else if 语句

你会如何使用 if 语句为数字考试成绩分配相应的字母等级？一种方法是编写一系列独立的 if 语句，如下所示：

```cpp
int numGrade;

string letterGrade;

cout << "Enter the numerical score: ";

cin >> numGrade;

if (numGrade >= 90)
    letterGrade = "A";

if (numGrade >= 80)
    letterGrade = "B";

if (numGrade >= 70)
    letterGrade = "C";

if (numGrade >= 60)
    letterGrade = "D";

if (numGrade < 60)
    letterGrade = "F";
```

该程序解决了问题，但造成了不必要的计算。如果用户输入数字 86，程序会将 `letterGrade` 赋值为 `"B"`，但随后会继续向下测试每个剩余 if 语句中的 `numGrade`。我们更希望发生的情况是，一旦程序将字母等级赋值给变量，程序就不应该再对 `numGrade` 执行任何测试，而是继续执行下一个任务。

这个问题的解决方案是使用 if 语句的另一种变体——if-else if 语句。if-else if 语句的一般形式如下：

```cpp
if (condition)
    statement;
else if (condition)
```
