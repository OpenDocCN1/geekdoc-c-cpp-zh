

## EXAMPLE: (continued)

一种设计算法的方法是依赖于问题的定义。在本例中，问题是对数组 a 从小到大进行排序。这意味着重新排列值，使得 a[0] 是最小的，a[1] 是次小的，以此类推。该定义给出了选择排序算法的大纲：

```
for (int index = 0; index < numberUsed; index++)
    Place the indexth smallest element in a[index]
```

实现这一通用方法的方式有很多。细节可以使用两个数组并以排序顺序从一个数组复制元素到另一个数组来开发，但一个数组应该足够且经济。因此，函数 sort 只使用包含要排序的值的那个数组。函数 sort 通过交换值对来重新排列数组 a 中的值。让我们通过一个具体的例子来说明算法的工作原理。

考虑 Display 5.7 中显示的数组。算法将把最小值放在 a[0] 中。最小值是 a[3] 中的值，因此算法交换 a[0] 和 a[3] 的值。然后算法寻找下一个最小的元素。a[0] 中的值现在是最小元素，因此下一个最小的元素是剩余元素 a[1]、a[2]、a[3]、...、a[9] 中最小的。在 Display 5.7 的示例中，下一个最小的元素在 a[5] 中，因此算法交换 a[1] 和 a[5] 的值。第二个最小元素的定位如图 Display 5.7 中的第四和第五个数组图所示。然后算法定位第三个最小的元素，以此类推。随着排序的进行，开始的数组元素被设为正确的排序值。已排序的数组部分通过从未排序的数组末尾逐个添加元素而增长。请注意，算法无需对最后一个索引变量 a[9] 的值做任何事情。一旦其他元素被正确定位，a[9] 也必须具有正确的值。毕竟，a[9] 的正确值是剩余待移动的最小值，而唯一剩余待移动的值就是已经在 a[9] 中的值。

函数 sort 的定义包含在一个演示程序中，给出在 Display 5.8 中。sort 使用函数 indexOfSmallest 来查找数组未排序末尾的最小元素的索引，然后执行交换以将这个下一个最小元素移入已排序的数组部分。

函数 swapValues，如 Display 5.8 所示，用于交换索引变量的值。例如，以下调用将交换 a[0] 和 a[3] 的值：

```
swapValues(a[0], a[3]);
```

函数 swapValues 在第 4 章中进行了说明。

## Display 5.8 Sorting an Array (part 2 of 3)

```
20 int main()
21 {
22     cout << "This program sorts numbers from lowest to highest.\n";
23     int sampleArray[10], numberUsed;
24     fillArray(sampleArray, 10, numberUsed);
25     sort(sampleArray, numberUsed);
26     cout << "In sorted order the numbers are:\n";
27     for (int index = 0; index < numberUsed; index++)
28         cout << sampleArray[index] << " ";
29     cout << endl;
30     return 0;
31 }
32 
33 void fillArray(int a[], int size, int& numberUsed)
34     <The rest of the definition of fillArray is given in Display 5.5.>
35 
34 void sort(int a[], int numberUsed)
35 {
36     int indexOfNextSmallest;
37     for (int index = 0; index < numberUsed - 1; index++)
38         {//Place the correct value in a[index]:
39         indexOfNextSmallest =
40             indexOfSmallest(a, index, numberUsed);
41         swapValues(a[index], a[indexOfNextSmallest]);
42         //a[0] <= a[1] <= ... <= a[index] are the smallest of the
43         //original array elements. The rest of the
44         //elements are in the remaining positions.
45     }
46 }
47 
46 void swapValues(int& v1, int& v2)
47 {
48     int temp;
49     temp = v1;
50     v1 = v2;
51     v2 = temp;
52 }
53 
54 int indexOfSmallest(const int a[], int startIndex, int numberUsed)
55 {
56     int min = a[startIndex],
57     indexOfMin = startIndex;
```

