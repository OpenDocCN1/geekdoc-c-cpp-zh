

在这些情况下，`switch` 函数的行为与一组堆叠的语句相同，因此它可以作为一种方便的快捷方式。然而，如果你需要同时检查多个条件，或者需要根据此决策执行一组更复杂的操作，你就需要使用显式的 `if` 和 `else` 控制结构。

## 练习 10.2

- a. 编写一组显式的堆叠 `if` 语句，其功能与之前插图的整数版本 `switch` 函数相同。如文中所示，使用 `mynum <- 3` 和 `mynum <- 0` 进行测试。
- b. 假设你被要求在一组假设性实验中计算某种药物的精确剂量。这些剂量取决于一组特定的“剂量阈值”（`lowdose`、`meddose` 和 `highdose`）以及一个名为 `doselevel` 的预设剂量水平向量。查看以下项目（i–v）以了解这些对象的预期形式。然后编写一组嵌套语句，根据以下规则生成一个名为 `dosage` 的新数值向量：
    - 首先，如果 `doselevel` 中存在任何 "High" 的实例，执行以下操作：
    - 检查 `dose` 是否大于或等于 10。如果是，用 10 覆盖 `lowdose`；否则，用 `lowdose` 自身除以 2。
    - 检查 `meddose` 是否大于或等于 26。如果是，用 26 覆盖 `meddose`。
    - 检查 `highdose` 是否小于 60。如果是，用 `highdose` 自身乘以 1.5。
    - 创建一个名为 `dosage` 的向量，其值为 `doselevel` 重复（`rep`）以匹配 `doselevel` 的长度。
    - 使用 `meddose` 覆盖 `dosage` 中对应 `doselevel` 中 "Med" 实例位置的元素。
    - 使用 `highdose` 覆盖 `dosage` 中对应 `doselevel` 中 "High" 实例位置的元素。
    - otherwise（也就是说，如果 `doselevel` 中没有 "High" 实例），执行以下操作：
    - 创建一个新版本的 `doselevel`，这是一个仅包含 "Low" 和 "Med" 水的因子向量，并分别将其标记为 "Small" 和 "Large"（详情参考第 4.3 节或查看 `?factor`）。
    - 检查 `lowdose` 是否小于 15 且 `meddose` 是否小于 35。如果是，用 `lowdose` 自身乘以 2 覆盖 `lowdose`，并用 `meddose` 加上 `highdose` 覆盖 `meddose`。
    - 创建一个名为 `dosage` 的向量，其值为 `lowdose` 重复（`rep`）以匹配 `doselevel` 的长度。
    - 使用 `meddose` 覆盖 `dosage` 中对应 `doselevel` 中 "Large" 实例位置的元素。

现在确认以下内容：

- i. 已知
```R
lowdose <- 12.5
meddose <- 25.3
highdose <- 58.1
doselevel <- factor(c("Low","High","High","Low","Low","Med","Med"),levels=c("Low","Med","High"))
```
运行嵌套语句后 `dosage` 的结果如下：
```
R dosage
d[1] 10.0 60.0 60.0 10.0 25.3 25.3
```

- ii. 使用与 (i) 相同的 `lowdose`、`meddose` 和 `highdose` 阈值，已知
```R
doselevel <- factor(c("Low","Low","Low","Low","Med","Med","Med"),levels=c("Low","Med","High"))
```
运行嵌套 `if` 语句后 `dosage` 的结果如下：
```
R dosage
d[1] 25.0 25.0 25.0 83.4 25.0 83.4
```
此外，`doselevel` 已如下如下覆盖：
```
R doselevel
d[1] Small Small Small Large Large Large
Levels: Small Large
```

- iii. 已知
```R
lowdose <- 9
meddose <- 49
highdose <- 61
doselevel <- factor(c("Low","Med","Med"),levels=c("Low","Med","High"))
```
运行嵌套 `if` 语句后 `dosage` 的结果如下：
```
R> dosage
[1] 9 49 49
```
此外，`doselevel` 已如下覆盖：
```
R> doselevel
[1] Small Large Large
Levels: Small Large
```

- iv. 使用与 (iii) 相同的 `lowdose`、`meddose` 和 `highdose` 阈值，以及与 (i) 相同的 `doselevel`，运行嵌套 `if` 语句后 `dosage` 的结果如下：
```
R> dosage
[1] 4.5 91.5 91.5 4.5 26.0 26.0
```

- v. 假设对象 `mynum` 只可能是 0 到 9 之间的单个整数。使用 `if` 和 `switch` 为 `mynum` 生成匹配的字符字符串，并为所有可能的数值 0, 1, ..., 9 返回匹配的字符串。例如，提供 3，它应该返回“three”；提供 0，应该返回“zero”。

## 10.2 循环编码

另一种编程机制是循环，它会重复一段代码，通常是在递增索引或计数器的情况下。循环有两种类型：`for` 循环在遍历向量元素时重复代码；而 `while` 循环只需重复代码，直到特定条件的评估结果为 `FALSE`。循环行为也可以通过 R 的系列函数来实现。

### 10.2.1 for 循环

`for` 循环始终采用以下形式：
```R
for(loopindex in vector){
  code
}
```
在这里，`loopindex` 是代表向量元素的占位符。当循环开始时，会执行大括号内的代码。当循环到达向量的最后一个元素时，`loopindex` 递增并移动到下一个元素，此时循环退出。这里有一个简单的示例：
```R
counter <- 0
for(myitem in 5:7){
  counter <- counter+1
  cat("the item in run",myitem,\n")
}
```
输出是：
```
the item in run 5
the item in run 6
the item in run 7
```
在这里，我最初定义了一个对象 `counter` 并将其设置为零。你可以使用循环来操作循环外部的对象。

### 10.2.2 通过索引循环

注意使用 `loopindex` 代表向量元素与使用它代表索引之间的区别。以下两个循环使用了两种不同的方法将 `myvec` 中的每个数字翻倍：
```R
myvec <- c(0.4,1,1.34,0.55)
R> for(i in myvec){
  print(2*i)
}
R> for(i in 1:length(myvec)){
  print(2*myvec[i])
}
```
第一个循环使用循环索引 `i` 直接代表 `myvec` 中的元素，打印每个元素乘以2。另一方面，第二个循环使用 `i` 代表序列 `1:length(myvec)` 中的整数。这些索引形成了 `myvec` 的所有位置，你使用这些索引提取 `myvec` 的元素（再次乘以 2 并打印结果）。尽管形式稍长，但使用向量索引在循环使用方面提供了更大的活性。当你需要更复杂的 `for` 循环时，这会更加清晰。

假设你想编写代码来检查任何列表并收集作为列表成员的矩阵对象的信息。考虑以下内容：
```R
foo <- list(aa=c(3,4,1),bb=matrix(1:4,2,2),cc=matrix(c(T,F,T,F,F),3,2),
d="string here",ee=matrix(c("red","green","blue","yellow")))
R> foo
$aa
[1] 3.4 1.0
```

```
$bb
[,1] [,2]
[1] 1 3
[2] 2 4
```

```
$cc
[,1] [,2]
[1] TRUE FALSE
[2] TRUE FALSE
[3] FALSE FALSE
```

