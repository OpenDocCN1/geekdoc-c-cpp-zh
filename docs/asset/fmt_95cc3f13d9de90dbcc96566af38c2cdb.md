
该程序读取一组整数并打印奇偶整数的数量。该程序读取 20 个整数，但你可以轻松地修改它以读取任何整数。事实上，你可以修改程序，让用户指定读取的整数个数。

### 输入
20 个整数——正数、负数或零。

### 输出
零、偶数和奇数的数量。

读取一个数字后，你需要判断它是奇是偶。假设该值存储在 `number` 中。除以 2 并检查余数。如果余数为 0，则为偶数。增加偶数计数，然后检查是否为零。如果余数不为 0，增加奇数计数。

```cpp // 检查偶数的逻辑
evens++;
// 检查零的逻辑
```

该程序使用 `switch` 语句来决定 `number` 是奇是偶。假设 `number` 是奇数。除以 2 得到的余数在正数时为 1，负数时为 -1。如果 `number` 是偶数，无论正负，除以 2 得到的余数均为 0。你可以使用取模运算符 `%` 来找到它：

```
6 % 2 = 0; -4 % 2 = 0; -7 % 2 = -1; 15 % 2 = 1
```

对列表中的每个数字重复之前的分析过程。

这种讨论转化为下面的算法：

- 1. 对于列表中的每个数字：
  a. 获取数字。
  b. 分析数字。
  c. 增加相应的计数。
- 2. 输出结果。

### 变量
因为你想要统计零、偶数和奇数的数量，你需要三个 `int` 类型的变量——例如 `zeros`, `evens` 和 `odds`——来跟踪计数。你还需要一个变量——例如 `number`——用于读取和存储要分析的数字，以及另一个变量——例如 `counter`——用于计算已分析的数字。因此，程序中需要以下变量：

## 282 | 第 5 章：控制结构 II（循环）

```cpp
int counter;      //循环变量
int number;      //用于存储读取数字的变量
int zeros;       //用于存储零的计数变量
int evens;       //用于存储偶数计数变量
int odds;        //用于存储奇数计数变量
```

显然，你必须将变量 `zeros`、`evens` 和 `odds` 初始化为 0。你可以在声明变量时对其进行初始化。

### 主算法
1. 初始化变量。
2. 提示用户输入 20 个数字。
3. 对于列表中的每个数字：
   a. 读取数字。
   b. 输出该数字（回显输入）。
   c. 如果该数字是偶数：
      i. 偶数计数加 1。
      ii. 如果数字为 0，零的计数加 1。
   否则：
      奇数计数加 1。
4. 打印结果。

在编写 C++ 程序之前，让我们更详细地描述一下第 1–4 步。这将让你在 C++ 中编写指令变得容易得多。

1. 初始化变量。你可以在声明变量时初始化 `zeros`、`evens` 和 `odds`。
2. 使用输出语句提示用户输入 20 个数字。
3. 对于步骤 3，你可以使用 `for` 循环来处理和分析这 20 个数字。在伪代码中，该步骤写如下：

```cpp
for (counter = 1; counter <= 20; counter++)
  read the number;
  output number;

  switch (number % 2) // 检查余数
  {
    case 0:
      increment even count;
      if (number == 0)
        increment zero count;
      break;
    case 1:
    case -1:
      increment odd count;
  }//end switch
}}//end for
```

4. 打印结果。输出变量 `zeros`、`evens` 和 `odds` 的值。

### 完整程序列表

```cpp
#include <iostream>
#include <iomanip>

using namespace std;

const int N = 20;

int main() {
    //声明变量
    //循环控制变量
    int counter;
    int number;
    //用于存储新数字的变量
    int zeros = 0; // 步骤1
    int odds = 0; // 步骤1
    int evens = 0; // 步骤1

    cout << "Please enter " << N << " integers,";
    cout << "positive, negative, or zeros.";
    cout << endl; // 步骤2

    cout << "The numbers you entered are:" << endl;

    for (counter = 1; counter <= N; counter++) { // 步骤3
        cin >> number;
        cout << number << " "; // 步骤3a
        // 步骤3b
        switch (number % 2) // 步骤3c
        {
          case 0:
            evens++;
            if (number == 0)
              zeros++;
            break;
          case 1:
          case -1:
            odds++;
            } //end switch
        }
    }

    cout << "There " << evens << " evens, "
      << "which includes " << zeros << " zeros.";
      << << endl;
    cout << "The number of odd numbers is: " << odds
      << endl;

    return 0;
}
```

示例运行：在此示例运行中，用户输入部分为阴影。

Please enter 20 integers, positive, negative, or zeros.

