

```
sex=factor(c("M", "F", "M", "M"),
stringsAsFactors=FALSE)
```

```
R mydata
person age sex
1 Peter 42 M
2 Lois 40 F
3 Meg 17 F
4 Chris 14 M
5 Stewie 1 M
```

```
R mydata$person
[1] "Peter" "Lois" "Meg" "Chris" "Stewie"
```

你现在已将 person 转换成了所需的形式，即非因子形式。

## 5.2.2 添加数据列并合并数据框

假设你想向现有数据框添加内容。这可能是一组新变量的观测值（增加列数），也可能是更多记录（增加行数）。同样，你可以使用之前已应用于矩阵的某些函数。

回顾第 3.1.2 节中的 rbind 和 cbind 函数，它们分别用于追加行和列。这些相同的函数也可以直观地用于扩展数据框。例如，假设你想在 mydata 中加入另一条记录：另一个个体 Brian 的年龄和性别。第一步是创建一个包含 Brian 信息的新数据框。

```
R newrecord <- data.frame(person="Brian", age=7,
sex=factor("M",levels=levels(mydata$sex)))
```

```
R newrecord
person age sex
1 Brian 7 M
```

为避免混淆，确保变量名和你计划添加到的该数据框一致。注意，对于因子，你可以使用 levels 提取现有因子变量的水平。
现在，你可以简单地调用以下命令：

```
R mydata <- rbind(mydata,newrecord)
R mydata
person age sex
1 Peter 42 M
2 Lois 40 F
3 Meg 17 F
4 Chris 14 M
5 Stewie 1 M
6 Brian 7 M
```

使用 rbind，你将 mydata 与新记录合并并用结果覆盖 mydata。

向数据框添加变量也非常简单。假设你现在获得了这六个个体搞笑程度分类的数据，定义为“搞笑程度”。搞笑程度可以取三个可能值：Low、低、Med（中等）和 High。假设 Peter、Lois 和 Stewie 的搞笑程度为高，Chris 和 Brian 的搞笑程度为中等，Meg 的搞笑程度为低。在 R 中，你会有这样的因子：

```
R funny <- c("High","Low","Low","Med","High","Med")
R funny <- factor(funny)
[1] High Low Med High Med
Levels: Low Med High
```

第一行创建了作为 funny 的基本字符向量，第二行通过将其转换为因子来覆盖 funny。这些元素的顺序必须与数据框中的记录相对应。现在，你可以使用 cbind 将此因子向量作为列追加到现有的 mydata。

R mydata <- cbind(mydata, funny)
R mydata

person age sex funny
1 Peter 42 M High
2 Lois 40 F High
3 Meg 17 F Low
4 Chris 14 M Med
5 Stewie 1 M High
6 Brian 7 M Med

rbind 和 cbind 函数并不是扩展数据框的唯一方法。添加变量的一种替代方法是使用数据运算符，类似于向命名列表添加新成员，如第 5.1.3 节所述。假设你想通过添加一列个体年龄（以月为单位，而非年）来向 mydata 添加另一个变量，将此新变量命名为 age.mon。

```
R mydata$age.mon <- mydata$age*12
R mydata
```

person age sex funny age.mon
1 Peter 42 M High 504
2 Lois 40 F High 480
3 Meg 17 F Low 204
4 Chris 14 M Med 168
5 Stewie 1 M High 12
6 Brian 7 M Med 84

这使用美元运算符创建了一个新的 age.mon 列，同时将年龄（以年为单位）向量乘以 12 并分配给它。

## 5.2.3 逻辑记录子集

在第 4.1 节中，你看到了如何使用逻辑标志标志来子集数据结构。这在处理数据框时特别有用，因为你经常想要检查满足某些条件的条目子集。例如，在临床药物试验的数据工作中，研究人员可能只想检查男性参与者的结果并将其与女性进行比较。研究人员可能还想查看对药物反应最积极的个体的特征。

让我们继续使用数据。假设你想检查所有与男性对应的记录。从第 4.3.1 节你知道以下行将标识 sex 向量中的相关位置：

```
R mydata$sex=="M"
[1] TRUE FALSE TRUE TRUE
```

