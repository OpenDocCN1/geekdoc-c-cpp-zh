
|---|---|---|---|---|---|

| 120267 | 15 | 15 | 15 | 15 | 60 |

| 120269 | 20 | 20 | 20 | 20 | 80 |

| 120271 | 20 | 20 | 20 | 20 | 80 |

| 120275 | 15 | 15 | 15 | 15 | 60 |

| 120279 | 20 | 20 | 20 | 20 | 80 |

| 120280 | 25 | 25 | 25 | 25 | 100 |

## 5.03 多选题调查

哪个 `SUBSTR` 函数可以从 `Item_Code` 值的中间提取五位数字？

| PDV Item_Code |

|---|---|

| $ 20 978-1-59994-397-8 |

- a. `substr(Item_Code,5,7)`
- b. `substr(Item_Code,5)`
- c. `substr(Item_Code,7,5)`
- d. `substr(Item_Code,'mid',5)`

为了学习目的，输出中包含了 `Acct_Code` 变量，以便方便其与 `ID` 变量进行比较。否则，没有需要它，可以将其从慈善机构数据集中删除。

## 创建慈善机构列表：步骤 1

> `Acct_Code` 值中的最后一个非空字符在不同的观测值位于不同的位置。

| 部分 orion.biz_list | Acct_Code |

|---|---|

| AEK3 | 位于位置 4 的最后一个字符 |

| AQI2 | 位于位置 3 的最后一个字符 |

| ATS1 | |

| CBO3 | |

| CCI2 | |

| ON12 | |

| CS1 | 需要某种方法来确定最后一个字符的位置，以便 `SUBSTR` 函数可以提取它。 |

| CS2 | |

## LENGTH 函数

`LENGTH` 函数返回非空字符字符串的长度，排除末尾空格。

`LENGTH` 函数的一般形式：

```
NewVar=LENGTH(argument);
```

示例：

```
Code='ABCD' ;
Last_NonBlank=length(Code);
```

| Code | Last_NonBlank |

|---|---|

| $6 | N 8 |

| ABCD | 4 |

## 创建慈善机构列表：步骤 1

`LENGTH` 函数是**嵌套**的，或者作为 `SUBSTR` 函数的参数使用。

```sas
data charities;
length ID $ 5;
set orion.biz_list;
if substr(Acct_Code,length(Acct_Code),1)='2';
ID=substr(Acct_Code,1,length(Acct_Code)-1);
run;
```

### 执行：步骤 1

```sas
data charities;
length ID $ 5;
set orion.biz_list;
if substr(Acct_Code,length(Acct_Code),1)='2';
ID=substr(Acct_Code,1,length(Acct_Code)-1);
run;
```

| ID | Acct_Code | Name |

|---|---|---|

| $5 | $6 | $ 30 |

| AQ12 | AQUAMISSIONS INTERNATIONAL |

### 执行：步骤 1

```sas
data charities;
length ID $ 5;
set orion.biz_list;
if substr(Acct_Code,length(Acct_Code),1)='2';
ID=substr(Acct_Code,1,length(Acct_Code)-1);
run;
```

| ID | Acct_Code | Name |

|---|---|---|

| $5 | $6 | $ 30 |

| AQI2 | AQUAMISSIONS INTERNATIONAL |

### 执行：步骤 1

```sas
data charities;
length ID $ 5;
set orion.biz_list;
if substr(Acct_Code,length(Acct_Code),1)='2';
ID=substr(Acct_Code,1,length(Acct_Code)-1);
run;
```

| ID | Acct_Code | Name |

|---|---|---|

| $5 | $6 | $ 30 |

| AQI2 | AQUAMISSIONS INTERNATIONAL |

### 执行：步骤 1

```sas
data charities;
length ID $ 5;
set orion.biz_list;
if substr(Acct_Code,length(Acct_Code),1)='2';
ID=substr(Acct_Code,1,length(Acct_Code)-1);
run;
```

| ID | Acct_Code | Name |

|---|---|---|

| $5 | $6 | $ 30 |

| AQI2 | AQUAMISSIONS INTERNATIONAL |

### 执行：步骤 1

```sas
data charities;
length ID $ 5;
set orion.biz_list;
if substr(Acct_Code,length(Acct_Code),1)='2';
ID=substr(Acct_Code,1,length(Acct_Code)-1);
run;
```

| ID | Acct_Code | Name |

|---|---|---|

| $5 | $6 | $30 |

| AQI2 | AQUAMISSIONS INTERNATIONAL |

