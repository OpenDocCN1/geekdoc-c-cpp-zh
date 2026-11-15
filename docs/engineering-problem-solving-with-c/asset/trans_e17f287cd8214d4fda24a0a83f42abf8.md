
该函数将正确执行。后条件描述了函数执行期间对形式参数所做的更改。函数 columnAvg() 没有后条件，因为该函数不会修改形式参数。在编写旨在多个应用程序中使用的函数时，始终包含前条件和后条件是一种良好的做法。

程序 chapter8_3 生成的输出如下：

```
Trial 1 Average Engine Temperature 319.35
----------------------------------------
Engine 2 performed below the average temp.

Trial 2 Average Engine Temperature 340.75
----------------------------------------
Engine 1 performed below the average temp.
Engine 2 performed below the average temp.
Engine 3 performed below the average temp.

Trial 3 Average Engine Temperature 375.85
----------------------------------------
Engine 2 performed below the average temp.
Engine 3 performed below the average temp.
```

- 1. 修改程序 chapter8_2 以使用函数 input2D() 和 columnBreakAvg()。不要修改函数定义。
- 2. 修改程序 chapter8_3 以报告每次试验中温度高于平均温度的发动机。
- 3. 修改程序 chapter8_3 以报告每次试验中温度低于平均温度的发动机的温度。

## 8.2 应用问题求解：地形导航

地形导航是机器人航天器设计中的关键组成部分。机器人航天器是指没有人类乘员的航天器。这些航天器可以在陆地上行驶，例如火星探测漫游者，也可以在陆地上方运行，例如火星勘测轨道飞行器。机器人航天器包含许多机载计算机，用于存储其运行区域的地形信息。通过随时知道自身位置（也许借助全球定位系统 [GPS] 接收器），车辆可以选择最佳路径到达指定地点。如果目的地发生变化，车辆可以参考其内部地图重新计算新路径。

引导这些车辆的计算机软件必须在各种地貌和拓扑结构上进行测试。大面积土地网格的高程信息可在计算机数据库中获得。衡量土地网格相对于地形导航的“难度”的一种方法是确定网格中的峰值数量，峰值是指四周海拔较低的点。对于此问题，我们假设下图中显示的四个位置的值是相对于网格位置 [m][n] 相邻的值，用于确定网格位置 [m][n] 中的值是否为峰值：

| | grid[m-1][n] | |
|---|---|---|
| grid[m][n-1] | grid[m][n] | grid[m][n+1] |
| | grid[m+1][n] | |

编写一个程序，从名为 grid1.dat 的数据文件中读取高程数据，然后打印峰值的数量及其位置。假设数据文件的第一行包含网格的行数和列数。随后按行顺序给出高程值。网格的最大尺寸为 25 行乘 25 列。

## 1. 问题陈述

确定并打印高程网格中峰值的数量及其位置。

## 2. 输入/输出描述

I/O 图显示输入是包含高程数据的文件，输出是峰值位置的列表。

![](img/0235a4ea835dc4575bd036e024a533b3_467_0.png)

## 3. 手算示例

假设以下数据表示一个网格的高程，该网格沿边有六个点，沿顶部有七个点。数据中的峰值已加下划线：

```
5039 5127 5238 5259 5248 5310 5299
5150 5392 5410 5401 5320 5820 5321
5290 5560 5490 5421 5530 5831 5210
5110 5429 5430 5411 5459 5630 5319
4920 5129 4921 5821 4722 4921 5129
5023 5129 4822 4872 4794 4862 4245
```

要指定峰值的位置，我们需要为数据分配寻址方案。因为我们将在 C++ 中实现此解决方案，所以选择其二维数组偏移表示法。因此，我们假设左上角是位置 [0][0]，向下移动时行号增加 1，向右移动时列号增加 1。这些峰值出现在位置 [2][1]、[2][5] 和 [4][3]。

要确定峰值，我们将潜在峰值与其四个相邻点进行比较。如果所有四个相邻点都小于潜在峰值，则该潜在峰值是真实峰值。请注意，数组或网格边缘上的点不能是潜在峰值，因为我们没有这些点四周的高程信息。

