

ifstream sensor3;
ofstream report;

// Prompt user for name of input file.
cout << "Enter the name of the input file";
cin >> filename;

// Open file and read the first data point.
sensor3.open(filename);
if (sensor3.fail())
{
    cerr << "Error opening input file\n";
    exit(1);
}

// open report file.
report.open("sensor3Report.txt");

// While not at the end of the file,
// read and accumulate information
sensor3 >> time >> motion; // initial input
while ( !sensor3.eof() )
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
    sensor3 >> time >> motion; // input next
}

// Set format flags.
report.setf(ios::fixed);
report.setf(ios::showpoint);
report.precision(2);

// Print summary information.
report << "Number of sensor readings: "
       << num_data_pts << endl
       << "Average reading: "
       << sum/num_data_pts << endl
       << "Maximum reading: "
       << max << endl
       << "Minimum reading: "
       << min << endl;
// Close file and exit program.
sensor3.close();
report.close();
return 0;
} //end main
/*--------------------------------------------------------------*/

使用 sensor3.txt 文件打印的报告与使用 sensor1.txt 或 sensor2.txt 打印的报告完全相同。

本节中的程序在数据文件存在且包含预期信息时可正常工作。如果该程序将常规用于传感器数据，则应包含语句以确保文件结构为预期结构。此外，如果点数为零，将发生除以零错误。可以通过在打印报告前将点数与零进行比较来避免除以零错误。

这三种文件结构在工程和科学应用中都很常用。因此，在处理数据文件时，了解使用的是哪种结构非常重要。如果假设错误，可能会得到错误答案而不是错误消息。有时，确定文件结构的唯一方法是打印文件的前几行和最后几行。

## 修改 5.2

在本章开发的程序 chapter5_3 中，循环包含一个条件，用于测试循环是否第一次执行。当条件为真时，max 和 min 值被初始化为第一个 motion 值。如果与这些程序一起使用的数据文件非常长，执行此选择语句所需的时间可能会变得相当可观。避免此测试的一种方法是在进入循环之前读取第一组数据并初始化对象。此更改可能还需要对程序进行其他更改。

- 1. 修改程序 chapter5_3，以便在移除测试循环是否第一次执行的条件后，它仍能正确工作。
- 
- 2. 使用空数据文件运行程序 chapter5_4。如果输出有误，请修改程序以纠正错误。

## 5.3 生成数据文件

生成数据文件类似于打印报告；不同之处在于，我们不是将行写入终端屏幕，而是将其写入数据文件。但在生成数据文件之前，我们必须决定要使用哪种文件结构。在前面的讨论中，我们介绍了三种最常见的文件结构：带有给出后续有效记录数量的初始记录的文件、带有尾记录或哨兵记录以指示有效数据结束的文件，以及仅包含有效数据记录且没有特殊开始或结束记录的文件。

所讨论的三种文件结构各有优缺点。带有尾信号的文件使用简单，但为尾信号选择值时必须小心，以免其包含可能出现在有效数据中的值。如果数据文件中的第一条记录将包含实际数据的行数，那么在开始生成文件之前，我们必须知道文件中将有多少行数据。在执行生成文件的程序之前，确定行数可能并不总是容易。最简单的生成文件是仅包含有效信息、文件开头和结尾没有特殊信息的文件。如果文件中的信息将与绘图包一起使用，通常最好使用仅包含有效信息的第三种文件结构。

我们现在介绍一个程序，它是第4章中介绍的打印气象气球时间、高度和速度值表格的程序的修改版。除了生成在屏幕上显示的信息表格外，我们还将时间、高度和速度信息写入数据文件。将此程序与程序 chapter4-8 进行比较：

/**--------------------------------*/
/* Program chapter5_5 */
/* */
/* This program generates a file of height and */
/* velocity values for a weather balloon. The */
/* information is also printed in a report. */
/* */

#include <iostream> //Required for cin, cout.
#include <fstream> //Required for ofstream.
#include <iomanip> //Required for setw().
#include <cmath> //Required for pow().
#include <string> //Required for string.
using namespace std;

int main()
{
    // Declare and initialize objects.
    double initial, increment, final, time, height,
    velocity, max_time(0), max_height(0);
    int loops, itime;
    string filename;
    ofstream balloon;

    // Prompt user for name of output file.
    cout << "Enter the name of the output file";
    cin >> filename;

    // Open output file
    balloon.open(filename);

    // Get user input.
    cout << "Enter initial value for table (in hours) \n";
    cin >> initial;
    cout << "Enter increment between lines (in hours) \n";
    cin >> increment;
    cout << "Enter final value for table (in hours) \n";
    cin >> final;

    // Set format flags for standard output.
    cout.setf(ios::fixed);
    cout.precision(2);

    // Set format flags for file output.
    balloon.setf(ios::fixed);
    balloon.precision(2);

    // Print report heading.
    cout << "\n\nWeather Balloon Information \n";
    cout << "Time Height Velocity \n";
    cout << " (hrs) (meters) (meters/s) \n";

    // Determine number of iterations required.
    // Use integer index to avoid rounding error.
    loops = (int)((final - initial)/increment);
    for (itime=0; itime<=loops; itime++)
    {
        time = initial + itime*increment;
        height = -0.12*pow(time,4) + 12*pow(time,3)
        - 380*time*time + 4100*time + 220;
        velocity = -0.48*pow(time,3) + 36*time*time
        - 760*time + 4100;

        // Print report information to the screen.
        cout << setw(6) << time << setw(10) << height
        << setw(10) << velocity/3600 << endl;

        // Write report information to a file.
        balloon << setw(6) << time << setw(10) << height
        << setw(10) << velocity/3600 << endl;

        if (height > max_height)
        {
        max_height = height;
        max_time = itime;
        }
    }

    // Report maximum height and corresponding time.
    cout << "\n\nMaximum balloon height was "
    << setw(8) << max_height
    << " meters\nand it occurred at "
    << setw(6) << max_time << endl;

    // Close file and exit program.
    balloon.close();
    return 0;
}
/*-------------------------------------------------------------*/

使用本程序生成的数据文件的前几行如下（初始时间为0小时，增量为0.5小时，最终时间为48小时）：

0.00 220.00 1.14
0.50 2176.49 1.04
1.00 3951.88 0.94
...

该文件采用易于使用诸如 MATLAB 之类的包进行绘图的形式（如附录 C 中所述）；第 4 章中的图 4.9 显示了此特定文件的图表。

## 修改 5.3

- 1. 修改程序 chapter5_5，使其生成一个文件，其中数据文件的最后一行包含时间、高度和速度的负值。
- 2. 修改程序 chapter5_5，使其生成一个文件，其中第一行包含一个数字，指定数据文件中后续有效数据行的数量。

## 5.4 应用问题求解：数据过滤器——修改 HTML 文件

数据过滤器

称为数据过滤器的程序常用于读取数据文件中的信息、修改文件内容，并将修改后的数据写入新文件。假设我们在网上找到了一个包含重要信息的 HTML 文档，希望将其保存为纯文本，并删除所有超文本标记语言（HTML）命令。HTML 命令（也称为标记）具有以下一般形式：

<html command>

我们可以编写一个 C++ 程序来读取 HTML 文件并过滤掉所有标记。文件中的文本（去除标记后）将输出到新文件。

### 1. 问题描述

编写一个程序，从 HTML 文件中删除标记，并将文本保存到新文件。

### 2. 输入/输出描述

下图显示，程序的输入是一个 HTML 文件。程序的输出是去除标记后的 HTML 文件文本。

