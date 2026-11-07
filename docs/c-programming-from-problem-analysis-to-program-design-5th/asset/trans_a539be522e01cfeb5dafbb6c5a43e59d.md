
列表中，我们将搜索列表的起始索引**first**和结束索引**last**相加，然后除以2来计算其中间索引。也就是说，\(mid = \frac{first + last}{2}\)。初始时，`first = 0`，并且（由于C++数组索引从0开始，`listLength`表示列表中的元素个数）`last = listLength - 1`。（注意，无论列表中的元素个数是偶数还是奇数，计算中间元素的这个公式都成立。）

下面的C++函数实现了二分查找算法。如果在列表中找到该项，则返回其位置。如果查找项不在列表中，则返回−1。

```cpp
int binarySearch(const int list[], int listLength, int searchItem)
{
    int first = 0;
    int last = listLength - 1;
    int mid;

    bool found = false;

    while (first <= last && !found)
    {
        mid = (first + last) / 2;

        if (list[mid] == searchItem)
            found = true;
        else if (list[mid] > searchItem)
            last = mid - 1;
        else
            first = mid + 1;
    }

    if (found)
        return mid;
    else
        return -1;
} // end binarySearch
```

注意，在二分查找算法中，每次循环都要进行两次关键（项）比较，除非是成功的情况——循环的最后一次——此时只进行一次关键比较。

接下来，我们在图10-19所示的列表上逐步演示二分查找算法。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_618_0.png)

**图10-19**  用于二分查找的有序列表

图10-19中列表的大小为12，因此`listLength = 12`。假设我们要查找的项是89，所以`searchItem = 89`。在执行while循环之前，first = 0，last = 11，found = false。下面我们跟踪while循环的执行，展示每次迭代中first、last、mid的值以及关键比较的次数。

| 迭代 | first | last | mid | list[mid] | 关键比较次数 |
|---|---:|---:|---:|---:|---:|
| 1 | 0 | 11 | 5 | 39 | 2 |
| 2 | 6 | 11 | 8 | 66 | 2 |
| 3 | 9 | 11 | 10 | 89 | 1（found为true） |

该项在位置10处找到，关键比较总次数为5。

接下来，让我们在列表中查找34，因此`searchItem = 34`。在执行while循环之前，first = 0，last = 11，found = false。与之前一样，下面我们跟踪while循环的执行，展示每次迭代中first、last、mid的值以及关键比较的次数。

| 迭代 | first | last | mid | list[mid] | 关键比较次数 |
|---|---:|---:|---:|---:|---:|
| 1 | 0 | 11 | 5 | 39 | 2 |
| 2 | 0 | 4 | 2 | 19 | 2 |
| 3 | 3 | 4 | 3 | 25 | 2 |
| 4 | 4 | 4 | 4 | 34 | 1（found为true） |

该项在位置4处找到，关键比较总次数为7。

现在让我们查找22，因此`searchItem = 22`。在执行while循环之前，first = 0，last = 11，found = false。与之前一样，下面我们跟踪while循环的执行，展示每次迭代中first、last、mid的值以及关键比较的次数。

| 迭代 | first | last | mid | list[mid] | 关键比较次数 |
|---|---:|---:|---:|---:|---:|
| 1 | 0 | 11 | 5 | 39 | 2 |
| 2 | 0 | 4 | 2 | 19 | 2 |
| 3 | 3 | 4 | 3 | 25 | 2 |
| 4 | 3 | 2 |  |  | 循环停止（因为first > last）；查找失败 |

这是一次不成功的查找。关键比较总次数为6。

从这些二分查找算法的跟踪过程可以看出，每次循环都会将子列表的大小减半。也就是说，下一次循环时你要搜索的子列表大小是上一次子列表的一半。

我们把它留作练习，请你编写一个程序来测试binarySearch函数。请参阅本章末尾的编程练习2。

## 二分查找的性能

假设L是一个大小为1024的有序列表，我们想确定一个项x是否在L中。根据二分查找算法，while循环的每次迭代都会将搜索列表的大小减半。（例如，参见图10-17和图10-18。）因为1024 = 2^{10}，所以while循环最多需要11次迭代来确定x是否在L中。由于while循环的每次迭代都会进行两次项（关键）比较，即x与L中的元素比较两次，因此二分查找最多需要22次比较来确定x是否在L中。另一方面，回顾一下，顺序查找平均需要512次比较来确定x是否在L中。

为了更好地理解二分查找相比顺序查找有多快，假设L的大小为1048576。因为1048576 = 2^{20}，所以二分查找中的while循环最多需要21次迭代来确定一个元素是否在L中。while循环的每次迭代都会进行两次关键（即项）比较。因此，要确定一个元素是否在L中，二分查找最多需要进行42次项比较。

注意，40 = 2 * 20 = 2 * log_2(2^{20}) = 2 * log_2(1048576)。

一般而言，假设L是一个大小为n的有序列表。进一步假设n是2的幂，即对于某个非负整数m，n = 2^m。while循环每次迭代之后，大约剩下一半的元素需要搜索，也就是说，下一次迭代的搜索子列表大小是当前子列表的一半。例如，第一次迭代后，搜索子列表的大小约为n/2 = 2^{m-1}。不难看出，while循环的最大迭代次数约为m + 1。同时m = log_2n。每次迭代进行两次关键比较。因此，确定一个元素x是否在L中的最大比较次数为2(m + 1) = 2(log_2n + 1) = 2log_2n + 2。

## vector 类型（类）

> 注意：本节可以跳过，不会导致任何不连贯。

第9章和本章前面几节描述了如何使用数组来实现和处理列表。到目前为止所讨论的数组的一个局限性是，一旦创建了数组，其大小就固定不变。这意味着数组中只能存储固定数量的元素。此外，在数组的特定位置插入元素可能需要移动数组中的元素。类似地，从数组中删除元素也可能需要移动数组中的元素，因为我们通常不会在存有数据的数组位置之间留下空位。通常，数组的空位在末尾。

除了数组之外，C++还提供了vector类型（通常称为vector类）来实现列表。使用vector类型声明的变量称为vector容器（或vector、vector对象，或简称为对象）。与数组不同，vector对象的大小在程序执行期间可以增大和缩小。因此，你无需担心数据元素的数量。

当你声明一个vector对象时，必须指定该vector对象存储的元素类型。表10-1描述了声明vector对象的多种方式。

**表10-1** 声明和初始化vector对象的各种方式

| 语句 | 作用 |
|---|---|
| `vector<elemType> vecList;` | 创建不包含任何元素的空vector对象vecList。 |
| `vector<elemType> vecList(otherVecList);` | 创建vector对象vecList，并用vector otherVecList的元素初始化vecList。vecList和otherVecList类型相同。 |
| `vector<elemType> vecList(size);` | 创建大小为size的vector对象vecList。vecList使用默认值初始化。 |
| `vector<elemType> vecList(n, elem);` | 创建大小为n的vector对象vecList。vecList使用元素elem的n个副本初始化。 |

在表10-1中，elemType指定要存储在vecList中的元素的数据类型。

### 示例10-3

- a. 下面的语句将intList声明为一个空的vector对象，元素类型为`int`。

```cpp
vector<int> intList;
```

- b. 下面的语句将intList声明为大小为10的vector对象，元素类型为`int`。intList的元素被初始化为0。

```cpp
vector<int> intList(10);
```

