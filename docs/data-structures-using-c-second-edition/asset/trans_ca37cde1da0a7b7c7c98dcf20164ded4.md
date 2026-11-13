

比较 ARR[I] 和 ARR[J]，将两者中较小的一个放置在 INDEX 指定的 TEMP 位置，随后递增 I 或 J 的值。

![](img/be6359df08208122bec6fad1103de211_457_0.png)

当 I 大于 MID 时，将右子数组中剩余的元素复制到 TEMP 中。

![](img/be6359df08208122bec6fad1103de211_457_1.png)

```
MERGE (ARR, BEG, MID, END)
Step 1: [INITIALIZE] SET I = BEG, J = MID + 1, INDEX = 0
Step 2: Repeat while ( I <= MID ) AND ( J <= END )
IF ARR[I] < ARR[J]
SET TEMP[INDEX] = ARR[I]
SET I = I + 1
ELSE
SET TEMP[INDEX] = ARR[J]
SET J = J + 1
[END OF IF]
SET INDEX = INDEX + 1
[END OF LOOP]
Step 3: [Copy the remaining elements of right sub-array, if any]
IF I > MID
Repeat while J <= END
SET TEMP[INDEX] = ARR[J]
SET INDEX = INDEX + 1, SET J = J + 1
[END OF LOOP]
ELSE
[Copy the remaining elements of left sub-array, if any]
Repeat while I <= MID
SET TEMP[INDEX] = ARR[I]
SET INDEX = INDEX + 1, SET I = I + 1
[END OF LOOP]
[END OF IF]
Step 4: [Copy the contents of TEMP back to ARR] SET K = 0
Step 5: Repeat while K < INDEX
SET ARR[K] = TEMP[K]
SET K = K + 1
[END OF LOOP]
Step 6: END
```

```
MERGE_SORT(ARR, BEG, END)
Step 1: IF BEG < END
    SET MID = (BEG + END)/2
    CALL MERGE_SORT (ARR, BEG, MID)
    CALL MERGE_SORT (ARR, MID + 1, END)
    MERGE (ARR, BEG, MID, END)
    [END OF IF]
Step 2: END
```

归并排序在平均情况和最坏情况下的运行时间可表示为 O(n log n)。尽管归并排序具有最优的时间复杂度，但它需要为临时数组 TEMP 额外分配 O(n) 的空间。

图 14.9 归并排序算法

## 编程示例

- 8. 编写一个程序来实现归并排序。

```
#include <stdio.h>
#include <conio.h>
#define size 100

void merge(int arr[], int, int, int);
void merge_sort(int arr[], int, int);
void main()
{
    int arr[size], i, n;
    printf("\n Enter the number of elements in the array : ");
    scanf("%d", &n);
    printf("\n Enter the elements of the array : ");
    for(i=0;i<n;i++)
    {
        scanf("%d", &arr[i]);
    }
    merge_sort(arr, 0, n-1);
    printf("\n The sorted array is: \n");
    for(i=0;i<n;i++)
    printf("\t %d", arr[i]);
    getch();
}
void merge(int arr[], int beg, int mid, int end)
{
    int i=beg, j=mid+1, index=beg, temp[size], k;
    while((i<=mid) && (j<=end))
    {
        if(arr[i] < arr[j])
        {
            temp[index] = arr[i];
            i++;
        }
        else
        {
            temp[index] = arr[j];
            j++;
        }
        index++;
    }
    if(i>mid)
    {
        while(j<=end)
        {
            temp[index] = arr[j];
            j++;
            index++;
        }
    }
    else
    {
        while(i<=mid)
        {
            temp[index] = arr[i];
            i++;
            index++;
        }
    }
    for(k=beg;k<=index;k++)
    arr[k] = temp[k];
}
void merge_sort(int arr[], int beg, int end)
{
    int mid;
    if(beg<end)
    {
        mid = (beg+end)/2;
        merge_sort(arr, beg, mid);
        merge_sort(arr, mid+1, end);
        merge(arr, beg, mid, end);
    }
}
```

## 14.11 快速排序

快速排序是由 C.A. R. Hoare 开发的一种广泛使用的排序算法，在平均情况下对 n 个元素的数组进行 O(n log n) 次比较。然而，在最坏情况下，其运行时间为二次时间 O(n^2)。基本上，快速排序算法比其他 O(n log n) 算法更快，因为其高效实现可以最大限度地降低需要二次时间的概率。快速排序也称为分区交换排序。

与归并排序类似，该算法通过使用分治策略将单个未排序数组分成两个较小的子数组。

快速排序算法的工作原理如下：

- 1. 从数组元素中选择一个基准值 pivot。
- 2. 重新排列数组中的元素，使得所有小于基准值的元素都出现在基准值之前，所有大于基准值的元素都出现在基准值之后（相等的值可以放在任一侧）。经过这样的分区后，基准值被放置在其最终位置。这称为分区操作。
- 3. 递归排序由此获得的两个子数组。（一个包含小于基准元素值的子列表，另一个包含较大值的元素。）

