

线性搜索(A, N, VAL)
步骤 1：[初始化] 设置 POS = -1
步骤 2：[初始化] 设置 I = 1
步骤 3：重复步骤 4，当 I <= N 时
步骤 4：如果 A[I] = VAL
        设置 POS = I
        打印 POS
        转到步骤 6
        [结束 IF]
        设置 I = I + 1
        [结束循环]
步骤 5：如果 POS = -1
        打印 "值不存在于
        数组中"
        [结束 IF]
步骤 6：退出

若要查找的值为 val = 7，则搜索意味着查找值“7”是否存在于数组中。如果是，则返回其出现的位置。这里，POS = 3（索引从 0 开始）。图 14.1 显示了线性搜索算法。在算法的步骤 1 和 2 中，我们初始化 POS 和 I 的值。在步骤 3 中，执行一个 while 循环，该循环将持续执行直到 I 小于 N（数组中元素的总数）。在步骤 4 中，检查当前数组元素与 VAL 之间是否存在匹配。如果找到匹配，则打印数组元素的位置，否则将 i 的值递增以将下一个元素与 val 匹配。但是，如果所有数组元素都与 val 进行了比较且未找到匹配，则意味着 val 不存在于数组中。

图 14.1 线性搜索算法

## 线性搜索算法的复杂度

线性搜索在 O(n) 时间内执行，其中 n 是数组中的元素数量。显然，线性搜索的最佳情况是 val 等于数组的第一个元素。在这种情况下，只会进行一次比较。同样，最坏情况发生在 val 不存在于数组中或等于数组的最后一个元素时。在这两种情况下，都需要进行 n 次比较。但是，通过使用已排序数组，可以改进线性搜索算法的性能。

## 编程示例

- 1. 使用线性搜索技术编写一个在数组中搜索元素的程序。

```c
#include <stdio.h>
#include <stdlib.h>
#include <conio.h>
#define size 20
int main()
{
int arr[size], num, i, n, found = 0, pos = -1;
printf("\n Enter the number of elements in the array : ");
scanf("%d", &n);
printf("\n Enter the elements : ");
for(i=0;i<n;i++)
{
scanf("%d",&arr[i]);
}
printf("\n Enter the number that has to be searched : ");
scanf("%d",&num);
for(i=0;i<n;i++)
{
if(arr[i] == num)
{
found =1;
pos=i;
printf("\n %d is found in the array at position=%d", num,i+1);
/* *1 added in Line 23 so that it would display the number in
the first place in the array as in position 1 instead of 0 */
break;
}
}
if (found == 0)
printf("\n %d does not exist in the array", num);
return 0;
}
```

## 14.3 二分查找

二分查找是一种在已排序列表上高效工作的搜索算法。二分查找的机制可以通过电话簿的类比来更好地理解。当我们在目录中搜索特定姓名时，首先从中间打开目录，然后决定在目录的第一部分还是第二部分查找该姓名。同样，我们在中间打开某一页，整个过程重复，直到最终找到正确的姓名。

举另一个类比。我们如何在字典中查找单词？我们首先在字典中间某处打开它。然后，将该页面上的第一个单词与我们要查找含义的所需单词进行比较。如果所需单词在页面上的单词之前，则在字典的前半部分查找，否则在后半部分查找。同样，我们在字典的前半部分打开一页，将该页面上的第一个单词与所需单词进行比较，并重复相同的过程，直到最终找到该单词。相同的机制应用于二分查找。

现在，让我们考虑如何将此机制应用于在已排序数组中搜索值。考虑一个声明并初始化为以下内容的数组 A[]：

```c
int A[] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
```

若要查找的值为 VAL = 9。算法将以以下方式进行。

```text
BEG = 0, END = 10, MID = (0 + 10)/2 = 5
```

现在，val = 9 且 A[MID] = A[5] = 5

A[5] 小于 val，因此，我们现在在数组的后半部分搜索该值。因此，我们更改 BEG 和 MID 的值。

```text
Now, BEG = MID + 1 = 6, END = 10, MID = (6 + 10)/2 = 16/2 = 8
```

VAL = 9 且 A[MID] = A[8] = 8

