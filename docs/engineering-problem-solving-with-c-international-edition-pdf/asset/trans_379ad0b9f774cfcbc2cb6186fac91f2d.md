

```
/*--------------------------------------------------------------*/
/* This function reads data from an input stream and            */
/* assigns the data to the 2D array, arr.                       */
/* Pre-conditions:                                              */
/*   The istream in has been defined.                           */
/*   The integer cols is <= MAXCOLSIZE                          */
/*   The integer rows is <= MAXROWSIZE                          */
/* Post-conditions:                                             */
/*   rows-cols values are assigned to the array. arr            */
/*--------------------------------------------------------------*/
void input2D(istream& in, double arr[][MAXCOLSIZE],
             int rows, int cols)
{
   for (int i=0; i<rows; ++i)
   {
      for (int j=0; j<cols; ++j)
         in >> arr[i][j];
   }
}
/*--------------------------------------------------------------*/
```

```
/*--------------------------------------------------------------*/
/* This function returns the average of a column in the array   */
/* arr. The integer colNum specifies the column number.         */
/* Pre-conditions:                                              */
/*   The array arr has rowSize rows of valid data               */
/*   The integer colNum is < MAXCOLSIZE                         */
/*--------------------------------------------------------------*/
double columnAvg(const double arr[][MAXCOLSIZE], int colNum,
                 int rowSize)
{
   //Declare and initialize local variables
   double avg = 0.0;

   //Sum all values in column colNum
   for(int i=0; i<rowSize; ++i)
      avg += arr[i][colNum];

   //Return the average
   return(avg/rowSize);
}
/*--------------------------------------------------------------*/
```

注意，我们在函数 input2D() 的初始注释块中包含了前置条件和后置条件。前置条件描述在调用函数时被假定为真的条件。如果前置条件不为真，则无法保证函数能正确执行。后置条件描述函数执行期间对形式参数所做的更改。函数 columnAvg() 没有后置条件，因为该函数不会修改形式参数。在编写旨在多个应用程序中使用的函数时，包含前置条件和后置条件始终是一种良好的做法。

程序 chapter8_3 生成的输出如下：

```
Trial 1 Average Engine Temperature 319.35
Engine 2 performed below the average temp.
Trial 2 Average Engine Temperature 340.75
Engine 1 performed below the average temp.
Engine 2 performed below the average temp.
Engine 3 performed below the average temp.
Trial 3 Average Engine Temperature 375.85
Engine 2 performed below the average temp.
Engine 3 performed below the average temp.
```

- 1. 修改程序 chapter8_2 以使用函数 input2D() 和 columnAvg()。不要修改函数定义。
- 2. 修改程序 chapter8_3 以报告每次试验中温度高于平均温度的发动机。
- 3. 修改程序 chapter8_3 以报告每次试验中温度低于平均温度的发动机的温度。

## 8.2 应用问题求解：地形导航

地形导航是机器人航天器设计中的关键组成部分。机器人航天器是指没有人类乘员的航天器。这些航天器可以在陆地上行驶，例如火星探测漫游者，也可以在陆地上方运行，例如火星勘测轨道飞行器。机器人航天器包含大量机载计算机，用于存储其运行区域的地形信息。通过随时知道自身位置（或许借助全球定位系统 [GPS] 接收器），车辆可以选择最佳路径到达指定地点。如果目的地发生变化，车辆可以参考其内部地图来重新规划路径。

指导这些车辆的计算机软件必须在各种地貌和拓扑结构上进行测试。大面积土地网格的高程信息可在计算机数据库中获得。衡量土地网格相对于地形导航的“难度”的一种方法是确定网格中的峰值数量，峰值是指四周高程均低于该点的点。对于本题，我们假设下图中显示的四个位置的值与网格位置 [m][n] 相邻，用于判断网格位置 [m][n] 的值是否为峰值：

| grid[m-1][n-1] | grid[m-1][n] | grid[m-1][n+1] |
|---|---|---|
| grid[m][n-1] | grid[m][n] | grid[m][n+1] |
| | grid[m+1][n] | |

编写一个程序，从名为 grid1.dat 的数据文件中读取高程数据，然后打印峰值的数量及其位置。假设数据文件的第一行包含网格的行数和列数。随后按行顺序给出高程值。网格的最大尺寸为 25 行乘 25 列。

### 1. 问题描述

确定并打印高程网格中峰值的数量及其位置。

### 2. 输入/输出说明

I/O 图显示，输入是包含高程数据的文件，输出是峰值位置的列表。

![](img/f2bfa570e453b020c16e048c79a3ea0e_415_0.png)

### 3. 手算示例

假设以下数据表示一个沿边有六个点、沿顶有七个点的网格的高程。数据中的峰值已加下划线：

```
5039 5127 5238 5259 5248 5310 5299
5150 5392 5410 5401 5320 5820 5321
5290 5560 5490 5421 5530 5831 5210
5110 5429 5430 5411 5459 5630 5319
4920 5129 4921 5821 4722 4921 5129
5023 5192 4822 4872 4949 4824 4245
```

要指定峰值的位置，我们需要为数据分配寻址方案。由于我们将使用 C++ 实现解决方案，因此选择其二维数组偏移表示法。因此，我们假设左上角是位置 [0][0]，向下移动时行号每次加 1，向右移动时列号每次加 1。这些峰值出现在位置 [2][11]、[2][5] 和 [4][3]。

要确定峰值，我们将潜在峰值与其四个相邻点进行比较。如果四个相邻点都小于潜在峰值，则该潜在峰值是真实峰值。请注意，数组或网格边缘上的点不能是潜在峰值，因为我们不具备这些点四周的高程信息。

### 4. 算法开发

我们首先开发分解大纲，因为它将解决方案划分为一系列顺序步骤：

### 分解大纲

- 1. 将地形数据读入数组。
- 2. 确定并打印峰值的位置。

步骤 1 包括读取数据文件并将信息存储在二维数组中。步骤 2 是一个循环，用于评估所有潜在峰值，如果确定它们是真实峰值，则打印它们的位置。我们将编写一个布尔函数来确定某个位置是否为峰值。

### 伪代码细化

```
main: read nrows and ncols from the data file
    read the terrain data into an array
    set i to 1
    while i < nrows - 1:
        set j to 1
        while j < ncols - 1:
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

伪代码中的步骤现在已经足够详细，可以转换为 C++ 了：

```
/* ---------------------------------------------------------- * /
* Program chapter8_4                                      * /
*                                                         * /
* This program determines the locations of                * /
* peaks in an elevation grid of data.                     * /
# include <iostream> //Required for cin, cout
# include <fstream> //Required for ifstream
```

