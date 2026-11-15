

分解大纲的第一步涉及一个循环，我们在其中从文件读取数据，同时将相应的值添加到计算线性模型所需的求和中。我们在读取文件时还需要确定数据点的数量。退出循环的条件将是对文件结束的测试，因为没有标头或尾随信息。由于文件结束标志必须在输入语句后立即测试，我们将使用 while 循环而不是 do-while 循环。for 循环不是合适的选择，因为我们不知道文件中包含多少个数据点。因为我们想跟踪高度范围，我们还需要保存第一个和最后一个高度值。分解大纲的步骤 2 和 3 是涉及计算和打印的顺序步骤。因此，伪代码的细化如下：

```
Refinement in Pseudocode
main: set count to zero
      set sumx, sumy, sumxy, sumx2 to zero
      while not at end-of-file
         read x, y
         increment count by 1
         if count = 1
            set first to x
            add x to sumx
            add y to sumy
            add x2 to sumx2
            add xy to sumxy
      set last to x
      compute slope and y intercept
      print first, last, slope, y intercept
```

伪代码中的步骤现在足够详细，可以转换为 C++：

```
/***************************************************************/
/* Program chapter5_8                                          */
/*                                                             */
/* This program computes a linear model for a set              */
/* of altitude and ozone mixing ratio values.                  */
/*                                                             */
#include <iostream> //Required for cin, cout
#include <fstream> //Required for ifstream
#include <string> //Required for string
using namespace std;

int main()
{
   // Declare and initialize objects.
   int count(0);
   double x, y, first, last, sumx(0), sumy(0), sumx2(0),
          sumxy(0), denominator, m, b;
   string filename;

   ifstream zone1;
   cout << "Enter name of input file:";
   cin >> filename;

   // Open input file.
   zone1.open(filename);
   if (zone1.fail())
   {
       cerr << "Error opening input file\n";
       exit(1);
   }

   // While not at the end of the file,
   // read and accumulate information.
   zone1 >> x >> y;
   while ( !zone1.eof() )
   {
       ++count;
       if (count == 1)
           first = x;
       sumx += x;
       sumy += y;
       sumx2 += x*x;
       sumy2 += y*y;
       zone1 >> x >> y;
   }
   last = x;

   // Compute slope and y-intercept.
   denominator = sumx*sumx - count*sumx2;
   m = (sumx*sumy - count*sumxy)/denominator;
   b = (sumx*sumxy - sumx2*sumy)/denominator;

   // Set format flags
   cout.setf(ios::fixed);
   cout.precision(2);

   // Print summary information.
   cout << "Range of altitudes in km: \n";
   cout << "First " << first << " to " << last << endl << endl;
   cout << "Linear model: \n";
   cout << "ozone-mix-ratio = " << m << " altitude + "
        << b << endl;

   // Close file and exit program.
   zone1.close();
   return 0;
}
/*---------------------------------------------------------------*/
```

## 5. 测试

使用手算示例的数据作为数据文件 zone1.dat 的内容，我们得到以下程序输出：

```
Range of altitudes in km:
20.00 to 28.00

linear model:
ozone-mix-ratio = 0.37 altitude + -4.60
```

这与手算示例计算出的值相匹配。该范围还表明，本问题中使用的测量是在平流层进行的。

### 修改 5.6

这些问题与本节开发的程序有关。在某些问题中，您可能需要使用以下关系：

1 km = 0.621 mi

- 1. 向程序添加语句，以便您可以输入以 km 为单位的高度，然后使用模型估计相应的臭氧混合比。
- 2. 修改问题 1 中的程序，以便它检查您输入的高度是否在该模型适用的范围内。
- 3. 修改问题 2 中的程序，以便它允许您以英里为单位输入高度。（程序应将英里转换为千米。）
- 4. 修改原始程序，使其也打印一个线性模型，以便它可以与以英里而非千米为单位的高度一起使用。假设数据文件仍然包含以千米为单位的高度。

## 5.8 使用 IDE 构建 C++ 解决方案：Xcode-天气模式

国家气象服务是国家海洋和大气管理局（NOAA）的一个组成部分。其使命是提供天气、水和气候数据、预报和警报，以保护生命和财产并促进国家经济。有关国家气象服务的更多信息，请访问其网站 www.weather.gov。

来自该网站的示例气候数据报告如下。请注意，降水列中的 T 表示痕量降水。

站点：ALAMOSA CO
月份：五月
年份：2015
纬度：37 27 N
经度：105 52 W

华氏温度 降水：

