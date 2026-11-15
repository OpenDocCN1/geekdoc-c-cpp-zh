

点 x9：短时功率 = (1 + 1)/2 = 1
长时功率 = (1 + 1 + 4 + 16 + 25)/5 = 9.4
比值 = 1/9.4 = 0.11
1 2 1 1 1 5 4 2 1 1
短时窗口
长时窗口
点 x10：短时功率 = (1 + 1)/2 = 1
长时功率 = (1 + 1 + 1 + 4 + 16)/5 = 4.6
比值 = 1/4.6 = 0.22

利用之前计算的比值，在点 x5 和 x6 处可能发生了地震事件。由于点之间的时间间隔为 0.01 秒，与地震事件对应的时间为 0.05 秒和 0.06 秒。（我们假设文件中的第一个点发生在 0.0 秒。）

## 4. 算法开发

我们首先开发分解大纲，因为它将解决方案划分为一系列顺序步骤。

### 分解大纲

- 1. 读取数据头并分配内存。
- 2. 从数据文件读取地震数据，并从键盘读取功率测量点数。
- 3. 计算功率比值并打印可能的地震事件时间。

步骤 3 涉及计算功率比值并将其与阈值进行比较，以确定是否发生了可能的事件。由于我们需要为每个可能的事件位置计算两个功率测量值，因此我们将功率测量实现为一个函数。现在可以开发主函数和功率函数的伪代码细化了：

### 伪代码细化

```
main: set threshold to 1.5
read npts and time-interval
allocate memory for sensor array
read the values into sensor array
read short-window, long-window from keyboard
set k to long-window - 1
while k < npts
    set short-power to power(sensor, short-window, k)
    set long-power to power(sensor, long-window, k)
    set ratio to short-power / long-power
    if ratio > threshold
        print k * time-interval
    increment k by 1
power(x, length, n):
    set xsquare to zero
    set k to 0
    while k < n
        add x[length - k] * x[length - k] to xsquare
    return xsquare / length
```

我们现在准备将伪代码转换为 C++：

```
/*
* Program chapter9_10
*
* This program reads a seismic data file and then
* determines the times of possible seismic events.
* Dynamic memory allocation is used.
*/
#include <fstream>//Required for ifstream
#include <string> //Required for string
#include <cmath> //Required for pow()
using namespace std;

// Set threshold.
const double THRESHOLD = 1.5;

// Function prototypes.
double power_w(double arr[], int length, int n);
int main()
{
    // Declare objects.
    int k, npts, short_window, long_window;
    double time_incr, *sensor, short_power, long_power,
        ratio;
    string filename;
    ifstream fin;

    // Prompt user for file name and open file for input.
    cout << " Enter name of input file\n";
    cin >> filename;
    fin.open(filename);

    if (fin.fail())
    {
        cerr << "error opening input file" << endl;
    }
    else
    // Read data header and allocate memory.
    fin >> npts >> time_incr;
    sensor = new double[npts];

    // Program continues if no exception is thrown.
    cout << "Memory allocated." << endl;

    // Read data into an array.
    for (k = 0; k < npts; ++k)
        fin >> sensor[k];

    // Read window sizes from the keyboard.
    cout << "Enter number of points for short-window: \n";
    cin >> short_window;
    cout << "Enter number of points for long-window: \n";
    cin >> long_window;

    // Compute power ratios and search for events.
    for (k = long_window - 1; k < npts; ++k)
    {
        short_power = power_w(sensor, k, short_window);
        long_power = power_w(sensor, k, long_window);
        ratio = short_power / long_power;
        if (ratio > THRESHOLD)
            cout << "Possible event at " << time_incr * k
                 << " seconds \n";
    }

    // Return memory to free-store, close file, and exit program.
    delete [] sensor;
    fin.close();

    return 0;
}

/**
*-------------------------------------------------------------*/
/*
* This function computes the average power in a
* specified window of a double array.
*/
double power_w(double arr[], int length, int n)
{
    // Declare and initialize objects.
    double xsquare = 0;

    // Compute sum of values squared in the array x.
    for (int k = 0; k < n; ++k)
    {
        xsquare += pow(arr[length - k], 2);
    }
    /* Return the average squared value. */
    return xsquare / n;
}
/*---------------------------------------*/
```

## 5. 测试

使用手算示例的数据文件运行程序的输出如下：

```
Memory allocated.
Enter number of points for short-window:
2
Enter number of points for long-window:
5
Possible event at 0.05 seconds
Possible event at 0.06 seconds
```

### 修改 9.3

修改事件检测程序以包含以下新功能：

