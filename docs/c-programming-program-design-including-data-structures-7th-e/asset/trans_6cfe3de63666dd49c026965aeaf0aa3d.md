

```cpp
group1.close();                         //Step 14
group2.close();                         //Step 14
outfile.close();                        //Step 14

return 0;
}

void calculateAverage(ifstream& inp, double& courseAvg)
{
    double totalScore = 0.0;
    int numberOfStudents = 0;
    int score;

    inp >> score;
    while (score != -999)
    {
        totalScore = totalScore + score;
        numberOfStudents++;
        inp >> score;
    }//end while

    courseAvg = totalScore / numberOfStudents;
} //end calculateAverage

void printResult(ofstream& outp, string courseId, int groupNo,
                double avg)
{
    if (groupNo == 1)
        outp << " " << courseId << " ";
    else
        outp << "        ";
    outp << setw(8) << groupNo << setw(17) << avg << endl;
} //end printResult
```

## 示例运行：

| 课程编号 | 组号 | 课程平均分 |
|---|---:|---:|
| CSC | 1 | 83.71 |
|  | 2 | 80.82 |
| ENG | 1 | 82.00 |
|  | 2 | 78.20 |
| HIS | 1 | 77.69 |
|  | 2 | 84.15 |
| MTH | 1 | 83.57 |
|  | 2 | 84.29 |
| PHY | 1 | 83.22 |
|  | 2 | 82.60 |

```
Avg for group 1: 82.04
Avg for group 2: 82.01
```

### 输入数据组 1

```
CSC 80 100 70 80 72 90 89 100 83 70 90 73 85 90 -999
ENG 80 90 80 94 90 74 78 63 83 80 90 -999
HIS 90 70 80 70 90 50 89 83 90 68 90 60 -999
MTH 74 80 75 89 90 73 90 82 74 90 84 100 90 79 -999
PHY 100 83 93 80 63 78 88 89 75 -999
```

### 输入数据组 2

```
CSC 90 75 90 75 80 89 100 60 80 70 80 -999
ENG 80 80 70 68 70 78 80 90 90 76 -999
HIS 100 80 80 70 90 76 88 90 90 75 90 85 80 -999
MTH 80 85 85 92 90 90 74 90 83 65 72 90 84 100 -999
PHY 90 93 73 85 68 75 67 100 87 88 -999
```

## 条形图

在商业世界中，公司高管通常喜欢以某种可视化形式查看结果，例如条形图。许多当前可用的软件包可以分析多种形式的数据，然后以可视化形式显示结果，例如条形图或饼图。本程序的第二部分旨在以条形图的形式显示前面得到的结果，如下所示：

```
Course                    Course Average
 ID       0    10    20    30    40    50    60    70    80    90   100
          |....|....|....|....|....|....|....|....|....|....|
CSC       *******************************
ENG       ###################################
          .
          .
          .
Group 1 -- ****
Group 2 -- ####

Avg for group 1: 82.04
Avg for group 2: 82.01
```

条形图中的每个符号（* 或 #）表示两分。如果某门课程的平均分低于 2，则不打印任何符号。

由于输出采用条形图形式，我们需要修改函数 `printResult`。

### 打印条形

函数 `printResult` 打印课程编号以及表示某门课程平均分的条形图。输出存储在文件中。因此，我们必须向该函数传递四个参数：与输出文件关联的 ofstream 变量、组号（用于打印 * 或 #）、课程编号以及该部门的课程平均分。要打印条形图，我们可以使用循环每两分打印一个符号。要计算要打印的符号数量，可以使用整数除法，如下所示：

```
numberOfSymbols = static_cast<int>(average) / 2;
```

例如，`static_cast<int>(78.45) / 2 = 78 / 2 = 39`。如果平均分为 78.45，我们必须打印 39 个符号来表示该平均分。

根据上述讨论，函数 `printResult` 的定义为：

```
void printResult(ofstream& out, string courseID,
                 int groupNo, double avg)
{
    int noOfSymbols;
    int count;

    if (groupNo == 1)
        out << setw(4) << courseID << "    ";
    else
        out << "             ";

    noOfSymbols = static_cast<int>(avg)/2;

    if (groupNo == 1)
        for (count = 1; count <= noOfSymbols; count++)
            out << '*';
    else
        for (count = 1; count <= noOfSymbols; count++)
            out << '#';

    out << endl;
} //end printResult
```

