
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

基础 apply 函数有不同的变体。例如，tapply 函数在感兴趣对象的子集上执行操作，这些子集是根据一个或多个因子变量（factor variables）定义的。例如，让我们阅读第 8.2.3 节的代码，该代码读取了一个关于定价的网络数据文件，为数据框设置了变量变量，并显示前五条记录。

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

使用 lapply，你可以用一行简短的代码检查列表中的矩阵。

```R
R lapply(baz,FUN=is.matrix)
$aa
[1] FALSE
$bb
[1] TRUE
$cc
[1] TRUE
$dd
[1] FALSE
$ee
[1] TRUE
```

注意，lapply 不需要 margin 或 index 信息：R 知道要将 FUN 应用于指定列表的每个成员。返回的值本身是一个列表。另一个变体 sapply 返回了与 apply 相同的结果，但以数组的形式呈现。

```R
R> apply(baz,FUN=is.matrix)
aa  bb cc dd ee
FALSE TRUE TRUE FALSE TRUE
```

在这里，结果以向量的形式提供。在这个示例中，baz 有名称属性，该属性被复制到返回对象的相应条。

apply 的其他变体包括 vapply（它与 sapply 类似，尽管有一些细微的差别）以及 mapply（它可以同时操作多个向量或列表）。要了解更多关于 mapply 的信息，请查看 ?maapply 帮助文件；vapply 和 sapply 都在 ?apply 帮助文件中。

所有的 apply 函数都允许向 FUN 传递额外的参数；它们大部分通过省略号（ellipsis）传递。例如，再次查看该矩阵：

```R
R> apply(foo,1,sort,decreasing=TRUE)
[1] [2] [3] [4]
[1,] 9 10 11 12
[2,] 5 6 7 8
[3,] 1 2 3 4
```

在这里，你对矩阵的每一行应用了 sort，并提供了额外的参数 decreasing=TRUE 来从大到小排序行。

有些程序员喜欢尽可能使用 apply 函数族来提高代码的紧凑性和整洁性。但请注意，这些函数在计算速度或效率方面通常没有比显式循环提供任何实质改进（在较新版本的 R 中特别是如此）。此外，当你开始学习 R 语言时，显式循环更容易阅读和理解，因为操作是按行清晰排列的。

# 练习 10.5

- a. 延续文本中最后的示例，编写一个隐式循环，计算 apply(foo,1,sort,decreasing=TRUE) 返回的矩阵所有列的乘积。

- b. 将以下循环转换为执行相同操作的隐式循环：
`matlist <- list(matrix(c(T,F,T,T),2,2)),`
`matlist(matrix(c("a","c","b","z","p","q"),3,2)),`
`matlist(1:8,2,4))`
`for(i in 1:length(matlist)){`
`matlist[[i]] <- t(matlist[[i]])`

- c. 在 R 中存储以下 asx：
`R> qux <- array(96:1,dim=c(4,4,2))`
  - i. 编写一个隐式循环以获取所有层的对角线元素。
  - ii. 编写一个隐式循环以返回每一层的第四列。

# 10.3 其他流机制

通常，for 循环只有在索引耗尽时才会退出，while 循环只有在条件求为 FALSE 时才会退出。但你也可以通过声明提前终止循环。

### 10.3.1 使用 break

例如，假设有一个数字 foo，你想对元素进行除法。此外，假设你想对 element 进行除法，但如果其中一个结果为 Inf 则停止执行（这在除以零时会发生）。为了做到，你可以用 is.finite 函数（第 6.1 节）检查每次迭代，并可以发布 break 命令来终止循环。

```R
R loop1.result <- rep(NA,length(bar))
R loop1.result
[1] NA NA NA NA
R+ for(i in 1:length(bar)){
   temp <- foo/bar[i]
   if(is.finite(temp)){
     loop1.result[i] <- temp
   } else {
     break
   }
}
R loop1.result
[1] 2.500000 1.666667 4.545455 1.250000
```

### 10.3.2 next

与其 break 并完全结束循环，你可以使用 next 跳到下一次迭代并继续执行。考虑以下情况，使用 next 避免了除零：

```R
R loop2.result <- rep(NA,length(bar))
R loop2.result
[1] NA NA NA NA
R+ for(i in 1:length(bar)){
   if(bar[i]==0){
     next
   }
   loop2.result[i] <- foo/bar[i]
}
R loop2.result
[1] 2.500000 1.666667 4.545455 1.250000
```