A[8] 小于 val，因此，我们现在在段的后半部分搜索该值。因此，我们再次更改 BEG 和 MID 的值。

```text
Now, BEG = MID + 1 = 9, END = 10, MID = (9 + 10)/2 = 9
```

现在，VAL = 9 且 A[MID] = 9。

在此算法中，我们看到 BEG 和 END 是我们要搜索元素的段的起始位置和结束位置。MID 计算为 (BEG + END)/2。最初，BEG = lower_bound 且 END = upper_bound。当 A[MID] = VAL 时，算法将终止。当算法结束时，我们将设置 pos = MID。pos 是值在数组中存在的位置。

但是，如果 val 不等于 A[MID]，则 BEG、END 和 MID 的值将根据 val 是小于还是大于 A[MID] 而更改。

- (a) 如果 val < A[MID]，则 val 将存在于数组的左段中。因此，END 的值将更改为 END = MID - 1。
- (b) 如果 val > A[MID]，则 val 将存在于数组的右段中。因此，BEG 的值将更改为 BEG = MID + 1。

最后，如果 val 不存在于数组中，则最终 END 将小于 BEG。当这种情况发生时，算法将终止且搜索将不成功。

图 14.2 显示了二分查找算法。

在步骤 1 中，我们初始化变量 BEG、END 和 pos 的值。在步骤 2 中，执行一个 while 循环，直到 BEG 小于或等于 END。在步骤 3 中，计算 MID 的值。在步骤 4 中，我们检查 MID 处的数组值是否等于 val（要在数组中搜索的项目）。如果找到匹配，则打印 pos 的值并退出算法。但是，如果未找到匹配，且 A[mid] 的值大于 val，则修改 end 的值；否则，如果 A[mid] 的值小于 val，则更改 beg 的值。在步骤 5 中，如果 pos = -1，则 val 不存在于数组中，并在算法退出前在屏幕上打印适当的消息。

```text
BINARY_SEARCH(A, lower_bound, upper_bound, VAL)
Step 1: [INITIALIZE] SET BEG = lower_bound
END = upper_bound, POS = -1
Step 2: Repeat Steps 3 and 4 while BEG <= END
Step 3: SET MID = (BEG + END)/2
Step 4: IF A[MID] = VAL
SET POS = MID
PRINT POS
Go to Step 6
ELSE IF A[MID] > VAL
SET END = MID - 1
ELSE
SET BEG = MID + 1
[END OF IF]
Step 5: IF POS = -1
PRINT "VALUE IS NOT PRESENT IN THE ARRAY"
Step 6: EXIT
```

图 14.2 二分查找算法

## 二分查找算法的复杂度

二分查找算法的复杂度可以表示为 f(n)，其中 n 是数组中的元素数量。算法的复杂度取决于进行的比较次数。在二分查找算法中，我们看到每次比较后，需要搜索的段的大小减半。因此，我们可以说，为了在数组中定位特定值，将进行的比较总数由以下公式给出：

2^{f(n)} > n 或 f(n) = log_2 n

## 编程示例

- 2. 使用二分查找编写一个在数组中搜索元素的程序。

```c
#include <stdio.h>
#include <stdlib.h>
#include <conio.h>
#define size 10 // Added to make changing size of array easier
int smallest(int arr[], int k, int n); // Added to sort array
void selection_sort(int arr[], int n); // Added to sort array
int main(int argc, char *argv[]) {
int pos, beg, end, mid, i, n, a[size], found=0;
printf("\n Enter the number of elements in the array: ");
scanf("%d", &n);
printf("\n Enter the elements: ");
for(i=0;i<n;i++)
{
scanf("%d",&a[i]);
}
selection_sort(a, n); // Added to sort the array
printf("\n The sorted array is: \n");
for(i=0;i<n;i++)
printf(" %d",a[i]);
printf("\n Enter the number that has to be searched: ");
scanf("%d",&num);
beg = 0, end = n-1;
while(beg<=end)
{
mid = (beg + end)/2;
if (a[mid] == num)
{
printf("\n %d is present in the array at position %d", num, mid+1);
found = 1;
break;
}
```

