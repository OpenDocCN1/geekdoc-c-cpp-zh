
```cpp
infile.open("inputdat.dat"); //open inputdat.dat
if (!infile)
{
    cout << "Cannot open the input file. "
    << "The program terminates." << endl;
    return 1;
}
```

假设文件 `inputdat.dat` 不存在。打开该文件的操作失败，导致输入流进入失败状态。作为一个逻辑表达式，流变量 `infile` 的结果为 `false`。因为 `infile` 为 `false`，`if` 语句中的表达式 `!infile` 结果为 `true`，因此执行 `if` 语句体。消息：

Cannot open the input file. The program terminates.

被打印在屏幕上，而 `return` 语句通过向操作系统返回值 `1` 来终止程序。

让我们在第3章的编程示例“学生成绩（Student Grade）”中包含这些特性，以响应输入失败。回想一下，该程序根据输入文件计算平均分，然后将结果输出到另一个文件中。以下编程代码与第3章中的代码相同，不同在于它包含了在输入文件不存在时退出程序的语句。

```cpp
//计算平均测试成绩的程序。
```

```cpp
#include <iostream>
#include <fstream>
#include <iomanip>
#include <string>
using namespace std;

int main()
{
    ifstream infile; //输入文件流变量
    ofstream outFile; //输出文件流变量

    double test1, test2, test3, test4, test5;
    double average;

    string firstName;
    string lastName;

    infile.open("test.txt"); //open input file
    if (!infile)
{
  cout << "Cannot open the input file. "
  << "The program terminates." << endl;
}
```

```cpp
outFile.open("testavg.out"); // open the output file
```

```cpp
outFile << fixed << showpoint;
outFile << setprecision(2);
```

```cpp
cout << "Processing data" << endl;
```

```cpp
inFile >> firstName >> lastName;
outFile << "Student name: " << firstName
  << " " << lastName << endl;
```

```cpp
inFile >> test1 >> test2 >> test3
  << test4 >> test5;
outFile << "Test scores: " << setw(4) << test1
  << setw(4) << test2 << setw(4) << test3
  << setw(4) << test4 << setw(4) << test5
  << endl;
```

```cpp
average = (test1 + test2 + test3 + test4 + test5) / 5.0;
```

```cpp
outFile << "Average test score: " << setw(6)
  << average << endl;
```

```cpp
inFile.close(); nFile.close();
```

```cpp
return 0;
```

## 等于运算符 (`==`) 与赋值运算符 (`=`) 的混淆

回想，如果 `if` 语句中的决策表达式结果为 `true`，则执行 `if` 语句的语句部分。此外，赋值通常是一个逻辑表达式。然而，C++ 允许在 `if` 语句中使用任何可以评估为 `true` 或 `false` 的表达式。考虑以下语句：

```cpp
if (x = 5)
  cout << "The value is five." << endl;
```

`if` 语句中的表达式——即决策——是 `x = 5`。表达式 `x = 5` 是一个赋值表达式，因为表达式中出现了运算符 `=` 且末尾没有分号。

其求值过程如下：首先计算运算符 `=` 的右侧，其结果为 `5`。然后将值 `5` 赋值给 `x`。此外，值 `5`——即 `x` 的新值——也成为了 `if` 语句中表达式的值——即赋值表达式的值。由于 `5` 非零，`if` 语句中的表达式求值为 `true`，因此 `if` 语句的语句输出：The value is five.

无论程序员多么经验丰富，几乎所有人都会某时某地犯下用 `=` 代替 `==` 的错误。这这两个运算符经常被混淆的原因之一是，大多数编程语言使用 `=` 作为等值运算符。因此，在其他编程语言中的经验可能会导致混淆。有时错误仅仅是拼写错误，这也是编写代码时需要小心的另一个原因。

尽管赋值表达式可以作为表达式使用，但用赋值运算符代替等值运算符会导致程序中出现严重问题。例如，假设汽车保险单的折扣基于被保险人的驾驶记录。驾驶记录为 `1` 意味着驾驶员没有事故，可以获得保单 25% 的折扣。该语句：

```cpp
if (drivingCode == 1)
cout << "The discount on the policy is 25.%" << endl;
```

输出：

The discount on the policy is 25.

```cpp
if (drivingCode == 1)
cout << "The discount on the policy is 25.%" << endl;
```

始终输出：

The discount on the policy is 25.