| 日期 | 最高 | 最低 | 平均 | 水量 | 雪量 |
|-----|-----|-----|-----|-------|------|
| 1 | 74 | 39 | 57 | 0.00 | 0.0 |
| 2 | 71 | 32 | 52 | 0.02 | 0.0 |
| 3 | 68 | 32 | 50 | 0.00 | 0.0 |
| 4 | 64 | 33 | 49 | T | 0.0 |
| 5 | 53 | 42 | 48 | 0.30 | 0.0 |
| 6 | 64 | 34 | 52 | T | 0.0 |
| 7 | 64 | 34 | 49 | T | 0.0 |
| 8 | 68 | 35 | 52 | 0.00 | 0.0 |
| 9 | 56 | 35 | 46 | 0.03 | T |
| 10 | 56 | 33 | 45 | T | 0.0 |
| 11 | 62 | 28 | 45 | T | 0.0 |
| 12 | 70 | 40 | 55 | T | 0.0 |
| 13 | 64 | 38 | 51 | 0.00 | 0.0 |
| 14 | 67 | 33 | 50 | 0.00 | 0.0 |
| 15 | 56 | 35 | 46 | 0.07 | 0.0 |
| 16 | 55 | 30 | 43 | 0.02 | 0.0 |
| 17 | 66 | 26 | 46 | T | 0.0 |
| 18 | 68 | 32 | 50 | 0.07 | 0.0 |
| 19 | 60 | 37 | 49 | 0.89 | 0.0 |
| 20 | 67 | 30 | 49 | 0.00 | 0.0 |
| 21 | 66 | 41 | 54 | T | 0.0 |
| 22 | 65 | 36 | 51 | 0.03 | 0.0 |
| 23 | 63 | 37 | 50 | 0.00 | 0.0 |
| 24 | 52 | 36 | 44 | 0.16 | 0.0 |
| 25 | 63 | 31 | 47 | 0.00 | 0.0 |
| 26 | 67 | 32 | 50 | 0.01 | 0.0 |
| 27 | 71 | 35 | 54 | 0.00 | 0.0 |
| 28 | 65 | 28 | 46 | T | 0.0 |
| 29 | 68 | 32 | 50 | 0.07 | 0.0 |
| 30 | 61 | 36 | 49 | 0.89 | 0.0 |
| 31 | 67 | 32 | 49 | 0.00 | 0.0 |

为此练习，我们将使用 Xcode IDE 编写一个 C++ 解决方案，以确定 2015 年 5 月平均温度高于 50 华氏度的天数。该程序将读取并打印前 5 个标题行到输出文件，然后是平均温度高于 50 华氏度的天数。我们的解决方案流程图如下：

开始

输入文件名

打开失败？

退出

i = 0
i < 5
i++

1

输入一个字符

文件结束
且
"n"

打印字符

输入一个字符

文件结束？

退出

打印换行符

1

输入一个字符

非文件结束 且 不是数字

文件结束？

退出

输入下一个字符

将数字退回

输入气候数据

文件结束？

打印计数

结束

平均温度 > 50？

递增计数

输入气候数据

我们的流程图足够详细，可以转换为 C++ 语句。启动 Xcode 后，我们在新建项目窗口中创建一个新项目，如下所示：

![](img/0235a4ea835dc4575bd036e024a533b3_262_0.png)

### 新建项目窗口

从新建项目窗口选择“下一步”并为项目提供名称后，Xcode 将创建一个包含名为 main.cpp 的文件的新项目。我们将选择此文件并添加实现流程图所需的 C++ 语句。完整的 C++ 解决方案如下主窗口所示：

![](img/0235a4ea835dc4575bd036e024a533b3_262_1.png)

### 主窗口

如第 2.4 章所述，我们可以通过从 Xcode 菜单栏的 Product 菜单中选择 Build 来编译程序。为了成功运行程序，我们必须提供一个用于输入的数据文件，因此接下来我们将向项目添加一个数据文件。从 Xcode 的 File 菜单中，选择 New > File...，然后选择 Other 和 Empty，如下所示的新建文件窗口所示：

![](img/0235a4ea835dc4575bd036e024a533b3_263_0.png)

### 新建文件窗口

从新建文件窗口选择“下一步”并为数据文件提供名称后，将向项目添加一个新的空文件。然后我们可以选择该文件并插入我们的示例数据集。完成的数据文件如下项目窗口所示。请注意，数据文件的名称是 WeatherData.txt。

![](img/0235a4ea835dc4575bd036e024a533b3_263_1.png)

### 项目窗口

