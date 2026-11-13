
第 n 步：在第 (n-1) 趟中，排除列表中的前两个元素，通过查找下一个最小元素并将其与适当元素交换来重复排序过程，直到整个列表排序完成。整个排序需要 (n-1) 趟。

要查找列表中所有元素中的最小元素，首先将变量 SMALL 设置为列表的第一个元素，将变量 POS 设置为第一个元素的位置，然后遍历列表，将 SMALL 与 DATA[i] 中的每个其他元素进行比较，如下所示：

- 1. 如果 SMALL < DATA[i]，则移动到下一个元素
- 2. 如果 SMALL > DATA[i]，则更新 SMALL 和 POS，即 SMALL=DATA[i] 和 POS=i

比较完所有元素后，SMALL 包含所有元素中的最小值，POS 包含其位置。

选择排序也可以通过选择最大元素而不是最小元素，并将其与列表末尾位置的元素交换，来对元素进行降序排序。算法 16.3 是选择排序的算法。算法 FINDMIN 查找列表中的最小元素并将其返回给算法 SELECTION-SORT，后者将最小元素放置在其适当位置。

```
Algorithm 16.3: SELECTION-SORT (DATA, N)
1. Repeat for k=1 to N-1
2. Call FINDMIN(DATA, K, N, POS)
3. Set temp=DATA[K]
4. DATA[K]=DATA[POS]
5. DATA[POS]=temp
6. End loop
7. End
```

```
Algorithm 16.3.1: FINDMIN(DATA, K, N, POS)
/*This algorithm is used to find the smallest element among DATA[K] , DATA[K+1] ,..., DATA[N] */
1. Set SMALL=DATA[K] and POS=K
2. Loop for i=K+1 to N
(i) Check whether SMALL is greater than DATA[i] then
(ii) Set SMALL=DATA[i] and POS=i
3. End loop
4. End
```

## 示例 16.3

设 DATA 为包含元素 88 44 55 22 99 33 77 66 的数组。

图 16.3 显示了数组 DATA 上的选择排序过程。

| 趟 | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] |
|---|---|---|---|---|---|---|---|---|
| K=1, POS=4 | 88 | 44 | 55 | 22 | 99 | 33 | 77 | 66 |
| K=2, POS=6 | 22 | 44 | 55 | 88 | 99 | 33 | 77 | 66 |
| K=3, POS=6 | 22 | 33 | 55 | 88 | 99 | 44 | 77 | 66 |
| K=4, POS=6 | 22 | 33 | 44 | 88 | 99 | 55 | 77 | 66 |
| K=5, POS=8 | 22 | 33 | 44 | 55 | 99 | 88 | 77 | 66 |
| K=6, POS=7 | 22 | 33 | 44 | 55 | 66 | 88 | 77 | 99 |
| K=7, POS=7 | 22 | 33 | 44 | 55 | 66 | 77 | 88 | 99 |
| 排序后的数组是 | 22 | 33 | 44 | 55 | 66 | 77 | 88 | 99 |

## 图 16.3 选择排序跟踪

观察图 16.3，在趟 K 中，POS 给出 DATA[K]、DATA[K+1]、...、DATA[N] 中的最小值。带圈元素表示要交换的元素。以类似方式，所有元素都将被排序。

**复杂度：** 选择排序的时间复杂度为 O(n^2)。

在第 1 趟中需要 n-1 次比较，在第 2 趟中需要 n-2 次比较，在第 n 趟中需要 i 次比较。因此，递推关系式为

```
F(n) = (n-1) + (n-2) + ... + 2 + 1 = n(n-1)/2 = O(n^2)
```

## 16.1.4 快速排序

快速排序属于交换排序家族，其中无序元素相互交换以获得有序列表。

快速排序基于将列表划分为两个子列表的原理进行排序，将列表中的任意一个元素作为关键元素，称为基准元素。基准元素左右两侧各出现一个子列表，即基准元素将被放置在其适当位置。接着，子列表再分别针对其各自的基准元素进一步划分，直到无法再划分为止。此时，列表中的所有元素都将处于有序状态。以下是快速排序的过程。

设 L 为包含元素 [A1, A2, ..., An] 的无序列表。

- 1. 步骤 1：假设选择 A1 作为基准元素，现在将 A1 与列表中的所有元素从左到右进行比较，直到找到第一个大于或等于 A1 的最大数 Ai，即 Ai>=A1。
- 2. 步骤 2：再次将 A1 与元素从右到左进行比较，直到找到第一个小于或等于 A1 的最小数 Aj，即 Aj<=A1。
- 3. 步骤 3：如果 i<j，则交换 Ai 和 Aj。

如果 i>j，则 A1 与 Aj 交换，即 A1 将小于 Aj 且大于 Ai。此时进行划分。列表将基于基准元素分为两个子列表。算法 16.4 是快速排序的算法。

## 算法 16.4：QUICK SORT (DATA, LOW, HIGH)

- 1. 检查 LOW 是否小于 HIGH，然后
   PQUICK(DATA, LOW, HIGH, POS)
   QUICKSORT(DATA, LOW, POS-1)
   QUICKSORT(DATA, POS+1, HIGH)