The numbers you entered are:

0 0 -2 -3 -5 6 7 8 3 0 -23 -8 0 2 9 0 12 67 54

There are 13 evens, which includes 6 zeros.

The number of odd numbers is: 7

我们建议你使用上述输入对此程序进行走读。

## do...while 循环（重复）结构
本节描述了第三种类型的循环或重复结构，称为 `do..while` 循环。`do..while` 语句的一般形式如下：

![](img/abc25bb507ebb3eb05460d88ce0e0fde_324_0.png)

当然，语句可以是简单语句，也可以是复合语句。如果是复合语句，请将其括在大括号之间。图 5-3 显示了 `do..while` 循环的执行流。

## do...while 循环（重复）结构 | 285

![](img/abc25bb507ebb3eb05460d88ce0e0fde_325_0.png)

在 C++ 中，`do` 是一个关键字。

语句首先执行，然后求值表达式。如果表达式求值为真（true），则再次执行该语句。只要 `do...while` 语句中的表达式为真，语句就会执行。为了避免死循环，你必须再次确保循环包含一个最终能使表达式为假（false）并确保其正常退出的语句。

### 示例 5-18
`i = 0;`

```cpp
do {
    cout << i << " ";
    i = i + 5;
} while (i <= 20);
```

此代码的输出为：

0 5 10 15 20

在输出 20 之后，执行语句：

`i = i + 5;`（注：此处原文逻辑断裂，意指判断条件不成立后退出）

## 控制结构 II（循环）
（注：原文后续部分存在大量重复与乱码，此处已根据技术逻辑进行整理翻译）

`while` 和 `for` 循环在执行循环体之前检查条件，因此被称为**前测试循环**。`do...while` 循环在执行循环体之后检查条件，因此被称为**后测试循环**，它保证至少执行一次。

### 选择合适的循环结构
在 C++ 中，三种循环都有其用武之地。如果你知道程序可以预先所需的重复次数，那么 `for` 循环是正确的选择。如果你不知道，且程序无法预判所需的重复次数，且次数可能为零，那么 `while` 循环是正确的选择。如果你不知道、程序无法预判所需的重复次数，但次数至少为一次，那么 `do...while` 循环是正确的选择。

### break 和 continue 语句
`break` 语句在 `switch` 结构中执行时，会立即退出 `switch` 结构。同样，你可以在 `while`、`for`、`do...while` 循环中使用 `break` 语句。当 `break` 语句在循环结构中执行时，它会立即退出该结构。`break` 语句通常用于两个目的：
- 退出循环。
- 跳过 `switch` 的剩余部分。

在执行 `break` 语句后，程序将继续执行结构之后的第一个语句。在循环中使用 `break` 语句可以消除对某些（标记）变量的使用。下面的 C++ 代码段有助于说明这一思想。（假设所有变量均已正确声明。）

```
sum = 0;
isNegative = false;
cin >> num;
while (cin && !isNegative)
{
    if (num < 0)
        //如果 num 为负数，则终止循环
        // 在本次迭代后
        cout << "Negative number found in the data." << endl;
        isNegative = true;
    }
    else
{
        sum = sum + num;
        cin >> num;
    }
}
```

`while` 循环旨在找到一组正数的和。如果数据包含负数，循环将带有相应的错误信息终止。`while` 循环使用标记变量 `isNegative` 来实现所需的结果。在 `while` 循环之前，变量 `isNegative` 初始化为 `false`。在将 `num` 加到 `sum` 之前，检查 `num` 是否为负数。如果 `num` 为负数，屏幕上会显示错误信息并将 `isNegative` 设置为 `true`。在下一次迭代中，当评估 `while` 语句中的表达式时，它的结果为 `false`，因为 `!isNegative` 为 `false`。（注意 `isNegative` 为 `true`，`!isNegative` 为 `false`。）

下面的 `while` 循环编写时没有使用变量 `isNegative`：

```
sum = 0;
cin >> num;

while (cin)
{
    if (num < 0) //如果 num 为负数，则终止循环
    {
        cout << "Negative number found in the data." << endl;
        break;
    }

    sum = sum + num;
    cin >> num;
}
```

在这个 `while` 循环中，当发现负数时，`if` 语句中的表达式评估为 `true`；在打印适当的消息后，`break` 语句终止循环。（在循环中执行 `break` 语句后，循环中剩余的语句将被忽略。）

> 注意：`break` 语句是避免使用额外变量控制循环并产生优雅代码的有效方法。然而，循环内必须谨慎使用 `break` 语句。在循环中过度使用这些语句会产生难以理解和管理的“面条代码”（具有许多退出条件的循环）。你在使用 `break` 语句时应该小心，并确保其使用使代码更易读还是更不可读。如果你不确定，可以使用 `break` 语句。

