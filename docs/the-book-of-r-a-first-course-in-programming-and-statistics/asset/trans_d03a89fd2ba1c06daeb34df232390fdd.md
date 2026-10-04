
同时，如果你将一个函数传递给 `try` 且它没有抛出错误，那么 `try` 就不起作用，你只会得到正常的返回值。

```
R> attempt2 <- try(myfibrec2(6),silent=TRUE)
R> attempt2
[1] 8
```

在这里，你使用有效参数 `n=6` 执行了 `myfibrec2`。由于这次调用没有导致错误，传递给 `attempt2` 的结果是 `myfibrec2` 的正常返回值，在本例情况下为 8。

# 在函数体中使用 try

让我们来看一个更完整的示例，展示如何在较大的函数中使用 `try`。后续的 `myfibvector` 函数接收一个索引向量作为参数 `nvec`，并提供斐波那契序列中对应的项：

```
myfibvector <- function(nvec)
nterms <- length(nvec)
result <- rep(0,nterms)
for(i in 1:nterms){
  result[i] <- myfibrec2(nvec[i])
}
return(result)
```

该函数使用 `for` 循环逐个处理 `nvec` 元素，并使用之前的函数 `myfibrec2` 计算对应的斐波那契数。只要 `nvec` 中的所有值都不为零，`myfibvector` 就能正常工作。例如，以下调用获取了第一、第二、第十和第八个斐波那契数：

```
R> foo <- myfibvector(nvec=c(1,2,10,8))
R> foo
[1] 1 55 21
```

假设由于错误，`nvec` 中的其中一项为零。

```
R> bar <- myfibvector(nvec=c(3,2,7,0,9,13))
Error in myfibrec2(nvec[1]) : 'n' is uninterpretable at 0
```

当在 `n=0` 时调用内部的 `myfibrec`，它抛出了错误，这终止了 `myfibvector` 的执行。没有返回任何内容，整个调用失败了。

你可以通过在循环中使用 `try` 来完全防止这种情况，检查每次对 `myfibrec` 的调用并捕获任何错误。后续的函数 `myfibvectorTRY` 正是这样做。

```
myfibvectorTRY <- function(nvec){
  nterms <- length(nvec)
  result <- rep(0,nterms)
  for(i in 1:nterms) {
    attempt <- try(myfibrec2(nvec[i]),silent=T)
    if(class(attempt)==="try-error"){
      result[i] <- NA
    } else {
      result[i] <- attempt
    }
  }
  return(result)
}
```

在这里，在 `for` 循环内部，使用 `attempt` 来存储每次调用 `myfibrec2` 的结果。然后，检查 `attempt`。如果该对象的类是 "try-error"，说明 `myfibrec2` 产生了错误，你在结果向量的相应槽位中填充 `NA`。否则，`attempt` 将代表来自 `myfibrec2` 的有效值，因此将其放入结果向量的相应槽位。现在，如果你在相同的 `nvec` 上导入并调用 `myfibvectorTRY`，你会看到一组完整的结果。

```
R baz <- myfibvectorTRY(nvec=c(3,2,7,0,9,13))
R baz
[1] 2 1 13 NA 34 233
```

> 原本会终止一切的错误被静默捕获，在这种情况下，替代响应 NA 被插入到结果向量中。

注意：该命令是 R 更复杂的 `tryCatch` 函数的简化版，这超出了本书的涉及范围，但它对如何测试和执行代码块提供了更精确的控制。如果你感兴趣并了解更多信息，请输入 `?tryCatch`。

## 抑制警告消息

在我显示的所有调用中，我将 `silent` 参数设置为 `TRUE`，这会停止任何错误消息。如果你将 `silent` 留为 `FALSE`（默认值），错误消息将被打印，但不会终止执行。`silent=TRUE` 仅抑制错误，而不是警告。观察以下：

```
R> attempt3 <- try(myfibrec2(-3),silent=TRUE)
Warning message: In myfibrec2(-3) : Assuming you meant 'n' to be positive -- doing that instead
R> attempt3
[1] 2
```

尽管设置了 `silent TRUE`，警告（针对负值 `n`）仍然被发出了。在这种情况下，警告与错误分开处理，因为它们突显了代码执行过程中未预见的问题。

```
R> attempt4 <- suppressWarnings(myfibrec2(-3))
R> attempt4
[1] 2
```

`suppressWarnings` 函数只有在你确定调用中的每个元素都可以安全忽略并且希望保持输出整洁时才使用。

