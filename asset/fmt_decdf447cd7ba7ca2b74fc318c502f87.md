
```
for (int degrees=0; degrees<=360; degrees+=10) {

    radians = degrees*PI/180;

    cout << setw(6) << degrees << setw(10) << radians << endl;

}

// 退出程序。

return 0;

}
```

`for` 循环中的初始化和修改表达式可以包含多个语句，正如这个 `for` 语句所示，它在循环中初始化并更新了两个对象。

## 第 4 章控制结构：重复

```cpp
for (int k=1, j=5; k<=10; k++, j++)
{
  sum_1 += k;
  sum_2 += j;
}
```

当使用更多一个语句时，它们用逗号隔开，并从左到右执行。这个`逗号运算符`在运算符优先级中是最后执行的。

逗号运算符

### 练习！

对于第 1 到 5 题，确定 `for` 循环执行的次数。

1. `for` (int k=3; k<=20; k++))
{
  statements;
}
2. `for` (int k=3; k<=20; ++k)
{
  statements;
}
3. `for` (int count=-2; count<=14; count++)
{
  statements;
}
4. `for` (int k=2; k>=10; k)
{
  statements;
}
5. `for` (int time=10; time>=5; time++)
{
  statements;
}
6. 在嵌套 `for` 循环执行后，`count` 的值是多少？
int count(0);
for(int k=-1; k<4; k++)
{
  for(int j=3; j>0; j--)
{
    count++;
  }
}

> $^1$http://en.wikipedia.org/wiki/Trilateration 上的“三边测量法”文章提供了确定球面表面交点的数学推导。

### 2. 输入/输出描述

下图显示了程序的输入包括四对连续的数据（卫星 ID, 穿中传输时间）。输出是每个卫星的伪距离，随后是距离接收器最近的卫星 ID。

![](img/4456642232e4f4a18bd7dfe37e70176d_171_0.png)

### 3. 手算示例

假设第一颗卫星的 ID 为 23，相应的传输时间为 .001 秒；第一颗卫星的伪距离计算为 `transit_time*c = 299792 m`。

### 4. 算法开发

我们首先开发分解大纲，因为它将解决方案分解为一系列顺序的步骤：

### 分解大纲
对于每颗卫星：

- 提示用户输入卫星 ID 和传输时间。
- 输入 ID 和传输时间。
- 计算伪距离。
- 确定卫星是否离接收器最近的。
- 打印 ID 和伪距离。
- 打印距离接收器最近的卫星 ID。

步骤 1 到 5 将对四颗卫星中的每一个进行重复。这表明需要计数循环或 `for` 循环。在完善此算法时，我们将特别注意第 4 步。为了确定哪颗卫星离接收器最近，我们必须跟踪已计算出的最小伪距离。每当我们计算一个新的伪距离时，我们将该值与最小值进行比较。如果该值较小，我们将更新最小值并跟踪相应的卫星编号。我们将使用嵌套在 `for` 循环中的 `if` 语句来实现第 4 步所需的选择结构。算法的完善描述在如下的流程图中。

![](img/4456642232e4f4a18bd7dfe37e70176d_172_0.png)

流程图中描述的步骤现在足够详细可以转换为 C++：

```cpp
********************************************************************/
/* * 程序第4_5节 */
/* 此程序计算并打印
 * 4 颗卫星的伪代码。它还打印了距离
 * 接收器最近的卫星编号*/#include<iostream> // 需要 cout
#include<float> // 需要 DBL_MAX
using namespace std;
int main() {
// 声明并初始化对象
const double C(299792); // 每秒
const int NUMBER_OF_SATELLITES(4);
int satID;
double tTime, pseudorange, minRange = DBL_MAX;
// 提示用户
cout << "Enter id and transit time for \n";
for(int i=0; i<NUMBER_OF_SATELLITES; i++) {
cin >> satID >> tTime;
pseudorange = tTime*C;
// 检查最近的卫星
if(pseudorange < minRange) {
minRange = pseudorange;
satID = satID;
}
cout << "ID: " << satID << " Pseudorange: " << pseudorange << "\n";
}
// 输出最近的卫星
cout << "Closest satellite ID: " << satID << endl;
return 0;
}
```

## 5. 测试

使用手算示例，在三颗卫星的情况下，得到如下输出：

```
度到弧度 
     0    0.000000
10    0.174533
    20    0.349066
    30    0.523599
    40    0.698132
    50    0.872665
    60    1.047198
    70    1.221730
    80    1.396263
    90    1.570796
   100   1.745329
   110   1.919862
   120   2.094395
   130   2.268928
   140   2.443461
   150   2.617994
   160   2.792527
   170   2.967060
   180   3.141593
   190   3.316127
   200   3.490660
   210   3.665193
   220   3.839726
   230   4.014259
   240   4.188792
   250   4.363325
   260   4.537858
   270   4.712391
   280   4.886924
   290   5.061457
   300   5.235990
   310   5.410523
   320   5.585056
   330   5.759589
   340   5.934122
   350   6.108655
   360   6.283185
```

使用四颗卫星的数据，我们得到如下输出：

