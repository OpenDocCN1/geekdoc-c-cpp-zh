

读取并汇总投票数据的代码如下：

```cpp
sum = 0;                         //Line 6
infile >> num;                   //Line 7; read the first number
while (num != -999)              //Line 8
{                                //Line 9
    sum = sum + num;             //Line 10; update sum
    infile >> num;               //Line 11; read the next number
}                                //Line 12
```

现在我们可以编写如下嵌套循环来处理数据：

```cpp
infile >> ID;                    //Line 1
while (infile)                   //Line 2
{                                //Line 3
    infile.get(ch);              //Line 4
    getline(infile, name);       //Line 5
    sum = 0;                     //Line 6
    infile >> num;               //Line 7; read the first number
    while (num != -999)          //Line 8
    {                            //Line 9
        sum = sum + num;         //Line 10; update sum
        infile >> num;           //Line 11; read the next number
    }

    cout << "Name: " << name
         << ", Votes: " << sum
         << endl;                //Line 12
    infile >> ID;                //Line 13; begin processing the next line
}
```

## 避免补丁，从而避免错误

前面章节中的调试部分展示了如何调试语法错误和逻辑错误，以及如何避免对概念的一知半解。在本节中，我们将说明如何避免使用软件补丁来修复代码。软件补丁是编写在现有代码之上的一段代码，用于修复原代码中的错误。

假设文件 `Ch5_LoopWithBugsData.txt` 中包含以下数据。

```text
87 78 83 94
23 89 92 70
92 78 34 56
```

目标是求出每一行数字的总和。对于每一行，输出这些数字及其总和。让我们考虑以下程序：

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

        cout << " sum = " << sum << endl;
    }

    return 0;
}
```

### 示例运行：

```text
87 78 83 94 sum = 342
23 89 92 70 sum = 274
92 78 34 56 sum = 260
56 56 56 56 sum = 224
```

示例运行表明程序中存在错误，因为文件中包含三行输入，而输出却包含四行。此外，最后一行中的数字 56 重复了四次。显然，程序中存在错误，我们必须修复代码。一些程序员，尤其是初学者，会通过添加软件补丁来处理问题的表象。在这种情况下，输出应该只有三行。初学者程序员可能会通过添加软件补丁来手动截断不需要的第四行，如下面的修改后程序所示：

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

显然，程序现在可以正确运行了。

正如我们所见，程序员只是观察到了现象，并通过添加软件补丁来解决问题。然而，如果你查看代码，不仅程序执行了多余的语句，而且这也是对概念一知半解的一个例子。看来程序员并没有很好地理解为什么之前的程序输出四行而不是三行。添加补丁消除了现象，但这是一种糟糕的编程实践。程序员必须弄清程序为什么会输出四行。仔细查看程序，我们可以发现产生四行的原因在于外层循环执行了四次。循环控制变量 i 被赋值为 1、2、3 和 4。这是典型的“差一错误”的例子。（在“差一错误”中，循环要么多执行一次，要么少执行一次。）我们可以通过正确设置循环控制变量的值来消除这个问题。例如，我们可以将循环重写如下：

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

这段代码修复了原始问题，而且没有使用软件补丁。这也代表了良好的编程实践。完整的修改后程序可在本书附带的网站上获取，文件名为 `Ch5_LoopWithBugsCorrectedProgram.cpp`。

## 调试循环

正如我们在前面的调试部分中所看到的，无论程序的设计和编码多么仔细，错误仍有可能发生。如果存在语法错误，编译器会将其识别出来。但如果是逻辑错误，我们必须仔细检查代码，甚至可能需要检查设计，并设法找出错误。为了提高程序的可靠性，必须在程序发布给用户之前发现并修复错误。

算法编写完成后，下一步是验证其是否正常运行。如果算法是简单的顺序流程或包含分支，则可以手工跟踪，或者使用 IDE 提供的调试器（如果有的话）。通常，循环更难调试。可以通过使用循环不变量来验证循环的正确性。循环不变量是在每次执行循环体时都保持为真的一组语句。设 p 为循环不变量，q 为循环语句中的（逻辑）表达式。那么 p && q 在每次循环迭代之前保持为真，而 p && not(q) 在循环终止后为真。关于循环不变量的完整讨论超出了本书的范围。不过，你可以在《离散数学：理论与应用（修订版）》（D.S. Malik 和 M.K. Sen 著，Cengage Learning Asia，新加坡，2010）一书中了解循环不变量。在此，我们给出一些可用于调试循环的提示。

如前所述，与循环相关的最常见错误是差一错误。如果循环变成了无限循环，那么错误很可能出在控制循环执行的逻辑表达式中。请仔细检查逻辑表达式，看看是否颠倒了不等式、赋值语句符号是否出现在相等运算符的位置，或者 `&&` 是否出现在 `||` 的位置。如果循环会改变变量的值，你可以在每次迭代之前和/或之后打印变量的值，或者使用 IDE 的调试器（如果有的话）在每次迭代期间监视变量的值。

本书中的调试部分旨在帮助你理解调试过程。然而，你也会意识到，调试可能是一个令人厌烦的过程。如果你的程序非常糟糕，不要调试。扔掉它，重新开始。

## 快速回顾

- 1. `C++` 有三种循环（重复）结构：`while`、`for` 和 `do...while`。
- 2. `while` 语句的语法是：

    ```cpp
    while (expression)
        statement
    ```

- 3. 在 `C++` 中，`while` 是保留字。
- 4. 在 `while` 语句中，表达式（决策者）两边的括号很重要；它们标记表达式的开始和结束。
- 5. `statement` 称为循环体。
- 6. `while` 循环体必须包含一条最终将表达式置为 `false` 的语句。
- 7. 计数器控制的 `while` 循环使用计数器来控制循环。
- 8. 在计数器控制的 `while` 循环中，必须在循环之前初始化计数器，并且循环体必须包含一条改变计数器变量值的语句。
- 9. 哨兵是一个特殊值，用于标记输入数据的结束。哨兵必须与所有数据项相似但又有所不同。
- 10. 哨兵控制的 `while` 循环使用哨兵来控制循环。`while` 循环一直执行，直到读入哨兵为止。
- 11. EOF 控制的 `while` 循环使用文件结束标记来控制循环。`while` 循环一直执行，直到程序检测到文件结束标记。
- 12. 在 Windows 控制台环境中，使用 `Ctrl+Z`（按住 Ctrl 键并按 Z）输入文件结束标记。在 UNIX 环境中，使用 `Ctrl+D`（按住 Ctrl 键并按 D）输入文件结束标记。
- 13. `for` 循环简化了计数器控制 `while` 循环的编写。
- 14. 在 `C++` 中，`for` 是保留字。
- 15. `for` 循环的语法是：

    ```cpp
    for (initialize statement; loop condition; update statement)
        statement
    ```

    `statement` 称为 `for` 循环的循环体。

- 16. 在 `for` 循环末尾（循环体之前）加上分号是一个语义错误。在这种情况下，`for` 循环的动作是空的。

