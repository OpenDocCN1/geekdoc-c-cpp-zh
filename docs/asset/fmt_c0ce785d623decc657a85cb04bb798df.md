
## 第 5.3 节 生成数据文件

使用 `sensor3.dat` 文件打印的报告与使用 `sensor1.dat` 或 `sensor2.dat` 输出的报告完全相同。

如果数据文件存在并包含信息，本节中的程序可以正常工作。如果该程序将经常用于处理传感器数据，则应该包含相应的语句以确保文件结构是预期的。此外，如果预期的点数为零，将会发生除零错误。通过在打印报告之前将点数与零进行比较，可以避免除零错误。

这三种文件结构在工程和科学应用中被广泛使用。在这些领域中，处理数据文件时，了解使用的是哪种结构是非常重要的。如果你做出了错误的假设，可能会得到错误的答案而不是错误信息。有时，确定文件结构的唯一方法是打印文件的前几行和最后几行。

![](img/4456642232e4f4a18bd7dfe37e70176d_212_0.png)

在本章开发的程序 `chapter5_3` 中，循环包含一个条件，用于首次测试循环是否被执行。当 `max` 和 `min` 值被初始化为第一个 `motion` 值时。如果与这些程序一起的数据文件非常长，那么执行该选择语句所需的时间可能会变得非常可观。避免这种测试的一种方法是读取第一组数据并初始化进入循环的对象。这可能还需要对程序进行其他更改。

- 1. 修改程序 `chapter5_3`，使其在移除测试循环是否首次执行的条件后仍能正确工作。
- 2. 使用空数据文件运行程序 `chapter5_4`。如果输出错误，请修改程序以纠正该错误。

## 5.3 生成数据文件

生成数据文件与打印报告类似；我们不是将行写入终端，而是将其写入数据文件。然而，在生成数据文件之前，我们必须决定想要使用哪种文件结构。在之前的讨论中，我们展示了最常见的三种文件结构：带有初始记录（给出有效记录数）的文件、带有尾部和哨兵记录（指示有效数据结束）的文件，以及仅包含数据记录而没有特殊起始或结束记录的文件。

所讨论的三种文件结构各有利优缺点。带有尾部的文件易于使用，但在选择尾部大小的值时可能需要更加仔细，以确保它不包含可能出现在有效数据中的值。如果数据文件中的第一条记录包含实际数据的行数，那么在生成文件之前，我们可能知道文件中会有多少行。在执行生成文件的程序之前，确定行数可能并不容易。最简单的生成的是仅包含有效信息的文件，在文件的开头或结尾没有特殊信息。如果文件中的信息将与绘图软件包配合使用，最好使用这种仅包含有效信息的第三种文件结构。

![](img/4456642232e4f4a18bd7dfe37e70176d_212_1.png)

## 第 5 章 处理数据文件

我们展示了一个程序，它是对第 4 章中演示程序的修改，该程序打印了气象球的时间、高度和速度值表格。除了生成显示在屏幕上的信息表格外，我们还将时间、高度和速度信息写入数据文件。将此程序与程序 `chapter_4` 进行比较：

```cpp
// 程序chapter5_
// 此程序为气象球生成一个高度和速度值文件。信息也会打印在报告中。
#include <iostream> // 需要 cin, cout.
#include <fstream> // 需要 ofstream.
#include <iomanip> // 需要 setw().
#include <cmath> // 需要 pow().
#include <string> // 需要 string.
using namespace std;
int main() {
    // 气象球的时间、高度和速度。
    double time, height, velocity, max, min, sum;
    int num_data_pts;
    string filename;
    ofstream report;
    // 提示输入文件名。
    cout << "Enter the name of the data file: ";
    cin >> filename;
    // 打开文件。
    report.open(filename);
    // 检查文件是否打开。
    if(report.fail()) {
        cerr << "Error opening input file\n";
        exit(1);
    }
    // 打开报告文件。
    report.open("sensor3Report.txt");
    // 当未到达文件末尾时。
    // 读取并累积信息
    report >> time >> motion; // 初始化
    while (!report.eof())
    {
        num_data_pts++;
        if (num_data_pts == 1)
        {
            max = min = motion;
        }
        sum += motion;
        if (motion > max)
        {
            max = motion;
        }
        if (motion < min)
        {
            min = motion;
        }
        report >> time >> motion; // 输入下一个
    }
    // 设置格式标志。
    report.setf(ios::fixed);
    report.setf(ios::showpoint);
    report.precision(2);
    // 输出摘要信息。
    report << "Number of sensor readings: " 
        << num_data_pts << endl
        << "Average reading: " 
        << sum/num_data_pts << endl
        << "Maximum reading: " 
        << max << endl
        << "Minimum reading: " 
        << min << endl;
    // 关闭文件并退出程序。
    report.close();
    report.close();
    return 0;
}
// 结束 main
```

```cpp
if(sensor3.fail())
{
    cerr << "Error opening input file\n";
    exit(1);
}
```

```cpp
// 打开报告文件。
report.open("sensor3Report.txt");
// 当未到达文件末尾时。
// 读取并累积信息
sensor3 >> time >> motion; // 初始化
while (!sensor3.eof())
{
    num_data_pts++;
    if (num_data_pts == 1)
    {
        max = min = motion;
    }
    sum += motion;
    if (motion > max)
    {
        max = motion;
    }
    if (motion < min)
    {
        min = motion;
    }
    sensor3 >> time >> motion; // 输入下一个
}
```

```cpp
// 设置格式标志。
report.setf(ios::fixed);
report.setf(ios::showpoint);
report.precision(2);
// 输出摘要信息。
report << "Number of sensor readings: " 
    << num_data_pts << endl
    << "Average reading: " 
    << sum/num_data_pts << endl
    << "Maximum reading: " 
    << max << endl
    << "Minimum reading: " 
    << min << endl;
// 关闭文件并退出程序。
sensor3.close();
report.close();
return 0;
}
// 结束 main
```
