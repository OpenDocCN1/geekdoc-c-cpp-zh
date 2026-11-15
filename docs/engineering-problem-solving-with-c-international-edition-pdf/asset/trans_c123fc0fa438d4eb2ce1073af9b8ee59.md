

该程序使用 `sensor1.dat` 文件打印的报告如下：

```
Number of sensor readings: 10
Average reading: 149.77
Maximum reading: 169.30
Minimum reading: 132.50
```

## 尾记录或哨兵信号

假设数据文件 `sensor2.dat` 包含与 `sensor1.dat` 文件相同的信息，但不是在文件开头给出有效数据记录的数量，而是在最后一条记录中包含一个尾记录信号。文件最后一行上的时间值将包含一个负值，因此我们知道它不是一行有效信息。数据文件的内容如下：

```
sensor2.dat
0.0 132.5
0.1 147.2
0.2 148.3
0.3 157.3
0.4 163.2
0.5 158.2
0.6 169.3
0.7 148.2
0.8 137.6
0.9 135.9
-99 -99
```

使用 do/while 循环结构可以轻松描述读取并累加信息直到读取尾记录信号的过程，如以下伪代码和程序所示：

```
Pseudocode
main:
    set sum to zero
    set number of points to 0
    read time, motion
    set max to motion
    set min to motion
    do
        add motion to sum
        if motion > max
            set max to motion
        if motion < min
            set min to motion
        increment number of points by 1
        read time, motion
    while time >= 0
    set average to sum/number of data points
    print average, max, min
```

```
/*-------------------------------------------------------------*/
/* Program chapter5_3                                          */
/* This program generates a summary report from
   a data file that has a trailer record with
   negative values. */
/* */
#include <iostream> //Required for cin, cout, cerr
#include <fstream> //Required for ifstream, ofstream
#include <string> //Required for string.
using namespace std;

int main()
{
   // Declare and initialize objects.
   int num_data_pts(0), k;
   double time, motion, sum(0.0), max, min;
   string filename;
   ifstream sensor2;
   ofstream report;

   // Prompt user for name of input file.
   cout << "Enter the name of the input file";
   cin >> filename;

   // Open file and read the first data point.
   sensor2.open(filename.c_str());
   if(sensor2.fail())
   {
      cerr << "Error opening input file\n";
      exit(1);
   }

   // Open report file.
   report.open("sensor2Report.txt");
   sensor2 >> time >> motion;

   // Initialize objects using first data point.
   max = min = motion;

   // Update summary data until trailer record read.
   do
   {
      sum += motion;
      if (motion > max)
         max = motion;
      if (motion < min)
         min = motion;
      num_data_pts++;
      sensor2 >> time >> motion;
   } while (time >= 0);

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

   // Close files and exit program.
   sensor2.close();
   report.close();

   return 0;
} // end main
//***********************************************************************/
```

该程序使用 sensor2.dat 文件打印的报告与使用 sensor1.dat 文件打印的报告完全相同。

## 文件结束符

每个数据文件的末尾都会自动插入一个特定的系统相关文件结束符指示符。可以使用 eof() 函数来检测数据文件中是否已到达此指示符。如果与文件流对象关联的数据文件中已读取文件结束符指示符，则该函数返回 true。请考虑以下语句：

```
sum = count = 0;
data1 >> x;
while ( !data1.eof() )
{
    ++count;
    sum += x;
    data1 >> x;
}
avg = sum / count;
```

第一个输入语句尝试从与输入文件流对象 data1 关联的数据文件中读取 x 的值。如果读取了数据值，则 eof() 函数返回 0，并执行循环内的语句。while 循环内的最后一条语句是一个输入语句，它尝试从数据文件中读取 x 的下一个值。只要未到达数据文件末尾，while 循环就会继续执行。当文件中没有更多数据且读取了文件结束符指示符时，下一次对 eof() 函数的调用将返回 1，控制将传递给 while

![](img/f2bfa570e453b020c16e048c79a3ea0e_209_0.png)