我们还包括一个函数 `printHeading`，用于打印输出的前两行。该函数的定义为：

```
void printHeading(ofstream& out)
{
    out << "Course          Course Average" << endl;
    out << "  ID    0    10    20    30    40    50    60    70";
    out << "    80    90    100" << endl;
    out << "        |....|....|....|....|....|....|....|....|";
    out << "....|....|" << endl;
} //end printHeading
```

替换前面程序中的函数 printResult，加入函数 printHeading，加入输出“Group 1 — ****”和“Group 2 — ####”的语句，然后重新运行程序。你的程序应生成类似于前面所示条形图的条形图。（完整程序清单可在本书配套网站上获得。）

## 快速回顾

- 1. 函数也称为模块，就像微型程序。
- 2. 函数使你能够将程序划分为可管理的任务。
- 3. C++ 系统提供标准（预定义）函数。
- 4. 要使用标准函数，你必须：
  - i. 知道包含该函数规范的头文件名称，
  - ii. 在程序中包含该头文件，并且
  - iii. 知道函数的名称和类型，以及参数（实参）的数量和类型。
- 5. 用户定义函数有两种类型：有返回值函数和 void 函数。
- 6. 在函数首部中定义的变量称为形参。
- 7. 在函数调用中使用的表达式、变量或常量值称为实参。
- 8. 在函数调用中，实参的数量及其类型必须按给定顺序与形参匹配。
- 9. 要调用函数，请使用其名称以及实参列表。
- 10. 有返回值函数会返回一个值。因此，有返回值函数用于（被调用）表达式、输出语句中，或作为函数调用中的参数。
- 11. 用户定义函数的一般语法为：

  ```cpp
  functionType functionName(formal parameter list)
  {
      statements
  }
  ```

- 12. 行 `functionType functionName(formal parameter list)` 称为函数首部（或函数头）。括在花括号（`{` 和 `}`）之间的语句称为函数体。
- 13. 函数首部和函数体称为函数的定义。
- 14. 如果函数没有参数，函数首部和函数调用中仍然需要空圆括号。
- 15. 有返回值函数通过 `return` 语句返回其值。
- 16. 一个函数可以有多个 `return` 语句。但是，每当函数中执行 `return` 语句时，其余语句将被跳过，函数退出。
- 17. `return` 语句只返回一个值。
- 18. 函数原型是去掉函数体的函数首部；函数原型以分号结尾。
- 19. 函数原型声明函数类型，以及函数中使用的参数类型和数量。
- 20. 在函数原型中，形参列表中变量的名称是可选的。
- 21. 函数原型帮助编译器正确翻译每个函数调用。
- 22. 在程序中，函数原型放在每个函数定义之前，包括 main 函数的定义。
- 23. 使用函数原型时，用户定义函数可以以任意顺序出现在程序中。
- 24. 程序执行时，执行总是从 main 函数中的第一条语句开始。
- 25. 函数仅在它们被调用时执行。
- 26. 对函数的调用将控制权从调用者转移到被调用函数。
- 27. 在函数调用语句中，你只指定实参，而不指定它们的数据类型或函数类型。
- 28. 当函数退出时，控制权返回给调用者。
- 29. 没有数据类型的函数称为 void 函数。
- 30. 不带任何值的 `return` 语句可用于 void 函数。如果在 void 函数中使用 `return` 语句，通常用于提前退出函数。
- 31. void 函数的首部以单词 void 开头。
- 32. 在 C++ 中，`void` 是保留字。
- 33. void 函数可以有参数，也可以没有参数。
- 34. 对 void 函数的调用是一条独立语句。
- 35. 要调用 void 函数，请在独立语句中使用函数名称以及实参。
- 36. 形参有两种类型：值形参和引用形参。
- 37. 值形参接收其对应实参的副本。
- 38. 引用形参接收其对应实参的地址（内存位置）。
- 39. 值形参对应的实参是表达式、变量或常量值。
- 40. 常量值不能传递给引用形参。
- 41. 引用形参对应的实参必须是变量。
- 42. 当在形参的数据类型后包含 `&` 时，该形参就成为引用形参。
- 43. 流变量应通过引用传递给函数。

