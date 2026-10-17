
语句块可以嵌套在其他语句块中，局部变量命名的基本规则也适用于这些嵌套块，但在嵌套块中应用这些规则会变得复杂。更好的规则是不要嵌套语句块。如果你觉得需要嵌套语句，请将某些语句块定义为函数，并使用函数调用而不是嵌套语句块。事实上，任何类型的语句块都应该节节使用。在大多数情况下，函数调用优于语句块。为了完整性，我们在随附的摘要框中包含了嵌套块的作用域规则。

| 块 |
| 块是封装在大括号内的某些 C++ 代码。块中声明的变量是该块部的，因此变量名可以在块外部用于其他用途（例如重用作为另一个变量名）。 |
| 嵌套块的作用域规则 |
| 如果标识符在两个嵌套的块中各被声明为变量，那么它们是两个不同的变量。一个变量仅存在于内部块中，在块外部无法访问。另一个变量仅存在于外部块中，在内部块中无法访问。这两个变量是独立的，因此对其中一个变量的更改对另一个没有影响。 |

# 第 3 章 / 更多控制流

## 陷阱 无意间的局部变量

当在一对大括号 `{ }` 内部声明变量时，该变量就变成了这对括号所包含代码块的局部变量。无论你是否想让该变量是局部的，事实都是如此。如果你想让一个变量在大括号外部可用，那么你必须在大括号之外声明它。

### 自测练习题

- 15. 当将以下代码嵌入到一个完整的程序时，会产生什么输出？

```cpp
int firstChoice = 1;
switch (firstChoice + 1)
{
    case 1:
        cout << "Roast beef\n";
        break;
    case 2:
        cout << "Roast worms\n";
        break;
    case 3:
        cout << "Chocolate ice cream\n";
    case 4:
        cout << "Onion ice cream\n";
        break;
    default:
        cout << "Bon appetit!\n"
}
```

- 16. 如果将第一行改为以下内容，自测练习题 15 的输出会是什么？

```cpp
int firstChoice = 3;
```

- 17. 如果将第一行改为以下内容，自测练习题 15 的输出会是什么？

```cpp
int firstChoice = 2;
```

- 18. 如果将第一行改为以下内容，自测练习题 15 的输出会是什么？

```cpp
int firstChoice = 4;
```

- 19. 当将以下代码嵌入到一个完整的程序时，会产生什么输出？

## 3.3 关于 C++ 循环语句的更多

```cpp
int number = 22;
{
  int number = 42;
  cout << number << " ";
  cout << number;
}
```

- 20. 尽管我们敦促不要使用这种风格编程，但我们提供了一个使用嵌套块的练习，以帮助你理解作用域规则。请给出该代码片段嵌入到另一个完整、正确的程序时会产生的结果输出。

```cpp
int x = 1;
cout << x << endl;
{
  cout << x << endl;
  int x = 2;
  cout << x << endl;
{
    cout << x << endl;
    int x = 3;
    cout << x << endl;
  }
  cout << x << endl;
}
cout << x << endl;
```

## 3.3 关于 C++ 循环语句的更多

> 人生并不是接接一个的倒霉事——它是一遍又一遍的倒霉事。

EDNA ST. VINCENT MILLAY, Letter to Arthur Darison Ficke, 1930年10月24日

循环是任何多次重复某个语句或语句序列的程序结构。我们已经过的 `while` 循环和 `do-while` 循环都是循环的例子。要重复的语句（或语句组）被称为循环体，而循环体的每次重复被称为循环的迭代。在构建循环时，两个主要的设计问题是：循环体应该是什么？循环体应该被迭代多少次？

### 复习 while 语句

`while` 语句及其变体 `do-while` 语句的语法在显示 3.9 中进行了回顾。这两种循环之间的重要区别在于何时检查控制布尔表达式。当执行 `while` 语句时，在执行循环之前会检查布尔表达式。如果布尔表达式求值为 `false`，则不执行循环体。在 `do-while` 语句中，首先执行循环体，然后在循环体执行后检查布尔表达式。因此，`do-while` 语句至少执行一次循环体。在启动之后，`while` 循环和 `do-while` 循环的行为非常相似。在循环体的每次迭代后，都会再次检查布尔表达式；如果它为 `true`，则循环再次迭代。如果它从 `true` 变为 `false`，则循环结束。

### 显示 3.9 while 语句和 do-while 语句的语法

带有单语句主体的 while 语句

![](img/67be1289808bc3852827f7f3e32e9d82_169_0.png)

带有多语句主体的 while 语句

```cpp
{ (Boolean_Expression)
Statement_1
Statement_2
.
Statement_Last
}
```

![](img/67be1289808bc3852827f7f3e32e9d82_169_1.png)

带有单语句主体的 do-while 语句

```cpp
do Statement while (Boolean_Expression);
```

