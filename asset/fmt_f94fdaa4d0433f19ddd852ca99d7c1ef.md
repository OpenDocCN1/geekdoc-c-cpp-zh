
# 第 5 章 循环与文件

## 程序 5-23（继续）

```cpp
24      // 关闭文件。
25      inputFile.close();
26  }
27  else
28  {
29      // 显示错误消息。
30      cout << "Error opening the file.\n";
31      return 0;
33  }
```

## 程序输出（假设 BadListOfOfNumbers.txt 不存在）

Error opening the file.

让我们仔细观察代码的某些部分。第 12 行调用 `inputFile` 对象的 `open` 成员函数打开文件 ListOfNumbers.txt。然后，第 15 行的语句像测试布尔表达式一样测试 `inputFile` 对象的值。用这种测试时，如果文件成功打开，`inputFile` 对象将给出一个 `true` 值。否则，它将给出一个 `false` 值。输出显示，如果程序无法打开文件，将显示错误消息。

另一种检测打开文件失败的方法是使用 `fail` 成员函数，如下代码所示：

```cpp
ifstream inputFile;
inputFile.open("customers.txt");
if (inputFile.fail()) {
    cout << "Error opening file.\n";
} else {
    // 处理文件。
}
```

当尝试的操作失败时，`fail` 成员函数返回 `true`。在使用 I/O 时，应该始终测试文件对象以确保文件已打开。如果文件无法打开，应该通知用户并由程序采取适当的操作。

## 让用户指定文件名

在之前的每个示例中，打开的文件名都被硬编码为字符串字面量到程序中。在许多情况下，你希望用户指定要打开的文件名。在 C++11，你可以将 `string` 对象作为参数传递给流对象的 `open` 函数。程序 5-24 显示程序 5-23 的修改版本。此版本提示用户输入文件名。在第 15 行，输入存储在名为 `filename` 的字符串对象中。在第 18 行，文件名作为参数传递给 `open` 函数。

## 程序 5-25（续）

## 程序输出（示例输入已加粗显示）

输入一个数字：2 回车
此程序将计算 2 的 0 次方到 10 次方。
2 的 0 次方是 1
输入 Q 退出或按任意键继续。回车
2 的 1 次方是 2
输入 Q 退出或按任意键继续。回车
2 的 2 次方是 4
输入 Q 退出或按任意键继续。回车

## 在嵌套循环中使用 break

在嵌套循环中，`break` 语句只会中断它所在的循环。下面的程序段会在屏幕上显示五行星号。外层循环控制行数，内层循环控制每行星号的数量。内层循环设计显示 20 个星号，但 `break` 语句在第 11 次迭代时停止了它。

```cpp
for (int row = 0; row < 5; row++)
    for (int star = 0; star < 20; star++)
    {
        cout << '*';
        if (star == 10)
            break;
        cout << endl;
    }
```

上述程序段的输出是：

```
**********
**********
************
************
************
```

## continue 语句

`continue` 语句会导致循环的当前迭代立即结束。当遇到 `continue` 时，循环体中位于其之后的所有语句都被忽略，循环准备进入下一次迭代。

在 `while` 循环中，这意味着程序将跳转到循环顶部的测试表达式。按照常例，如果表达式仍为真，则开始下一次迭代。在 `do-while` 循环中，程序跳转到循环底部的测试表达式，该表达式决定了是否开始下一次迭代。在 `for` 循环中，`continue` 会导致执行更新表达式，然后评估测试表达式。

下面的程序段演示了在 `while` 循环中使用 `continue`：

```cpp
int testVal = 0;
while (testVal++ < 10) {
    if (testVal == 4) {
        continue;
        cout << testVal << " ";
    }
}
```

这个循环看起来像是显示整数 1 到 10。然而，当 `testVal` 等于 4 时，`continue` 语句导致循环跳过 `cout` 语句并开始下一次迭代。循环的输出为：

- 1 2 3 4 5 6 7 8 9 10

程序 5-26 演示了 `continue` 语句。程序计算 DVD 租赁费用，其中新发行的价格为 $3.50，其他所有为 $2.50。如果客户租了多张 DVD，每第三张免费。`continue` 语句用于跳过计算每三个 DVD 费用的循环。

## 程序 5-26

```cpp
// 此程序计算 DVD 租赁费用。
// 每第三张 DVD 免费。
#include <iostream>
#include <iomanip>
using namespace std;
int main() {
    int dvdCount = 1; // DVD 计数器
    int numDVDs;
    double total = 0.0; // 加器
    char current; // 当前发行情况，Y 或 N
    // 获取 DVD 数量。
    cout << "How many DVDs are being rented? ";
    cin >> numDVDs;
    // 确定费用。
    do {
        if ((dvdCount % 3) == 0) {
            cout << "DVD " << dvdCount << " is free!\n";
            continue; // 立即开始下一次迭代
        }
        cout << "Is DVD " << dvdCount << " a current release? (Y/N) ";
        cin >> current;
        if (current == 'Y' || current == 'y') {
            total += 3.50;
        } else {
            total += 2.50;
        }
    } while (dvdCount++ < numDVDs);
```

## 程序 5-26（续）

```cpp
    // 显示总额。
    cout << fixed << showpoint << setprecision(2);
    cout << "The total is $" << total << endl;
    return 0;
}
```

## 输出（示例输入已加粗显示）

How many DVDs are being rented? 6 回车
DVD #1 a current release? (Y/N) y 回车
DVD #2 a current release? (Y/N) n 回车
DVD #3 is free!
DVD #4 a current release? (Y/N) n 回车
DVD #5 a current release? (Y/N) y 回车
DVD #6 is free!
The total is $12.00

案例研究：请访问 www.pearsonhighered.com/gaddis 上的计算机科学门户查看贷款摊销案例研究。

