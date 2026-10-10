
最初，将 `loopindex` 设置为 1，以便它能遍历 `foo` 的索引位置（序列 `1:length(foo)`）。在括号代码中，第一条命令是将 `foo` 的成员写入一个对象成员。接下来，你可以使用 `is.matrix` 检查 `member` 是否为矩阵（参见第 6.2.3 节）。如果是 TRUE，执行以下操作：`is.mat` 向量的第 i 个位置设置为 "yes"；`nr` 和 `nc` 的第 i 个位置分别设置为 `member` 的行数和列数；`data.type` 的元素被设置为 `class(as.vector(member))` 的结果。最后这条命令通过 `as.vector` 将矩阵强制转换为向量，然后使用 `class` 函数（第 6.2.2 节介绍）找到元素的数据类型。

如果 `member` 不是矩阵且 `if` 条件失败为 "No"，则其他向量中的条目不会发生改变（因此将保持原样）。
循环运行时，将从向量创建一个数据框（注意使用 `stringsAsFactors=FALSE` 以防止 `bar` 中的字符串向量被自动转换为因子；见第 5.2.1 节）。执行代码后，`bar` 如下所示：

| name | is.mat | nr | nc | data.type |
| :--- | :--- | :--- | :--- | :--- |
| aa | No | NA | NA | <NA> |
| bb | Yes | 2 | 2 | integer |
| cc | Yes | 3 | 2 | logical |
| dd | No | NA | NA | <NA> |
| ee | Yes | 4 | 1 | character |

如你所示，这与列表 `foo` 中存在的矩阵性质相匹配。

# 嵌套循环

你也可以嵌套 `for` 循环，就像 `if` 语句一样。当一个 `for` 循环嵌套在另一个循环中时，在外部循环索引增加之前，内部循环会完整执行完毕，此时内部循环将再次从头开始执行。在你的 R 控制台中创建以下对象：

```
R> loopvec1 <- 5:7

R> loopvec1

[1] 5 6 7

R> loopvec2 <- 9:6

R> loopvec2

[1] 9 8 7 6

R> foo <- matrix(NA,length(loopvec1),length(loopvec2))
```

```
R> foo

[,1] [2] [3] [4]

[1] NA NA NA NA

[2] NA NA NA NA

[3] NA NA NA NA
```

以下嵌套循环用 `loopvec1` 中每个整数与 `loopvec2` 的乘积结果填充了 `foo`：

```
R> for(i in 1:length(loopvec1))
+   for(j in 1:length(loopvec2))
+     foo[i,j] <- loopvec1[i]*loopvec2[j]
+
R> foo
```

```
[,1] [2] [3] [4]

[1] 45 40 35 30

[2] 54 48 42 36

[3] 63 56 49 42
```

注意，嵌套循环要求每个 `for` 使用都有一个唯一的循环索引。在这种情况下，循环索引 `i` 用于外部循环，`j` 用于内部循环。当执行代码时，`i` 被赋值为 1，内部循环开始，`j` 也赋值为 1。内部循环的唯一命令是将 `loopvec1` 与 `loopvec2` 的乘积赋值给 `foo`。内部循环直到 `j` 达到 `length(loopvec2)`，`i` 增加。当 `i` 达到 `length(loopvec1)` 后，整个过程完成。

内部向量可以定义为匹配 `loopvec2` 的值，以填充 `foo` 的第一列。这里有一个例子：

```
R> foo <- matrix(NA,length(loopvec1),length(loopvec2))

R> foo

[,1] [2] [3] [4]

[1] NA NA NA NA

[2] NA NA NA NA

[3] NA NA NA NA

R> for(i in 1:length(loopvec1))
+   for(j in 1:length(loopvec2))
+     foo[i,j] <- loopvec1[i]*loopvec2[j]
+
R> foo
```

[,1] [2] [3] [4]
[1] 45 40 35 30
[2] 54 48 42 36
[3] 63 56 49 42

注意，嵌套循环要求每个 `for` 使用都有一个唯一的循环索引。在这种情况下，循环索引 `i` 用于外部循环，`j` 用于内部循环。当执行代码时，`i` 被赋值为 1，内部循环开始，`j` 也赋值为 1。内部循环的唯一命令是将 `loopvec1` 与 `loopvec2` 的乘积赋值给 `foo`。内部循环直到 `j` 达到 `length(loopvec2)`，`i` 增加。当 `i` 达到 `length(loopvec1)` 后，整个过程完成。

内部向量可以定义为匹配 `loopvec2` 的值，以填充 `foo` 的第一列。这里有一个例子：

```
R> foo <- matrix(NA,length(loopvec1),length(loopvec2))

R> foo

[,1] [2] [3] [4]

[1] NA NA NA NA

[2] NA NA NA NA

[3] NA NA NA NA

R> for(i in 1:length(loopvec1))
+   for(j in 1:length(loopvec2))
+     foo[i,j] <- loopvec1[i]*loopvec2[j]
+
R> foo
```

[,1] [2] [3] [4]
[1] 45 40 35 30
[2] 54 48 42 36
[3] 63 56 49 42

# 2.2 while Loops

