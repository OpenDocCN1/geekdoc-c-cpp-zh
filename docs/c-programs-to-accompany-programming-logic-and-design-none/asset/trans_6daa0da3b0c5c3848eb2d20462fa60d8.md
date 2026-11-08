
```cpp
30  else
31  {
32      cout << "Enter the book's author: ";
33      cin >> author;
34      cout << "Enter the book's category: ";
35      cin >> category;
36      cout << "Enter the book's price: ";
37      cin >> price;
38      prevCategory = category;
39  }
40  while(notDone == true)
41  {
42      if(category != prevCategory)
43      {
44          grandTotal = categoryChange(categoryTotal, grandTotal);
45          categoryTotal = 0;
46          prevCategory = category;
47      }
48      categoryTotal++;
49      cout << "\t\t\t\t\t" << title << endl;
50      cout << "Enter a book title or done to quit: ";
51      cin >> title;
52      if(title == SENTINEL)
53      {
54          notDone = false;
55      }
56      else
57      {
58          cout << "Enter the book's author: ";
59          cin >> author;
60          cout << "Enter the book's category: ";
61          cin >> category;
62          cout << "Enter the book's price: ";
63          cin >> price;
64      }
65  }
66  cout << "\t\t\t\t\t" << CATEGORY_FOOTER << categoryTotal << endl;
67  grandTotal += categoryTotal;
68  cout << "\t\t\t\t\t" << FOOTER << grandTotal << endl;
69  return 0;
70  } // End of main function
71
72  // categoryChange function
73  int categoryChange(int categoryTotal, int grandTotal)
74  {
75      const string CATEGORY_FOOTER = "Category count ";
76
77      cout << "\t\t\t\t\t" << CATEGORY_FOOTER << categoryTotal << endl;
78      grandTotal += categoryTotal;
79      return(grandTotal);
80  } // End of categoryChange function
```

**图 8-3** 用 C++ 编写的书店程序（*续*）

正如你在图 8-3 中看到的，这个 C++ 程序从第 1 行开始，用注释描述程序的功能。（请记住，此程序中显示的行号不是 C++ 代码的一部分。它们仅用于参考。）程序还包含描述程序输入和输出的注释。接下来是第 6 行和第 7 行的两条预处理指令、第 8 行的 `using namespace std;` 语句，以及第 9 行的 `categoryChange` 函数声明。注意，`categoryChange` 函数返回一个 `int`，并接受两个 `int` 作为参数。开始 `main` 函数的 C++ 代码位于第 10 行。

在 `main` 函数内，第 12 行到第 23 行声明变量和常量，在适当的时候初始化它们，然后打印报表标题。第 23 行的 `cout` 语句在生成的输出中包含字符串“\t\t\t\t\t\t”。在 C++ 中，“\t”表示制表符。因此，字符串“\t\t\t\t\t\t”表示由六个制表符组成的字符串。在 `cout` 语句中包含此字符串会强制将行缩进六个制表符。这意味着语句 `cout << "\t\t\t\t\t\t" << HEADING << endl;` 在打印常量 `HEADING` 和换行符之前缩进六次。

下一步是执行一次预读，以获取第一条输入记录，该记录由单本书的书名、作者、价格和类别组成。你已在本书第 3 章和 *《编程逻辑与设计（第五版）》* 第 2 章中学习过如何执行预读。

注意，预读中的 C++ 代码（第 24 行和第 25 行）与伪代码略有不同。当要求用户输入书名时，还会指示用户在输入记录后输入单词“done”。此外，第 26 行使用 `if` 语句测试用户输入的是书名还是单词“done”。如果用户已完成记录输入，此测试的结果将为 `true`，导致第 28 行将 `bool` 值 `false` 赋给名为 `notDone` 的变量，并且询问作者、类别和价格的其余输入语句将不会执行。名为 `notDone` 的 `bool` 变量稍后在程序中用于控制 `while` 循环。如果用户尚未完成记录输入，则提示他在第 32 行到第 37 行输入书籍的其余数据：作者、类别和价格。在第 38 行，当前书籍类别（`category`）的值被赋给名为 `prevCategory` 的变量。变量 `category` 用作控制中断变量。

