

## 练习 8.3 续

```
2. int sum[1];
   for (int i=1; i<3; i++)
   {
       for (int j=0; j<1; j++)
       {
           sum *= g[i][j];
       }
   }
```

```
3. int sum = 0;
   for (int j=0; j<3; ++j)
   {
       sum -= g[2][j];
   }
```

```
4. int sum = 0;
   for (int i=0; i<3; ++i)
   {
       sum += g[1][1];
   }
```

## 函数参数

当数组用作函数参数时，默认是按引用传递，而不是按值传递。如第 7 章所讨论，这意味着函数中的数组参数引用的是原始数组，而不是数组的副本。因此，我们必须小心，在不打算进行更改时不要更改原始数组中的值。

当使用一维数组作为函数参数时，函数只需要数组中第一个元素的地址，该地址由数组名指定。当使用二维数组作为函数参数时，函数还需要关于数组声明列大小的信息。一般来说，函数头和函数原型需要给出二维数组的声明列大小。为了说明，假设我们需要编写一个程序来计算包含四行四列的数组中元素的和。计算此和需要两个嵌套循环，因此如果我们将计算和的步骤放在一个函数中，程序会更易读。然后程序可以用一条语句引用该函数，如下所示：

![](img/0235a4ea835dc4575bd036e024a533b3_460_0.png)

```
#include <iostream> //Required for cout
using namespace std;
const int NROWS(4), NCOLS(4);
// Function prototypes.
int sum(int x[][NCOLS]);
...
int main()
{
    // Declare objects.
    int a[NROWS][NCOLS];
    ...
    // Reference function to compute array sum.
    cout << "Array sum = " << sum(a) << endl;
```

如果我们需要在程序的多个地方重新计算数组和，该函数会更加有效。如果有几个不同的数组，我们可以使用同一个函数来计算它们的和：

```
#include <iostream> //Required for cout
using namespace std;
const int NROWS(4), NCOLS(4);
// Function prototypes.
int sum(int x[][NCOLS]);
...
int main()
{
    // Declare objects.
    int a[NROWS][NCOLS], b[NROWS][NCOLS];
    ...
    // Reference function to compute array sums.
    cout << "Sum of a = " << sum(a) << endl;
    cout << "Sum of b = " << sum(b) << endl;
```

我们现在展示这些语句中引用的函数：

```
/*--------------------------------------------------------------*/
/* This function returns the sum of the values in             */
/*   an array with NROWS rows and NCOLS columns.              */
/* PreCondition: Array X has NROWS and NCOLS.                 */
/* PostCondition: Sum of integer Values is returned.          */
/*--------------------------------------------------------------*/
int sum(int x[][NCOLS])
{
    // Declare and initialize local objects.
    int total(0);
    // Compute a sum of the array values.
    for (int i=0; i<NROWS; ++i)
    {
        for (int j=0; j<NCOLS; ++j)
        {
            total += x[i][j];
        }
    }
    // Return sum of array values.
    return total;
}
/*-----------------------------------------------------*/
```

在下一个示例中，我们开发一个计算数组中元素部分和的函数。要求求和的元素被假定位于数组左上角的一个**子数组**中。函数的参数包括原始数组以及子数组中的行数和列数。函数原型是

```
// Function prototype
int partial_sum( int x[][NCOLS], int m, int n );
```

因此，如果我们想求和数组 a 中阴影区域显示的元素，我们将使用引用

```
partial_sum(a, 2, 3);
```

| 2 | 3 | -1 | 9 |
|---|---|---|---|
| 0 | -3 | 5 | 7 |
| 2 | 6 | 3 | 2 |
| -2 | 10 | 4 | 6 |

此引用应计算从左上角开始、包含两行三列的子数组中元素的和；函数应返回值 6。该函数如下：

```
/*-----------------------------------------------------*/
/* This function returns the sum of the values       */
/* in a subarray of an array with a declared         */
/* NCOLS column size of NCOLS.                       */
int partialSum( int x[][NCOLS], int m, int n )
{
   // Declare and initialize local objects.
   int total( 0 ); // Compute a sum of subarray values.
   for ( int i = 0; i < m; ++i )
   {
      for ( int j = 0; j < n; ++j)
      {
         total += x[ i ][ j ];
      }
   }
   // Return sum of subarray values.
   return total;
}
/*--------------------------------------------------*/
```

![](img/0235a4ea835dc4575bd036e024a533b3_463_0.png)