循环之后的语句。这是文件结束循环的正确结构。`eof()` 函数只有在读取文件结束符指示符之后才会返回 true。出于此原因，在输入语句后立即测试文件结束非常重要。

您也可以自动检测文件结束符指示符，如以下语句所示：

```
while ( data1 >> x )
{
    ++count;
    sum += x;
}
```

这个 while 循环使用输入请求返回的值来控制执行。如果从 data1 文件流中读取了数据值，则输入请求返回 true；如果无法从文件流中读取数据值，则返回 false。在我们的示例中，将使用 eof() 函数以提高清晰度。

现在假设数据文件 sensor3.dat 包含与 sensor2.dat 文件相同的信息，但不包括尾记录信号。在以下程序中，我们读取并累加信息，直到到达文件末尾：

```
/*....................................................*/
/* Program chapter5_4                                  */
/*                                                     */
/* This program generates a summary report from        */
/* a data file that does not have a header record      */
/* or a trailer record.                                */
/*                                                     */
#include <iostream> //Required for cin, cout, cerr
#include <fstream> //Required for ifstream, ofstream.
#include <string> //Required for string.
using namespace std;
int main()
{
    // Declare and initialize objects.
    int num_data_pts(0), k;
    double time, motion, sum(0.0), max, min;
    string filename;
    ifstream sensor3;
    ofstream report;
    // Prompt user for name of input file.
    cout << "Enter the name of the input file";
    cin >> filename;
    // Open file and read the first data point.
    sensor3.open(filename.c_str());

    if(sensor3.fail())
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
/*--------------------------------------*/
```

使用 `sensor3.dat` 文件打印的报告与使用 `sensor1.dat` 或 `sensor2.dat` 打印的报告完全相同。

如果数据文件存在并包含预期信息，本节中的程序即可正常工作。如果该程序将常规用于传感器数据，则应包含语句以确保文件结构是预期的结构。另外，如果点数为零，将发生除以零错误。可以通过在打印报告之前将点数与零进行比较来避免除以零错误。

这三种文件结构在工程和科学应用中都很常用。因此，在使用数据文件时，了解使用的是哪种结构非常重要。如果假设错误，您可能会得到错误答案而不是错误消息。有时，确定文件结构的唯一方法是打印文件的前几行和最后几行。

## 修改！

在本章开发的程序 `chapter5_3` 中，循环包含一个条件，用于测试循环是否第一次执行。当条件为真时，`max` 和 `min` 值将初始化为第一个 motion 值。如果这些程序使用的数据文件非常长，执行此选择语句所需的时间可能会变得相当可观。避免此测试的一种方法是在进入循环之前读取第一组数据并初始化对象。此更改可能还需要对程序进行其他更改。

- 1. 修改程序 `chapter5_3`，以便在删除测试循环是否第一次执行的条件后，它仍能正确工作。
- 2. 使用空数据文件运行程序 `chapter5_4`。如果输出有误，请修改程序以纠正错误。

## 5.3 生成数据文件

生成数据文件类似于打印报告；不同之处在于，我们不是将行写入终端屏幕，而是将其写入数据文件。不过，在生成数据文件之前，我们必须决定要使用哪种文件结构。在之前的讨论中，我们介绍了三种最常见的文件结构：包含初始记录的文件（用于给出随后的有效记录数量）、包含尾记录或哨兵记录的文件（用于指示有效数据的结束），以及仅包含有效数据记录且没有特殊开始或结束记录的文件。

所讨论的三种文件结构各有优缺点。带有尾信号的文件使用简单，但必须仔细选择尾信号的值，以确保其不包含可能出现在有效数据中的值。如果数据文件的第一条记录将包含实际数据的行数，那么在开始生成文件之前，我们必须知道文件中将有多少行数据。在执行生成文件的程序之前，确定行数并不总是容易的。最简单的生成文件是仅包含有效信息的文件，文件开头和结尾没有特殊信息。如果文件中的信息将与绘图包一起使用，通常最好使用仅包含有效信息的第三种文件结构。