> **注意** 为简单起见，此示例程序只允许用户输入单字书名和作者的姓氏。这种简化旨在使输入保持简单直接。输入包含多个单词的字符串涉及学习 C++ 的一些复杂细节，你将在学习 C++ 课程时接触到这些内容。

接下来是 `while` 循环（第 40 行），只要 `bool` 变量 `notDone` 的值为 `true`，它就会继续执行。在 `while` 循环体内，`if` 语句在第 42 行测试控制中断变量 `category`。`if` 语句的作用是确定用户当前处理的记录是否与上一条记录的类别相同。如果不同，则表示新类别的开始。因此，程序调用 `categoryChange` 函数（第 44 行），即控制中断函数。注意，此函数的返回值被赋给名为 `grandTotal` 的变量，并且两个参数 `categoryTotal` 和 `grandTotal` 被传递给该函数。

`categoryChange` 函数从第 73 行开始，执行以下操作：

- 1. 打印六个制表符，然后打印名为 `CATEGORY_FOOTER` 的局部常量的值和 `categoryTotal` 的值，其中 `categoryTotal` 包含当前类别的书籍数量（第 77 行）。
- 2. 将 `categoryTotal` 的值加到 `grandTotal`，后者是用于累计所有书籍总数的变量（第 78 行）。
- 3. 将 `grandTotal` 的值（第 79 行）返回到 `main` 函数中调用 `categoryChange` 函数的位置（第 44 行）。

当 `categoryChange` 函数执行完毕后，会发生以下情况：

- 该函数的返回值在第 44 行被赋给名为 `grandTotal` 的变量，从而更新书籍总数。
- 名为 `categoryTotal` 的变量被赋值为 0，以便为新类别的开始做准备（第 45 行）。
- 前一类别变量 `prevCategory` 被赋为当前类别（`category`）的值，以便为新类别做准备（第 46 行）。

下一条要执行的语句（第 48 行）将名为 `categoryTotal` 的类别计数器变量加 1。重要的是要理解，无论类别发生变化还是未发生变化，此语句都会执行。最后，第 49 行到第 64 行打印当前书籍的书名，然后使用与预读相同的技术获取下一本书的输入数据。随后再次测试第 40 行 `while` 循环中的条件，使循环继续执行，直到用户输入单词“done”而不是书名。

退出 `while` 循环后，程序执行最后一部分。这部分包括：

- 在第 66 行打印六个制表符，然后打印名为 `CATEGORY_FOOTER` 的局部常量的值以及 `categoryTotal` 的值（即用户输入的最后一个类别的总计）。
- 在第 67 行将 `categoryTotal` 的值加到名为 `grandTotal` 的变量。
- 在第 68 行打印六个制表符，然后打印名为 `FOOTER` 的局部常量的值以及 `grandTotal` 的值，后者现在包含书店所经营所有书籍的总数。

既然你已经看到了一个单层控制中断程序，在下一节中，你将学习如何编写多层控制中断 C++ 程序。

![](img/08ab7b9c5b7606ff5c1616ca55d8b41c_164_0.png)

## 练习 8-1：在单层控制中断程序中累计总计

在本练习中，你将运用所学到的关于在单层控制中断程序中累计总计的知识来回答具体问题。首先，研究下面的 C++ 代码：

```cpp
if(itemNum != oldItemNum)
{
    cout << "Item Number " << oldItemNum << endl;
    totalItems = itemNum;
    oldItemNum = itemNum;
}
```

- 1. 什么是控制中断变量？
- 2. 控制中断变量的值绝不应被更改。对还是错？
- 3. totalItems 的计算正确吗？

  如果不正确，你如何修复代码？
- 4. 在控制中断程序中，输入文件中的记录是否按指定顺序排列并不重要。对还是错？

## 实验 8-1：在单层控制中断程序中累计总计

在本实验中，你将运用所学到的关于在单层控制中断程序中累计总计的知识来完成一个 C++ 程序。该程序应为一家快餐店老板生成一份报告，帮助她跟踪兼职员工的工作小时数。报告应包括星期几、每位员工在每周每天的工作小时数、当天（星期几）的总小时数，以及在周末时该周的总工作小时数。报告应类似于图 8-4 中所示的报告。