![](img/67be1289808bc3852827f7f3e32e9d82_169_2.png)带有多语句主体的 do-while 语句

```cpp
do
    Statement_1
    Statement_2
    .
    Statement_Last
} while (Boolean_Expression);
```

![](img/67be1289808bc3852827f7f3e32e9d82_169_3.png)

## 3.3 关于 C++ 循环语句的更多

并不是人生是接接一个的倒霉事——它是一遍又一遍的倒霉事。当执行 `while` 语句时，在执行循环之前会检查布尔表达式。如果布尔表达式求值为 `false`，则不执行循环体。在 `do-while` 语句中，首先执行循环体，然后在循环体执行后检查布尔表达式。因此，`do-while` 语句至少执行一次循环体。在启动之后，`while` 循环和 `do-while` 循环的行为非常相似。在循环体的每次迭代后，都会再次检查布尔表达式；如果它为 `true`，则循环再次迭代。如果它从 `true` 变为 `false`，则循环结束。

### 增减运算符的复习

`number++` 表达式返回变量的值，然后变量的值增加了 1。例如，考虑以下代码：

```cpp
int number = 2;
number++;
```

`number++` 表达式返回变量的值，然后变量的值增加了 1。例如，考虑以下代码：

```cpp
int number = 2;
int valueProduced = 2 * number++;
cout << valueProduced << endl;
```

```
4
3
```

`number++` 表达式返回变量的值，然后变量的值增加了 1。例如，考虑以下代码：

```cpp
int number = 2;
int valueProduced = 2 * number++;
cout << valueProduced << endl;
cout << number << endl;
```

```
4
3
```

注意 `2 * (number++)`。当 C++ 评估这个表达式时，它使用的是变量增加之前的值，而不是增加之后的值。

`++number` 表达式首先增加变量的值，然后返回增加后的值。例如，考虑以下代码：

```cpp
int number = 2;
int valueProduced = 2 * (++number);
cout << valueProduced << endl;
cout << number << endl;
```

```
6
3
```

注意两个自增运算符 `++` 和 `++number` 对变量的效果相同：它们都将变量的值增加了 1。但这两个表达式求值不同。记住，如果 `++` 在变量之前，则增量是在返回值之前完成的；如果 `++` 在变量之后，则增量是在返回值之后完成的。

显示 3.10 中的程序在 `while` 循环中使用增运算符来计数循环体执行的次数。自增运算符的主要用途之一是控制循环的迭代，类似于显示 3.10 中的做法。

### 显示 3.10 增运算符作为表达式（部分 1，共 2）

```cpp
//热量计数程序。
#include <iostream>
using namespace std;

int main() {
    int numberOfItems, count,
    caloriesForItem, totalCalories;

    cout << "你今天吃了多少食物？ ";
    cin >> numberOfItems;

    totalCalories = 0;
    count = 1;
    cout << "请输入你吃过的每件食物的热量数：\n";
    << numberOfItems << " 件：\n";

    while (count++ <= numberOfItems)
```

## 3.3 关于 C++ 循环语句的更多

```cpp
19 {
  cin >> caloriesForItem;
  totalCalories = totalCalories
  + caloriesForItem;
} 
  
  cout << "Total calories eaten today = "
  << totalCalories << endl;
  return 0;
}
```

显示 3.10 作为表达式的递增运算符（部分 2 / 2）

![](img/67be1289808bc3852827f7f3e32e9d82_172_0.png)

我们关于递增运算符的所有结论也适用于递减运算符，区别在于变量的值减少 1 而不是增加 1。例如，考虑以下代码：

```cpp
int number = 8;
int valueProduced = number--;
cout << valueProduced << endl;
cout << number << endl;
```

这产生输出输出

- 8

- 7

另一方面，代码

```cpp
int number = 8;
int valueProduced = --number;
cout << valueProduced << endl;
cout << number << endl;
```

产生输出

- 7

- 7

`number--` 返回 `number` 的值，然后递减 `number`；另一方面，`--number` 先递减 `number`，然后返回 `number` 的值。

`++ --` 只能用于变量

你不能将递增和递减运算符应用于单个变量以外的任何地方。如 `(x + y)++`、`--(x + y)`、`5++` 等表达式在 C++ 中都是非法的。

### 自测练习题

- 21. 下述代码的输出是什么（当嵌入完整程序中时）？

```cpp
int count = 3;
while (count-- > 0)
  cout << count << " ";
```

- 22. 下述代码的输出是什么（当嵌入完整程序中时）？

```cpp
int count = 3;
while (--count > 0)
  cout << count << " ";
```

- 23. 下述代码的输出是什么（当嵌入完整程序中时）？

```cpp
int n = 1;
do
  cout << n << " ";
while (n++ <= 3);
```

- 24. 下述代码的输出是什么（当嵌入完整程序中时）？

```cpp
int n = 1;
do
  cout << n << " ";
while (+n <= 3);
```

