

## 8.3 处理数组的内容 307

图 8-8 查找数组中最小值的流程图

![](img/c939132f78787c7f339c6977b3fc8c85_331_0.png)

```
Program 8-12
1 // 定义数组大小常量。
2 Constant Integer SIZE = 5
3
4 // 定义一个带有初始值的数组。
5 Declare Integer numbers[SIZE] = 8, 1, 12, 6, 2
6
7 // 为数组定义计数器变量。
8 Declare Integer index
9
10 // 定义一个用于存储最低值的变量。
11 Declare Integer lowest
12
13 // 将第一个元素赋值给 lowest。
14 Set lowest = numbers[0]
15
16 // 遍历数组剩余部分，
17 // 从元素 1 开始。当找到比 lowest
18 // 小的值时，将该值
19 // 赋值给 lowest。
20 For index = 1 TO SIZE - 1
21  If numbers[index] < lowest Then
22      Set lowest = numbers[index]
23  End If
24  End For
25
26 // 显示最低值。
27 Display "The lowest value in the array is ", lowest
```

# 程序输出

数组中的最低值为 1

# 复制数组

在编程语言中，如果你需要将一个数组的内容复制到另一个数组，必须将正在复制的数组元素单独赋值给另一个数组的元素。通常，使用循环完成最好。例如，查看以下伪代码：

```
Constant Integer SIZE = 5
Declare Integer firstArray[SIZE] = 100, 200, 300, 400, 400
Declare Integer secondArray[SIZE]
```

假设你想将 `firstArray` 中的值复制到 `secondArray`。以下伪代码将 `firstArray` 的每个元素赋值给 `secondArray` 对应的元素。

```
Declare Integer index
For index = 0 To SIZE - 1
Set secondArray[index] = firstArray[index]
End For
```

# 将数组作为参数传递给模块或函数

大多数语言允许你将数组作为参数传递给模块或函数。这让你能够对在数组上执行的许多操作进行模块化。将数组作为参数通常需要传递两个参数：(1) 数组，以及 (2) 指定数组中元素数量的索引。程序 8-13 中的伪代码显示了一个接受整数作为参数的函数示例。该函数返回数组元素的总和。

# 程序 8-13

![](img/c939132f78787c7f339c6977b3fc8c85_332_0.png)

```
1 Module main()
2     // 数组大小常量。
3     Constant Integer SIZE = 5
4
5
6
7     定义一个带有初始值的数组。
8     Declare Integer numbers[SIZE] = 2, 4, 6, 8, 10
9
10
11 // 用于存储元素之和的变量。
12 Declare Integer sum
13 // 获取元素的总和。
14 Set sum = getTotal(numbers, SIZE)
15
16 // 显示数组元素的总和。
17 Display "The sum of the array elements is ", sum
18 End Module
19 // getTotal 函数接受一个整数数组和
20 数组大小作为参数。它返回数组
21 // 元素的总和。
22 Function getTotal(Integer array[], Integer arraySize)
23 // 循环计数
24 Declare Integer index
25
26 // 累加器，初始化为 0
27 Declare Integer total = 0
28
29 // 计算数组元素的总和。
30 For index = 0 To ArraySize - 1
31 Set total = total + array[index]
32 End For
33
34 // 返回总和。
35 Return total
36 End Function
```

# 程序输出

数组元素的总和为 30

在主模块中，第 6 行声明了一个整数数组并初始化了五个值。第 12 行的以下语句调用了 `getTotal` 函数并将其返回值赋值给变量 `sum`：

```
Set sum = getTotal(numbers, SIZE)
```

该语句向 `getTotal` 函数传递了两个参数：`numbers` 数组和 `SIZE` 常量的值。这里是 `getTotal` 函数的第一行，出现在第 21 行：

Function getTotal(Integer array[], Integer arraySize)

注意该函数具有这两个参数：

- Integer array[]—此参数接受一个整数数组作为参数。
- Integer arraySize—此参数接受一个整数，指定数组中元素的数量。

当在第 12 行调用函数时，它将 `numbers` 数组传递给 `array` 参数，并将 `SIZE` 常量的值传递给 `arraySize` 参数。如图 8-9 所示。该函数计算 `array` 中值的总和并返回该值。

# 图 8-9 向 getTotal 函数传递参数

Set sum = getTotal(numbers, SIZE)

![](img/c939132f78787c7f339c6977b3fc8c85_334_0.png)

Function Integer getTotal(Integer array[], Integer arraySize)

# 焦点：
处理数组

LaClaire 博士在她的化学课上学期内进行了四次考试。学期结束时，她要求你设计一个程序，找出最低分并在删除最低分后计算平均分。以下是该算法：

- Integer array[]—此参数接受一个整数数组作为参数。
- Integer arraySize—此参数接受一个整数，指定数组中元素的数量。

## 8.3 处理数组的内容 309

## 8.3 处理数组的内容 311

## 第 8 章 数组 312