## Display 5.8 Sorting an Array (part 3 of 3)

```
58  for (int index = startIndex + 1; index < numberUsed; index++)
59      if (a[index] < min)
60      {
61          min = a[index];
62          indexOfMin = index;
63          //min is the smallest of a[startIndex] through a[index]
64      }
65  
65  return indexOfMin;
66 }
```

## Sample Dialogue

```
This program sorts numbers from lowest to highest.
Enter up to 10 nonnegative whole numbers.
Mark the end of the list with a negative number.
80 30 50 70 60 90 20 30 40 -1
In sorted order the numbers are:
20 30 30 40 50 60 70 80 90
```

## EXAMPLE: Bubble Sort

我们刚刚描述的选择排序算法并不是排序数组的唯一方法。事实上，计算机科学家已经设计了数十种排序算法！其中一些算法比其他算法更高效，有些仅适用于特定类型的数据。冒泡排序是一种简单且通用的排序算法，与选择排序类似。

如果我们使用冒泡排序按升序对数组进行排序，则最大值会依次“冒泡”到数组末尾。例如，如果我们从由以下整数组成的未排序数组开始：
Initial array: {3, 10, 9, 2, 5}
那么在第一次遍历后，我们将把最大值 10 移到数组末尾：
After first pass: {3, 9, 2, 5, 10}
第二次遍历将把第二大值 9 移到数组倒数第二个索引：
After second pass: {3, 2, 5, 9, 10}

VideoNote
Bubble Sort
Walkthrough

第三次遍历将把第三大值 5 移到数组倒数第三个索引（它已经在那里）：

After third pass: {2, 3, 5, 9, 10}

第四次遍历将把第四大值 3 移到数组倒数第四个索引（它已经在那里）：

After fourth pass: {2, 3, 5, 9, 10}

此时算法完成。数组开头剩余的数字无需检查，因为它是唯一剩下的数字，必须是最小的。

要基于冒泡排序设计程序，请注意我们将最大项放在索引 length-1，第二大项放在 length-2，接下来放在 length-3，等等。这对应于一个从数组索引 length-1 开始并递减到索引 1 的循环。我们不需要包含索引 0，因为那里将包含最小元素。实现循环的一种方法是使用以下代码，其中变量 i 对应目标索引：

```
for (int i = length-1; i > 0; i--)
```

冒泡排序中的“冒泡”部分发生在该循环的每次迭代内部。冒泡步骤由另一个循环组成，该循环将最大数字向数组末尾移动。首先，索引 0 和索引 1 之间的最大数字将被冒泡到索引 1。我们通过比较索引 0 处的数字与索引 1 处的数字开始冒泡过程。如果索引 0 处的数字大于索引 1 处的数字，则交换值，从而使较大数字位于索引 1。如果索引 0 处的数字小于或等于索引 1 处的数字，则什么也不发生。我们从以下未排序数组开始：

Initial array: {3, 10, 9, 2, 5}

冒泡过程的第一步将比较 3 和 10。由于 10 > 3，什么也不发生，结果是数字 10 位于索引 1：

After step 1: {3, 10, 9, 2, 5}

## 1. 引言

本文档旨在介绍一种新型的文档解析方法，该方法能够高效地从复杂版面中提取结构化信息。该方法结合了深度学习与传统规则，适用于多种文档类型。

- 支持标题、段落、表格等元素的识别
- 支持阅读顺序的还原
- 支持版面方向（横/竖）的自动判断

| 方法 | 准确率 | 召回率 |
|------|--------|--------|
| 传统方法 | 85% | 80% |
| 深度方法 | 95% | 92% |

> > 注意：本方法在扫描件上的效果优于纯文本文件。

![](img/c76bba8c1d927f399768ffe2ab5f5bee_249_0.png)

```
```
```python
import docx
print("Hello, world!")
```
```

综上所述，该方法在文档解析任务中表现优异，未来可进一步扩展到多模态场景。