### for 语句

`while` 语句和 `do-while` 语句是你绝对需要的全部循环机制。事实上，有一种循环非常常见，以至于 C++ 为其包含了一个特殊的语句。在进行数值计算时，通常通常会先用数字 1 进行计算，然后用数字 2，然后是 3，以此此类推，直到达到某个最后一个值。例如，为了将 1 到 10 相加，你希望计算机执行以下语句十次，其中 `n` 的值在第一次等于 1，之后每次 `n` 增加 1：

```cpp
sum = sum + n;
```

以下是使用 `while` 语句实现这一目标的一种方法：

```cpp
sum = 0;
n = 1;
while (n <= 10)
{
  sum = sum + n;
  n++;
}
```

虽然在这里使用 `while` 循环可以，但这种情况正是为 `for` 语句（也称为 `for` 循环）设计的。以下语句将整洁地完成任务：

```cpp
sum = 0;
for (n = 1; n <= 10; n++)
  sum = sum + n;
```

让我们逐段分析这条语句。

首先，注意 `while` 循环版本和 `for` 循环版本是通过组合相同的部分制成的：它们都从一个赋值语句开始，将变量 `sum` 设置为 0。在两种情况下，这个对 `sum` 的赋值语句都放在循环语句开始之前。循环本身由这些部分组成：

```cpp
n = 1; n <= 10; n++ and sum = sum + n;
```

这些部分在 `for` 语句中的作用与在 `while` 语句中相同。`for` 语句是表达这一点的一种更简洁的方式。其他方式也是可能的，但我们将只使用 `for` 语句来执行由一个变量控制的循环。例如，那就是变量 `n`。在前面两个循环等效性的指导下，让我们来看 `for` 语句的规则。

`for` 语句以关键字开头，后面跟着括号内的三三个内容，这些内容告诉计算机如何处理控制变量。`for` 语句的开头如下：

```cpp
for (Initialization_Action; Boolean_Expression; Update_Action)
```

第一个表达式告诉如何初始化变量，第二个给出一个布尔表达式，用于检查循环是否应该结束，最后一个表达式告诉在每次执行循环体迭代后如何更新循环控制变量。例如，`for` 循环开始于

```cpp
for (n = 1; n <= 10; n++)
```

`n = 1` 表示 `n` 初始化为 1。`n <= 10` 表示只要 `n` 小于或等于 10，循环就会继续迭代循环体。最后一个表达式 `n++` 表示在每次执行循环体后，`n` 递增 1。

`for` 语句开头的三个表达式由两个、且仅两个分号隔开。不要屈从在第三个表达式后面放置分号的诱惑。（技术解释是这三点是表达式，而不是语句，因此结尾不需要分号。）

显示 3.11 显示了 `for` 语句的语法，并通过展示它如何转换为等 `while` 语句来描述 `for` 语句的操作。注意在 `for` 语句中，与相应的 `while` 语句一样，会在第一次迭代之前测试停止条件。因此，可以存在一个执行零次的 `for` 循环。

### 显示 3.11 for 语句（部分 1 / 2）

`for` 语句

### 语法

```cpp
for (Initialization_Action; Boolean_Expression; Update_Action)
Body_Statement
```

### 示例

```cpp
for (number = 1; n <= 10; n++)
  sum = sum + n;
```

## 等效循环

## 等效语法

```cpp
Initialization_Action;
while (Boolean_Expression)
{
  Body_Statement
  Update_Action;
}
```

## 等效示例

```cpp
number = 100;
while (number >= 0);
```

### 显示 3.11 for 语句（部分 2 / 2）

```cpp
3 {
  cout << number
  << bottles of beer on the shelf.\n";
  number--;
}
```

### 显示 3.12 一个 for 语句

```cpp
//演示循环
#include <iostream>
using namespace std;
int main() {
    int sum = 0;
    for (int n = 1; n <= 10; n++) // 注意变量 n 是循环体内的局部变量
        sum = sum + n;
    cout << "The sum of the numbers 1 to 10 is " << sum << endl;
    return 0;
}
```

输出:

1 到 10 的数字之和为 55

### 显示 3.13 带有多语句体的 for 循环

```cpp
for (int number = 100; number >= 0; number--)
{
    cout << " bottles of beer on the shelf.\n";
    if (number > 0)
        cout << "Take one down and pass it around.\n";
}
```

## 3.3 关于 C++ 循环语句的更多内容

循环体可以没有任何语句。特别是，循环体可以是复合语句。这允许我们在 `for` 循环的体中放置多条语句，如显示 3.13 所示。

因此，你已经见过在每次迭代后将循环变量加 1 的循环，也见过 `for` 循环在每次迭代后将循环控制变量减 1。更新的方式有很多种。变量可以增加或减少 2、3 或任何数字。如果变量是 `double` 类型，则可以增加或减少一个小数值。以下所有内容都是法的循环：