```
度到弧度 
     0    0.000000
    10    0.174533
    20    0.349066
    30    0.523599
    40    0.698132
    50    0.872665
    60    1.047198
    70    1.221730
    80    1.396263
    90    1.570796
   100   1.745329
   110   1.919862
   120   2.094395
   130   2.268928
   140   2.443461
   150   2.617994
   160   2.792527
   170   2.967060
   180   3.141593
   190   3.316127
   200   3.490660
   210   3.665193
   220   3.839726
   230   4.014259
   240   4.188792
   250   4.363325
   260   4.537858
   270   4.712391
   280   4.886924
   290   5.061457
   300   5.235990
   310   5.410523
   320   5.585056
   330   5.759589
   340   5.934122
   350   6.108655
   360   6.283185
ID: 23 Pseudorange: 299.792
ID: 45 Pseudorange: 599.584
ID: 12 Pseudorange: 159.876
ID: 88 Pseudorange: 879.3744
Closest satellite ID: 12
```

使用五颗卫星的数据，我们得到如下输出：

```
度到弧度 
     0    0.000000
    10    0.174533
    20    0.349066
    30    0.523599
    40    0.698132
    50    0.872665
    60    1.047198
    70    1.221730
    80    1.396263
    90    1.570796
   100   1.745329
   110   1.919862
   120   2.094395
   130   2.268928
   140   2.443461
   150   2.617994
   160   2.792527
   170   2.967060
   180   3.141593
   190   3.316127
   200   3.490660
   210   3.665193
   220   3.839726
   230   4.014259
   240   4.188792
   250   4.363325
   260   4.537858
   270   4.712391
   280   4.886924
   290   5.061457
   300   5.235990
   310   5.410523
   320   5.585056
   330   5.759589
   340   5.934122
   350   6.108655
   360   6.283185
ID: 23 Pseudorange: 299.792
ID: 45 Pseudorange: 599.584
ID: 12 Pseudorange: 159.876
ID: 88 Pseudorange: 879.3744
ID: 5 Pseudorange: 149.896
Closest satellite ID: 5
```

## 第4.5节 循环结构 159

![](img/4456642232e4f4a18bd7dfe37e70176d_176_0.png)

**图 4.6** 计数控制循环。

键盘输入并存储在计数器中。然后使用该计数器来控制输入循环的迭代次数。图4.6 是这种循环结构的流程图。
该循环可以使用 `while` 循环或 `for` 循环轻松实现。在下面的示例中，我们使用 `for` 循环来计算从键盘输入的组考试成绩的平均值：

```cpp
/*----------------------------------------------------------*/
/* Program chapter4_6 */
/* 此程序计算一组考试成绩的平均值。 */
#include<iostream>//Required for cin, cout
using namespace std;
int main()
{
// Declare and initialize objects.
double exam_score, sum(0), average;
int counter;
// Prompt user for input.
cout << "Enter the number of exam scores to be read: ";
cin >> counter;
cout << "Enter " << counter << " exam scores separated by ";
     << "whitespace: ";
// Input exam scores using counter-controlled loop.
for(int i=1; i<=counter; ++i)
```

图 4.7 哨兵控制循环。

## 第4.5节 输入循环的结构

```cpp
#include<iostream>//Required for cin, cout
using namespace std;
int main()
{
// Declare and initialize objects.
double exam_score, sum(0), average;
int count(0);
// Prompt user for input.
cout << "Enter exam scores separated by whitespace.\n";
cout << "Enter a negative value to indicate the end of data. ";
// Input exam scores using sentinel-controlled loop.
cin >> exam_score;
while(exam_score >= 0) {
  sum = sum + exam_score;
  count++;
  cin >> exam_score;
}
// Calculate average exam score.
average = sum/count;
cout << count << " students took the exam.\n";
cout << "The exam average is " << average << endl;
// Exit program
return 0;
}
```

### 数据末尾循环

数据末尾循环是读取输入数据最灵活的循环。该循环结构为：只要有新数据可用就继续执行循环内部的语句。不需要预先知道数据值的数量，也不需要哨兵值。当遇到数据末尾时，循环终止。记住 `cin` 的类型是 `istream`。可以通过 `cin` 调用 `eof()` 函数来确定是否遇到了数据末尾。`eof()` 函数是 `istream` 类的成员，如果调用对象时遇到了数据末尾，它返回 `true`。图4.8 是这种循环结构的流程图。数据末尾循环使用 `while` 循环实现，如下例所示，该示例计算了从键盘输入的组考试成绩的平均值：

- 程序 chapter4_7
- 此程序计算一组考试成绩的平均值。

```cpp
#include<iostream>//Required for cin, cout
using namespace std;
```

## 第4章 控制结构：重复

![](img/4456642232e4f4a18bd7dfe37e70176d_179_0.png)

图 4.8 数据末尾循环。

```cpp
int main()
{
// Declare and initialize objects.
double exam_score, sum(0), average;
int count(0);
// Prompt for input.
cout << "Enter exam scores separated by whitespace. ";
// Input exam scores using end-of-data loop.
cin >> exam_score;
while(!cin.eof()) {
    sum = sum + exam_score;
    count++;
    cin >> exam_score;
}
// Calculate average exam score.
average = sum/count;
cout << count << " students took the exam.\n";
cout << "The exam average is " << average << endl;
// Exit program
return 0;
}
```
