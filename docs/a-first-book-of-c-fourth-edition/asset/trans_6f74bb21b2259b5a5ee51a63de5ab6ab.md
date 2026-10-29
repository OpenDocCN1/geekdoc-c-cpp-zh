

# 第7章

章节补充：搜索和排序方法

![](img/202cface8244f523c2641baa2e00d7dd_348_0.png)

**图 7.11** 二分搜索算法

在伪代码和图 7.11 的流程图中，都使用了一个 while 循环来控制搜索。初始列表是通过将左索引值设为 0 并将右索引值设为列表中元素数量减 1 来定义的。然后将中间元素取为左索引值和右索引值整数化后的平均值。

在与中间元素进行比较之后，通过将左索引移动到中间值上方一个整数值，或将右索引移动到中间值下方一个整数值来随后限制搜索。此过程一直持续到找到该元素或左索引值和右索引值变得相等为止。`binarySearch()` 函数展示了该算法的 C++ 版本：

// this function returns the location of key in the list
// a -1 is returned if the value is not found
int binarySearch( int list[], int size, int key)
{
    int left, right, midpt;
    left = 0;
    right = size - 1;

    while (left <= right)
    {
        midpt = (int) ((left + right) / 2);
        if (key == list[midpt])
        {
            return midpt;
        }
        else if (key > list[midpt])
            left = midpt + 1;
        else
            right = midpt - 1;
    }

    return -1;
}
```

为测试此函数，使用了程序 7.10。程序 7.10 的一次示例运行产生了以下结果：

```
Enter the item you are searching for: 101
The item was found at index location 9
```

## 程序 7.10

```
#include <iostream>
using namespace std;

int binarySearch(int [], int, int);  // function prototype
int main()
{
    const int NUMEL = 10;
    int nums[NUMEL] = {5,10,22,32,45,67,73,98,99,101};
    int item, location;

    cout << "Enter the item you are searching for: ";
    cin >> item;
    location = binarySearch(nums, NUMEL, item);
    if (location > -1)
        cout << "The item was found at index location "
             << location << endl;
    else
        cout << "The item was not found in the list\n";
    return 0;
}

// this function returns the location of key in the list
// a -1 is returned if the value is not found
int binarySearch(int list[], int size, int key)
{
    int left, right, midpt;
    left = 0;
    right = size - 1;
    while (left <= right)
    {
        midpt = (int) ((left + right) / 2);
        if (key == list[midpt])
        {
            return midpt;
        }
        else if (key > list[midpt])
            left = midpt + 1;
        else
            right = midpt - 1;
    }

    return -1;
}
```

使用二分搜索算法的价值在于，每次通过 while 循环时必须搜索的元素数量都会减半。因此第一次通过循环时，必须搜索 n 个元素；第二次通过循环时，n / 2 个元素已被消除，只剩下 n / 2 个。第三次通过循环时，又有一半的剩余元素被消除，以此类推。

一般来说，经过 p 次循环后，剩余待搜索的值的数量为 n / (2^p)。在最坏情况下，搜索可以一直持续到剩余待搜索的元素少于或等于一个元素为止。数学上，此过程可表示为 n / (2^p) ≤ 1。或者可以重新表述为 p 是使 2^p > n 成立的最小整数。例如，对于一个 1000 个元素的数组，n 为 1000，二分搜索所需的最大循环次数 p 为 10。表 7.1 比较了不同列表大小的线性搜索和二分搜索所需的循环次数。

## 表 7.1 线性搜索和二分搜索 while 循环次数的比较

| 数组大小 | 10 | 50 | 500 | 5000 | 50,000 | 500,000 | 5,000,000 | 50,000,000 |
|---|---|---|---|---|---|---|---|---|
| 平均线性搜索次数 | 5 | 25 | 250 | 2500 | 25,000 | 250,000 | 2,500,000 | 25,000,000 |
| 最大线性搜索次数 | 10 | 50 | 500 | 5000 | 50,000 | 500,000 | 5,000,000 | 50,000,000 |
| 最大二分搜索次数 | 4 | 6 | 9 | 13 | 16 | 19 | 23 | 26 |

如图所示，对于 50 个项目的列表，线性搜索的循环最大次数几乎是二分搜索的 10 倍，对于更大的列表而言，差异更明显。作为经验法则，通常以 50 个元素作为切换点：对于少于 50 个元素的列表，线性搜索是可以接受的；对于更大的列表，应使用二分搜索算法。

## 大 O 表示法

平均而言，在对包含 n 个项目的列表进行大量线性搜索时，你预计在找到所需项目之前需要检查一半 (n / 2) 的项目。在二分搜索中，最大循环次数 p 出现在 n / (2^p) = 1 时。此关系可以通过代数运算转换为 2^p = n，从而得到 p = log₂n，这大约等于 3.33 × log₁₀n。

例如，在包含 n = 1000 个姓名的字母目录中查找特定姓名，使用线性搜索平均需要 500 (= n / 2) 次比较。而使用二分搜索，只需要大约 10 (= 3.33 × log₁₀(1000)) 次比较。

用列表中 n 个项目表达任何搜索算法所需比较次数的常用方法是给出平均定位所需项目所需比较次数的数量级。因此，线性搜索被称为 n 阶，

而二分搜索为 log₂n 阶。用符号表示，它们分别表示为 O(n) 和 O(log₂n)；O 读作“阶”。

## 两种算法

用于排序数据的排序技术主要有两大类，称为内部排序和外部排序。内部排序用于数据列表不太大且完整列表可以存储在计算机内存中，通常在数组中时使用。外部排序用于存储在外部存储介质上的更大数据集，无法作为完整单元容纳在计算机内存中。接下来，你将学习两种内部排序算法，可用于排序包含少于约 50 个元素的列表。对于更大的列表，通常使用更复杂的排序算法。

## 选择排序

最简单的排序技术之一是选择排序，其中从完整的数据列表中选择最小值并与列表中的第一个元素交换。在第一次选择和交换之后，修订后的列表中下一个最小的元素将被选中并与列表中的第二个元素交换。由于最小元素已在列表的第一位置，因此第二次遍历只需考虑第二到最后一个元素。对于包含 n 个元素的列表，此过程重复 n - 1 次，每次遍历列表所需的比较次数比前一次少一次。

例如，看看图 7.12 中显示的数字列表。第一次遍历初始列表导致数字 32 被选中并与列表中的第一个元素交换。第二次遍历对重新排序的列表进行，结果是从第二个到第五个元素中选择了数字 155。然后此值与列表中的第二个元素交换。第三次遍历从列表的第三到第五个元素中选择数字 307 并将此值与第三个元素交换。最后，第四次也是最后一次遍历列表，选择剩余的最小值并将其与第四个列表元素交换。尽管此示例中的每次遍历都导致了交换，但如果最小值已在正确位置，则不会进行交换。

| 初始列表 | 第 1 次遍历 | 第 2 次遍历 | 第 3 次遍历 | 第 4 次遍历 |
|---|---|---|---|---|
| 690 | 32 | 32 | 32 | 32 |
| 307 | 307 | 155 | 144 | 144 |
| 32 | 690 | 690 | 307 | 307 |
| 155 | 155 | 307 | 690 | 426 |
| 426 | 426 | 426 | 426 | 690 |

图 7.12 选择排序示例

在伪代码中，选择排序描述如下：

```
Set exchange count to 0 (not required, but done to keep track of the exchanges)
For each element in the list from first to next to last
```

