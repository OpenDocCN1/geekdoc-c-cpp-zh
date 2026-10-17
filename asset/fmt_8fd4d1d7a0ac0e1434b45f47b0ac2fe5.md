
Freedman

Xriedman

Friedman

Friedmann

Alfred

FRIEDMAN

;

以下是数据集 Fuzzy 的数据列表：

图 12.17：数据集 Fuzzy 的列出

| Name | Value |
|---|---|
| Friedman | 0 |
| Freedman | 12 |
| Xriedman | 25 |
| Friedman | 6 |
| Friedmann | 3 |
| Alfred | 100 |
| FRIEDMAN | 87 |

如果两个参数完全匹配，`SPEDIS` 函数返回 0。该函数为每种类型的拼写错误分配惩罚分。例如，写错第一个字母的分数比写错其他字母多。交换两个字母是一个较小的错误，在单词中增加一个字母也是如此。

一旦计算出总惩罚分，得到的值是相对于第一个参数长度的百分比。这是很有道理的，因为在一个 3 个字母的单词中写错一个字母比在一个 10 个字母的单词中写错一个字母要严重得多。

注意，`SPEDIS` 函数评估的两个字符值是区分大小写的（请查看列表中的观察结果）。如果大小写可能是问题，在用 `SPEDIS` 测试名称之前，请使用 `UPPERCASE`、`PROPCASE` 或 `VALUE` 函数。

要识别任何与 Friedman 相似的名称，你可以提取所有 `SPEDIS` 函数返回的值小于某个预定值的名称。在本文的程序中，小于 15 或 20 的值将识别出该名字的一些合理拼写错误。

## 12.16 替换字符串或单词

本章中的两个函数是 `TRANSL` 和 `TRANWRD`。`TRANSL` 允许你用一个字符值替换另一个。`TRANWRD` 允许你用一个单词替换另一个（因此名为 translate word——`TRANWRD`）。

在第一个示例中，你想用字符值 A, B, C, D 和 E 替换字符值 1, 2, 3, 4 和 5。

### 程序 12.16：演示 TRANSLATE 函数

```sas
data Trans;

  input Answer : $5;

  Answer = translate(Answer,'ABCDE','12345');

datalines;

14325

AB123

51492

;
```

生成的数据集 `Trans` 包含以下三个观测：

图 12.18：数据集 Trans 的列出

| Listing of Data Set Trans |
| Answer |
| ABCDE |
| ABABC |
| EAD9B |

值 1–5 被 A–E 替换。任何其他字符都不会改变。`translate` 函数接受三个参数：第一个参数是你想要更改的字符字符串；第二个和第三个参数是目标字符串（to-string）和源字符串（from-string）。目标字符串中的每个字符都会替换源字符串中对应的字符。在上面的程序中，1 变成 A，2 变成 B，依此类推。

本章的最后一个函数（万岁！）是 `TRANWRD`。此函数允许你用一个单词替换另一个。

该函数通常用于标准化地址（将 Street 改为 St.，将 Road 改为 Rd. 等）。这里有一个例子：

### 程序 12.17：使用 TRANWRD 函数标准化地址

```sas
data Address;

input Name $30 Line $40 City $20 State $5;

Line = tranwd(Line, 'Street', 'St.');

Line = tranwd(Line, 'Road', 'Rd.');

Line = tranwd(Line, 'Avenue', 'Ave.');

datalines;

Dr. Peter Benchley 123 Street Oceanside NY 1518

Mr. Robert Merrill 878 Road Long Beach CA 9018

Mrs. Laura Smith 80 Avenue NJ 0822
```