与归并排序类似，递归的基本情况发生在数组包含零个或一个元素时，因为在这种情况下数组已经是有序的。每次迭代后，一个元素（基准值）始终位于其最终位置。因此，每次迭代后，数组中待排序的元素就少一个。因此，主要任务是找到基准元素，它将把数组分成两半。要了解如何找到基准元素，请按照以下步骤操作。（我们将数组中的第一个元素作为基准值。）

### 技术

快速排序的工作原理如下：

- 1. 将数组中第一个元素的索引设置为 `loc` 和 `left` 变量。同时，将数组中最后一个元素的索引设置为 `right` 变量。即，`loc = 0`，`left = 0`，`right = n-1`（其中 `n` 是数组中的元素个数）
- 2. 从 `right` 指向的元素开始，从右向左扫描数组，沿途将每个元素与变量 `loc` 指向的元素进行比较。即，`a[loc]` 应小于 `a[right]`。
    (a) 如果是这种情况，则继续比较，直到 `right` 等于 `loc`。一旦 `right = loc`，就表示基准值已放置在正确位置。
    (b) 但是，如果在任何时刻 `a[loc] > a[right]`，则交换这两个值并跳转到步骤 3。
    (c) 设置 `loc = right`。
- 3. 从 `left` 指向的元素开始，从左向右扫描数组，沿途将每个元素与变量 `loc` 指向的元素进行比较。即，`a[loc]` 应大于 `a[left]`。
    (a) 如果是这种情况，则继续比较，直到 `left` 等于 `loc`。一旦 `left = loc`，就表示基准值已放置在正确位置。
    (b) 但是，如果在任何时刻 `a[loc] < a[left]`，则交换这两个值并跳转到步骤 2。
    (c) 设置 `loc = left`。

### 示例 14.6 使用快速排序算法对以下数组中的元素进行排序

我们选择第一个元素作为基准值。设置 loc = 0，left = 0，right = 5。
[27 10 36 18 25 45]
loc left right

从右向左扫描。由于 a[loc] < a[right]，减小 right 的值。
[27 10 36 18 25 45]
loc right left

开始从左向右扫描。由于 a[loc] > a[left]，递增 left 的值。
[25 10 36 18 27 45]
left right loc

由于 a[loc] > a[right]，交换这两个值并设置 loc = right。
[25 10 36 18 27 45]
left right loc

由于 a[loc] < a[left]，交换这两个值并设置 loc = left。
[25 10 27 18 36 45]
loc right left

从右向左扫描。由于 a[loc] < a[right]，减小 right 的值。
[25 10 27 18 36 45]
loc right left

![](img/be6359df08208122bec6fad1103de211_461_0.png)

现在 left = loc，因此过程终止，因为基准元素（数组的第一个元素，即 27）已被放置在正确位置。所有小于 27 的元素都放在它前面，所有大于 27 的元素都放在它后面。

包含 25、10、18 的左子数组和包含 36 和 45 的右子数组以同样的方式进行排序。

快速排序算法（图 14.10）使用名为 Partition 的函数将数组分成两个子数组。

```
PARTITION (ARR, BEG, END, LOC)
Step 1: [INITIALIZE] SET LEFT = BEG, RIGHT = END, LOC = BEG, FLAG = 0
Step 2: Repeat Steps 3 to 6 while FLAG = 0
Step 3: Repeat while ARR[LOC] <= ARR[RIGHT] AND LOC != RIGHT
    SET RIGHT = RIGHT - 1
[END OF LOOP]
IF LOC = RIGHT
    SET FLAG = 1
ELSE IF ARR[LOC] > ARR[RIGHT]
    SWAP ARR[LOC] with ARR[RIGHT]
    SET LOC = RIGHT
[END OF IF]
Step 5: IF FLAG = 0
    Repeat while ARR[LEFT] <= ARR[LOC] AND LOC != LEFT
        SET LEFT = LEFT + 1
    [END OF LOOP]
    IF LOC = LEFT
        SET FLAG = 1
    ELSE IF ARR[LOC] < ARR[LEFT]
        SWAP ARR[LOC] with ARR[LEFT]
        SET LOC = LEFT
    [END OF IF]
[END OF IF]
Step 7: [END OF LOOP]
Step 8: END

QUICK_SORT (ARR, BEG, END)
Step 1: IF (BEG < END)
    CALL PARTITION (ARR, BEG, END, LOC)
    CALL QUICK_SORT(ARR, BEG, LOC - 1)
    CALL QUICK_SORT(ARR, LOC + 1, END)
[END OF IF]
Step 2: END
```

图 14.10 快速排序算法