只要符号常量 NCOLS 在函数作用域内，此函数可用于各种大小的二维数组。

## 练习 8.4

假设以下语句来自 main 函数：

```
int a[4][4] = {{2, 3, -1, 9}, {0, -3, 5, 7},
       {2, 6, 3, 2}, {-2, 10, 4, 6}};
```

手动确定本节开发的 partialSum 函数的以下引用的值：

- 1. partialSum(a,1,4);
- 2. partialSum(a,1,1);
- 3. partialSum(a,4,2);
- 4. partialSum(a,2,4,4);

作为最后一个示例，我们将通过添加两个新函数来修改程序 chapter8_1。假设我们想确定数据文件 engine.dat 中每次试验的平均发动机温度，然后报告每次试验中哪些发动机的温度低于平均温度。由于每次试验存储为数组中的一列，我们将编写一个函数来返回双精度型二维数组中指定列的平均值。我们还将编写一个函数从输入文件读取数据并将值存储在双精度型二维数组中。修改后的程序和函数定义如下。

```
/*--------------------------------------------------*/
/* Program chapter8_3 */
/* This program reads and stores temperature values */
/* for multiple trials from the input file engine.dat, */
/* then determines which engines performed below the */
/* average trial temperature. */
/*--------------------------------------------------*/
#include<iostream> //Required for cerr, cout
#include<fstream> //Required for ifstream
using namespace std;
```

```
//Declare constants and Function Prototypes
const int MAXCOLSIZE(50);
const int MAXROWSIZE(50);
double columnAvg(const double a[][MAXCOLSIZE],
                 int colNum, int rows);
void input2D(istream& in, double a[][MAXCOLSIZE],
             int rows, int cols);
int main()
{
   //Declare objects.
   int numEngines, numTrials;
   ifstream datal;
   double temps[MAXROWSIZE][MAXCOLSIZE];
   double avgTemp;

   //Open input file.
   datal.open("engine.dat");
   if(datal.fail())
   {
      cerr << "could not open engine.dat";
      exit(1);
   }

   //Input row and column size
   datal >> numEngines >> numTrials;

   //Read temperature data and store in array.
   input2D(datal, temps, numEngines, numTrials);

   datal.close();
   //Generate Report
   for(int i=0; i<numTrials; ++i)
   {
      //Calculate average engine temperature for each trial.
      avgTemp = columnAvg(temps, i, numEngines);

      //Generate Report
      cout << "\nTrial "<<(i+1)<<"\tAverage Engine Temperature "
           << avgTemp << endl;
      cout << "---------------------------------------------------\n";
      for(int j=0; j<numEngines; ++j)
      {
         if(temps[j][i] < avgTemp)
         {
            cout << "Engine " << (j+1)
                 << " performed below the average temp." << endl;
         }
      }
   }
   return 0;
}
/* end main -------------------------------------------------------------- */
```

```
/*-----------------------------------------------*/
/* This function reads data from an input stream and */
/* assigns the data to the 2D array, arr. */
/* Pre-conditions: */
/* The input stream in has been defined. */
/* The integer cols is < MAXCOLSIZE */
/* The integer rows is <= MAXROWSIZE */
/* Post-conditions: */
/* rows*cols values are assigned to the array, arr */
/*-----------------------------------------------*/
void input2D(istream& in, double arr[][MAXCOLSIZE],
             int rows, int cols)
{
   for (int i=0; i<rows; ++i)
   {
      for (int j=0; j<cols; ++j)
      {
         in >> arr[i][j];
      }
   }
}
/*-----------------------------------------------*/
```

```
/*-----------------------------------------------*/
/* This function returns the average of a column in the array */
/* arr. The integer colNum specifies the column number. */
/* Pre-conditions: */
/* The array arr has rowSize rows of valid data */
/* The integer colNum is < MAXCOLSIZE */
/*-----------------------------------------------*/
double columnAvg(const double arr[][MAXCOLSIZE], int colNum,
                 int rowSize)
{
   //Declare and initialize local variables
   double avg (0.0);

   //Sum all values in column colNum
   for(int i=0; i<rowSize; ++i)
   {
      avg += arr[i][colNum];
   }

   //Return the average
   return(avg/rowSize);
}
/*-----------------------------------------------*/
```

前置条件
后置条件

请注意，我们已在函数 input2D() 的初始注释块中包含了前置条件和后置条件。前置条件描述在调用函数时被假定为真的条件。如果前置条件不为真，则无法保证

