

```r
n1 <- sum(is.na(A[, i]))
n2 <- sum(is.na(A[, j]))
m1 <- mean(A[, i], na.rm = TRUE)
v1 <- var(A[, i], na.rm = TRUE)
m2 <- mean(A[, j], na.rm = TRUE)
s2 <- var(A[, j], na.rm = TRUE)
n <- n1 + n2 - 
sdFactor <- sqrt((n1-1) + (n2-1))
spooled <- sqrt((n1-1)*s1 + (n2-1)*s2)/n
mDiff <- m1 - m2
B[count] <- mDiff/(pooled*sdFactor)
count <- count + 1
```

将 `meanComp` 应用于 5.2 节讨论的 `group2.txt` 文件数据，其输出结果表明第四个样本的父级“总体”均值与其他三个样本均值之间存在显著差异。

```r
> A <- as.matrix(read.table("group2.txt",
  na.string = c("n", "q", "NA")))
> meanComp(A)
```

[1] 0.592930 0.550235 -1.739142 -0.2231317 -1.760245 -2.168691

打印 `meanComp` 输出时使用的格式是本示例所用安装版本的默认设置。这对于我们的目的以及其他地方已经足够了。可以通过 R 函数 `formatC`、`prettyNum` 和 `sprintf` 来控制格式。

上一个示例可以使用附录 B 中的 R `apply` 函数以及下一个示例进行更直接的编码。有许多预存在方法可以执行均值计算，这些方法是 R 原生的，或者通过下载 `multcomp` 包来实现。`TukeyHHSD` 函数（在初始 R 安装附带的 R 基础包中可用）使用“诚实差异”（Honest Difference）方法进行均值比较。它可以与例如执行方差分析的 R 函数返回的对象配合。

R 语言拥有一种异常或条件机制，与第 3.8.7 节讨论的 C++ 版本有些相似。关于此主题的 R 帮助页面提供了信息来源，而 Gentleman (2009) 的著作则对该主题提供了易于理解的介绍。

异常管理设施的最简单入口是 `tryCatch` 函数。R 中的异常/条件以消息（message）、警告（warning）和错误（error）对象的形式出现。这些是类实例提供了有关程序执行过程中发生的条件的信息。在最简单的形式下，`tryCatch` 函数由一个要评估的表达式和一个或多个处理器函数组成，这些函数定义了当特定条件发生时要采取的一个或多个操作。如果评估表达式没有产生条件，则返回评估结果。否则，将进行搜索以找到匹配条件的处理器。

错误可能发生的一个地方是数据输入。这些可能表现为 R 会话中的错误（练习 5.5）或可能是错误的文件名。例如，下面的摘录显示了尝试读取 5.1 节中的 `group1.txt` 文件失败的结果。

# 编写 R 函数

```r
> scan(grop1.txt, quiet = TRUE)
Error in file(file, "r") : cannot open the connection
Addition: Warning message:
In file(file, "r") :
cannot open file "grop1.txt": No such file or directory
```

由于我们的拼写错误，生成了警告和错误对象。可以使用 `tryCatch` 函数通过“捕捉”这两个条件之一并建立适当的修复来减少这种情况。下面给出了实现此点的函数：

```r
readFile <- function(fileName) {
  out <- tryCatch(suppressWarnings(scan(fileName)),
    error = function(e) {
      print("Please enter a valid filename")
      return(NULL)
    },
    warning = function(w) {
      print("A warning occurred")
      return(NULL)
    ))
  return(out)
}

# > readFile("grop1.txt")
[1] "Please enter a valid filename"
```

