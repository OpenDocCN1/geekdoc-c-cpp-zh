

在上一节中讨论过。与语音信号一起使用的其他测量值包括平均幅度，即平均绝对值，其计算方法如下所示，其中 n 为数据值的数量：

平均幅度 = \(\frac{\sum_{k=0}^{n-1} |x_k|}{n}\). (7.3)

语音分析中使用的另一种指标是信号的平均功率，即平均平方值：

平均功率 = \(\frac{\sum_{k=0}^{n-1} x_k^2}{n}\). (7.4)

语音信号中的零交叉次数也是一种有用的统计测量值。该值是语音信号从负值变为正值或从正值变为负值的次数：从非零值变为零值不算作零交叉。

编写一个程序，从名为 zero.dat 的数据文件中读取语音信号。该文件包含表示单词“zero”的一次发音的值。文件的每一行包含一个单一值，表示麦克风在 0.0002 秒的时间增量内进行的测量，因此 5000 个测量值代表 1 秒的数据。该数据文件仅包含有效数据，没有标题或尾行；文件中最多包含 2,500 个值。从文件中计算并打印以下统计测量值：均值、标准差、方差、平均功率、平均幅度和零交叉次数。

## 1. 问题描述

计算语音发音的以下统计测量值：均值、标准差、方差、平均功率、平均幅度和零交叉次数。

## 2. 输入/输出描述

I/O 图显示数据文件作为输入，统计测量值作为输出。

![](img/f2bfa570e453b020c16e048c79a3ea0e_352_0.png)

## 3. 手算示例

对于手算示例，假设文件包含以下值：

```
2.5 8.2 -1.1 -0.2 1.5
```

使用计算器，我们可以计算以下值：

均值 = \(\mu = \frac{(2.5 + 8.2 - 1.1 - 0.2 + 1.5)}{5}\)
\(\approx 2.18\);
方差 = \([(2.5 - \mu)^2 + (8.2 - \mu)^2 + (-1.1 - \mu)^2\)
\(+ (-0.2 - \mu)^2 + (1.5 - \mu)^2]/4\)
\(\approx 13.307\);
标准差 = \(\sqrt{13.307}\)
\(\approx 3.648\);
平均功率 = \(\frac{(2.5)^2 + (8.2)^2 + (-1.1)^2 + (-0.2)^2 + (1.5)^2}{5}\)
\(\approx 15.398\);
平均幅度 = \(\frac{|2.5| + |8.2| + |-1.1| + |-0.2| + |1.5|}{5}\)
\(\approx 2.7\);

零交叉次数 = 2。

## 4. 算法开发

我们首先开发分解大纲，因为它将解决方案分为一系列顺序步骤。

分解大纲

- 1. 将语音信号读入数组。
- 2. 计算并打印统计测量值。

步骤 1 涉及读取数据文件并确定数据点的数量。步骤 2 涉及计算和打印统计测量值，在可能时使用已开发的函数。主函数和所需的其他统计函数的伪代码细化如下所示；结构图在图 5.1 中显示，以说明一个引用多个程序员定义函数的主函数示例。

伪代码细化

```
main: read speech signal from data file and
determine the number of points. n
compute and print mean
compute and print standard deviation
compute and print variance
compute and print average power
compute and print average magnitude
compute and print zero crossings
Additional Functions
ave_power(x: n):
  set sum to zero
  set k to zero
  while k < n
    add x[k]^2 to sum
    increment k by 1
  return sum/n
ave_magn(x: n):
  set sum to zero
  set k to zero
  while k <= n - 1
    add | x[k] | to sum
    increment k by 1
  return sum/n
crossings(x: n):
  set count to zero
  set k to zero
  while k <= n-2
    if x[k]*x[k + 1] < 0
      increment count by 1
  return count
```

请注意，对于 n 个数据点的集合，潜在的零交叉次数为 n - 1 次，因为每个交叉由一对值确定。因此，最后测试的值对将位于偏移量 n - 2 和 n - 1 处。伪代码中的步骤足够详细，可以转换为 C++：