# 练习 12.1

- a. 在练习11.3 (b) 第238页中，你的任务是编写一个递归R函数来计算给定非负整数 `x` 的阶乘。现在修改你的函数，如果 `x` 为负，则抛出一个相应的错误。使用以下内容测试你的函数：
  - i. x为5
  - ii. x为8
  - iii. x为8
- b. 矩阵逆的想法在第3.6节中简要讨论过，对于方矩阵（行数等于列数的矩阵）是可能的。这些逆可以使用 `solve` 函数计算，例如：

```
R> solve(matrix(1:4,2,2))
     [,2]
[1,]    2 -1
[2,] -1  0.5
```

注意，如果矩阵无法逆会抛出一个错误。基于此，编写一个R函数尝试逆列表中的每个矩阵，遵循以下指南：
- 函数应接收四个参数：
- 待测试逆的列表 `x`
- 当 `x` 的某个成员无法逆时填充的值，默认为 `NA`
- 字符字符串 `mat`，当 `x` 的某个成员不是矩阵时的结果，默认为 "not a matrix"
- 布尔值 `silent`，默认为 `TRUE`，传递给体内的 `try`
- 函数首先应该检查 `x` 是否为列表。如果不是，应抛出一个相应的错误。
- 然后，函数应该确保 `x` 至少有一个成员。如果不是，应抛出一个相应的错误。
- 接下来，函数应该检查 `mat` 是否为字符字符串。如果不是，使用相应的 `as.character`（见第6.2节）将其转换为字符字符串，并应发出相应的警告。
- 在这些检查之后，循环应该搜索 `x` 的每个成员。
- 如果 `i` 是矩阵，尝试对其逆。如果没有错误即可逆，则用结果覆盖成员 `x`。如果捕获到错误，则用值 `NA` 覆盖成员 `x`。
- 如果 `i` 不是矩阵，则用值 `mat` 覆盖成员 `x`。
- 最后，应返回修改后的列表 `x`。

现在，使用以下参数测试你的函数：
- i. x为
```
list(1:4,matrix(1:4,1,4),matrix(1:4,4),matrix(1:4,2,2))
```
其他参数使用默认。
- ii. x为 Inf，mat为 Inf，silent为默认。
- iii. 重复 (ii)，但现在 `silent=FALSE`。
- iv. x为
```
list(diag(9),matrix(c(0,2,0.4,0.2,0.1,2),3,3),cbind(c(5,1,5,2),c(2,2,1,8)),as.vector(diag(2)))
```
mat为 "unsuitable matrix"；其他值使用默认。

最后，通过以下内容调用你的函数来测试错误消息：
- v. x为 "hello"
- vi. x为 list()

# 12.2 进度与计时

R 通常用于长期的数值练习，例如模拟或随机变量生成。对于这些复杂的、耗时的操作，跟踪进度或查看完成某项任务需要多久通常很有有用。例如，你可能想比较解决问题的两种不同编程方法的速度。在本节中，你将查看为代码执行计时并显示进度的方法。

## 12.2.1 文本进度条：我们到了吗？

进度条显示了 R 在执行一组操作时进展了多远。要显示这一点，你需要运行执行需要时间的代码，这将通过让 R 来实现。`Sys.sleep` 命令让 R 暂停指定的时间（秒为单位），然后继续。

```
Sys.sleep(3)
```

如果你运行这段代码，R 将暂停三秒才能继续执行代码。在本节中，睡眠将用作计算密集型操作引起延迟的替代方案，而这正是进度条最有用的地方。

要以更常见的方式使用 `Sys.sleep`，请考虑以下：

```
sleep_test <- function(n){
  result <- 0
  for(i in 1:n){
    result <- result + 1
    Sys.sleep(0.5)
  }
  return(result)
}
```

`sleep_test` 函数非常基础——它接收一个正整数 `n`，并在 n 次迭代中为结果值加1。在每次迭代中，你还告诉循环睡眠半秒。因为该睡眠命令，执行以下代码大约需要四秒返回结果：

```
sleep_test(8)
[1] 8
```

现在，假设你想跟踪这类函数在执行时的进度。你通过三个步骤实现：使用 `txtProgressBar` 初始化进度条对象，使用 `txtProgressBar` 更新进度条，以及使用 `close` 终止进度条。下一个函数 `prog_test` 修改了 `sleep_test` 以包含这三个命令。