因为赋值表达式的右侧求值为 `1`，它是非零的，因此求值为 `true`。因此，`if` 语句中的表达式求值为 `true`，输出文本行：The discount on the policy is 25.

## 第 4 章章：控制结构 I（选择）

`if` 语句中的表达式求值为 `true`，输出文本行：The discount on the policy is 25.

# 使用伪代码进行程序的开发、测试和调试 | 213

如果 (a) 中的语句为真，则 x 较大。如果 (b) 中的语句为真，则 y 较大。然而，为了让这段代码协同工作以确定两个整数中的较大值，计算机需要评估这些表达式：

```
(x > y)    and    (y > x)
```

即使第一条语句为真也是如此。评估两个表达式是浪费时间。

让我们将这段伪代码重写如下：

```
if (x > y) then
    x is larger
else
    y is larger
```

在这里，只需要评估一个条件。这段代码看起来没问题，所以让我们把它放入 C++ 中吧。

```cpp
#include <iostream>
```

```cpp
using namespace std;
```

```cpp
int main()
{
    if (x > y)
```

等等……一旦你开始将伪代码翻译成 C++ 程序，你就会立即注意到没有可以存储 x 或 y 值的地方。变量没有声明，这是一个常见的疏忽，特别是对于新学者来说。如果你检查这段伪代码，你会发现程序需要三个变量，你也可以让它们具有自文档性。让我们重新开始程序代码：

```cpp
#include <iostream>
```

```cpp
using namespace std;
```

```cpp
int main()
{
    int num1, num2, larger;      //Line 1
    if (num1 > num2)           //Line 2; error
        larger = num1;          //Line 3
    else
        larger = num2;          //Line 4
    return 0;               //Line 5
}
```

编译此程序将识别出第 2 行中常见的语法错误。记住，在 if..else 语句中，表达式后面不能分号。然而，即使你修正了这个语法错误，程序也不会得到满意的结果，因为它尝试使用没有值的标识符。变量没有初始化，这是另一个常见的错误。此外，由于没有输出语句，你无法看到程序的结果。

由于程序中有许多错误，你应该尝试进行走读（walk-through），看看它在任何时候是否能够工作。在走读过程中，你应该始终使用广泛范围的值，以便在尽可能不同的情况下评估程序。例如，如果其中一个数字为零，如果一个为负数另一个为正数，或者如果两个数字相同，此程序可以工作吗？检查程序可以发现它没有检查两个数字是否相等。考虑到所有这些点，你可以重写程序如下：

```cpp
//程序: 比较数字
// 此程序比较两个整数并输出最大的。

#include <iostream>

using namespace std;

int main() {
	int num1, num2;

	cout << "Enter any two integers: ";
	cin >> num1 >> num2;
	cout << endl;

	cout << "The two integers entered are " << num1
		<< " and " << num2 << endl;

	if (num1 > num2) {
		cout << "The larger number is " << num1 << endl;
	} else if (num2 > num1) {
		cout << "The larger number is " << num2 << endl;
	} else {
		cout << "Both numbers are equal." << endl;
	}

	return 0;
}
```

**示例运行：** 在此运行中，用户输入被阴影显示。

Enter any two integers: `78 90`

The two integers entered are 78 and 90

The larger number is 90

你可以从前面的程序中学到的一点是，你必须首先用纸和笔开发程序。虽然先写在纸上的程序并不能保证第一次就能成功运行，但这一步仍然是一个很好的起点。在纸上，更容易发现错误并改进程序，特别是在处理很多程序时。

## switch 结构

回想一下，C++ 中有两种选择（分支）结构。第一种选择结构通过 `if` 和 `if..else` 语句实现，通常需要评估一个（逻辑）表达式。第二不需要评估逻辑表达式的选择结构被称为 `switch` 结构。C++ 的 switch 结构赋予计算机从许多替代方案中选择的能力。

switch 语句的一般语法为：

```
switch (expression)
{
case value1:
    statements1
    break;
case value2:
    statements2
    break;
    .
case value n:
    statementsn
    break;
default:
    statements
}
```

在 C++ 中，`switch`、`case`、`break` 和 `default` 都是关键字。在 switch 结构中，首先评估表达式。然后使用表达式的值来执行在关键字 case 之后的后续语句中指定的动作。记住，在语法中，阴影表示定义中的可选部分。