### 执行：步骤 1

```sas
data charities;
length ID $ 5;
set orion.biz_list;
if substr(Acct_Code,length(Acct_Code),1)='2';
ID=substr(Acct_Code,1,length(Acct_Code)-1);
run;
```

| ID | Acct_Code | Name |

|---|---|---|

| $5 | $6 | $30 |

| AQI2 | AQUAMISSIONS INTERNATIONAL |

### 执行：步骤 1

```sas
data charities;
length ID $ 5;
set orion.biz_list;
if substr(Acct_Code,length(Acct_Code),1)='2';
ID=substr(Acct_Code,1,length(Acct_Code)-1);
run;
```

| ID | Acct_Code | Name |

|---|---|---|

| $5 | $6 | $30 |

| AQI2 | AQUAMISSIONS INTERNATIONAL |

### 执行：步骤 1

```sas
data charities;
length ID $ 5;
set orion.biz_list;
if substr(Acct_Code,length(Acct_Code),1)='2';
ID=substr(Acct_Code,1,length(Acct_Code)-1);
run;
```

| ID | Acct_Code | Name |

|---|---|---|

| $5 | $6 | $30 |

| AQI2 | AQUAMISSIONS INTERNATIONAL |

### 执行：步骤 1

```sas
data charities;
length ID $ 5;
set orion.biz_list;
if substr(Acct_Code,length(Acct_Code),1)='2';
ID=substr(Acct_Code,1,length(Acct_Code)-1);
run;
```

| ID | Acct_Code | Name |

|---|---|---|

| $5 | $6 | $30 |

| AQI2 | AQUAMISSIONS INTERNATIONAL |

## 5-22 第 5 章 数据转换

a. Orion Star 希望从这些观测值中创建一个仅包含小型零售店的数据集。

- 创建一个新变量 `Country`，其包含 `ID` 的前两个字符。
- 创建一个新变量 `Store_Code`，其包含 `ID` 值中的其他字符。将该值左对齐，以确保没有前导空格。
- `Store_Code` 值中的第一个字符表示商店的大小，其中 `1` 是小型零售店的代码。
- 编写一个程序，仅输出小型零售店的观测值。

提示：你可能需要在子集筛选 `IF` 语句中使用 `SUBSTR` 函数。

- 确保 `City` 值显示为属性大小写格式（如下所示）。

b. 使用适当的标题打印结果。

仅显示 `Store_Code`、`Country`、`City` 和 `Postal_Code` 列。

PROC PRINT output (5 Total Observations)

| Store_Code | Country | City | Postal_Code |

| --- | --- | --- | --- |

| 15301W | AU | Perth | 6002 |

| 12217E | AU | Sydney | 2000 |

| 150 | CA | Toronto | M5V 3C6 |

| 1013CO | US | Denver | 80201 |

| 12CA | US | San Diego | 92139 |

### 挑战

### 3. 将美国邮政编码转换为州名

数据集 `or.contacts` 包含了 Orion Star 运营的美国慈善机构联系人列表。

部分 `or.contacts`

| ID | Title | Name | Address | Address2 |

| --- | --- | --- | --- | --- |

| AQI | Ms. | Farr, Sue | 15 Harvey Rd. | Macon, GA 31298 |

| CCI | Dr. | Cox, Kay B. | 163 McNeil Pl. | Kern, CA 93280 |

| CNI | Mr. | Mason, Ron | 442 Glen Ave | Miami, FL 33054 |

| CS | Ms. | Ruth, G. H. | 2491 Brady St. | Munger, MI 48747 |

| CU | Prof. | Florentino, Helen-Ashe | PO Box 2253 | Washington, DC 20018 |

a. 创建一个名为 `labels` 的新数据集，其中包含变量 `ID` 和 `Name`，以及一个新变量 `Location`，该变量显示联系人所在州的属性大小写全名。

提示：`Address2` 长度为 24 个字符，`Address2` 的最后一项总是邮政编码。

查看在线帮助中以邮政编码作为参数的字符函数。

b. 打印你的结果。

## 5.3 处理字符值（部分 2）

部分 PROC PRINT 输出（12 Total Observations）

| ID | Name | Location |

|---|---|---|

| AQ | Farr, Sue | Georgia |

| CCI | Cox, Kay B. | California |

| CNI | Mason, Ron | Florida |

| CS | Ruth, G. H. | Michigan |

| CU | Florentino, Helen-Ashe H. | District of Columbia |

