

# 直接递归与间接递归

我们目前为止讨论的示例都是直接调用自身的递归模块或函数。这被称为直接递归。程序中也存在间接递归的可能性。当模块 A 调用模块 B，而模块 B 又调用模块 A 时，就会发生这种情况。递归可能涉及多个模块。例如，模块 A 可以调用模块 B，B 可以调用模块 C，C 再调用模块 A。

![](img/c939132f78787c7f339c6977b3fc8c85_530_0.png)

# 检查点

- 13.1 说递归算法的开销大于迭代算法。这意味着什么？
- 13.2 什么是基本情况（base case）？
- 13.3 什么是递归情况（recursive case）？
- 13.4 什么导致递归算法停止调用自身？
- 13.5 什么是直接递归？什么是间接递归？

![](img/c939132f78787c7f339c6977b3fc8c85_530_1.png)

# 递归算法示例

# 使用递归计算数组元素范围的和

在这个示例中，我们查看一个名为 `rangeSum` 的函数，它使用递归来计算范围内元素的和。该函数接受以下参数：一个包含要和元素范围的整数数组，一个指定范围起始元素的整数，以及一个指定范围结束元素的整数。以下是该函数可能用法的示例：

```
Constant SIZE = 9
Declare Integer numbers[SIZE] = 1, 2, 3, 4, 5, 6, 7, 8, 9
Declare Integer sum;
Set sum = rangeSum(numbers, 3, 7)
```

这段伪代码的最后一条语句指定 `rangeSum` 函数应该返回 `numbers` 数组中从元素 3 到 7 的元素的和。该返回值（在这种情况下为 30）被赋值给变量 `sum`。以下是 `rangeSum` 函数的伪代码定义：

```
Function rangeSum(Integer array[], Integer start,
  Integer end)
  If start > end Then
    Return 0
  Else
    Return array[start] + rangeSum(array, start + 1, end)
  End If
End Function
```

# 13.3 递归算法示例

该函数的基本情况是 `start` 参数大于 `end` 参数。如果条件为真，函数返回值 0。否则，函数执行以下语句：

```
Return array[start] + rangeSum(array, start + 1, end)
```

该语句返回 `array[start]` 加上递归调用的返回值。请注意，在递归调用中，范围内的起始元素是 `start + 1`。从本质上说，这意味着“返回范围内第一个元素的值加上范围内所有元素的和”。程序 13-4 中的伪代码演示了：

# 程序 13-4

```
Module main(){
    // 声明一个数组大小的常量。
    Constant Integer SIZE = 9

    // 声明一个整数数组。
    Declare Integer numbers[SIZE] = 1, 2, 3, 4, 5, 6, 7, 8, 9

    // 声明一个存储和的变量。
    Declare Integer sum
    Set sum = rangeSum(numbers, 2, 5)

    // 显示元素 2 到 5 的和。
    Display "The sum of elements 2 through 5 is ", sum
End Module

    // rangeSum 函数返回数组中指定
    // 范围元素的和。start 参数
    // 指明了起始元素。end 参数
    // 指明了结束元素。
    Function rangeSum(Integer array[], Integer start, Integer end)
        If start > end
            Return 0
        Else
            Return array[start] + rangeSum(array, start + 1, end)
    End Function
```

# 程序输出

元素 2 到 5 的和为 18

# 斐波那契数列

某些数学问题是通过递归解决的。其中一个广为人知的例子是斐波那契数的计算。斐波那契数以意大利数学家利奥昂纳·斐波波那契（出生于约 1170 年）命名，其序列如下：

0, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, . . .

注意在第二个数字之后，序列中的每个数字都是前两个数之和。斐波那契数列可以定义如下：

如果 n = 0 则 Fib(n) = 0
如果 n = 1 则 Fib(n) = 1
如果 n > 2 则 Fib(n) = Fib(n-1) + Fib(n-2) （注：原文为 n > 2，逻辑上通常为 n > 1）

以下是递归计算斐波那契数的 `fib` 函数：

```
Function fib(Integer n)
    If n == 0
        Return 0
    Else If n == 1
        Return 1
    Else
        Return fib(n - 1) + fib(n - 2)
    End If
```

注意 `fib` 函数实际上有两种情况：`n` 等于 0 和 `n` 等于 1。程序 13-5 的伪代码通过显示递归调用来演示这一点。

# 程序 13-5

显示斐波那契数列的前 10 个数字：

```
Module main()
    // 用作计数器的局部变量。
    Declare Integer counter

    // 显示引导信息。
    Display "The Fibonacci numbers are:"

    // 使用循环调用 fib 函数。
    For counter = 1 To 10
        Display fib(counter)
    End For

    // fib 函数返回第 n 个数字。
    Function fib(Integer n)
        If n == 0
            Return 0
        Else If n == 1
            Return 1
        Else
            Return fib(n - 1) + fib(n - 2)
    End If
```

# 程序输出

The Fibonacci numbers are:
1
1
2
3
5
8
13
21
34
55

# 求公约数

我们的下一个递归示例是计算两个整数 x 和 y 的最大公约数（GCD），方法如下：

如果 x 能被 y 整除，则 GCD 为 y。否则，GCD 为 x mod y。

# 程序 13-6

```
Module main()
    // 用于输入的变量。
    Declare Integer num1, num2

    // 获取输入。
    Display "Enter an integer: "
    Input num1

    // 获取输入。
    Display "Enter another integer: "
    Input num2

    // 显示 GCD。
    Display "The greatest divisor of these numbers is ", gcd(num1, num2)
End Module

    // gcd 函数判断 x 是否能被 y 整除。
    Function Integer gcd(Integer x, Integer y)
        If x mod y == 0
            Return y
        Else
            Return gcd(y, x mod y)
        End If
```

# 程序输出

Enter an integer: 48
Enter another integer: 18
The greatest divisor of these numbers is 6

# 二分查找函数

在第 9 章中，你学习了二分查找算法并看到了循环示例。二分查找算法也可以通过递归实现。对于该示例，过程可以表示为：

```
If array[middle] 等于搜索值，则找到了该值。
Else if array[middle] 小于搜索值，则对数组的右半部分进行二分查找。
Else if array[middle] 大于搜索值，则对数组的左半部分进行二分查找。
```

当你将递归算法与循环算法进行比较时，会发现递归版本更加优雅且容易理解。递归二分查找也是将问题分解为更小部分直到解决的良好示例。递归 `binarySearch` 的伪代码如下：

```
Function binarySearch(Integer array[],
Integer first, Integer last, Integer value)
// 存储搜索区域中间元素下标的局部变量。
Declare Integer middle

// 首先，检查是否有元素可以搜索。
If first > last Then
    Return -1
End If

// 计算搜索区域的中点。
Set middle = (first + last) / 2

// 查看是否在中点处找到了该值 . .
If array[middle] == value Then
    Return middle
End If

// 搜索右半部分或左半部分。
If array[middle] < value Then
    Return binarySearch(array, middle + 1, last, value)
Else
    Return binarySearch(array, first, middle - 1, value)
End If
End Function
```

