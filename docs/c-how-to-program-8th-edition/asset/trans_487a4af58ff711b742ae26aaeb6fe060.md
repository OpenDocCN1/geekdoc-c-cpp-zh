
选择数组中最小的元素，并将其与第一个元素交换。第二次迭代选择第二小的元素（即剩余元素中最小的元素），并将其与第二个元素交换。该算法继续执行，直到最后一次迭代选择第二大的元素，并将其与倒数第二个索引交换，从而将最大的元素留在最后一个索引中。第 *i* 次迭代后，数组中最小的 *i* 个项将按递增顺序排列在数组的前 *i* 个元素中。

例如，考虑以下数组

|  |  |  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|---|---|
| 34 | 56 | 4 | 10 | 77 | 51 | 93 | 30 | 5 | 52 |

实现选择排序的程序首先确定数组中的最小值（4），它包含在元素 2 中。程序将 4 与元素 0（34）中的值交换，结果为

|  |  |  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|---|---|
| 4 | 56 | 34 | 10 | 77 | 51 | 93 | 30 | 5 | 52 |

然后，程序确定剩余元素（除 4 之外的所有元素）中的最小值，即 5，它包含在元素 8 中。程序将 5 与元素 1 中的 56 交换，结果为

|  |  |  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|---|---|
| 4 | 5 | 34 | 10 | 77 | 51 | 93 | 30 | 56 | 52 |

在第三次迭代中，程序确定下一个最小值 10，并将其与元素 2（34）中的值交换。

|  |  |  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|---|---|
| 4 | 5 | 10 | 34 | 77 | 51 | 93 | 30 | 56 | 52 |

该过程一直持续到数组完全排序。

|  |  |  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|---|---|
| 4 | 5 | 10 | 30 | 34 | 51 | 52 | 56 | 77 | 93 |

第一次迭代后，最小元素位于第一个位置。第二次迭代后，两个最小元素按顺序位于前两个位置。第三次迭代后，三个最小元素按顺序位于前三个位置。

图 8.13 使用函数 selectionSort 和 swap 实现选择排序。函数 selectionSort（第 32–49 行）对数组进行排序。第 34 行声明变量 smallest，它将存储剩余数组中最小的元素的索引。第 37–48 行循环 size − 1 次。第 39 行将最小元素的索引设置为当前索引。第 42–45 行循环遍历剩余数组元素。对于每个元素，第 44 行将其值与最小元素的值进行比较。如果当前元素小于最小元素，第 45 行将当前元素的索引赋给 smallest。当这个循环结束时，smallest 将包含剩余数组中最小的元素的索引。第 47 行调用函数 swap（第 53–58 行），将剩余的最小元素放到数组中的下一个位置（即交换数组元素 array[i] 和 array[smallest]）。

```cpp
// Fig. 8.13: fig08_13.cpp
// Selection sort with pass-by-reference. This program puts values into an
// array, sorts them into ascending order and prints the resulting array.
#include <iostream>
#include <iomanip>
using namespace std;
```

**图 8.13**  |  按引用传递的选择排序。（第 1 部分，共 3 部分。）

```
Data items in original order
    2    6    4    8   10   12   89   68   45   37
Data items in ascending order
    2    4    6    8   10   12   37   45   68   89
```

**图 8.13** | 按引用传递的选择排序。（第 3 部分，共 3 部分。）

现在让我们更仔细地看看函数 swap。请记住，函数之间强制实施*信息隐藏*，因此 swap 无法访问 selectionSort 中的各个数组元素。由于 selectionSort *希望*能够访问要交换的数组元素，因此 selectionSort 将每个元素按引用传递给 swap——每个数组元素的地址被显式传递。尽管整个数组是按引用传递的，但单个数组元素通常按值传递。因此，selectionSort 在 swap 调用（第 47 行）中对每个数组元素使用地址运算符（&），以实现按引用传递。函数 swap（第 53–58 行）在指针变量 `element1Ptr` 中接收 `array[i]`。信息隐藏使 swap 无法“知道”名称 `array[i]`，但 swap 可以将 `*element1Ptr` 用作 `array[i]` 的同义词。因此，当 swap 引用 `*element1Ptr` 时，它实际上引用的是 selectionSort 中的 `array[i]`。类似地，当 swap 引用 `*element2Ptr` 时，它实际上引用的是 selectionSort 中的 `array[smallest]`。

