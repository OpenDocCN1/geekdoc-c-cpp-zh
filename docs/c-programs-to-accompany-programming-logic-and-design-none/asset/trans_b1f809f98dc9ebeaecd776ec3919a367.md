
> **注意** 请注意，在 C++ 中，左花括号（`{`）和右花括号（`}`）用于标记作为循环一部分执行的代码的开始和结束。

根据伪代码，循环体由三条顺序语句组成。第一条语句计算 `inputNumber` 乘以 2；第二条语句打印 `calculatedAnswer`；第三条语句从用户处获取下一个 `inputNumber`。在 C++ 中，我们实际上需要在标记 `while` 循环体的花括号之间添加一条额外语句。这条额外语句提示用户输入下一个要翻倍的数。

在下面的示例中，构成循环体的代码以粗体显示：

```cpp
int main()
{
    cout << "Enter a number to double or 0 to end: " << endl;
    cin >> inputNumber;
    while( inputNumber != 0)
    {
        calculatedAnswer = inputNumber * 2;
        cout << inputNumber << " doubled is " << calculatedAnswer << endl;
        cout << "Enter a number to double or 0 to end: " << endl;
        cin >> inputNumber;
    }
}
```

伪代码的最后一行指示你结束程序。在 C++ 中，`main` 函数的右花括号（`}`）表示 `main` 函数的结束，因此也表示程序的结束。请注意，前面的代码包含两个右花括号。最后一个用于结束 `main` 函数，倒数第二个用于结束 `while` 循环。

我们几乎已经完成将伪代码转换为 C++ 代码。我们只需处理几项收尾工作。正如你在《*编程逻辑与设计（第五版）*》第 3 章中所学，声明变量就是其中一项收尾工作。接下来的代码是用于数字翻倍的完整 C++ 程序。以粗体显示的代码是声明变量的代码。你在本书第 1 章学过的 `#include` 预处理指令和 `using` 语句也以粗体显示。此外，你还会看到 `return 0;` 语句。该语句指示编译器从 `main` 函数返回数值 0。

```cpp
#include <iostream>
using namespace std;
int main()
{
    int inputNumber;
    int calculatedAnswer;
    cout << "Enter a number to double or 0 to end: " << endl;
    cin >> inputNumber;
    while( inputNumber != 0)
    {
        calculatedAnswer = inputNumber * 2;
        cout << inputNumber << " doubled is " << calculatedAnswer << endl;
        cout << "Enter a number to double or 0 to end: " << endl;
        cin >> inputNumber;
    }
    return 0;
}
```

此时，程序已准备好进行编译。假设没有语法错误，它应该按计划执行。尽管你还没有学会自己编写此程序所需的全部知识，但你可以从这个示例中看到，如果你从设计良好、功能完整、结构清晰的流程图或伪代码开始，用 C++ 编写程序会更容易。

## 实验 3-1：使用流程图和伪代码编写 C++ 程序

在本实验中，你将使用图 3-2 中的流程图和伪代码，向一个部分创建的 C++ 程序添加代码。完成后，大学招生人员应能使用该 C++ 程序，根据学生的班级排名来决定是否录取该学生。你在《*编程逻辑与设计（第五版）*》第 2 章中学习过这个流程图和伪代码。

![](img/08ab7b9c5b7606ff5c1616ca55d8b41c_48_0.png)

## 编写结构化 C++ 程序

![](img/08ab7b9c5b7606ff5c1616ca55d8b41c_49_0.png)

```text
start
    read testScore, classRank
    if testScore >= 90 then
        if classRank >= 25 then
            print "Accept"
        else
            print "Reject"
        endif
    else
        if testScore >= 80 then
            if classRank >= 50 then
                print "Accept"
            else
                print "Reject"
            endif
        else
            if testScore >= 70 then
                if classRank >= 75 then
                    print "Accept"
                else
                    print "Reject"
                endif
            else
                print "Reject"
            endif
        endif
    endif
stop
```

![](img/08ab7b9c5b7606ff5c1616ca55d8b41c_49_1.png)

图 3-2 结构化大学录取程序的流程图和伪代码

- 1. 研究图 3-2 中的流程图和伪代码。
- 2. 使用记事本或你选择的文本编辑器打开名为 `CollegeAdmission.cpp` 的源代码文件。
- 3. 声明两个名为 `testScore` 和 `classRank` 的整数变量。
- 4. 编写交互式输入语句，从程序用户处获取学生的考试成绩和班级排名。不要忘记提示用户输入考试成绩和班级排名。
- 5. 程序的其余部分已为你编写好。将此源代码文件保存到你选择的目录中，然后使该目录成为你的工作目录。
- 6. 编译源代码文件 `CollegeAdmission.cpp`。
- 7. 通过输入考试成绩 75 和班级排名 80 来执行程序。记录该程序的输出。
  ____________________________________________________________
- 8. 通过输入考试成绩 80 和班级排名 40 来执行程序。记录该程序的输出。
  ____________________________________________________________

## C++ 注释

在《*编程逻辑与设计（第五版）*》第 3 章中，你学习了**程序注释**，即不会执行的语句。你在 C++ 程序中使用注释向阅读源代码的人解释你的逻辑。C++ 编译器会忽略注释。

在 C++ 中，你可以选择两种注释风格。第一种，在希望编译器忽略的每条注释开头键入两个正斜杠字符（`//`）。当你只想将单行或一行的一部分标记为注释时，这种风格很有用。第二种风格，用 `/*` 和 `*/` 字符括住一组行。当你想要将多行标记为注释时，这种风格很有用。你可以将注释放在 C++ 程序中的任何位置，但不能放在语句内部。

下面的示例展示了添加到上一节数字翻倍程序中的两种注释风格。请注意，程序的前八行组成一个多行块注释，解释程序的一些基本信息。

第二个块注释紧随第一个块注释之后，介绍创建数字翻倍程序的代码。接下来，程序中各处还包含若干单行注释，用于描述程序的各个部分。

> **注意**
> 包含提供程序基本信息的头部注释是一种良好的编程实践。

```cpp
/*
    Program Name: NumberDouble.cpp
    Function: This program doubles a number that is input by
    a user and prints the calculated result on the user's
    screen.
    Input:  Interactive
    Output: The doubled number
*/
#include <iostream>
using namespace std;

/*
The following code creates the number-doubling program. It has a single
function named main.
*/
int main()
{
    // Declaration of variables
    int inputNumber;
    int calculatedAnswer;

    // Prompt user and get interactive user input
    cout << "Enter a number to double: " << endl;
    cin >> inputNumber;

    // Continue until user enters a 0 to end the program
    while( inputNumber != 0)
    {
        // Calculate the number doubled
        calculatedAnswer = inputNumber * 2;
        // Output the result
        cout << inputNumber << " doubled is " << calculatedAnswer << endl;
        // Prompt user and get interactive user input
        cout << "Enter a number to double: " << endl;
        cin >> inputNumber;
    } // End of while loop
    return 0;
} // End of main function
```

> **注意：** 你有责任在编写的所有程序中加入写得良好、有意义的注释。事实上，有些人认为注释源代码与源代码本身同样重要。

接下来，你将看到如何使用流程图和伪代码在 C++ 中编写模块化程序。
