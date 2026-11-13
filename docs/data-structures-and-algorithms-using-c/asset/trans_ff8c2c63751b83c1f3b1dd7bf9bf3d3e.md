

## C 语言中的希尔排序程序

希尔排序是一种高效的排序算法，基于插入排序算法。当较小的值位于最右侧且需要移动到最左侧时，该算法避免了像插入排序那样的大规模移动。

### C 语言实现

```c
#include <stdio.h>
#include <stdbool.h>
#define MAX 7
int intArray[MAX] = {4, 6, 3, 2, 1, 9, 7};

void printline(int count) {
   int i;
   for (i = 0; i < count - 1; i++) {
      printf("=");
   }
   printf("=\n");
}

void display() {
   int i;
   printf("[");
   // navigate through all items
   for (i = 0; i < MAX; i++) {
      printf("%d ", intArray[i]);
   }
   printf("]\n");
}

void shellSort() {
   int inner, outer;
   int valueToInsert;
   int interval = 1;
   int elements = MAX;
   int i = 0;

   while (interval <= elements / 3) {
      interval = interval * 3 + 1;
   }

   while (interval > 0) {
      printf("iteration %d#:", i);
      display();

      for (outer = interval; outer < elements; outer++) {
         valueToInsert = intArray[outer];
         inner = outer;

         while (inner > interval - 1 && intArray[inner - interval] >= valueToInsert) {
            intArray[inner] = intArray[inner - interval];
            inner -= interval;
            printf(" item moved :%d\n", intArray[inner]);
         }

         intArray[inner] = valueToInsert;
         printf(" item inserted :%d, at position :%d\n", valueToInsert, inner);
      }

      interval = (interval - 1) / 3;
      i++;
   }
}

int main() {
   printf("Input Array: ");
   display();
   printline(50);
   shellSort();
   printf("Output Array: ");
   display();
   printline(50);
   return 1;
}
```

如果编译并运行上述程序，将产生以下结果 –

```
Input Array: [4, 6, 3, 2, 1, 9, 7]
==========================================
iteration 0#: [4, 6, 3, 2, 1, 9, 7]
item moved :4
item inserted :1, at position :0
item inserted :9, at position :5
item inserted :7, at position :6
iteration 1#: [1, 6, 3, 2, 4, 9, 7]
item inserted :6, at position :1
item moved :6
item inserted :3, at position :1
item moved :6
item moved :3
item inserted :2, at position :1
item moved :6
item inserted :4, at position :3
item inserted :9, at position :5
item moved :9
item inserted :7, at position :5
Output Array: [1, 2, 3, 4, 6, 7, 9]
==========================================
```

## 26. 快速排序 数据结构与算法

快速排序是一种高效的排序算法，基于将数据数组划分为更小数组的方式。大数组被划分为两个数组，一个存储小于指定值（称为基准值 pivot）的值，另一个存储大于基准值的值，划分依据即为该基准值。

快速排序对数组进行分区，然后递归调用自身两次来对生成的两个子数组进行排序。该算法对于大型数据集非常高效，因为其平均和最坏情况复杂度为 O(nlogn)，其中 n 为项目数量。

### 快速排序中的分区

以下动画表示说明如何在数组中找到基准值。

![](img/30fc9e3f8ee01facfae8d1c9621936b3_187_0.png)

基准值将列表分为两部分。然后递归地，为每个子列表找到基准值，直到所有列表只包含一个元素。

### 快速排序基准值算法

基于我们对快速排序中分区的理解，我们现在尝试为其编写一个算法，如下所示。

- 步骤 1 – 选择最高索引值作为基准值
- 步骤 2 – 取两个变量指向列表左侧和右侧（不包括基准值）
- 步骤 3 – left 指向低索引
- 步骤 4 – right 指向高索引
- 步骤 5 – 当 left 处的值小于基准值时，向右移动
- 步骤 6 – 当 right 处的值大于基准值时，向左移动
- 步骤 7 – 如果步骤 5 和步骤 6 都不匹配，交换 left 和 right
- 步骤 8 – 如果 left ≥ right，则它们相遇的点即为新基准值

### 快速排序基准值伪代码

上述算法的伪代码可推导如下 –