尽管在图 8.13 的 swap 函数中，swap 不允许使用以下语句

```
hold = array[i];
array[i] = array[smallest];
array[smallest] = hold;
```

但通过以下代码可以达到完全相同的效果

```
int hold = *element1Ptr;
*element1Ptr = *element2Ptr;
*element2Ptr = hold;
```

应当注意函数 selectionSort 的几个特点。函数头（第 32 行）将 array 声明为 `int * const array`，而不是 `int array[]`，以表明该函数接收一维数组作为参数。参数 array 的指针和参数 size 都声明为 const，以强制实施最小权限原则。尽管参数 size 接收 main 中某个值的副本，但修改该副本不能改变 main 中的值；selectionSort 不需要修改 size 来完成其任务——在 selectionSort 执行期间，数组大小保持不变。因此，size 被声明为 const，以确保它不会被修改。如果在排序过程中修改数组的大小，排序算法将无法正确运行。

函数 selectionSort 接收数组的大小作为参数，因为该函数必须拥有该信息才能对数组进行排序。当数组传递给函数时，函数*仅*接收数组第一个元素的内存地址；数组大小必须单独传递给函数。

通过将函数 selectionSort 定义为接收数组大小作为参数，我们使该函数可供*任何*对*任意*大小的一维 int 数组进行排序的程序使用。数组大小本可以直接编程到函数中，但这会限制函数只能处理特定大小的数组，并降低函数的可重用性——只有处理函数中“硬编码”的特定大小的一维 int 数组的程序才能使用该函数。

> **软件工程观察 8.4**  
> *将数组传递给函数时，还要传递数组的大小（而不是在函数中内置对数组大小的了解）——这会使函数更具可重用性。*

## 8.7 sizeof 运算符

编译时一元运算符 sizeof 在程序编译期间以字节为单位确定数组（或任何其他数据类型、变量或常量）的大小。当应用于数组名时，如图 8.14（第 13 行）所示，sizeof 运算符返回数组中总的字节数，作为 size_t 类型的值（一种无符号整数类型，至少与 unsigned int 一样大）。例如，这与 vector<int> 的大小不同，后者是 vector 中整数元素的个数。我们用来编译此程序的计算机将 double 类型的变量存储在 8 字节内存中，而 array 被声明为具有 20 个元素（第 11 行），因此 array 在内存中使用 160 字节。当应用于接收数组作为参数的函数中的指针参数（第 22 行）时，sizeof 运算符返回指针的大小（以字节为单位）（在我们使用的系统上为 4）——而不是数组的大小。

> **常见编程错误 8.7**  
> *在函数中使用 sizeof 运算符查找数组参数的字节大小时，得到的是指针的字节大小，而不是数组的字节大小。*

```cpp
// Fig. 8.14: fig08_14.cpp
// Sizeof operator when used on an array name
// returns the number of bytes in the array.
#include <iostream>
using namespace std;

size_t getSize( double * ); // prototype

int main()
{
   double array[ 20 ]; // 20 doubles; occupies 160 bytes on our system

   cout << "The number of bytes in the array is " << sizeof( array );

   cout << "The number of bytes returned by getSize is "
        << getSize( array ) << endl;
} // end of main

// return size of ptr
size_t getSize( double *ptr )
{
   return sizeof( ptr );
} // end of function getSize
```

**图 8.14** | sizeof 运算符应用于数组名时返回数组中的字节数。（第 1 部分，共 2 部分。）