虽然不一定，但表达式通常是一个标识符。无论它是标识符还是表达式，其值只能是整型的。表达式有时被称为选择器（selector）。switch 结构赋予计算机从许多替代方案中选择的能力。

The larger number is 90。...

The larger number is 90。

你可以从前面的程序中学到的一点是，你必须首先用纸和笔开发程序。虽然先写在纸上的程序并不能保证第一次就能成功运行，但这一步仍然是一个很好的起点。在纸上，更容易发现错误并改进程序，特别是在处理很多程序时。

## switch 结构

回想一下，C++ 中有两种选择（分支）结构。第一种选择结构通过 `if` And `if..else` 语句实现，通常需要评估一个（逻辑）表达式。第二不需要评估逻辑表达式的选择结构被称为 `switch` 结构。C++ 的 switch 结构赋予计算机从许多替代方案中选择的能力。

switch 语句的一般语法为：

```
switch (expression)
{
case value1:
    statements1
    break;
case value2:
    statements2
    break;
    .
case value n:
    statementsn
    break;
default:
    statements
}
```

在 C++ 中，`switch`、`case`、`break` 和 `default` 都是关键字。在 switch 结构中，首先评估表达式。然后使用表达式的值来执行在关键字 case 之后的后续语句中指定的动作。记住，在语法中，阴影表示定义中的可选部分。

虽然不一定，但表达式通常是一个标识符。无论它是标识符还是表达式，其值只能是整型的。表达式有时被称为选择器。

switch 语句根据以下规则执行：

1. 当表达式匹配某个 case 标签时，执行语句，直到找到 break 语句或 switch 结构的结束。

2. 如果 `break` 语句缺失，程序将继续执行后续 case 的语句，这被称为“贯穿”（fall through）。

3. 如果表达式没有匹配任何 case 值，则执行 `default` 语句。

示例 4-22

以下程序展示了 break 语句的影响。它要求用户输入 0 到 10 之间的数字。

```cpp
//程序：switch 结构中的 break 语句
#include <iostream>
using namespace std;
int main()
{
    int num;
    cout << "Enter an integer between 0 and 7: ";
    cin >> num;
    cout << endl;
}
```

# 第 4 章：控制结构 I（选择）

```cpp
cout << "你输入的数字是 " << num
    << endl;

switch (num)
{
    case 0:
    case 1:
        cout << "正在学习";
    case 2:
        cout << "C++";
    case 3:
        cout << " 结构。" << endl;
        break;
    case 4:
        break;
    case 5:
        cout << "此程序展示了 ";
    case 6:
    case 7:
        cout << "break 语句的影响。" << endl;
        break;
    default:
        cout << "数字超出范围。" << endl;
}

cout << "退出 switch 结构。" << endl;

return 0;
```

示例运行：这些输出通过多次运行前面的程序得到的。在这些示例运行中，用户输入被阴影显示。

# 示例运行 4:

输入 0 到 7 之间的整数: 5

你输入的数字是 5

此程序显示了 break 语句的效果。

退出 switch 结构。

# 示例运行 5:

输入 0 到 7 之间的整数: 7

你输入的数字是 7

break 语句的。

退出 switch 结构。

# 示例运行 6:

输入 0 到 7 之间的整数: 8

你输入的数字是 8

数字超出了范围。

退出 switch 结构。

通过使用 switch 表达式 `num` 的特定值对此程序进行逐步演练，可以帮助你理解 break 语句的功能。如果 `num` 的值为 0，则 switch 表达式的值将匹配 case 值 0。case 0: 之后的所有语句将执行，直到出现 break 语句为止。

第一个 break 语句出现在第 13 行，紧接在 case 值 4 之前。即使 switch 表达式的值不匹配任何 case 值（即 1、2 或 3），这些值之后的语句仍然会执行。

当 switch 表达式匹配某个 case 值时，所有语句将执行到 break 为止，程序将跳过所有的 case 标签。同样，如果 `num` 的值为 3，它将匹配 case 值 3，该标签后的语句将执行，直到在第 13 行遇到 break 语句。如果 `num` 的值为 4，它匹配 case 值 4。在这种情况下，操作是空的，只有第 15 行的 break 语句跟在 case 值 4 之后。

示例 2-23

虽然 switch 结构的 case 值（标签）有限，但 switch 表达式可以根据需要变得复杂。例如，考虑以下 switch 语句：