- 2. 结束

## 算法 16.4.1：PQUICK (DATA, LOW, HIGH, POS)

```
/*This algorithm is used to partition the list into sublists. POS is the position of the pivot element at the end of the partition. LEFT and RIGHT variables hold the first and last positions of the array DATA. The variable PIVOT holds the pivot element.*/
```

- 1. 设置 LEFT=LOW、RIGHT=HIGH 和 PIVOT=DATA[LOW]
- 2. 当 LEFT<RIGHT 时循环
   1. 重复直到 DATA[LEFT]>=PIVOT
      设置 LEFT=LEFT+1 //基准元素从左向右移动
   2. 重复直到 DATA[RIGHT]<PIVOT
      设置 RIGHT=RIGHT-1 //基准元素从右向左移动
   3. 检查 LEFT 是否小于 RIGHT，然后
      交换(DATA[LEFT], DATA[RIGHT])
   4. 结束循环
- 3. 设置 POS=RIGHT
- 4. 交换(DATA[LEFT], DATA[RIGHT])
- 6. 结束

## 示例 16.4

设 DATA 为包含元素 6 2 25 10 75 33 10 的数组。

图 16.4 显示了快速排序的各个阶段

## 阶段 1：

- 选择第一个元素作为基准元素：
  [图示：6 2 25 10 75 33 10，6 被圈出]
- 从左到右扫描，直到出现第一个最大数：
  [图示：2 (25) 10 75 33 10，LEFT 在 25 下方]
- 从右到左扫描，直到出现第一个最小数：
  [图示：6 (2) (25) 10 75 33 10，RIGHT 在 2 下方]
- 由于 LEFT > RIGHT，将基准元素与 RIGHT 交换：
  [图示：2 6 | 25 10 75 33 10]
- 子列表 1 子列表 2
- 现在基准元素已放置在其位置，列表被划分为两个子列表。使用与上述相同的过程对两个子列表进行排序。

## 图 16.4 快速排序跟踪

## 阶段 2：

- 无需对子列表 1 进行排序，因为只有一个元素。
- 对子列表 2 [25, 10, 75, 33, 10] 执行快速排序。
- 选择基准元素为 25
- 从左到右扫描
  [图示：25 10 75 33 10]
- 从右到左扫描
  [图示：25 10 75 33 10，带有 LEFT、RIGHT 箭头]
- 由于 LEFT<RIGHT，交换 LEFT 和 RIGHT：
  [图示：10 25 10 33 75]
- 从左到右扫描
  [图示：10 25 10 33 75]
- 从右到左扫描
  [图示：10 25 10 33 75，带有 RIGHT、LEFT 箭头]
- 由于 LEFT > RIGHT，交换基准元素和 RIGHT：
  [图示：10 10 25 33 75]
- 此时划分后的列表为：
  [图示：2 6 10 10 25 33 75，带有标签 子列表 1、子列表 2]

## 阶段 3：

- 对子列表 {10, 10} 执行快速排序：
  基准 [10]
  [带箭头的图示]
- LEFT=RIGHT
- 将基准元素与 RIGHT 交换。
- 此时划分后的列表
  [图示：2 6 10 10 25 33 75]

## 阶段 4：

- 无需对子列表 [10] 进行排序，因为只有一个元素。
- 对子列表 {33, 75} 执行快速排序。
- 选择基准元素为 33
- 从左到右扫描
  [图示：33 75]
- 从右到左扫描
  [图示：33 75，带有 RIGHT、LEFT 箭头]
- 无需交换。

| 此时排序后的数组是 | 2 | 6 | 10 | 10 | 25 | 33 | 75 |
| 最终排序后的数组是 | 2 | 6 | 10 | 10 | 25 | 33 | 75 |

## 图 16.4 续

## 程序 16.4

```
/*To Sort The Given List Using QUICK SORT*/
#include<iostream.h>
#include<conio.h>
void quicksort(int a[],int lb,int ub)
{
 int key,lb,i=lb,j=ub,temp;
 while(i<j)
 {
 while(a[i]<=a[key])
 i++;
 while(a[j]>=a[key])
j--;
 if(i<j)
 {
a[i]=a[i]+a[j]-(a[j]=a[i]); //Single Line Swapping
a[key]=(a[key]+a[j])-(a[j]=a[key]);
 quicksort(a,lb,j-1);
 quicksort(a,j+1,ub);
 }
 }
void main()
{
 int i,a[30],n;
 clrscr();
 cout<<"Enter Size Of Array:";
 cin>>n;
 cout<<"Enter Size<<"Elements:";
 for(i=0;i<n;i++)
 cin>>a[i];
 cout<<"Before Sorting List Is:\n";
 for(i=0;i<n;i++)
 cout<<a[i]<<" ";
 quicksort(a,0,n-1);
 cout<<"\nAfter Sorting List Is:\n";
 for(i=0;i<n;i++)
 cout<<a[i]<<" ";
 getch();
}
```

## 输出

Enter Size Of Array:8
Enter 8 Elements:7