要使用循环，你必须知道或能够计算出循环重复的次数。在不知道需要运行多少次操作的情况下，可以使用 `while` 循环。`while` 循环在特定条件返回 TRUE 时运行并重复，其通用格式如下：

```
while(loopcondition){
  do any code
}
```

`while` 循环使用简单的逻辑值 `loopcondition` 来控制其重复次数。执行时，`loopcondition` 被求值。如果发现为 TRUE，则逐行执行括号区域，直到再次检查 `loopcondition`。循环只有当条件为 FALSE 时才会终止，并且是立即终止——这意味着括号内执行的操作必须以某种方式导致循环退出，通过影响 `loopcondition` 或打破它，否则会导致无限循环，冻结控制台（取决于括号内指定的运算，R 可能会崩溃）。如果发生这种情况，你可以通过点击用户界面上的停止按钮或按 ESC 键来终止循环。

# 0.3 Exercise

假设你有一个包含矩阵的列表。编写一些代码来计数有多少个矩阵。提示：在开始循环之前设置一个计数器。

a. 出于高效编码考虑，仅使用 `while` 循环重写本节的嵌套循环示例。
b. 在第 10.5 节中，你使用了命令
`switch(Homer=12,Marge=34,Bart=56)`
c. 对以下向量进行测试：
`c("Peter","Lois","Stewie","Maggie")`

无论它是否是 `mylist` 的成员。然后确认以下内容：

i. 如果你有以下内容，答案是 4：
`mylistist <- list(aa=c(3,4),bb=matrix(1:4,2,2),cc=matrix(T,T,T,F,F),3,2),dd="string here",ee=list(c("hello", "you"),matrix(c("hello", "there"))),ff=matrix(c("red","green","blue","yellow")))`

ii. 如果你有以下内容，答案是 0：
`mylistist <- list("tricked you",as.vector(matrix(1:6,3,2)))`

iii. 如果你有以下内容，答案是 2：
`mylistist <- list(list(1,2,3),list(c(3,2),2),list(c(1,2),matrix(1,2))),rbind(1:10,100:91))`

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

传递给 FUN 的操作应与所选择的 MARGIN 匹配。因此，如果你选择了 MARGIN=1 或 MARGIN=2 的行或列，请确保 FUN 函数适用于向量（vectors）。或者或者，如果你有一个三维数组并使用 MARGIN=3 运行 apply，请确保将 FUN 设置为适用于矩阵（matrices）的函数。这里有一个供你输入的示例：

```R
R_bar <- array(1:18,dim=c(3,3,2))

R_bar

, 1

[,1] [,2] [3]

[,1] 1 4 7

[,2] 2 5 8

[,3] 3 6 9

, 2

[,1] [,2] [3]

[,1] 10 13 16

[,2] 11 14 17

[,3] 12 15 18
```

然后，进行如下调用：

```R
R apply(bar,3,FUN=diag)

[,1] 1 10

[,2] 5 14

[,3] 9 18
```

这提取了 bar 中每个矩阵层的对角线元素。对矩阵进行的每次 diag 调用 都会返回一个向量，而这些向量将作为新矩阵的列返回。FUN 参数也可以是任何适当的自定义定义函数，你将在第 11 节中看到一些使用你自己的函数进行 apply 的示例。

# 其他 apply 函数

基础 apply 函数有不同的变体。例如，`tapply` 函数在感兴趣对象的子集上执行操作，这些子集是根据一个或多个因子变量（factor variables）定义的。例如，让我们阅读第 8.2.3 节的代码，该代码读取了一个关于定价的网络数据文件，为数据框设置了变量变量，并显示前五条记录。

```R
R data.url <- "http://www.amstat.org/publications/jse/v9n2/4data.txt"

R diamonds <- read.table(data.url)

R names(diamonds) <- c("Carat","Color","Clarity","Cert","Price")

R diamonds[1:5],
```

## 克重量 颜色 净度 证书 价格

| Carat | Color | Clarity | Cert | Price |
|---|---|---|---|---|
| 1 | 0.30 | D VS2 | GIA | 1302 |
| 2 | 0.30 | E VS1 | GIA | 1510 |
| 3 | 0.30 | G VVS | GIA | 1510 |
| 4 | 0.30 | G VS1 | GIA | 1260 |
| 5 | 0.31 | D VS1 | GIA | 1641 |

要计算整个数据集中所有钻石的总价值，但按颜色分类，你可以这样使用 apply：

```R
R apply(diamonds$Price, INDEX=diamonds$Color,FUN=sum)

 D E F G H I

113598 242349 392485 287702 302866 207001
```

此操作加了目标向量 diamonds$Price 的相关元素。相应的因子向量 diamonds$Color 被传递给 INDEX，感兴趣的函数通过 FUN-sum 正如之前所示指定。
另一个特别有用的替代是 lapply，它可以对列表的每个成员进行操作。在第 10.2.1 节中，我们让你写过一个循环来检查以下列表中的矩阵：

```R
R baz <- list(aa=(3.4,1),bb=matrix(1:4,2),cc=matrix(c(T,T,F,T,F,F),3,2),dd="string here",ee=matrix(c("red","green","blue","yellow")))
```
