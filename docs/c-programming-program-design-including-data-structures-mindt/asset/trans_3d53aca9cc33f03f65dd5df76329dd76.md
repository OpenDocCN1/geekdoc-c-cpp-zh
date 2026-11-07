
现在，我们可以编写以下嵌套循环来按如下方式处理数据：

```cpp
infile >> ID;                //Line 1
while (infile)               //Line 2
{                            //Line 3
    infile.get(ch);          //Line 4
    getline(infile, name);   //Line 5
    sum = 0;                 //Line 6
    infile >> num;           //Line 7; read the first number
    while (num != -999)      //Line 8
    {                        //Line 9
        sum = sum + num;     //Line 10; update sum
        infile >> num;       //Line 11; read the next number
    }
    cout << "Name: " << name
         << ", Votes: " << sum
         << endl;            //Line 12
    infile >> ID;            //Line 13; begin processing the next line
}
```

## 通过避免补丁来避免错误

前几章中的调试部分说明了如何调试语法错误和逻辑错误，以及如何避免一知半解的概念。在本节中，我们将说明如何避免使用软件补丁来修复代码。软件补丁是在现有代码之上编写的一段代码，旨在修复原始代码中的错误。

假设文件 Ch5_LoopWithBugsData.txt 中包含以下数据。

```text
87 78 83 94
23 89 92 70
92 78 34 56
```

目标是求每一行中数字的和。对于每一行，输出这些数字及其和。让我们考虑以下程序：

```cpp
#include <iostream>
#include <fstream>

using namespace std;

int main()
{
    ifstream infile;

    int i;
    int j;
    int sum;
    int num;

    infile.open("Ch5_LoopWithBugsData.txt");

    for (i = 1; i <= 4; i++)
    {
        sum = 0;

        for (j = 1; j <= 4; j++)
        {
            infile >> num;
            cout << num << " ";
            sum = sum + num;
        }

        cout << "sum = " << sum << endl;
    }

    return 0;
}
```

### 示例运行：

```text
87 78 83 94  sum = 342
23 89 92 70  sum = 274
92 78 34 56  sum = 260
56 56 56 56  sum = 224
```

示例运行表明程序中存在错误，因为文件包含三行输入，而输出包含四行。此外，最后一行的数字56重复了四次。显然，程序中存在错误，我们必须修复代码。有些程序员，尤其是一些初学者，通过添加软件补丁来处理问题的症状。在这种情况下，输出应只包含三行。初学者可能会通过添加软件补丁来手动截去不需要的第四行，从而修复代码，如下面的修改后程序所示：

```cpp
#include <iostream>
#include <fstream>

using namespace std;

int main()
{
    ifstream infile;

    int i;
    int j;
    int sum;
    int num;

    infile.open("Ch5_LoopWithBugsData.txt");

    for (i = 1; i <= 4; i++)
    {
        sum = 0;

        if (i != 4)        //software patch
        {
            for (j = 1; j <= 4; j++)
            {
                infile >> num;
                cout << num << " ";
                sum = sum + num;
            }

            cout << "sum = " << sum << endl;
        }
    }
    return 0;
}
```

### 示例运行：

```text
87 78 83 94  sum = 342
23 89 92 70  sum = 274
92 78 34 56  sum = 260
```

显然，程序现在运行正确。

正如我们所见，程序员只是观察到了症状，并通过添加软件补丁来解决问题。然而，如果查看代码，程序不仅执行了多余的语句，它还是一个一知半解概念的示例。看来程序员并没有很好地理解为什么先前的程序产生四行而不是三行。添加补丁消除了症状，但这是一种糟糕的编程实践。程序员必须弄清楚为什么程序会产生四行。仔细查看程序，我们可以看到产生四行是因为外层循环执行了四次。赋给循环控制变量 i 的值是1、2、3和4。这是经典的“差一”（off-by-one）问题的示例。（在“差一”问题中，循环要么多执行一次，要么少执行一次。）我们可以通过正确设置循环控制变量的值来消除这个问题。例如，我们可以将循环重写如下：

```cpp
for (i = 1; i <= 3; i++)
{
    sum = 0;

    for (j = 1; j <= 4; j++)
    {
        infile >> num;
        cout << num << " ";
        sum = sum + num;
    }

    cout << "sum = " << sum << endl;
}
```

## 调试循环

