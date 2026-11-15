

| 0.6 | 3.5 |
| --- | --- |
| 0.7 | 1.5 |
| 0.8 | 1.5 |
| 0.9 | 1 |

## 练习 7.1

显示以下各组语句中定义的数组的内容：

- 1. `int x[10]={-5, 4, 3};`
- 2. `char letters[] = {'a', 'b', 'c'};`
- 3. `double z[5];`
  ...
  `z[1] = -5.5;`
  `z[2] = z[3] = fabs(z[1]);`
- 4. `double time[9];`
  ...
  `for (int k=0; k<8; k++)`
  {
  `time[k] = (k-4)*0.1;`
  }

- 5. 显示以下程序生成的输出：
  ```
  #include<iostream>
  using namespace std;
  int main()
  {
   int arr[5], i, k;
   for(i=0; i<5; ++i)
   {
    for(k=1; k<3; ++k)
    {
     arr[i] += k*1;
    }
    cout << "arr[" << i << "] is " << arr[i] << endl;
   }
   return 0;
  }
  ```

## 基于范围的 for 语句

C++11 支持基于范围的 for 语句，用于遍历一组数据或数据集合。基于范围的 for 的一般形式如下：

```
for(declaration: range)
{
 statements;
 }
```

声明用于声明与指定范围中包含的数据相同类型的变量。该变量将依次取范围中的每个值，从开始到结束。

### 语句框 7.2
**基于范围的 for 语句：** 基于范围的 for 语句遍历一组数据。

**语法：**
`for(declaration:range)`
`statement;`
`{`
`statement block`
`}`

**示例：**
`double time[5] = {0.0,0.1,0.2,0.3,0.4};`
`for(double t:time)`
`cout << t << endl;`
`for(double& t:time)`
`cin >> t;`

`string aString("Salutations:");`
`for(char ch:aString)`
`{`
`    if(ispunct(ch))`
`        ++punctCount;`
`}`

范围可以是数组、字符串或 C++ 标准模板库中的任何容器。声明变量可以定义为获取范围中数据的值或对范围中数据的引用。程序 chapter7_3 说明了基于范围的 for 语句的用法。

```
/* * --------------------------------------------------------------*/
/* * Program chapter7_3 */
/* * This program reads time and motion data from a file */
/* * then finds maximum motion and time of occurrence. */
/* */
#include<iostream> //Required for cout
#include<fstream> //Required for ifstream
using namespace std;
int main()
{
// Declare objects.
double time[10], motion[10];
ifstream sensor3("sensor3.dat");
// Check for successful open and read data into arrays.
if(!sensor3.fail())
{
    for(int k=0; k<10; ++k)
    {
        sensor3 >> time[k] >> motion[k];
        cout << time[k] << '\t' << motion[k] << endl;
    }
    //find max motion and time of occurrence
    int count(0);
    double maxMotion, timeOfMax;
    //initialize maxMotion;
    maxMotion = motion[0];
    for(double m:motion)
    {
        if(m > maxMotion)
        {
            maxMotion = m;
            timeOfMax = time[count];
        }
        ++count;
    }
    cout << "Maximum motion of " << maxMotion
         << " occurred at time " << timeOfMax << endl;
}
else
{
    cout << " Could not open file sensor3.dat..goodbye." << endl;
}
return 0;
}
```

如果数据文件 sensor3.dat 包含以下数据

| 0.0 | 1 |
| --- | --- |
| 0.1 | 1 |
| 0.2 | 2.5 |
| 0.3 | 1.7 |
| 0.4 | 2 |
| 0.5 | 2.5 |
| 0.6 | 3.5 |
| 0.7 | 1.5 |
| 0.8 | 1.5 |
| 0.9 | 1 |

程序 chapter7_3 的输出如下：

| 0 | 1 |
| --- | --- |
| 0.1 | 1 |
| 0.2 | 2.5 |
| 0.3 | 1.7 |
| 0.4 | 2 |
| 0.5 | 2.5 |
| 0.6 | 3.5 |
| 0.7 | 1.5 |
| 0.8 | 1.5 |
| 0.9 | 1 |

最大运动量为 3.5，发生在时间 0.6。

