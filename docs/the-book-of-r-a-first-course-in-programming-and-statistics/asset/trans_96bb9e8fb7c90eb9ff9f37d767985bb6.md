

作为一个 while 循环的简单示例，请考虑以下代码：

```r
myval <- 5
while(myval<10){
  myval <- myval+1
  cat("\nmyval' is now",myval,"\n")
  cat("\ncondition' is now",myval<10,"\n")
}
```

在这里，你将一个新对象 `myval` 设置为 5。然后你启动了一个条件为 `myval<10` 的 while 循环。由于初始条件为 TRUE，你进入了大括号区域。在循环内部，你将 `myval` 增 1，打印它的当前值，并打印条件 `myval<10` 的逻辑值。循环将一直持续，直到下一次评估时 `myval<10` 变为 FALSE 为止。执行该代码块，你看到以下内容：

'myval' is 6
'condition' is now TRUE

'myval' is 7
'condition' is now TRUE

'myval' is 8
'condition' is now TRUE

'myval' is 9
'condition' is now TRUE

'myval' is 10
'condition' is now FALSE

正如预期的，循环不断重复，直到 `myval` 被设置为 10，此时 `myval<10` 返回 FALSE，由于初始条件不再为 TRUE，循环退出。

在更复杂的设置中，将条件设置为一个独立的对象通常很有用，这样你就可以在大括号区域根据需要对其进行修改。在下一个示例中，你将使用 while 循环遍历向量，并创建一个与当前整数维度匹配的单位矩阵（参见第 3.3.2 节）。当该循环遇到向量中大于 5 的数字或到达整数向量的末尾时，应该停止。

在编辑器中，定义一些初始对象，然后是循环本身。

```r
mylist <- list()
counter <- 1
mynumbers <- c(4,5,1,2,6,2,4,6,6,2)
mycondition <- numbers[counter]<=5
while(mycondition){
```

```r
mylist[[counter]] <- diag(mynumbers[counter])
counter <- counter+1
if(counter<=length(mynumbers)){
  mycondition <- mynumbers[counter]<5
} else {
  mycondition <- FALSE
}
n
```

第一个对象 `mylist` 将存储循环创建的所有矩阵。你将使用 `mynumbers` 来提供矩阵大小，并使用 `counter` 和 `mycondition` 来控制循环。

循环条件 `mycondition` 最初被设置为 TRUE，因为 `mynumbers` 的第一个元素小于或等于 5。在 `while` 循环内部，第一行使用双方括号和 `counter` 的值在 `mylist` 的指定位置动态创建一个新条目（你之前在第 5.1.5 节中使用列表名称进行过操作）。该条目被分配了一个单位矩阵，其大小与 `mynumbers` 对应的元素匹配。接下来，`counter` 增，你现在需要更新 `mycondition`。你想检查 `mynumbers[counter]<5`，但还需要检查是否已经到达整数向量的末尾（否则，可能会因为尝试检索 `mynumbers` 范围外的索引位置导致错误）。因此，你可以使用语句首先检查条件 `<-mynumbers[counter]<5`。如果是 TRUE，则将 `mycondition` 设置为 `mynumbers[counter]<5` 的结果。如果不是，则意味着你已经到达 `mynumbers` 的末尾，因此通过设置 `mycondition <- FALSE` 来确保循环退出。

使用这些预定义对象执行循环，它将产生所示的 `mylist` 对象：

# R mylist

```r
[[1]]
[,1] [2] [3] [4]
[1,] 1 0 0 0
[2,] 0 1 0 0
[3,] 0 0 1 0
[4,] 0 0 0 1
```

```r
[[2]]
[,1] [2] [3] [4] [5]
[1,] 1 0 0 0 0
[2,] 0 1 0 0 0
[3,] 0 0 1 0 0
[4,] 0 0 0 1 0
[5,] 0 0 0 0 1
```

```r
[[3]]
[,1]
[1,] 1
```

```r
[[4]]
| [1,] | 1 |
| [2,] | 1 |
```

正如预期的，你有一个包含四个成员的列表——大小为 $4 \times 4, 5 \times 5, 1 \times 1$ 和 $2 \times 2$ 的单位矩阵——与 `mynumbers` 的前四个元素匹配。
循环在遇到 `mynumbers` 的第五个元素 (6) 时停止执行，因为它大于 5。

# 练习 10.4

- a. 根据在列表中存储单位矩阵的最新示例，在不执行任何代码的情况下，确定以下每可能的 `mynumbers` 得到的 `mylist` 会什么样：
  - i. `mynumbers <- c(2,2,2,2,5,2)`
  - ii. `mynumbers <- 2:20`
  - iii. `mynumbers <- c(10,1,10,1,2)`

然后在 R 中确认你的答案（注意你每次都需要重置 `mylist`、`counter` 和 `mycondition` 的初始值）。

- b. 对于这个问题，我将引入阶乘的概念。非负整数 $x$ 的阶乘（记作 $x!$）是指小于或等于 $x$ 的所有整数的乘积。形式上，它的写法为：$x! = x \times (x-1) \times \dots \times 1$。

