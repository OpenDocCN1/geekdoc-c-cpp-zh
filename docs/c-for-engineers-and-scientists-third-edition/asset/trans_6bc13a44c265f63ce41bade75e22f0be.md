
# 第 7 章

## 深入观察：搜索与排序

## 程序 7.14

```cpp
#include <iostream>
using namespace std;

int selectionSort(int [], int int);

int main() {
    const int NUMEL = 10;
    int nums[NUMEL] = {22,56,67,98,45,32,101,99,73,10};
    int i, moves;

    moves = selectionSort(nums, NUMEL);

    cout << "The sorted list, in ascending order, is:\n";
    for (i = 0; i < NUMEL; i++) {
        cout << " * " << nums[i] << endl;
    }

    cout << endl << moves << " moves were made to sort this list\n";

    return 0;
}

int selectionSort(int num[], int numel) {
    int i, j, min, minidx, temp, moves = 0;

    for (i = 0; i < (numel - 1); i++) {
        min = num[i]; // assume minimum is the first array element
        minidx = i; // index of minimum element
        for (j = i + 1; j < numel; j++) {
            if (num[j] < min) // if you've located a lower value
            {
                min = num[j]; // capture it
                minidx = j;
            }
        }
        if (min < num[i]) // check if you have a new minimum
        {
            // and if you do, swap values
            temp = num[i];
            num[i] = min;
            num[minidx] = temp;
            moves++;
        }
    }
    return moves;
}
```

### 冒泡排序

在交换排序中，列表中相邻的元素之间进行交换，使得列表变得有序。这种交换序列的一个例子就是冒泡排序，它从前两个元素开始，对列表中的连续值进行比较。如果按升序（从小到大）排序列表，则将比较的两个值中较小的那个始终放在较大的值之前。对于按降序（从大到小）排序的列表，则将两个值中较小的那个始终放在较大的值之后。

例如，一个要升序排序的数值列表。如果列表中的第一个元素大于第二个元素，则交换这两个元素。然后比较第二个和第三个元素。同样，如果第三个比第四个大，就交换这两个。这个过程一直持续，直到最后两个元素经过了比较和交换。如果在第一轮扫描中没有进行任何交换，则数据处于正确顺序，处理结束；否则，对数据进行第二轮扫描，从第一个元素开始，到倒数第二个元素停止。第二轮扫描停止在倒数第二个元素的原因是，第一轮会导致最大的值“沉”到列表的底部。

为了看到一个具体的例子，请考虑图 7.16 中的数字列表。第一次比较产生前两个元素 690 和 307。修改后的列表中，第二个和第三个元素之间的比较会导致第二个和第三个元素（690 和 32）之间的值交换。这种对相邻值的比较和可能的切换将一直进行，直到最后一个元素经过比较和交换。这个过程完成了对数据的第一次扫描，并将最大值移动到列表底部。随着最大值沉到列表底部，较小的元素缓慢地上升或“冒泡”到列表顶部。较小元素的这种冒泡效应正是“冒泡排序”算法名称的由来。

| 690 | 307 | 307 | 307 |
| 307 | 690 | 32 | 32 |
| 32 | 32 | 690 | 155 |
| 155 | 155 | 155 | 690 |
| 426 | 426 | 426 | 426 | 690 |

**图 7.16** 交换排序的第一轮扫描

对列表的第一轮扫描确保了最大值总是移动到列表底部，第二轮扫描停止在倒数第二个元素。这个过程持续进行，每一轮停止的位置都比上一轮高一个元素，直到完成 n-1 轮列表扫描，或者在单次扫描中没有进行任何交换。在这两种情况下，结果列表都是有序的。描述此过程的伪代码如下：

- 将交换计数置零（不是必须的，但为了跟踪交换次数）
- 从列表的第一个元素到倒数第二个元素（i 索引）
- 从列表的第二个元素到最后一个元素（j 索引）

```cpp
{
    if num[j] < num[j-1]
        Swap num[j] with num[j-1]
        Increment exchange count
}
EndFor
EndPoint
Return exchange count
```

该排序算法在 C++ 中被编码为 `bubbleSort()` 函数，该函数包含在程序 7.15 中用于测试目的。程序使用相同的数字列表测试 `bubbleSort()`。