![](img/d3bde6e6ab06b1fc622215d982111742_196_0.png)

### 目标

- 使用 SAS 函数提取、编辑和搜索字符值。

### 业务场景

创建一个包含适用于创建邮寄标签的数据集。

Ms. Sue Farr

15 Harvey Rd.

Macon, GA 31298

## 部分 orion.contacts

| ID | Title | Name | Address | Address2 |

|---|---|---|---|---|

| AGI | Ms. | Farr Sue | 15 Harvey Rd. | Macon, GA 31298 |

| CCI | Dr. | Cox, Kay B. | 163 McNeil, Pl. | Kern, GA 93280 |

| CNI | Mr. | Mason, Ron | 442 Glen Ave. | Miami, FL 33054 |

| CS | Ms. | Ruth, G. H. | 2491 Brady St. | Munger, MI 48747 |

![](img/d3bde6e6ab06b1fc622215d982111742_197_0.png)

Ms. Sue Farr

15 Harvey Rd.

Macon, GA 31298

## 创建邮寄列表数据

部分 orion.contacts

| Title | Name |

|---|---|

| Ms. | Farr, Sue |

| Dr. | Cox, Kay B. |

| Mr. | Mason, Ron |

| Ms. | Ruth, G. H. |

| Prof. | Florentino, Helen-Ashe H |

| Ms. | Van Alsburg, Jan F. |

| Mr. | Laff, Stanley X. |

| Mr. | Rizen, George G. |

| Dr. | Mitchell, Mer J. |

| Ms. | Webb, Jonathan W. |

| Dr. | Keenan, Maynard J. |

需要完成两个步骤：

- **步骤 1** 将姓与名、中间名分离。
- **步骤 2** 将头衔、名、中间名和姓结合。

## 灵感交流

使用 `SUBSTR` 函数根据逗号的位置将联系人姓名拆分为两部分是否合适？

| Name | |

|---|---|

| Farr | Sue |

| Cox | Kay B. |

![](img/d3bde6e6ab06b1fc622215d982111742_198_0.png)

## SCAN 函数：步骤 1

提取 `Name` 的第二个单词。

```
NewVar=SCAN(string,n,charlist);
```

```
FMName=SCAN(string,n,charlist);
```

| Name | FMName |

|---|---|

| Farr, Sue | Sue |

![](img/d3bde6e6ab06b1fc622215d982111742_198_0.png)

`SCAN` 函数返回字符值的第 n 个单词。当位置未知时，使用 `SCAN` 函数从字符串中提取单词。

默认分隔符如下：

```
ASCII (空格)
EBCDIC (逗号)
```

## SCAN 函数详情

当你使用 `SCAN` 时：

- 如果单词少于 n，则返回缺失值。
- 如果 n 为负数，`SCAN` 函数从字符串末尾选择单词。
- 两个或多个连续分隔符被视为单个分隔符。

## 5.3 多选题

哪个表达式可以完成从 `Text` 中正确提取 `Name`？

```
data test;
a='a - ';
b=' b - ';
c=' c - ';
```

a. `scan(Text,6);`
b. `cat(Text,-6);`
d. 以上均可。（等我重新处理提供的文本）

# 业务场景：数据清理

互联网销售组误用了错误的数据文件用于 Orion Star Catalog 网站。

| Product_ID | Product |

|---|---|

| 21 02 002 00003 | Sunfit Trunks, Blue |

| 21 02 002 00003 | Luci Knit Mittens, Red |

| 21 02 002 00004 | Luci Knit Mittens, Blue |

| 21 02 002 00004 | Sunfit Trunks, Aqua |

| 21 02 002 00005 | Sunfit Trunks, Yellow |

![](img/d3bde6e6ab06b1fc622215d982111742_203_0.png)

### 数据清理：步骤 1

创建正确数据集的第一步是执行以下操作：

- 1. 找到 `Product` 值中包含 `Mittens`（手套）的观测值。
- 2. 修改这些观测值 `Product_ID` 值的中间字符。

| Product_ID | Product |

|---|---|

| 21 02 002 00003 | Luci Knit Mittens, Red |

![](img/d3bde6e6ab06b1fc622215d982111742_203_1.png)

| Product_ID | Product |

|---|---|

| 21 02 005 00003 | Luci Knit Mittens, Red |

### 数据清理：步骤 1

使用 `SUBSTR` 和 `FIND` 函数更改手套的错误的产品 ID。

```
Position=FIND(string,substring<modifiers,startpos);
```
