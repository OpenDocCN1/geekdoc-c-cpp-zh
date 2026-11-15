

```cpp
//Read and print data from file
count = 0;//Reset count to zero.
fin >> iVal;
while(!fin.eof())
{
    //Test state of fin.
    if(fin) //if fin is bad
    {
        cerr << "Bad data encountered.\n";
        cerr << "The state of fin is:"
        << fin.rdstate()<< endl;
        cerr << "badbit:"
        << setw(0) << fin.bad() << endl;
        cerr << "failbit:"
        << setw(0) << fin.fail() << endl;
        cerr << "eofbit:"
        << setw(0) << fin.eof() << endl;
        cerr << "goodbit:"
        << setw(0) << fin.good() << endl;
        cerr << "********************" << endl;
        //Reset fin to good state
        fin.clear();
        //Remove bad character from input stream.
        fin.get(junk);
        cerr << "The bad character is:" << junk << endl;
        continue; //Force next iteration of while loop.
    }
    ++count;
    fout << setw(5) << count
    << setw(10) << iVal << endl;
    fin >> iVal;
}
//Print current state of fin to standard output.
cout << "Outside of while, state of fin is:"
<< fin.rdstate() << endl;
cout << setw(10) << "badbit:" <<
setw(10) << fin.bad() << endl;
cout << setw(10) << "failbit:" <<
setw(10) << fin.fail() << endl;
cout << setw(10) << "eofbit:" <<
setw(10) << fin.eof() << endl;
cout << setw(10) << "goodbit:" <<
setw(10) << fin.good() << endl;
cout << "********************" << endl;
fin.close();
fout.close();
return 0;
}
```

A sample run of this program is shown below. First we enter the name of a file that does not exist. When prompted for a new file name we enter the filename test.dat. The file test.dat contains the following data:

```
20 30
5 9
1.5
8 9
- 7 4
```

Sample run:

```
enter the name of input file badfilename
could not open badfilename. The state of the fin stream is 4
badbit: 0
failbit: 1
eofbit: 0
goodbit: 0
****************************************
fin state reset to 0
badbit: 0
failbit: 0
eofbit: 0
goodbit: 1
****************************************
enter the name of a file test.dat
File test.dat is open. State of fin is 0
Bad data encountered.
The state of fin is: 4
badbit: 0
failbit: 1
eofbit: 0
goodbit: 0
****************************************
The bad character is:.
Outside of while, state of fin is: 6
badbit: 0
failbit: 1
eofbit: 1
goodbit: 0
****************************************
```

After running the program, the output file output.dat contains the following data:

| 计数 | iVar2 |
|---|---|
| 1 | 20 |
| 2 | 30 |
| 3 | 5 |
| 4 | 9 |
| 5 | 1 |
| 6 | 1 |
| 7 | 5 |
| 8 | 8 |
| 9 | 9 |
| 10 | -7 |
| 11 | 4 |

## 修改！

- 1. 程序 chapter5_7 在首次尝试失败后允许用户再尝试 5 次以输入有效的输入文件名。修改程序，仅允许用户再尝试 1 次，并使用布尔控制变量代替整数变量 count。
- 2. 通过禁用直接测试 fin 状态的代码块来修改程序 chapter5_7。编译并运行修改后的程序。标准输出显示什么？输出文件中写入了什么？解释结果。注意：可以通过在代码块周围放置注释行来禁用该代码块，以指示编译器将该代码视为注释块。

## 练习！

假设在键盘上输入以下数据行：
1.2.3

执行以下每组语句后，给出相应的内存快照和流状态标志的值：

- 1. int i(0), j(0);
  cin >> i >> j;

- 2. double x(0), y(0);
  cin >> x >> y;

- 3. char ch1, ch2;
  cin >> ch1 >> ch2;

- 4. char ch;
  double x, y;
  cin >> x >> ch >> y;

## 5.6 数值技术：线性建模*

线性建模是指确定一组数据点的最佳拟合直线方程的过程，其目标是最小化直线与数据点之间平方距离之和。（此过程也称为线性回归。）为了理解该过程，我们首先考虑第 2.5 节中介绍的从新发动机气缸头收集的一组温度值。

