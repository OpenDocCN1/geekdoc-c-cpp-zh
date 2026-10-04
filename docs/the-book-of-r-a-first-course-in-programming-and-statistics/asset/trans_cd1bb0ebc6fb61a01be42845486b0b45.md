

R> cat("here is a string\nsplit\to neww\b\n\ntlines")
here a string
split      to new

lines

R> cat("I really want a backslash: \\\and a double quote: \"")
I really want a backslash: \\
and double quote: ""

这些转义序列意味着在 R 中你不能使用单独的反斜杠作为文件路径。如第 1.2.3 节所述（在该节中你使用 getwd 打印当前工作目录并使用 setwd 更改它），文件夹分隔必须使用正斜杠 / 而不是反斜杠。

R> setwd("/folder1/folder2/folder3")

文件规范在读写文件时出现，你将在第 8 章中探索。

## 4.2.4 子字符串和匹配

模式匹配让你能够检查给定的字符串以识别其中的较小字符串。
函数 substr 接受一个字符串 x 并提取字符串中介于两个字符位置（包含）之间的部分，由作为 start 和 stop 参数传递的数字指示。让我们在第 4.2.1 节的对象 foo 上尝试它。

R> foo <- "This is a character string!"
R> substr(x=foo,start=21,stop=27)
[1] "string!"

这里，你提取了位置 21 到 27 之间的字符，包含两端，得到了 "string!"。函数 substr 也可与赋值运算符一起使用以替换为新的字符集。在这种情况下，替换字符串应包含与所选区域相同数量的字符。

R> substr(x=foo,start=1,stop=4) <- "Here"
R> foo
[1] "Here is a character string!"

如果替换字符串比 start 和 stop 指示的字符数长，替换仍然会进行，从 start 开始到 stop 结束。它会截断超出要替换字符数的部分。如果字符串比要替换的字符数短，替换会在字符串完全插入时结束，原始字符保持不变。

使用函数 sub 和 gsub 进行替换更灵活。sub 函数在其中搜索包含的较小字符串模式。它用作为参数给出的新字符串替换第一个实例。gsub 函数做同样的事情，但它替换模式的每个实例。以下是一个示例：

R> bar <- "How much wood could a woodchuck chuck"
R> sub(pattern="chuck",replacement="hurl",x=bar)
[1] "How much wood would a woodlurl chuck"
R> gsub(pattern="chuck",replacement="hurl",x=bar)
[1] "How much wood would a woodlurl hurl"

对于 sub，替换值不必与被替换的模式具有相同数量的字符。这些函数还具有诸如大小写敏感性之类的搜索选项。帮助文件 ?substr 和 ?sub 有更多详细信息，并指出一些其他模式匹配函数和技术。你可能还想查看 grep 命令及其变体；请参阅相关帮助文件 ?grep。

## 练习 4.4

a. 精确重现以下输出：
"The quick brown fox
jumped over
the lazy dogs"
b. 假设你存储了值 num1 <- 4 和 num2 <- 0.75。写一行 R 代码返回以下字符串：
[1] "The result of multiplying 4 by 0.75 is 3"
确保你的代码对存储为 num1 和 num2 的任意两个数字都能产生正确的乘法结果字符串。
c. 在我的本地机器上，本书工作的目录在 R 中指定为 "/Users/tdavis/Documents/RBook/"。想象一下你的机器——写一行代码将此字符串中的 tdavis 替换为你的名字首字母和姓氏。

+   d. 在第 4.2.4 节中，你存储了以下字符串：
  R> bar <- "How much wood could a woodchuck chuck"
  i. 通过将单词 "if a woodchuck could chuck wood" 粘贴到 bar 上存储一个新字符串。
  ii. 在 (i) 的结果中，将所有 wood 实例替换为 metal。
e. 存储字符串 "Two 6-packs for $12.99"。然后执行以下操作：
  i. 使用相等性检查确认从第 5 个字符开始到第 10 个字符结束的子字符串是 "6-pack"。
  ii. 通过将价格更改为 $10.99 使其成为更好的交易。

## 4.3 因子