## 4. 算法开发

我们首先开发分解大纲，因为它将解决方案分为一系列顺序步骤：

### 分解大纲

- 1. 将地形数据读入数组。
- 2. 确定并打印峰值的位置。

步骤 1 涉及读取数据文件并将信息存储在二维数组中。步骤 2 是一个循环，用于评估所有潜在峰值，如果确定它们是真实峰值，则打印它们的位置。我们将编写一个布尔函数来确定某个位置是否为峰值。

```
main: read nrows and ncols from the data file
read the terrain data into an array
set i to 1
while i < nrows - 1;
set j to 1
while j < ncols - 1;
if (ispeak(grid,i,j))
print peak location
increment j by 1
increment i by 1
peak:
if ((grid[i-1][j]<grid[i][j]) &&
(grid[i+1][j]<grid[i][j]) &&
(grid[i][j-1]<grid[i][j]) &&
(grid[i][j+1]<grid[i][j]))
return true;
else
return false;
```

伪代码中的步骤现在足够详细，可以转换为 C++：

```cpp
/*----------------------------------------------------------*/
/* Program chapter8_4 */
/* */
/* This program determines the locations of */
/* peaks in an elevation grid of data. */
/*----------------------------------------------------------*/
#include <iostream> //Required for cin, cout
#include <fstream> //Required for ifstream
#include <string> //Required for string
using namespace std;
// Function prototypes.
bool isPeak(const double grid[][N], int r, int c);
int main()
{
   // Declare objects.
   int const N (25);
   int nrows, ncols;
   double elevation[N][N];
   string filename;
   ifstream filein;

   // Prompt user for file name and open file for input.
   cout << "Enter the name of the input file.\n";
   cin >> filename;
   filein.open(filename);
   if(filein.fail())
   {
      cerr << "Error opening input file\n";
      exit(1);
   }
   filein >> nrows >> ncols;
   if(nrows > N || ncols > N)
   {
      cerr << "Grid is too large, adjust program.";
      exit(1);
   }

   // Read information from data file into array.
   for (int i=0; i<nrows; ++i)
   {
      for (int j=0; j<ncols; ++j)
         filein >> elevation[i][j];
   }

   // Determine and print peak locations.
   cout << "Top left point defined as row 0, column 0 \n";
   for (int i=1; i<nrows-1; ++i)
   {
      for (int j=1; j<ncols-1; ++j)
      {
         if(isPeak(elevation, i, j))
         {
            cout << "Peak at row: " << i
                 << " column: " << j << endl;
         }
      }
   }

   // close file
   filein.close();
   // Exit program.
   return 0;
}

bool isPeak(const double grid[][N], int i, int j)
{
    if ((grid[i-1][j]<grid[i][j]) &&
        (grid[i+1][j]<grid[i][j]) &&
        (grid[i][j-1]<grid[i][j]) &&
        (grid[i][j+1]<grid[i][j]))
        return true;
    else
        return false;
}
/*---------------------------------------------*/
```

## 5. 测试

使用与手算示例对应的数据文件打印了以下输出（请记住，该文件必须包含指定高程数据行数和列数的特殊第一行）：

```
Top Left point defined as row 0, column 0
Peak at row: 2 column: 1
Peak at row: 2 column: 5
Peak at row: 4 column: 3
```

## 修改 8.2

- 1. 打印网格中峰值的数量。
- 2. 打印山谷的位置而不是峰值。假设山谷是海拔低于四周四个海拔的点。编写一个名为 isValley 的布尔函数，由你的程序调用。
- 3. 查找并打印高程数据中最高点和最低点的位置和海拔。编写一个名为 extremes 的函数，由你的程序调用。
- 4. 假设垂直和水平方向上点之间的距离为 100 英尺，给出从网格左下角起算的峰值位置（英尺）。
- 5. 修改函数 isPeak()，以在确定峰值时使用所有八个相邻点，而不仅仅是四个相邻点。
- 6. 为函数 isPeak() 添加前条件。
