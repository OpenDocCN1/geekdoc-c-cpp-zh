
使用行主序表示的 A[R,C] 如图 4.7 所示。

![](img/45784b9f0334626143002ec0d63692fd_135_0.png)

### 图 4.7 使用行主序的数组表示

列主序表示如图 4.8 所示。

![](img/45784b9f0334626143002ec0d63692fd_135_1.png)

### 图 4.8 使用列主序的数组表示

不同顺序数组的索引公式如下：

**行主序：** A[i,j] 的地址为 A[i,j] = 前 (i-1) 行的所有元素 + 从第 i 列到第 j 列的元素个数 = (i-1) * c + j

**列主序：** A[i,j] = 前 (j-1) 列的所有元素 + 从第 j 列到第 i 行的元素个数 = (j-1) * r + i

## 4.4 初始化数组

声明局部作用域的常规数组（例如在函数内）时，不会对元素进行默认初始化。因此应对其进行初始化，而全局数组和静态数组的元素会自动初始化为默认值，即零。在局部和全局两种情况下，声明数组时，可以通过将值括在花括号 { } 中为每个元素赋予初始值。例如：

```
int A[5]={3,4,5,2,8};
```

它创建如图 4.9 所示的数组。

![](img/45784b9f0334626143002ec0d63692fd_135_2.png)

### 图 4.9 数组初始化

花括号 { } 中的值的数量不得超过数组大小。在图 4.9 的示例中，数组 A 声明了 5 个元素，花括号 { } 中的初始值列表被分配给这 5 个元素中的每一个。

在数组初始化期间，不必指定大小，方括号可以留空 [ ]，如

```
int A[]={3,4,5,2,8};
```

在这种情况下，编译器将假设数组的大小与花括号 { } 中的值的数量匹配。

## 4.5 访问数组值

数组的元素可以像普通变量一样单独访问，从而能够读取和修改它们的值。格式如下：

```
Array-name[index]
```

考虑前一个示例，其中 A 有 5 个元素，每个元素的类型均为 int，用于引用每个元素的名称如图 4.10 所示。

| A[0] | A[1] | A[2] | A[3] | A[4] |
|---|---|---|---|---|
| | | | | |

### 图 4.10 引用元素

要将值 75 存储在 A 的第三个元素中，语句写为 A[2]=75；要将 A 的第三个元素的值传递给任何变量，则语句为 a = A[2]。请注意，A 的第三个元素指定为 A[2]，因为数组索引从零开始，即第一个是 A[0]，第二个是 A[1]，因此第三个是 A[2]，最后一个元素是 A[4]。因此，A[5] 指的是 A 的第六个元素，这超过了数组的大小。

在 C++ 中，超出数组有效索引范围在语法上是正确的。这会造成问题，因为访问越界元素不会导致编译错误，但可能导致运行时错误。此时，有必要清楚地区分与数组相关的下标 [ ] 的两种用途。它们执行两项不同的任务：一是在声明数组时指定数组的大小，第二是为具体的数组元素指定索引。

```
int A[5];        //declaration of a new array
A[2];            //access to an element of the array
```

数据类型始终位于变量或数组声明之前，而从不位于访问之前。

## 4.6 数组操作

可对数组执行的各种操作如下：

- 遍历
- 插入
- 删除
- 排序
- 查找

### 4.6.1 遍历

访问数组中每个元素恰好一次称为遍历。此操作用于显示数组中每个元素的内容，以便轻松计算数组中的元素数量。

### 算法 4.1

```
1 Set i=LB //Initializing the counter variable
2 Repeat step3 and 4 while i<=UB
3 VISIT (A[i]) //process the element
4 i=i+1 //Moving to next location, increment the counter
5 End
```

或使用 for 循环

```
1. Repeat for i=LB to UB
2. VISIT (A[i])
3. End
```

在算法 4.1 中，VISIT() 是一个对数组执行操作的过程，例如显示数组的元素等。

### 4.6.2 插入