## 复习题与练习题

### 简答

1. 为什么应该缩进循环体中的语句？
2. 描述预测试循环（pretest loops）和后测试循环（posttest loops）之间的区别。
3. 为什么循环体中的语句被称为条件执行语句？
4. `while` 循环和 `do-while` 循环之间的区别是什么？
5. 在希望循环重复到测试表达式为假为止，且如果测试表达式为假则不执行循环的情况下，你应该使用哪种循环？
6. 当你知道迭代次数时，应该使用哪种循环？
7. 为什么计数器变量必须初始化？
8. 为什么累加变量必须初始化？
9. 在 `for` 循环中，第一个表达式是初始化，第三个表达式是更新。
10. 执行操作需要哪个头文件？
11. 向文件写入数据时使用哪种数据类型？
12. 从文件读取时使用哪种数据类型？
13. 为什么程序结束时应该关闭文件？
14. 什么是 ________？

### 填空

1. ________ 一个值意味着增加 1，________ 一个值意味着减少 1。
2. 当增减运算符位于操作数之前（左侧）时，使用的是 ________ 模式。
3. 当增减运算符位于操作数之后（右侧）时，使用的是 ________ 模式。
4. 重复执行的语句或块被称为循环的 ________。
5. 循环的每次迭代被称为 ________。
6. 在每次重复之前评估测试表达式的循环是 ________。
7. 在每次重复后评估测试表达式的循环是 ________。
8. 没有停止值的循环是。
9. ________ 是记录循环重复次数的变量。
10. ________ 是在每次迭代中累加的变量。
11. ________ 是标记系列结束的特殊值。
12. ________ 循环至少执行一次。
13. 如果测试表达式为假，________ 和 ________ 循环都不会执行。
14. 在另一个循环内部的循环被称为 ________。
15. ________ 语句导致循环立即终止。
16. ________ 语句跳过迭代中的剩余语句。

## 算法设计

35. 写一个 `while` 循环让用户输入一个数字。将该数字乘以10并将结果存储在变量 `product` 中。只要 `product` 的值小于 100，循环继续进行。
36. 写一个 `do-while` 循环要求用户输入两个数字。这两个数字相加并显示和。询问用户是否再次执行。如果是，则重复循环；否则终止。
37. 写一个循环显示以下数字集：0, 10, 20, 30, 40, 50 ... 1000
38. 写一个循环要求用户输入一个数字。循环执行 10 次，并保持输入数字的运行总和。
39. 写一个嵌套循环显示 10 行 '#' 字符。每行应有 15 个 '#' 字符。

41. 将以下 `do-while` 循环转换为 `while` 循环：
```cpp
char sure;
do{
    cout << "Are you sure you want to quit? ";
    cin >> sure;
} while (sure == 'Y' && sure != 'N');
```

42. 将以下 `while` 循环转换为 `for` 循环：
```cpp
int count = 0;
while (count < 50)
{
    cout << "count is " << count << endl;
    count++;
}
```

43. 将以下循环转换为 `while` 循环：
```cpp
for (int x = 50; x > 0; x--)
{
    cout << x << " seconds to go.\n";
}
```

44. 编写代码实现以下功能：打开一个名为 `Numbers.txt` 的输出文件，使用循环将 1 到 100 的数字写入文件，然后关闭文件。

45. 编写代码实现以下功能：打开第 44 题中创建的 `Numbers.txt` 文件，读取文件中所有的数字并显示它们，然后关闭文件。

46. 修改你在第 45 题中编写的代码，使其累加从文件中读取的所有数字并显示总和。

### 判断对错

- 47. T F 递增运算符和递减运算符的操作数可以可以是任何有效的数学表达式。
- 48. T F 下述程序段中的语句将显示 5：
```cpp
int x = 5;
cout << x;
```
- 49. T F 下述程序段中的语句将显示 5：
```cpp
int x = 5;
cout << ++x;
```
- 50. T F `while` 循环是预测试循环。
- 51. T F `do-while` 循环是预测试循环。
- 52. T F `for` 循环是后测试循环。
- 53. T F 没必要初始化计数器变量的。
- 54. T F `for` 循环的三个表达式都可以省略。
- 55. T F `for` 循环的一个局限性是在初始化表达式中只能初始化变量。
- 56. T F 变量可以在循环体内定义。
- 57. T F 变量可以在 `for` 循环的初始化表达式中定义。
- 58. T F 在嵌套循环中，外层循环的执行速度比内层循环快。
- 59. T F 在嵌套循环中，外层循环每执行一次迭代，内层循环都会完成其所有的迭代。
- 60. T F 要计算嵌套循环的总迭代次数，需要将所有循环的迭代次数相加。
- 61. T F `break` 语句会导致循环停止当前迭代并开始下一次迭代。
- 62. T F `continue` 语句会导致已终止的循环继续执行。
- 63. T F 在嵌套循环中，`break` 语句只会中断它所在的那个循环。
- 64. T F 当你调用 `ofstream` 对象的成员函数时，如果指定的文件已存在，则它将被擦除。

## 找错误

以下每个程序都有错误。请尽可能多地找出。

```cpp
65. // Find此程序中的错误。
#include <iostream>
using namespace std;
int main() {
    int num1 = 0, num2 = 10, result;
    num1++;
    result = +(num1 + num2);
    cout << num1 << " " << num2 << " " << result;
    return 0;
}
```

```cpp
66. // 此程序将用户输入的两个数字。
#include <iostream>
using namespace std;
int main() {
    int num1, num2;
    char again;
    while (again == 'y' || again == 'Y') {
        cout << "Enter a number: ";
        cin >> num1;
        cout << "Enter another number: ";
        cin >> num2;
```
