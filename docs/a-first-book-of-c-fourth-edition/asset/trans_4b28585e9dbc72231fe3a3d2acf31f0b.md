

从当前被引用的元素到最后一个元素查找最小元素的方法如下：

- 将最小值设为当前元素
- 保存（存储）当前元素的索引
- 对于列表中的每个元素，从当前元素 + 1 到列表中的最后一个元素
- 如果 element[内层循环索引] < 最小值
- 设置最小值 = element[内层循环索引]
- 保存新找到的最小值的索引
- EndIf
- EndFor
- 将当前值与新的最小值交换
- 增加交换次数
- EndFor
- 返回交换次数

selectionSort() 函数将此过程纳入到一个 C++ 函数中：

```
int selectionSort(int num[], int numel)
{
    int i, j, min, minidx, temp, moves = 0;

    for ( i = 0; i < (numel - 1); i++)
    {
        min = num[i];    // assume minimum is the first array element
        minidx = i;      // index of minimum element
        for(j = i + 1; j < numel; j++)
        {
            if (num[j] < min)    // if you've located a lower value
            {                   // capture it
                min = num[j];
                minidx = j;
            }
        }
        if (min < num[i])    // check whether you have a new minimum
        {                   // and if you do, swap values
            temp = num[i];
            num[i] = min;
            num[minidx] = temp;
            moves++;
        }
    }

    return moves;
}
```

selectionSort() 函数期望两个参数：要排序的列表和列表中元素的数量。如伪代码所述，一组嵌套的 for 循环执行排序。外层 for 循环使遍历列表的次数比列表中的项目总数少一次。对于每次遍历，变量 min 最初被赋值为 num[i]，其中 i 是外层 for 循环的计数变量。因为 i 从 0 开始并以 numel 减 1 结束，所以列表中的每个元素，除了最后一个，会依次被指定为当前元素。

内层循环遍历当前元素下面的元素，并用于选择下一个最小值。因此，此循环从索引值 i + 1 开始并一直持续到列表末尾。当找到新的最小值时，其值和在列表中的位置存储在变量 min 和 minIdx 中。内层循环完成后，只有在找到小于当前位置的值时才会进行交换。

程序 7.11 被构建用于测试 selectionSort()。该程序对之前用于测试搜索算法的同一组 10 个数字列表实现选择排序。为了与其它排序算法进行后续比较，程序对将数据排序所需实际进行的移动次数进行计数并显示。

## 程序 7.11

```
#include <iostream>
using namespace std;

int selectionSort(int [], int);
int main()
{
const int NUMEL = 10;
int nums[NUMEL] = {22,5,67,98,45,32,101,99,73,10};
int i, moves;

moves = selectionSort(nums, NUMEL);

cout << "The sorted list, in ascending order, is:\n";
for (i = 0; i < NUMEL; i++)
    cout << " " << nums[i];

cout << '\n' << moves << " moves were made to sort this list\n";

return 0;
}
int selectionSort(int num[], int numel)
{
int i, j, min, minIdx, temp, moves = 0;

for ( i = 0; i < (numel - 1); i++)
```

```
{ min = num[i]; // assume minimum is the first array element minidx = i; // index of minimum element for(j = i + 1; j < numel; j++) { if (num[j] < min) // if you've located a lower value { // capture it min = num[j]; minidx = j; } } if (min < num[i]) // check whether you have a new minimum { // and if you do, swap values temp = num[i]; num[i] = min; num[minidx] = temp; moves++; } } return moves; }
```

程序 7.11 产生的输出如下：

```
The sorted list, in ascending order, is: 5 10 22 32 45 67 73 98 99 101 8 moves were made to sort this list
```

显然，显示的移动次数取决于列表中值的初始顺序。选择排序的一个优点是必须进行的移动的最大次数为 n - 1，其中 n 是列表中项目的数量。此外，每次移动都是最终移动，导致一个元素驻留在排序列表中的最终位置。

选择排序的一个缺点是无论数据的初始排列如何，始终需要 n(n - 1) / 2 次比较。比较次数的获得如下：最后一次遍历始终需要一次比较，倒数第二次遍历需要两次比较，依此类推，直到第一次遍历，需要 n - 1 次比较。因此，比较的总次数如下：

1 + 2 + 3 + ... + n - 1 = n(n - 1) / 2 = n² / 2 - n / 2

对于较大的 n 值，n²占主导地位，选择排序的阶为 O(n²)。

## 交换（冒泡）排序

在交换排序中，列表的相邻元素相互交换，使得列表变得有序。这种交换序列的一个例子是冒泡排序，其中列表中连续的值进行比较，从前两个元素开始。如果列表要按升序（从最小到最大）排序，则每次比较的两个值中较小的总是放在较大的值之前。对于按降序（从最大到最小）排序的列表，每次比较的两个值中较小的总是放在较大的值之后。

例如，一个值列表要按升序排序。如果列表中的第一个元素大于第二个，则交换这两个元素。然后比较第二个和第三个元素。同样，如果第二个元素大于第三个，则交换这两个元素。此过程继续，直到最后两个元素已被比较并在必要时交换。如果在此初始遍历数据过程中未进行交换，则数据已处于正确顺序，过程结束；否则，从第一个元素开始，对数据进行第二次遍历，停止在倒数第二个元素。第二次遍历停止在倒数第二个元素的理由是，第一次遍历总是导致最正值“下沉”到列表底部。

为了看一个具体例子，检查图 7.13 中的数字列表。第一次比较导致交换前两个元素值，690 和 307。下一个比较，在修订后的列表中第二个和第三个元素之间，导致在第二个和第三个元素之间交换值，690 和 32。此比较和相邻值的可能交换继续进行，直到最后两个元素已被比较并可能交换。此过程完成了对数据的第一次遍历，并导致最大数字移动到列表底部。随着最大值的下沉到列表底部，较小的元素缓慢上升，或“冒泡”，到列表顶部。这种较小元素的冒泡效应导致了这种排序算法被称为“冒泡排序”的名称。

| 690 ↔ | 307 | 307 | 307 | 307 |
| 307 ↔ | 690 ↔ | 32 | 32 | 32 |
| 32 | 32 ↔ | 690 ↔ | 155 | 155 |
| 155 | 155 | 155 ↔ | 690 ↔ | 426 |
| 426 | 426 | 426 | 426 ↔ | 690 |

### 图 7.13 交换排序的第一次遍历

由于第一次遍历列表确保最大值的总是移动到列表底部，第二次遍历停止在倒数第二个元素。此过程继续，每次遍历停止的元素比前一次遍历高一个，直到完成 n - 1 次遍历或在任何一次遍历中不需要交换。在这两种情况下，结果列表都处于排序顺序。描述此排序的伪代码如下：

```
Set exchange count to 0 (not required, but done to keep track of the exchanges)
For the first element in the list to 1 less than the last element (i index)
For the second element in the list to the last element (j index)
If num[j] < num[j - 1]
{
Swap num[j] with num[j - 1]
increment exchange count
}
```
