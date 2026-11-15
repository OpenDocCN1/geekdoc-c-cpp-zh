

内存中的新对象。要为类型 int 的单个对象分配内存，可以使用以下任意一组语句：

```cpp
// Example 1
// Dynamically allocate memory for one integer object.
// No initial value is given to the object.
int *ptr;
ptr = new int;
```

```cpp
// Example 2
// Dynamically allocate memory for one integer object.
// Give an initial value of -1 to the object.
int *ptr;
ptr = new int(-1);
```

在前面两个示例中，new 运算符返回一个值，该值被赋给指针。如果堆上有可用内存，指针将包含已分配内存的地址。在第一个示例中，未为新分配的内存分配初始值，如图 9.1 所示。在第二个示例中，指定了值 -1 作为初始值，并将其赋给新分配的内存，如图 9.2 所示。

由于堆是有限的，因此新内存请求可能无法得到满足。如果堆上没有足够的内存来满足内存请求，通常情况下，new 运算符会抛出名为 bad_alloc 的异常。此异常将终止程序的执行。C++ 支持一种机制，允许程序检测异常并从潜在错误中恢复。这种机制称为异常处理。本文不涉及异常处理。

![](img/0235a4ea835dc4575bd036e024a533b3_525_0.png)

图 9.1 堆图。示例 1。

![](img/0235a4ea835dc4575bd036e024a533b3_526_0.png)

图 9.2 堆图。示例 2。

## 动态分配的数组

动态内存分配在解决需要大型数组的工程问题时非常有用。假设我们想要动态分配一块内存来存储包含 npts 个元素的 double 数组。（在此示例中，我们为 npts 赋予一个小值以作说明，但更常见的是它是一个大值，由程序中的其他语句计算得出，或从键盘或数据文件读取。）以下语句指定所需的分配：

```cpp
// Declare objects.
int npts = 10;
double *dptr;
...
// Dynamically allocate memory.
dptr = new double[npts];
```

如图 9.3 所示，在堆上分配一块连续内存来容纳 10 个 double 类型的对象。指针 dptr 被赋予数组中第一个元素的内存地址。可以使用指针表示法引用数组，例如 *(dptr+2)。也可以使用标准数组表示法引用数组，例如 dptr[2]。

使用 new 动态分配对象时，为对象指定的数据类型可以是任何内置数据类型或任何程序员定义的类类型。

## delete 运算符

当程序使用完通过 new 动态分配的内存后，可以使用 delete 运算符将内存返回给堆，即释放内存。以下程序说明了 new 和 delete 运算符的使用：

![](img/0235a4ea835dc4575bd036e024a533b3_527_0.png)

图 9.3 在堆上分配的内存块。

```cpp
/*-------------------------------- Program chapter9_9 --------------------------------*/
/* Program chapter9_9 */
/* This program illustrates the use of operators new and delete. */
/* */
#include <iostream> //Required for cout
using namespace std;

int main()
{
// Declare objects.
int *ptr, npts(10);
double *darr_ptr;

// Dynamically allocate one integer object.
ptr = new int(-1);

// Dynamically allocate array of type double.
darr_ptr = new double[npts];

// Assign what is pointed to by ptr to all elements of dynamic array.
for(int i=0; i<npts; ++i)
{
    darr_ptr[i] = *ptr;
}

// Print all values in dynamic array.
for(int i=0; i<npts-1; ++i)
{
    cout << darr_ptr[i] << ' ';
}
cout << endl;
}

// Return memory to free-store.
delete ptr;
delete[] darr_ptr;
return 0;
}
*********************************************************************************/
```

该程序的输出如下：

-1 -1 -1 -1 -1 -1 -1 -1 -1 -1

![](img/0235a4ea835dc4575bd036e024a533b3_528_0.png)

> 释放数组时，delete 运算符需要空方括号。如果省略方括号，程序可能无法继续正确执行。

## 9.5 应用问题求解：地震事件检测

使用称为地震仪的特殊传感器来收集地球运动信息。这些地震仪可以在被动环境中使用，记录地球的运动，包括地震和潮汐运动。通过使用多个地震仪的数据分析地震的地面运动，可以确定地震的震中和强度。地震强度通常使用里氏震级来测量，这是一个以美国地震学家 C. F. Richter 命名的 1 到 10 的等级。

编写一个程序，从名为 seismic.dat 的数据文件中读取一组地震仪数据。文件的第一行包含两个值：文件中随后的地震仪数据读数的数量，以及连续测量之间发生的时间间隔（以秒为单位）。数组内存根据地震数据文件中的地震仪数据读数数量动态分配。时间间隔是一个浮点值，我们假设所有测量之间都有相同的时间间隔。读取并存储数据测量值后，程序应使用功率比识别可能的地震，也称为地震事件。在特定时间点，该比率是短时功率测量值除以长时功率测量值的商。如果比率大于给定阈值，则在该时间点可能发生了事件。给定数据测量中的特定点时，短时功率是使用指定点加上紧邻指定点之前的少量点的测量值的平均功率，即平均平方值。长时功率是使用指定点加上紧邻指定点之前的较多点的测量值的平均功率。（用于计算的点集有时称为数据窗口。）阈值通常大于 1，以避免在恒定数据中检测事件，因为如果数据值全部相同，短时功率等于长时功率。假设短时功率和长时功率的测量数量从键盘读取。将阈值设置为 1.5。

### 1. 问题描述

使用数据文件中的一组地震仪测量值确定可能地震事件的位置。

### 2. 输入/输出描述

该程序的输入是名为 seismic.dat 的数据文件，以及用于短时功率和长时功率的测量数量。输出是一份报告，给出潜在地震事件的时间。

![](img/0235a4ea835dc4575bd036e024a533b3_529_0.png)

### 3. 手算示例

假设数据文件包含以下数据，其中包括随后的点数（11）和点之间的时间间隔（0.01），随后是对应于值序列 x0, x1, ... x10 的 11 个值：

```
11 0.01
1 2 1 1 1 5 4 2 1 1 1
```

如果短时功率测量使用两个样本，长时功率测量使用五个测量值，那么我们可以从窗口中最右侧的点开始计算功率比：

```
1 2 1 1 1 5 4 2 1 1 1
```

```
short window
_______
long window
```

点 x4：短时功率 = (1 + 1)/2 = 1

长时功率 = (1 + 1 + 1 + 4 + 1 )/5 = 1.6

比率 = 1/1.6 = 0.63

```
1 2 1 1 1 5 4 2 1 1 1
             _______
short window
long window
```

点 x5：短时功率 = (25 + 1)/2 = 13

长时功率 = (25 + 1 + 1 + 1 + 4)/5 = 6.4

比率 = 13/6.4 = 2.03

```
1 2 1 1 1 5 4 2 1 1 1
short window
long window
```

点 x6：短时功率 = (16 + 25)/2 = 20.5

长时功率 = (16 + 25 + 1 + 1 + 1)/5 = 8.8

比率 = 20.5/8.8 = 2.33

```
1 2 1 1 1 5 4 2 1 1 1
short window
long window
```

点 x7：短时功率 = (4 + 16)/2 = 10

长时功率 = (4 + 16 + 25 + 1 + 1)/5 = 9.4

比率 = 10/9.4 = 1.06

```
1 2 1 1 1 5 4 2 1 1 1
short window
long window
```

点 x8：短时功率 = (1 + 4)/2 = 2.5

长时功率 = (1 + 4 + 16 + 25 + 1)/5 = 9.4

比率 = 2.5/9.4 = 0.27

```
1 2 1 1 1 5 4 2 1 1 1
short window
long window
```