`continue` 语句用于 `while`、`for` 和 `do..while` 结构。当 `continue` 语句在循环中执行时，它会跳过循环中的剩余语句并进入循环的下次迭代。在 `while` 和 `do..while` 结构中，表达式（即循环测试）在 `continue` 语句之后立即评估。在 `for` 结构中，更新语句在 `continue` 语句之后执行，然后执行循环条件（即循环继续测试）。

如果之前的程序段遇到负数，`while` 循环将终止。如果你想忽略负数并读取下一个数字而不是终止循环，请将 `break` 语句替换为 `continue` 语句，如下例所示：

```
sum = 0;
cin >> num;

while (cin)
{
    if (num < 0)
    {
        cout << "Negative number found in the data." << endl;
        cin >> num;
        continue;
    }
    sum = sum + num;
    cin >> num;
}
```

前面提到过 C++ 中的三种循环都有其用之地，且一个循环通常可以替代另一个。然而，`continue` 语句的执行是 `while` 和 `do..while` 结构不同于 `for` 结构的地方。当 `while` 或 `do..while` 循环执行 `continue` 时，更新语句可能不会执行。在 `for` 结构中，更新语句始终执行。

### 嵌套控制结构
在本节中，我们将给出示例说明如何使用嵌套循环来实现有用的结果并处理数据。

### 示例 5-21
假设你想创建以下模式：

```
*
**
***
****
*****
```

显然，你想打印五行星号。在第一行，你想打印一个星号；在第二行打印两个星号，依此类推。因为将打印五行，所以从以下 `for` 语句开始：

```
for (i = 1; i <= 5; i++)
```

`i` 在第一次迭代中的值是 1，在第二次迭代中为 2，依此类推。你可以将 `i` 的值作为嵌套在此循环中的另一个 `for` 循环的限制条件，以控制每行星号的数量。经过思考后代码如下：

```
for (i = 1; i <= 5; i++)
{
    for (j = 1; j <= i; j++)
        cout << "*";
    cout << endl;
}
```

对这段代码的分析显示，第1 行的 `for` 循环从 `i = 1` 开始。当 `i` 为 1 时，第3 行的内部 `for` 循环输出一个，插入点移动到下一行。当 `i` 变为 2 时，内部 `for` 循环输出两个星号，第5 行的输出将插入点移动到下一行，依此类推。这个过程持续到 `i` 变为 6 循环停止。

如果你将第1 行的 `for` 语句替换为以下内容，代码会产生什么模式？

```
for (i = 5; i >= 1; i--)
```

### 示例 5-22
假设你想创建以下表格：

```
1 2
3 4 5
6 7 8 9
10 11 12 13 14
15 16 17 18 19 20
```

这个表格有五行。第一行有两个数字，第二行有三个，第三行有四个，第四行五个，第五行六个。第 $i$ 行的元素数量为 $i+1$。为了创建这个表格，我们可以使用嵌套的 `for` 循环：

```
for (i = 1; i <= 5; i++)
{
    int count = 1;
    for (j = 1; j <= i + 1; j++)
    {
        cout << count << " ";
        count++;
    }
    cout << endl;
}
```

在这段代码中，外部 `for` 循环控制行，内部 `for` 循环控制每行打印的元素。`count` 变量跟踪要打印的数字。这种方法允许我们处理每行元素数量变化的表格。

```cpp
counter = 0;
while (counter < 4)
{
    sum = 0;
    infile >> num;
    while (num != -999)
    {
        sum = sum + num;
        infile >> num;
    }
}

cout << "Line " << counter + 1 << ": " << sum << endl;
counter++;
```

### 示例 5-24
假设我们想要处理与示例 5-23 中的数据相似的数据，但输入文件的长度是不指定的。也就是说，每行包含的数据与示例 5-23 中每行的数据相同，但我们不知道输入行的数。

由于我们不知道输入行的数，我们必须使用一个由 EOF（文件结束）控制的循环来处理数据。在这种情况下，所需的代码如下（假设所有变量已正确声明，并且已使用输入流变量打开了输入文件）。

```cpp
counter = 0;
infile >> num;
while (infile)
{
    sum = 0;
    while (num != -999)
    {
        sum = sum + num;
        infile >> num;
    }
}

cout << "Line " << counter + 1 << ": " << sum << endl;
counter++;
infile >> num;
```

注意，我们再次使用了变量 `counter`。之所以这样做唯一的原因是我们想要打印每行的行号和行和。

### 示例 5-25
考虑以下数据：
