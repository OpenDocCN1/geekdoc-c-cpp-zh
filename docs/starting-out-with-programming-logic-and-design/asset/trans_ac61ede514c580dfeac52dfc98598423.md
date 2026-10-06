

```
Module main(){
    // 数组大小常量
    Constant Integer SIZE = 6

    // 整数数组
    Declare Integer numbers[SIZE] = 4, 6, 1, 3, 5, 2

    // 循环计数器
    Declare Integer index

    // 按原始顺序显示数组。
    Display "Original order":
    For index = 0 To SIZE - 1
        Display numbers[index]
    End For

    // 排序数字。
    Call selectionSort(numbers, SIZE)

    // 显示空行。
    Display

    // 显示排序后的数组。
    Display "Sorted order":
    For index = 0 To SIZE - 1
        Display numbers[index]
    End For
End Module

    // selectionSort 模块接收整数数组
    // 和数组的大小作为参数。当模块完成后，
    // 数组中的值将按升序排序。
Module selectionSort(Integer Ref array[], Integer arraySize)
    // startScan 将保存扫描的起始位置。
    Declare Integer startScan

    // minIndex 将找到扫描区域内
    // 数值最小元素的索引。
    Declare Integer minIndex

    // minValue 将保存扫描区域内
    // 找到的最小值。
    Declare Integer minValue

    // index 是用于存储下标的计数变量。
    Declare Integer index

    // 外层循环遍历数组中的每个元素（除最后一个元素）。
    // startScan 变量标记了扫描应该开始开始的位置。
    For startScan = 0 To arraySize - 2

      // 假设可扫描区域的第一个元素
    // 是最小值。
      Set minIndex = startScan
      Set minValue = array[startScan]

      // 扫描数组，从可扫描区域的第二个元素
      // 开始。我们正在寻找可扫描区域内的最小值。
      For index = startScan + 1 To arraySize - 1
          If array[index] < minValue Then
              Set minValue = array[index]
              Set minIndex = index
          End If
      End For

      // 将具有最小值的元素
      // 与可扫描区域的第一个元素交换。
      Call swap(array[minIndex], array[startScan])
  End For
  End Module

  // swap 模块接收两个整数参数
  // 并交换它们的内容。
  Module swap(Integer Ref a, Integer b)
      // 用于临时存储的局部变量 a
      Declare Integer temp

      // 交换 a 和 b 中的值。
      Set temp = a
      Set a = b
      Set b = temp
  End Module
```

## 9.2 选择排序算法 357

## 程序输出

原始顺序：

![](img/c939132f78787c7f339c6977b3fc8c85_381_0.png)

排序顺序：

## 第 9 章 数组的排序与查找

selectionSort 模块的流程图

![](img/c939132f78787c7f339c6977b3fc8c85_382_0.png)

## 9.3 插入排序算法

> 注意：你可以修改 selectionSort 模块，通过将第 63 行的“小于”运算符改为“大于”来使数组按降序排序，如下所示：

If array[index] > maxValue Then

注意，我们还将 `minValue` 变量名更改为 `maxValue`，这对于降序排序更为合适。你需要在整个模块中进行此更改。

## 9.3 插入排序算法

概念：插入排序算法比冒泡排序更高效。它处理前两个元素，使其成为排序部分。它将剩余元素逐一个地插入到排序部分的正确位置。

插入排序算法是另一种比冒泡排序更高效的算法。它开始处理数组的前两个元素，并在必要时交换它们以使其处于正确的顺序。

然后，目标是将数组的第三个元素纳入排序部分。这是通过将第三个元素插入到相对于前两个元素的正确位置来实现的，此时前三个元素成为排序部分。

这个过程对于第四个元素及后续元素继续进行，直到所有元素都插入到它们的正确位置。让我们来看一个例子。假设我们从图 9-18 所示的整数数组开始。如图所示，前两个元素无序的，因此它们将进行交换。

## 图 9-18 未排序的数组

| 7 | | 4 | 6 | | 1 |
|---|---|---|---|---|

交换完成后，前两个元素成为排序部分。下一步是移动第三个元素，使其处于相对于前两个元素的正确位置。如图 9-19 所示，第三个元素必须插入到前两个元素之间。

## 图 9-19 第三个元素必须移动

第三个元素必须插入到前两个元素之间。

| 2 | 7 | 4 | 6 | 3 | 1 |
|---|---|---|---|---|

这是数组的排序部分。

第三个元素移动到新位置后，前三个元素成为排序部分。下一步是移动第四个元素，使其处于相对于前三个元素的正确位置。如图 9-20 所示，第四个元素必须插入到第二个和第三元素之间。

## 图 9-20 第四个元素必须移动

第四个元素必须插入到第二个和第三元素之间。

| 2 | 4 | 7 | 6 | 3 | 1 |
|---|---|---|---|---|

这是数组的排序部分。

第四个元素移动到新位置后，前四个元素成为排序部分。下一步是移动第五个元素，使其处于相对于前四个元素的正确位置。如图 9-21 所示，第五个元素必须插入到前一个和第二个元素之间。

## 图 9-21 第五个元素必须移动

第五个元素必须插入到前一个和第二个元素之间。

| 2 | 4 | 6 | 7 | 3 | 1 |
|---|---|---|---|---|

这是数组的排序部分。

第五个元素移动到新位置后，前五个元素成为排序部分。下一步是移动第六个元素，使其处于相对于前五个元素的正确位置。如图 9-22 所示，第六个元素必须移动到数组的开头。

## 图 9-22 第六个元素必须移动

![](img/c939132f78787c7f339c6977b3fc8c85_385_0.png)

第六个元素是数组中的最后一个元素。一旦它移动到正确位置，整个数组就排序完成了。如图 9-23 所示。

## 图 9-23 所有元素都处于正确位置

![](img/c939132f7878c7f339c6977b3fc8c85_385_1.png)

图 9-24 显示执行插入排序的模块流程图。该模块接收一个整数数组（引用传递）和一个指定大小的整数。模块完成后，数组将按升序排序。程序 9-6 显示了伪代码形式的 insertionSort 模块。

## 第 9 章 数组的排序与查找

# 程序 9-6

```
Module main()
    // 数组大小常量
    Constant Integer SIZE = 6

    // 整数数组
    Declare Integer numbers[SIZE] = 4, 6, 1, 3, 5, 2

    // 循环计数器
    Declare Integer index

    // 按原始顺序显示数组。
    Display "Original order":
    For index = 0 To SIZE - 1
        Display numbers[index]
    End For

    // 排序数字。
    Call insertionSort(numbers, SIZE)

    // 显示空行。
    Display

    // 显示排序后的数组。
    Display "Sorted order":
    For index = 0 To SIZE - 1
        Display numbers[index]
    End For
End Module

// insertionSort 模块接收整数数组
// 和数组的大小作为参数。当模块完成后，
// 数组中的值将按升序排序。
 insertionSort(Integer Ref array[], Integer arraySize)
    // 循环计数器
    Declare Integer index

    // 用于扫描数组的变量
    Declare Integer scan

    // 存储第一个未排序值的变量
    Declare Integer unsortedValue

    // 外层循环通过 index 遍历数组的
    // 每个下标，从 1 开始。这是因为
    // 元素 0 被认为已经是排序的。
    For index = 1 To arraySize - 1
        Set unsortedValue = array[index]
        Set scan = index - 1
        While scan >= 0 AND array[scan] > unsortedValue
            Set array[scan + 1] = array[scan]
            Set scan = scan - 1
        End While
        Set array[scan + 1] = unsortedValue
    End For
End Module
```