插入是一种用于向数组中添加元素的操作。在内存可用时，在数组末尾插入元素很容易。当需要在数组中间进行插入时，则必须将大部分元素向下移动，以保持元素的顺序。

算法 4.2 说明了将元素 ITEM 插入到数组 ARR 的给定索引位置 POS。

### 算法 4.2

```
INSERT(ARR,N,POS,ITEM)
ARR is an array of size N. POS is the index to insert the element.
1. Set i=n //Initialize the counter variable
2. Repeat steps 3 and 4 while i>=POS
3. Move ith element downwards
   Set ARR[i+1] = ARR[i].
4. Set i=i-1 //decrement the counter variable.
5. Insert element at 'POS'
   Set ARR[POS]=ITEM
6. Set N=N+1 //Increment N value
7. End
```

算法 4.2 通过从 POS 位置开始将每个元素向下移动来创建内存空间。按逆序移动元素，即移动 ARR[N-1] 和 ARR[POS]，否则数据可能会重叠。创建空间后，将元素 ITEM 插入到 POS 位置。

示例：ARR 是一个大小为 10、包含 6 个元素的数组。数组中的所有项目均按递增顺序排列，如图 4.11(a) 所示。假设向数组中添加 25，则数据元素 30、40、50、60 必须各向下移动一个位置，如图 4.11(b) 所示。

![](img/45784b9f0334626143002ec0d63692fd_138_0.png)

### (a) 包含 6 个元素的数组

### (b) 向下移动元素

### 图 4.11 插入操作

首先将元素 ARR[6]=60 移动到 ARR[7]，将 ARR[5] 移动到 ARR[6]，依此类推。

### 4.6.3 删除

删除是一种用于从数组中移除元素的操作。在数组末尾删除元素可以轻松完成，而在数组中间或指定位置删除元素会导致数据元素各向上移动一个位置以填充数组。

算法 4.3 从包含 N 个元素的数组 ARR 中删除指定位置 POS（其中 POS<=N）处的元素，并将其赋给变量 ITEM。

### 算法 4.3

```
DELETE (ARR, N, POS, ITEM)
1. Set ITEM=ARR [POS]
2. Repeat for i=POS to N-1
3. Set ARR [i] =ARR [i+1] //move elements upward
4. Set N=N-1
5. End
```

示例：考虑一个大小为 10 且包含 6 个数据元素的数组 ARR。删除 A[2] 处的元素会导致其他元素各向上移动一个位置，如图 4.12 所示。

![](img/45784b9f0334626143002ec0d63692fd_139_0.png)

### 4.6.4 排序

排序是一种用于将数组元素按升序或降序排列的操作。算法 4.4 说明了按升序对元素进行排序。

### 算法 4.4

```
SORT : N=UB
1. Set N=UB
2. while i>=LB do
3. Set q=LB //comparing the first
4. while j<=i do
5. check whether A[j] and A[j+1] are in order, if so swap the elements
   SWAP (A[j], A[j+1])
6. Set j=j+1
7. Set i=i-1
8. End
```

### 4.6.5 查找

查找是一种用于从数组元素列表中查找特定元素位置的操作。找到项目后，查找被认为是成功的。存在不同类型的查找算法。这些算法的使用取决于数据元素在数据结构中的排列方式。关于查找技术的详细讨论可见第 16 章。

### 程序 4.1

```
#include<iostream.h>
#include<conio.h>
#include<stdlib.h>
template<class t>
class array
{
    t a[50];
    int n,size;
    public:
    array(int m)
    {
    size=0;
    n=m;
    }
    void insert();
    void delete();
    void display();
};
template<class t>
void array<t>::insert()
{
    t ele;
    if(size==n)
    {
    cout<<"array is overflow\n";
    return;
    }
    size++;
    cout<<"enter the element\n";
    cin>>ele;
    a[size]=ele;
}
template<class t>
void array<t>::deletee()
{
    t ele;
    if(size==0)
    {
    cout<<"array is underflow\n";
    return;
    }
    ele=a[size];
    size--;
    cout<<"the deleted element is"<<ele<<"\n";
}
template<class t>
void array<t>::display()