```
function partitionFunc(left, right, pivot)
   leftPointer = left - 1
   rightPointer = right

   while True do
      while A[++leftPointer] < pivot do
      // do nothing
      end while

      while rightPointer > 0 && A[--rightPointer] > pivot do
      // do nothing
      end while

      if leftPointer >= rightPointer then
         break
      else
         swap leftPointer, rightPointer
      end if
   end while

   swap leftPointer, right
   return leftPointer
end function
```

### 快速排序算法

递归使用基准值算法，最终得到尽可能小的分区。然后对每个分区进行快速排序。我们定义快速排序的递归算法如下 –

- 步骤 1 – 将最右侧索引值设为基准值
- 步骤 2 – 使用基准值对数组进行分区
- 步骤 3 – 递归对左侧分区进行快速排序
- 步骤 4 – 递归对右侧分区进行快速排序

### 快速排序伪代码

要深入了解，让我们看看快速排序算法的伪代码 –

```
procedure quickSort(left, right)
   if right - left <= 0 then
      return
   else
      pivot = A[right]
      partition = partitionFunc(left, right, pivot)
      quickSort(left, partition - 1)
      quickSort(partition + 1, right)
   end if
end procedure
```

要了解 C 语言中快速排序的实现，请单击此处。

### C 语言中的快速排序程序

快速排序是一种高效的排序算法，基于将数据数组划分为更小数组的方式。大数组被划分为两个数组，一个存储小于指定值（称为基准值 pivot）的值，另一个存储大于基准值的值，划分依据即为该基准值。

### C 语言实现

```c
#include <stdio.h>
#include <stdbool.h>
#define MAX 7
int intArray[MAX] = {4, 6, 3, 2, 1, 9, 7};

void printline(int count) {
   int i;
   for (i = 0; i < count - 1; i++) {
      printf("=");
   }
   printf("=\n");
}

void display() {
   int i;
   printf("[");
   // navigate through all items
   for (i = 0; i < MAX; i++) {
      printf("%d ", intArray[i]);
   }
   printf("]\n");
}

void swap(int num1, int num2) {
   int temp = intArray[num1];
   intArray[num1] = intArray[num2];
   intArray[num2] = temp;
}

int partition(int left, int right, int pivot) {
   int leftPointer = left - 1;
   int rightPointer = right;

   while (true) {
      while (intArray[++leftPointer] < pivot) {
         // do nothing
      }

      while (rightPointer > 0 && intArray[--rightPointer] > pivot) {
         // do nothing
      }

      if (leftPointer >= rightPointer) {
         break;
      } else {
         printf(" item swapped :%d,%d\n", intArray[leftPointer], intArray[rightPointer]);
         swap(leftPointer, rightPointer);
      }
   }

   printf(" pivot swapped :%d,%d\n", intArray[leftPointer], intArray[right]);
   swap(leftPointer, right);

   printf("Updated Array : ");
   display();
   return leftPointer;
}

void quickSort(int left, int right) {
   if (right - left <= 0) {
      return;
   } else {
      int pivot = intArray[right];
      int partitionPoint = partition(left, right, pivot);
      quickSort(left, partitionPoint - 1);
      quickSort(partitionPoint + 1, right);
   }
}

int main() {
   printf("Input Array : ");
   display();
   printline(50);
   quickSort(0, MAX - 1);
   printf("Output Array : ");
   display();
   printline(50);
}
```

如果编译并运行上述程序，将产生以下结果 –

```
Input Array: [4 6 3 2 1 9 7]

pivot swapped :9,7
Updated Array: [4 6 3 2 1 7 9 ]
pivot swapped :4,1
Updated Array: [1 6 3 2 4 7 9 ]
item swapped :6,2
pivot swapped :6,4
Updated Array: [1 2 3 4 6 7 9 ]
pivot swapped :3,3
Updated Array: [1 2 3 4 6 7 9 ]
Output Array: [1 2 3 4 6 7 9 ]
```

## 图数据结构

## 27. 图 数据结构与算法

图是一组对象的图形表示，其中一些对象对通过链接相连。相互连接的对象由称为**顶点**的点表示，连接顶点的链接称为**边**。

形式上，图是一组集合 (V, E)，其中 V 是顶点集合，E 是连接顶点对的边集合。请看下图 –

![](img/30fc9e3f8ee01facfae8d1c9621936b3_194_0.png)

在上图中，

```
V = {a, b, c, d, e}
E = {ab, ac, bd, cd, de}
```