## 计算与输出

对数组元素的计算与对简单对象的计算方式相同，但必须使用偏移量来指定单个数组元素。为说明这一点，下一个程序使用 `for` 循环从数据文件中读取指定数量的浮点值，并将值赋给数组 y。y 的声明大小为 100，因此程序最多允许向 y 分配 100 个值，以避免超出数组边界。程序确定数据的平均值并将其存储在 yAve 中。然后，统计并打印数组中大于平均值的值的数量。

```
/*
 * Program chapter7_4
 *
 * This program reads at most 100 values from a data
 * file and determines the number of values greater
 * than the average.
 */
#include<iostream> //Required for cin, cout, cerr.
#include<fstream> //Required for ifstream.
#include<string> //Required for string.
using namespace std;

int main()
{
 // Define maximum array size constant
 const int N = 100;

 // Declare and initialize objects.
 // stream filename:
 int count=0, numberofValues;
 string filename;
 double y[N], yAve, sum=0;
 ifstream lab;

 // Prompt user for name of input file
 cout << "Enter name of the input file";
 cin >> filename;

 // Open data file and read data into an array.
 // Compute a sum of the values.
 lab.open(filename);
 if(lab.fail())
 {
 cerr << "Error opening input file\n";
 exit(1);
 }

 /* File has been opened. */
 /* Read number of data values. */
 lab >> numberOfValues;
 // Don't exceed the bound of the array.
 if(numberOfValues > N)
 {
     cerr << "Number of data values, " << numberOfValues
          << " exceeds maximum array size of " << N << endl
          << N << " values will be read." << endl;
     numberOfValues = N;
 }
 int k;
 for(k=0; k<numberOfValues; ++k)
 {
     lab >> y[k];
     sum += y[k];
 }
 // Compute average and count values that
 // are greater than the average.
 yAve = sum/numberOfValues;
 for(k=0; k<numberOfValues; ++k)
 {
     if(y[k] > yAve)
         count++;
 }
 // Print count.
 cout << count << " values greater than the average \n";
 // Close file and exit program.
 lab.close();
 return 0;
}
```

如果此程序的目的是确定数据文件中值的平均值，则不需要数组。读取值的循环可以将每个值读入同一个对象，在读取下一个值之前将其值加到总和中。然而，因为我们需要将每个值与平均值进行比较，以统计大于平均值的值的数量，所以我们选择使用数组来存储值，以便可以第二次访问它们。

打印数组值时使用偏移量来指定所需的单个值。例如，以下语句打印前一个示例中数组 y 的第一个值和最后一个值：

```
cout << "first and last array values: \n";
cout << y[0] << " " << y[numberOfValues-1] << endl;
```

以下循环打印 y 的所有 100 个值，每行一个：

```
cout << "y values: \n";
for(int k=0; k<N; ++k)
{
 cout << y[k] << endl;
}
```

请注意，数组中的值必须逐个打印，因为 C++ 通常不支持对数组进行聚合输出操作。在打印像这样的大数组时，我们可能希望在同一行打印几个数字。以下语句使用取模运算符在每组五个值打印之前换行：

```
cout << "y values: \n";
for (int k=0; k<numberOfValues; ++k)
{
 if (k%5 == 0)
 cout << y[k] << endl;
 else
 cout << y[k] << " ";
}
cout << endl;
```

类似于此处说明的语句也可用于将数组值写入数据文件。例如，以下语句将使用文件流 sensor 将 y[k] 的值打印到数据文件的一行中：

```
sensor << y[k] << endl;
```

由于包含了 endl 操纵符，写入文件的下一个值将在新行上。

## 修改 7.1

- 1. 不使用数组重写程序 chapter7_4。提示：计算平均值，然后关闭并重新打开输入文件，统计大于平均值的值的数量。在第二次读取文件之前，是否需要清除 eofbit？

- 2. 考虑以下程序：

  ```
  #include<iostream>
  using namespace std;
  int main()
  {
   char greeting[] = "HelloWorld";
   int numbers[] = {1,2,3,4,5};
   cout << greeting << endl;
   cout << numbers << endl;
   return 0;
  }
  ```

  编译并运行此程序。解释输出。