这标记了男性记录。你可以使用第 5.2.1 节中看到的类似矩阵的语法来获取仅男性子集。

```
R mydata[mydata$sex=="M",]
 age funny age.mon
1 Peter 42 High 504
4 Chris 14 Med 168
5 Stewie 1 M High 12
6 Brian 7 M Med 84
```

这返回了所有变量中仅男性参与者的数据。你可以使用相同的行为来挑选和选择子集中返回的变量。例如，由于你知道只选择了男性，你可以使用列维度的负数值索引从结果中省略 sex。

```
R mydata[mydata$sex=="M",-3]
 age funny age.mon
1 Peter 42 High 504
4 Chris 14 Med 168
5 Stewie 1 High 12
6 Brian 7 Med 84
```

如果你不知道列号或想要控制返回的列，可以改用变量名的字符向量。

```
R> mydata[mydata$sex=="M",c("person","age","funny","age.mon")]
person age funny age.mon
1 Peter 42 High 504
4 Chris 14 Med 168
5 Stewie 1 High 12
6 Brian 7 Med 84
```

你用来子集数据框的逻辑条件可以简单或复杂，视需要而定。你在方括号中使用的逻辑标志向量必须与数据框中的记录数匹配。让我们提取年龄超过 10 岁 或 具有高健身程度 的个体的完整记录。

```
R> mydata[mydata$age>10 | mydata$funny=="High",]
person age funny age.mon
1 Peter 42 High 504
2 Lois 40 F 480
3 Meg 17 F 204
4 Chris 14 M 168
5 Stewie 1 M 12
```

有时，请求子集会产生零条记录。在这种情况下，R 返回一个零行的数据框，看起来像这样：

```
R> mydata[age>45]
[1] person age sex funny age.mon
<0 rows (or 0-length row.names)
```

在此示例中，没有从 mydata 返回记录，因为没有个体年龄超过 45。要检查子集是否包含任何记录，可以使用结果上的 nrow——如果它等于零，则没有记录满足指定的条件。

# 练习 5.2

a. 在你的 R 工作区中创建并存储此数据框作为 dfame：

| person | sex | funny |
|---|---|---|
| Stan | M | High |
| Francine | F | Med |
| Steve | M | Low |
| Roger | M | High |
| Hayley | F | Med |
| Klaus | M | Med |

变量 person、sex 和 funny 应与第 5.2 节中研究的 mydata 对象中的变量在性质上相同。也就是说，person 应为字符向量，sex 应为因子，其水平为 f 和 M，funny 应为因子，其水平为 Low、Med 和 High。

b. Stan 和 Francine 年龄为 41 岁，Steve 为 15 岁，Hayley 为 21 岁，Kaus 为 60 岁。Roger 极其年长——1,600 岁。将这些数据作为数值列变量追加到 dataframe age 中。

c. 使用你对基于列索引位置重新排序变量的知识来覆盖 dataframe 中的 mydata。也就是说，第一列应为 person，第二列，第三列，第四列为 funny。

d. 将注意力转向在第 5.2.2 节中加入 age.mon 变量后 mydata 的状态。通过删除 age.mon 列创建 mydata 的新版本，命名为 mydata2。

e. 现在，将 mydata2 与 dataframe 合并，将 resulting 对象命名为 dataframe。

f. 编写一行代码，从 mydataframe 中提取个体为女性且公平程度等级等于 Med 或 的记录的名称和年龄。

g. 使用你对 R 中处理字符字符串的知识，从 mydataframe 中提取所有名称以 S 开头的记录。提示：回忆第 4.2.4 节中的 substr（注意 substr 可以应用于多个字符字符串的向量）。

# 本章重要代码

| Function/operator | Brief description | First occurrence |
|---|---|---|
| list | Create a list | Section 5.1.1, p. 89 |
| [[ ]] | Unnamed member reference | Section 5.1.1, p. 90 |
| [ ] | List slicing (multiple members) | Section 5.1.1, p. 91 |
| $ | Get named member/variable | Section 5.1.2, p. 92 |
| data.frame | Create a data frame | Section 5.2.1, p. 96 |
| [, ] | Extract data frame row/columns | Section 5.2.1, p. 96 |

