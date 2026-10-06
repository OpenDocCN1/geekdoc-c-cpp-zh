

## 焦点聚焦：

## 使用二分查找算法

Constance 管理着一所有六名导师的烹饪学校。她请你设计一个程序，让她查询导师的电话号码。你决定使用两个并行数组：一个名为 `names`，用于存储导师的名字；另一个名为 `phones`，用于存储每个导师的电话号码。以下是通用算法：

- 1. 从用户处获取导师的姓氏。
- 2. 在 `names` 数组中搜索该姓。
- 3. 如果找到了姓，获取其下标。使用该下标显示并行数组的内容。如果未找到姓，则显示一条消息，表示数组中未找到该值。

程序 9-8 显示了程序的伪代码。注意数组内容已经按升序排列。这非常重要，因为程序使用二分查找算法在 `names` 数组中定位一个姓名。

## 程序 9-8

```cpp
Module main()
  // 数组大小的常量
  Integer SIZE = 6

  // 导师姓名数组，已按升
  // 序排列。
  Declare String names[SIZE] = "Hall", "Harrison", "Hoyle", "Kimura", "Lopez", "Pike"

  // 导师电话的并行数组。
  Declare String phones[SIZE] = "555-6783", "555-0199", "555-9974", "555-2377", "555-7772", "555-1716"

  // 用于存储要搜索的姓变量。
  Declare String searchName

  // 用于存储姓下标的变量。
  Declare Integer index

  // 控制循环的变量。
  Declare String again = "Y"
  While (again == "Y" OR again == "y") // 获取要搜索的姓
    Display "Enter a name to search"
    Input searchName

    // 搜索姓。
    index = binarySearch(names, searchName, SIZE)

    If index = -1 Then
      // 显示电话。
      Display "The phone number is ", phones[index]
    Else
      // 数组中未找到该姓。
      Display searchName, " was not found."
    End If

    // 再次搜索？
    Display "Do you want to search again? (Y=Yes, N=No)"
    Input again
  End While

// binarySearch 函数接收参数
// 要搜索的数组以及数组的大小。
// 如果在数组中找到值，则返回下标。
// 否则返回 -1。
Function Integer binarySearch(String array[], String value, Integer arraySize)
  // 存储第一个元素下标的变量。
  Declare Integer first = 0
  // 最后一个元素的下标。
  Declare Integer last = arraySize - 1
  // 搜索值的位置。
  Declare Integer position = -1
  // 标记
  Declare Boolean found = False
  // 存储中间位置下标的变量。
  Declare Integer middle
  While (NOT found) AND (first <= last)
    Set middle = (first + last) / 2
    // 查看是否在中间位置找到值...
    If array[middle] == value Then
      Set position = middle
      Set found = True
    // 否则，如果值在左半部分...
    Else If array[middle] > value Then
      Set last = middle - 1
    // 否则，如果值在右半部分...
    Else
      Set first = middle + 1
    End If
  End While
  // 返回元素的位置，或者在
// 未找到元素时返回 -1。
  Return position
End Function
```

## 第9章 数组的排序与查找

## 程序输出（输入加粗）

输入要搜索的姓。
**Lopez** 
电话号码是 555-7772
再次搜索？(Y=是, N=否)
**Y** 
输入要搜索的姓。
**Harrison** 
电话号码是 555-0199
再次搜索？(Y=是, N=否)
**Y** 
输入要搜索的姓。
**Lee** 
未找到 Lee。
再次搜索？(Y=是, N=否)
**N** 

## 节点

- 9.4 描述顺序查找和二分查找的区别。
- 9.5 平均而言，对于一个有 1,000 个元素的数组，顺序查找将执行多少次比较？（假设要搜索的对象在数组中。）
- 9.6 对于一个有 1,000 个元素的数组，二分查找执行的最大比较次数是多少？

## 复习题

### 单选题
1. 这种算法将数组中存储的值按特定顺序重新排列。
   a. 查找算法
   b. 排序算法
   c. 排序算法
   d. 选择算法
2. 如果数组按此顺序排序，值从低到高存储。
   a. 渐近
   b. 对数
   c. 升序
   d. 降序
3. 如果数组按此顺序排序，值从高到低存储。
   a. 渐近
   b. 对数
   c. 升序
   d. 降序
4. 这种算法多次遍历数组，使较大的值向后移动。
   a. 泡排序
   b. 选择排序
   c. 插入排序
   d. 顺序查找
5. 在这种查找中，找到数组中的最小值并将其移动到 0。继续找到并移动下一个较小值。
   a. 泡排序
   b. 选择排序
   c. 插入排序
   d. 顺序查找
6. 这种算法通过排序前两个元素开始。然后放置第三个元素相对于前两个元素。
   a. 泡排序
   b. 选择排序
   c. 插入排序
   d. 顺序查找
7. 这种算法顺序遍历数组，比较每个项目。
   a. 顺序查找
   b. 二分查找
   c. 自然顺序
   d. 选择排序
8. 这种算法反复将数组部分一半。
   a. 顺序查找
   b. 二分查找
   c. 自然顺序
   d. 选择排序
9. 这种查找对于小数组足够，但对于大数组不是。
   a. 顺序查找
   b. 二分查找
   c. 自然顺序
   d. 选择排序
10. 这种查找需要数组排序。
    a. 顺序查找
    b. 二分查找
    c. 自然顺序
    d. 选择排序

### 判断对错
1. 如果数据按升序排序，则是从低到高排列。
2. 如果数据按降序排序，则是从高到低排列。
3. 无论使用什么编程语言，无法使用泡排序对字符串进行排序。
4. 顺序查找对 n 个元素执行的平均比较次数是 n/2。
5. 顺序查找对 n 个元素执行的最大次数。

## 算法工作

1. 设计一个接受两个 Real 类型参数的模块并交换它们。
2. 以下伪代码执行什么算法？
```cpp
Declare Integer maxElement

For maxElement = arraySize - 1 To 0
  For index = 0 To maxElement - 1
    If array[index] > array[index + 1] Then
      Call swap(array[index], array[index + 1])
    End If
  End For
End For
```
3. 以下伪代码执行什么算法？
```cpp
Declare Integer
Declare Integer scan
Declare Integer unsortedValue

For index = 1 To arraySize - 1
  Set unsortedValue = array[index]
  Set scan = index

  While scan > 0 AND array[scan-1] < array[scan]
    Call swap(array[scan-1], array[scan])
    Set scan = scan - 1
  End While
  Set array[scan] = unsortedValue
End For
```
4. 以下伪代码执行什么算法？
```cpp
Declare Integer startScan

Declare Integer minIndex
Declare Integer minValue
Declare Integer index

For startScan = 0 To arraySize - 2
  Set minIndex = startScan
  Set minValue = array[startScan]

  For index = startScan + 1 To arraySize - 1
    If array[index] < minValue
      Set minValue = array[index]
      Set minIndex = index
    End If
  End For

  Call swap(array[minIndex], array[startScan])
End For
```

## 简答

1. 如果顺序查找搜索存储在 10,000 个元素数组最后一个元素的值，搜索代码需要读取多少元素来定位该值？
2. 对于有 n 个元素的数组，平均而言，顺序查找函数需要读取数组多少找到找到特定值？
3. 二分查找函数在有 1,000 个元素的数组中搜索一个值时，最大比较次数是多少？