这段代码在不使用软件补丁的情况下修复了原始问题。它也体现了良好的编程实践。完整的修改后程序可在本书配套网站上获得，名称为 Ch5_LoopWithBugsCorrectedProgram.cpp。

正如我们在前面的调试部分中所见，无论程序设计和编码得多么仔细，错误都可能发生。如果存在语法错误，编译器会识别它们。然而，如果存在逻辑错误，我们必须仔细查看代码，甚至可能查看设计，并尝试找出错误。为了提高程序的可靠性，必须在程序发布给用户之前发现并修复错误。

算法编写完成后，下一步是验证它能否正确工作。如果算法是简单的顺序流程或包含分支，可以手工追踪，也可以使用 IDE 提供的调试器（如果有）。通常，循环更难调试。循环的正确性可以通过使用循环不变式来验证。循环不变式是一组语句，每次执行循环体时都保持为真。设 `p` 为循环不变式，`q` 为循环语句中的（逻辑）表达式。那么，在循环的每次迭代之前，`p && q` 保持为真；在循环终止之后，`p && !(q)` 为真。关于循环不变式的完整讨论超出了本书的范围。不过，你可以在《*离散数学：理论与应用（修订版）*》，D.S. Malik 和 M.K. Sen，Cengage Learning Asia，新加坡，2010 一书中学习循环不变式。这里，我们给出一些可用于调试循环的提示。

正如上一节所讨论的，与循环相关的最常见错误是差一错误。如果循环变成无限循环，错误很可能出在控制循环执行的逻辑表达式中。仔细检查逻辑表达式，看看是否把不等号写反了，是否在应使用相等运算符的地方出现了赋值语句符号，或者是否在应使用 `||` 的地方出现了 `&&`。如果循环改变了变量的值，你可以在每次迭代之前和/或之后打印变量的值，或者使用 IDE 的调试器（如果有），并在每次迭代期间观察变量的值。

本书中的调试部分旨在帮助你理解调试过程。然而，你会意识到，调试可能是一个令人疲惫的过程。如果你的程序非常糟糕，不要调试它。把它扔掉，重新开始。

## 快速回顾

- 1. C++ 有三种循环（重复）结构：`while`、`for` 和 `do...while`。
- 2. `while` 语句的语法是：
  
  ```cpp
  while (expression)
      statement
  ```
- 3. 在 C++ 中，`while` 是保留字。
- 4. 在 `while` 语句中，`expression`（决策者）两边的圆括号很重要；它们标记表达式的开始和结束。
- 5. `statement` 称为循环体。
- 6. `while` 循环的循环体必须包含一条最终将表达式设置为 `false` 的语句。
- 7. 计数器控制的 `while` 循环使用计数器来控制循环。
- 8. 在计数器控制的 `while` 循环中，必须在循环之前初始化计数器，并且循环体必须包含一条改变计数器变量值的语句。
- 9. 哨兵是一个特殊值，用于标记输入数据的结束。哨兵必须与所有数据项相似，但又有所不同。
- 10. 哨兵控制的 `while` 循环使用哨兵来控制循环。`while` 循环继续执行，直到读入哨兵。
- 11. EOF 控制的 `while` 循环使用文件结束标记来控制循环。`while` 循环继续执行，直到程序检测到文件结束标记。
- 12. 在 Windows 控制台环境中，使用 `Ctrl+z`（按住 `Ctrl` 键并按 `z`）输入文件结束标记。
- 13. `for` 循环简化了计数器控制的 `while` 循环的编写。
- 14. 在 C++ 中，`for` 是保留字。
- 15. `for` 循环的语法是：
  
  ```cpp
  for (initialize statement; loop condition; update statement)
      statement
  ```
  
  `statement` 称为 `for` 循环的循环体。
- 16. 在 `for` 循环末尾（`for` 循环体之前）放置分号是一个语义错误。在这种情况下，`for` 循环的动作是空的。
- 17. `do...while` 语句的语法是：
  
  ```cpp
  do
      statement
  while (expression);
  ```
  
  `statement` 称为 `do...while` 循环的循环体。
- 18. `while` 和 `for` 循环都称为前测试循环。`do...while` 循环称为后测试循环。
- 19. `while` 和 `for` 循环的循环体可能根本不执行，但 `do...while` 循环体总是至少执行一次。
- 20. 在循环体中执行 `break` 语句会立即终止循环。
- 21. 在循环体中执行 `continue` 语句会跳过循环剩余的语句，并继续下一次迭代。