| 时间, s | 温度, 华氏度 |
|---|---|
| 0 | 0 |
| 1 | 20 |
| 2 | 60 |
| 3 | 68 |
| 4 | 77 |
| 5 | 110 |

![](img/f2bfa570e453b020c16e048c79a3ea0e_225_0.png)

图 5.4 用于对一组点进行建模的线性估计。

如果绘制这些数据点，我们会发现它们似乎靠近一条直线。事实上，我们可以通过在图上绘制直线然后计算斜率和 y 截距来确定穿过这些点的直线的良好估计。图 5.4 包含点的图表（横轴为时间，纵轴为温度），以及方程为

$y = 20x.$

为了衡量该线性估计与数据的拟合优度，我们首先确定每个点到线性估计的垂直距离；这些距离如图 5.5 所示。前两个点正好落在直线上，因此 \(d_1\) 和 \(d_2\) 为零。\(d_3\) 的值等于 \(60 - 40\)，即 20；其余距离可以以类似方式计算。如果计算距离之和，一些正值和负值会相互抵消，导致和小于应有的值。为避免此问题，我们可以使用绝对值或平方值；线性回归使用平方值。因此，该线性估计拟合优度的度量是点与线性估计之间平方距离之和。该和易于计算，结果为 573。

如果通过这些点绘制另一条直线，我们可以计算与这条新直线对应的平方和。在两条直线中，最佳拟合由平方距离之和最小的直线提供，即

![](img/f2bfa570e453b020c16e048c79a3ea0e_225_1.png)

图 5.5 点与线性估计之间的距离。

**最小二乘** 距离。为了找到平方距离之和最小的直线，我们从一般线性方程开始：

$y = mx + b$

然后，我们编写一个方程来计算给定数据点与该一般方程之间的平方距离之和。使用微积分技术，我们可以分别对 m 和 b 求该方程的导数，并将导数设为零。

以这种方式确定的 m 和 b 值表示平方距离之和最小的直线。在给出 m 和 b 的这些方程之前，我们先定义 **求和符号**。

### 求和符号

本节开头给出的一组数据点可以用点 $(x_1, y_1), (x_2, y_2), \dots, (x_6, y_6)$ 表示。符号 $\sum$ 表示求和，因此 x 坐标之和可以用以下符号表示：

\(\sum_{k=1}^{6} x_k\)

此求和读作“当 k 从 1 到 6 时 $x_k$ 之和”。对于示例数据点，此求和的值为 $(0+1+2+3+4+5)$，即 15。使用示例数据点可以计算的其他求和如下：

\(\sum_{k=1}^{6} y_k = 0 + 20 + 60 + 68 + 77 + 110 = 335,\)
\(\sum_{k=1}^{6} y_k^2 = 0^2 + 20^2 + 60^2 + 68^2 + 77^2 + 110^2 = 26,653,\)
\(\sum_{k=1}^{6} x_k y_k = 0 \times 0 + 1 \times 20 + 2 \times 60 + 3 \times 68 + 4 \times 77 + 5 \times 110 = 1,202.\)

我们现在回到寻找一组点的最佳线性拟合的问题。使用前面基于微积分结果描述的过程，我们发现一组 n 个数据点的最佳线性拟合（在最小二乘意义下）的斜率和 y 截距如下：

\(m = \frac{\sum_{k=1}^{n} x_k \cdot \sum_{k=1}^{n} y_k - n \cdot \sum_{k=1}^{n} x_k y_k}{\left(\sum_{k=1}^{n} x_k\right)^2 - n \cdot \sum_{k=1}^{n} x_k^2}.\) (5.1)

\(b = \frac{\sum_{k=1}^{n} x_k \cdot \sum_{k=1}^{n} x_k y_k - \sum_{k=1}^{n} x_k^2 \cdot \sum_{k=1}^{n} y_k}{\left(\sum_{k=1}^{n} x_k\right)^2 - n \cdot \sum_{k=1}^{n} x_k^2}.\) (5.2)