- 1. 允许用户输入阈值。检查该值以确保它是大于 1 的正值。
- 2. 打印程序检测到的事件数量。（假设时间连续的事件都属于同一事件。因此，对于手算示例，检测到了一个事件。）
- 3. 使用 vector 类而不是数组，从而无需使用 new 和 delete。

## 9.6 使用 new 和 delete 时的常见错误

一旦动态分配的内存不再需要，就应始终将其返回到堆中，以便内存可用于另一次动态分配。这需要小心跟踪指向该内存空间的所有指针。在将 delete 运算符与指针一起用于将内存返回到堆后，该指针将指向无效的内存空间，或者，取决于编译器，它可能保留已删除内存的内存地址。在任何一种情况下，在指针被赋予新的有效地址之前，不应再次引用该指针。

使用指针和动态内存分配时容易出错，且这些错误难以查找。以下是一些更常见的错误：

- 在使用 `delete` 运算符将内存返回到堆后，引用指向动态分配内存的指针。
- 在内存不再使用时未将其返回到堆中。这通常被称为内存泄漏。
- 将 `delete` 运算符与未引用使用 `new` 运算符动态分配的内存的指针一起使用。
- 使用 `delete` 释放动态分配的数组时省略方括号。

为了避免与动态分配数组内存相关的许多错误，我们建议使用 `vector` 类。

## 练习 9.5

假设指针 `iptr`、`jptr` 和 `arr_ptr` 已通过以下语句定义：

```cpp
int *iptr, *jptr, *arr_ptr;
iptr = new int(10);
arr_ptr = new int[5];
```

绘制内存分配图，并显示以下每组语句生成的输出行（或行）。我们建议您对每个示例进行编程并运行，以确定在您的系统上生成的输出。

- 1.
  ```cpp
  jptr = iptr;
  cout << *iptr << ' ' << *jptr << endl;
  cout << iptr << ' ' << jptr << endl;
  delete iptr;
  cout << iptr << ' ' << jptr << endl;
  ```

- 2.
  ```cpp
  cout << arr_ptr << endl;
  for (int i = 0; i < 4; ++i)
      arr_ptr[i] = i;
  for (int i = 0; i < 4; ++i)
      cout << *arr_ptr++ << ' ';
  cout << endl << arr_ptr << endl;
  for (int i = 0; i < 4; ++i)
      cout << arr_ptr[i] << ' ';
  ```

### 练习 9.5 续

- 3.
  ```cpp
  for (int i = 0; i < 4; ++i)
      arr_ptr[i] = i;
  jptr = &arr_ptr[2];
  cout << arr_ptr << ' ' << jptr << endl;
  cout << *arr_ptr << ' ' << *jptr << endl;
  delete [] arr_ptr;
  cout << arr_ptr << ' ' << jptr << ' ' << *jptr << endl;
  ```

## 9.7 链式数据结构

当我们使用数组和向量等数据结构时，我们正在处理一个连续的内存块。访问数组或向量的单个元素很容易，因为每次访问都是从起始地址的固定偏移量。但是，除非该元素是最后一个元素，否则插入或删除元素并不容易。在除最后一个位置以外的任何位置插入或删除元素，需要将插入或删除元素下方的所有元素复制到新的内存位置。这非常低效，尤其是在处理非常大量的数据时。

链式数据结构，如链表、栈和队列，旨在实现高效的插入和删除。程序执行期间根据需要分配和删除内存，并使用指针链接元素，因为元素不形成连续的内存块。使用指针链接元素允许高效地插入和删除元素；链接需要重新分配，但不需要复制元素。但是，访问链式结构中的元素比数组访问效率低，因为我们必须为每次访问遍历结构。要遍历链式数据结构，我们必须从结构中的第一个元素开始，沿着链接访问后续元素，直到到达要访问的元素。

- 遍历

### 链表

- 链表

链表是一种由指针链接的一组元素组织起来的数据结构。单个元素由数据和指向下一个元素的指针组成。我们通常假设元素中存储的数据有一定顺序，例如升序，并且我们可能希望从这个有序列表中插入新元素或删除元素。

图 9.4 说明了一个包含四个元素的链表，包含有序信息 10、14、21、35。一个单独的指针（我们将其标记为 head）指向链表中的第一个元素。

要访问链表中的数据，我们使用 head 指针来引用第一个元素中的信息（本示例中包含值 10 的元素）。然后，由于第一个元素包含指向下一个元素（包含值 14 的元素）的指针，我们可以使用此信息移动到第二个元素。同样，我们使用第二个元素中的指针移动到第三个元素。链表中的最后一个元素将包含指针值 nullptr，以指示我们已到达列表中的最后一个元素。我们在图表中使用符号 $\Omega$ 来表示 nullptr 值。