```
/*
 * Program chapter7_6
 *
 * This program computes a set of statistical
 * measurements from a speech signal.
 */
#include<iostream> //Required for cin, cout.
#include<fstream> //Required for ifstream.
#include<string> //Required for string
#include<cmath> //Required for abs()
#include "stat_lib.h" /*Required for mean(), variance(), std_dev()
using namespace std;

// Declare function prototypes and define constants.
double ave_power(double x[], int n);
double ave_magn(double x[], int n);
int crossings(double x[], int n);

int main()
{
    // Declare objects.
    const int MAXIMUM = 2500;
    int npts(0);
    double speech[MAXIMUM];
    string filename;
    ifstream file_1;

    // Prompt user for file name and
    // open file.
    cout << " Enter filename ";
    cin >> filename;
    file_1.open(filename.c_str());
    if( file_1.fail() )
    {
        cout << " error opening file " << filename
             << endl;
        return 0;
    }

    // Read information from a data file.
    while (npts <= MAXIMUM-1 && file_1 >> speech[npts])
        npts++;
    // end while

    // Compute and print statistics.
    cout << "Digit Statistics:\n";
    cout << "\tmean: " << mean(speech,npts) << endl;
    cout << "\tstandard deviation: "
         << std_dev(speech,npts) << endl;
    cout << "\tvariance: " << variance(speech,npts)
         << endl;
    cout << "\taverage power: " << ave_power(speech,npts)
         << endl;
    cout << "\taverage magnitude: "
         << ave_magn(speech,npts) << endl;
    cout << "\tzero crossings: " << crossings(speech,npts)
         << endl;

    // Close file and exit program.
    file_1.close();
    return 0;
}
/*--------------------------------------------------------------*/
/* This function returns the average power */
```

```
/* of an array x with n elements. */
double ave_power(double x[], int n)
{
    // Declare and initialize objects.
    double sum(0);

    // Determine average power.
    for (int k=0; k<=n-1; ++k)
        sum += x[k]*x[k];

    // Return average power.
    return sum/n;
}
```

```
/**...................................................*/
/* This function returns the average magnitude */
/* of an array x with n values. */
*/
double ave_magn(double x[], int n)
{
    // Declare and initialize objects.
    double sum(0);

    // Determine average magnitude.
    for (int k=0; k<=n-1; ++k)
        sum += abs(x[k]);

    // Return average magnitude.
    return sum/n;
}
```

```
/**...................................................*/
/* This function returns a count of the number */
/* of zero crossings in an array x with n values. */
*/
int crossings(double x[], int n)
{
    // Declare and initialize objects.
    int count(0);

    // Determine number of zero crossings.
    for (int k=0; k<=n-2; ++k)
    {
        if (x[k]*x[k+1] < 0)
            count++;
    }
    // Return number of zero crossings.
    return count;
}
/*******************************************************/
```

## 5. 测试

此程序需要访问上一节开发的 stat_lib.h 头文件和 stat_lib.cpp 文件。使用文件 zero.dat 为发音“zero”计算出了以下值：

```
Digit Statistics:
mean: 0.002931
standard deviation: 0.121763
variance: 0.014826
average power: 0.014820
average magnitude: 0.089753
zero crossings: 106
```

## 修改！

- 1. 使用教师资源光盘上提供的文件 two_a.dat、two_b.dat 和 two_c.dat 运行此程序。这些发音均为单词“two”，但由不同的人说出。
- 2. 比较三个文件的问题 1 程序输出。输出说明了在设计与说话人无关的语音识别系统时存在的一些困难。

## 7.5 排序和搜索算法

### 排序

对一组数据值进行排序是在分析数据时常规使用的另一种操作。有许多完整的教材介绍了各种不同的排序算法。存在如此多排序算法的原因之一是，不存在一种“最佳”排序算法。如果数据已经接近正确顺序，某些算法速度更快，但如果顺序是随机的或接近相反顺序，这些算法可能效率非常低。因此，要为特定应用选择最佳排序算法，通常需要了解原始数据的顺序情况。与其试图对排序算法进行完整讨论，不如在本文中介绍两种算法。我们鼓励你参考其他教材，以获得更完整的排序算法讨论。在本节中，我们介绍了一种选择排序，它易于理解，也易于在函数中编码。