在本节中，你将查看一些与创建、处理和检查因子相关的简单函数。因子是 R 表示数据点仅适合有限数量不同类别之一而不是属于连续体时最自然的方式。这种分类数据在数据科学中可以发挥重要作用，你将在第 13 章中从统计角度更详细地查看因子。

### 4.3.1 识别类别

为了了解因子如何工作，让我们从一个简单的数据集开始。假设你找到八个人并记录他们的名字、性别和出生月份，如表 4-4 所示。

表 4-4：八个个体的示例数据集

| Person | Sex | Month of birth |
|---|---|---|
| Liz | Female | April |
| Jolene | Female | January |
| Susan | Female | December |
| Boris | Male | September |
| Rochelle | Female | November |
| Tim | Male | July |
| Simon | Male | July |
| Amy | Female | June |

在 R 中表示每个人的名字几乎只有一种合理的方式——作为字符字符串的向量。

R> firstname <- c("Liz", "Jolene", "Susan", "Boris", "Rochelle", "Tim", "Simon", "Amy")

记录性别时你有更多灵活性。将女性编码为 0，男性编码为 1，数值选项如下：

R> sex.num <- c(0,0,0,1,0,1,1,0)

当然，字符字符串也是可能的，许多人更喜欢这种方式，因为你不需要记住每个组的数字代码。

R> sex.char <- c("female", "female", "female", "male", "female", "male", "male", "female")

然而，个体的名字与其性别作为数据存储之间存在根本区别。一个人名字是唯一标识符，可以取无限多种可能性，而记录一个人的性别通常只有两个选项。这种数据，其中所有可能的值都落入有限数量的类别中，最好使用因子表示。

因子通常从数值或字符向量创建（注意你不能使用因子值填充矩阵或多维数组；因子只能以向量的形式存在）。要创建因子，使用函数 factor，如使用 sex.num 和 sex.char 的示例所示：

R> sex.num.fac <- factor(x=sex.num)
R> sex.num.fac
[1] 0 0 0 1 0 1 1 0
Levels: 0 1
R> sex.char.fac <- factor(x=sex.char)
R> sex.char.fac
[1] female female female male female male male
Levels: female male

这里，你获得了存储性别值的两个向量的因子版本。乍一看，这些对象与它们创建的字符和数值向量并没有太大不同。事实上，因子对象与向量以相同的方式工作，但附带了一些额外的信息（R 对因子对象的内部表示也略有不同）。例如，length 和 which 等函数与向量一样工作。

因子对象包含的最重要的额外信息（或属性；参见第 6.2.1 节）是其 levels，它存储因子中的可能值。这些 levels 打印在每个因子向量的底部。你可以使用 levels 函数将其作为字符字符串的向量提取。

R> levels(x=sex.num.fac)
[1] "0" "1"
R> levels(x=sex.char.fac)
[1] "female" "male"

你可以使用 levels 重新标记因子。以下是一个示例：

R> levels(x=sex.num.fac) <- c("1","2")
R> sex.num.fac
[1] 1 1 1 1 2 2 1
Levels: 1 2

这将女性标记为 1，男性标记为 2。
因子值向量以与任何其他向量相同的方式进行子集化。

R> sex.char.fac[2:5]
[1] female male female female
Levels: female male
R> sex.char.fac[c(1:3,5,8)]
[1] female female female female
Levels: female male

注意，对因子对象进行子集化后，对象仍保留所有已定义的 levels，即使某些 levels 在子集化对象中不再表示。

如果你想使用逻辑标志向量从因子中进行子集化，请记住因子的 levels 存储为字符字符串，即使原始数据向量是数值，也需要使用字符串请求或测试特定 level。例如，要使用重新标记的 sex.num.fac 识别所有男性，使用以下方法：

R> sex.num.fac=="2"
[1] FALSE FALSE FALSE TRUE FALSE TRUE

由于 firstname 和 sex 在其因子向量中有对应位置，你可以使用此逻辑向量获取所有男性的名字（使用 "male"/"female" 因子向量时）。

R> firstname[sex.char.fac=="male"]
[1] "Boris" "Tim" "Simon"

当然，这种简单的子集化也可以用原始数值向量 sex.num 或原始字符向量 sex.char 以相同的方式实现。在下一节中，你将探索在 R 中将分类数据表示为因子所具有的更独特的优势。

