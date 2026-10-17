
![](img/e9e15d853989558188e1c83b0ae655b0_200_0.png)

单位并不是统一大写或小写，单位中可能有的或没有点，而且它们略有不同。这看起来像是一个困难的问题——当你拥有 SAS 字符函数时，就不是了。

这类问题非常常见。看看下面的程序，然后我们讨论一下方法：

## 程序 12.8：演示 `COMPRESS` 和 `FIND` 函数

```
data Metric;
set Learn.Mixed_Units;
Wt_Kg = input(compress(Weight,'kd'),12);
if find(Weight,'lb','i') then Wt_Kg = Wt_Kg/2.2;
Ht_Cm = input(compress(Height,'kd'),12);
if find(Height,'in','i') then Ht_Cm = Ht_Cm*2.54;
```

`COMPRESS` 函数从字符值中提取数字。尽管你将此变量命名为 `Wt_Kg`，但此时你并不知道读取的重量是磅还是公斤。

接下来，你使用 `FIND` 函数在 `Weight` 的值中搜索字符 `1b`。以下是该函数的工作原理：

在最简单的形式中，你向 `FIND` 函数提供两个参数，如下所示：

```
find(string, find_string)
```

在这里，`string` 是你想要搜索的字符串，`find_string` 是你正在寻找的字符串。如果没有找到 `find_string`，函数返回 0。例如，以下语句的值：

实例实例学习 SAS：程序员指南，第二版

`find("what hat is that","hat")`

返回值为 2，即字符串 `hat` 开始的位置。一个较旧的函数 `INDEX` 与这里描述的 `FIND` 函数 类似。然而，`FIND` 函数 更多功能；你可以为 `FIND` 函数添加两个参数。其中一个参数是改变搜索开始方式的修饰符。最实用的修饰符是 `i`（忽略大小写）修饰符。你还可以指定从哪个位置位置开始搜索。如果你使用负值，搜索将从左向右进行。总结一下，`FIND` 函数具有以下语法：

```
find(string, find-string, modifiers, starting-position)
```

顺便说，你可以使用修饰符、起始位置或两者，并且它们的顺序可以是任意的！这怎么可能？因为修饰符总是字符值，而起始位置总是数值值，SAS 可以判断哪个参数是修饰符，哪个是起始位置。

在之前的程序中，使用了 `i` 修饰符，以便搜索 `LB` 或 `IN` 的大小写值。

如果你使用字符 `'LB'`（大小写）确定 `Weight` 的单位，则将 `Wt_Kg` 的值除以 2.2 将磅转换为公斤。如果你使用字符 `'IN'` 确定 `Height` 的单位，则将 `Ht_Cm` 的值乘以 2.54 将厘米转换为英寸。你可以使用修饰符、起始位置或两者，并且它们的顺序可以是任意的！

图 12.9：数据集列表

| Weight | Height | Wt_Kg | Ht_Cm |
|---|---|---|---|
| 100lb | 70in | 45 | 65 |
| 150lb | 65in | 68 | 165 |
| 200lb | 72in | 90 | 182 |
| 250lb | 68in | 113 | 172 |

单位并不是统一大写或小写，单位中可能有的或没有点，而且它们略有不同。这看起来像是一个困难的问题——当你拥有 SAS 字符函数时，就不是了。

这类问题非常常见。看看下面的程序，然后我们讨论一下方法：

第 12 章：字符函数

## 12.9 搜索单个字符

`FIND` 的伴随函数是 `FINDC`。`FIND` 在字符串中搜索特定的子字符串，而 `FINDC` 在字符串中搜索任意字符。

| 行 | 函数 | 返回值 |
|---|---|---|
| 1 | `find('XYZBA', 'ABC')` | 0 |
| 2 | `findc('XYZBA', 'ABC')` | 4 |
| 3 | `findc('ABCDE', 'D')` | 4 |
| 4 | `findc('ABCDE', 'D')` | 4 |
| 5 | `findc('XYZba', 'ABC', 'i')` | 0 |
| 6 | `findc('XYZba', 'ABC', 'i')` | 4 |

在表格第 1 行中，你正在寻找字符串 `ABC`。因为该字符串没有出现，函数返回 0。在第 2 行中，`FINDC` 返回 4（`C` 的位置）。当你寻找单个字符时（如第 3 行和第 4 行所示），函数值相同。表格最后两行演示了你可以使用的 `i`（忽略大小写）修饰符。

## 12.10 在字符串中搜索单词

`FINDW` 与 `FIND` 函数相似，只是搜索单词（因此函数名中带有 `W`）。

单词被定义为以单词边界开始并结束的字符序列。默认单词边界是字符串的开头、结尾、空格，以及以下符号：`$%&*()+-/.`如果你使用 EBCDIC 字符集，分隔符列表略有不同。你可以指定替代参数作为第三参数（你可能想使用默认字符列表中的空格）。

该函数的语法如下：

```
findw(string, delimiters, modifiers, starting-position)
```

在这里，`string` 是你想要搜索的字符串，`find-string` 是你正在寻找的字符串，`delimiters` 提供单词分隔符列表。注意，如果你想提供修饰符（最可能是 `i` 忽略大小写修饰符），你必须提供一个或多个分隔符（即使你只想使用默认值）。

下表显示了 `FIND` 和 `FINDW` 两个函数之间的差异。

| 函数 | 返回值 |
|---|---|
| `find('there is the dog', 'the')` | 1（字符串的位置） |
| `findw('there is the dog', 'the')` | 10（单词 `the` 的开始） |
| `findw('there is THE dog','the',' 'i')` | 10（`THE` 开始） |
| `findw('pear:apple','apple',':')` | 6（单词 `apple` 的开始） |

# 192 实例式学习 SAS：程序员指南，第二版

举例来说，假设你想在一组字符值列表中查找名字 `"Roger"`（不忽略大小写）。以下是该程序：

# 程序 12.9：演示 `FINDW` 函数

```sas
data Look_for_Roger;
input String $40;
if findw(String,'Roger','i') then Match = 'Yes'
else Match = 'No';
datalines;
Will Rogers
Roger Cody
Was Roger here?
Was Roger here?;
```

以下是列表显示：

# 图 12.10：数据集 `Look_for_Roger` 的列表

| String | Match |
| Will Rogers | No |
| Roger Cody | Yes |
| Was Roger here? | Yes |
| Was Roger here? | Yes |

该程序展示了当你需要查找可能是长字符串一部分的单词时，`FINDW` 函数是很有用的。

## 12.11 搜索字符类

一组被某些称为 `ANY` 函数的函数（`ANYNUMAL`, `ANYALPHA`, `ANYDIGIT`, `ANYPUNCT` 和 `ANYSPACE`）允许你分别搜索字母数字值（大小写字母和数字）、字母（所有字母）、数字、标点字符和空格字符（空格、制表符、换行符）。

例如，假设你有一些 ID 值，有些包含数字，有些不包含。你想搜索每个 ID 并创建一个包含一个或多个数字的 ID 列表。这些 ID 存储在一个名为 `ID.txt` 的文本文件中。

`ID.txt` 文件的内容如下：

```
abcABC
NJ1234
987654
123XYZ
TX78010
```

# 第 12 章：使用字符函数 193

以下是该程序：

# 程序 12.10：演示 `ANYDIGIT` 函数

```sas
data Any_Digit;
infile 'C:\books\learning\ID.txt';
input ID : $10;
Position = anydigit(ID);
if Position then output;
```

如果 `ANYDIGIT` 的参数包含任何数字，该函数将返回第一个数字的位置。如果没有，`ANYDIGIT` 则返回 0。该程序额外添加了一行代码，是为了让你清楚地看到 `ANYDIGIT` 函数是如何工作的的。记住，对于任何包含数字的 ID，`Position` 的值将是非零的。因为在逻辑表达式中，所有非 0 或缺失的值都被视为真，因此这些 ID 被写入数据集 `Any_Digit` 中。以下是列表：

# 图 12.11：数据集 `Any_Digit` 的列表

| ID | Position |
|---|---|
| NJ1234 | 3 |
| 987654 | 1 |
| 123XYZ | 1 |
| TX78010 | 3 |

所有的 `ANY` 函数都有一个可选的第二个参数。该参数指示了开始查找指定字符的起始位置。如果起始值为负数，则搜索将从右向左进行，从该参数的绝对值开始。

## 12.12 使用 `NOT` 函数进行数据清洗

另一组函数——`NOT` 函数，与 `ANY` 函数相似。区别在于，这些函数返回字符串中第一个**不**属于指定类的字符的位置。

这使得这组函数在检查字符值是否包含不属于该类的字符时特别有用。例如，如果你预计一个字符串只包含数字，你可以看到 `NOTDIGIT` 函数返回任何大于 0 的值。让我们来看一些例子。

你有一个 SAS 数据集 (`Cleaning`)，其中包含三个变量：`Letters`、`Digits` 和 `Both`。正如你从这些变量名中推出的那样，`Letters` 应该只包含大小写字母；`Digits` 应该只包含数字；`Both` 可以包含字母或数字。你想写一个程序来生成错误报告。以下是 `Cleaning` 数据集的列表：

# 194 实例式学习 SAS：程序员指南，第二版

## 12.12：`Cleaning` 数据集的列表

| Subject | Letters | Digits | Both |
|---|---|---|---|
| 1 | Apple | 12345 | XYZ12 |
| 2 | Ice9 | 123X | Abc.23 |
| 3 | Help! | 999 | XIY23 |

这是一个生成错误报告的程序：

# 程序 12.11：用于数据清洗的 `NOT` 函数

```sas
data Cleaning _null;
  file print;
  set Cleaning;
  if notalpha(trim(Letters)) then put Subject=Letters;
  if notdigit(trim(Digits)) then put Subject=Digits;
  if notalnum(trim(Both)) then put Subject=Both;
run;
```

理解为什么在这个程序中使用 `TRIM` 函数是非常重要的。如果不使用 `TRIM` 函数，使用的三个 `NOT` 函数将返回每个字符值末尾空格的位置。以下是前两个变量的输出：

# 图 12.13：程序 12.11 的输出

| Subject | Letters | Digits | Both |
| 2 | Ice9 | 123X | Abc.23 |
| 3 | Help! | 999 | XIY23 |

（注）

## 12.13 提取字符串的一部分

从字符变量中提取一个或多个字符是有用的。例如，像 `NJ12M99` 这样的 ID 可能包含两个字母的国家缩写和一个第五位的性别代码。你可能还想提取状态代码和性别代码之间的数字。`SUBSTR` 函数允许你胜任这些任务。

# 程序 12.12：使用 `SUBSTR` 函数提取子字符串

```sas
data Extract;
input ID : $10 @@
length State $2 Gender $1 Last $5;
State = substr(ID,1,2);
Gender = substr(ID,5,1);
Last = substr(ID,6);
datalines;
NJ12M99 NY764512
```

该函数的第一个参数是你要搜索的字符串。`SUBSTR` 函数的第二个和第三个参数指定了子字符串的起始位置和长度。例如，变量 `Gender`是从 `ID` 的第五位提取的，长度为 1。变量 `Name` 复杂一点。`SUBSTR` 函数从位置 3 开始提取两个，然后使用 `INPUT` 函数进行字符到数字的转换。注意，创建 `Last` 变量的 `SUBSTR` 函数没有使用参数；`SUBSTR` 函数提取到最后一个非空格字符。

等等！`State` 呢？为什么赋值语句中没有使用 `SUBSTR` 函数？注意 `State` 在 `LENGTH` 语句中声明为长度 2。当你将 `State` 设置 `ID` 时，因为 `State` 的存储长度为 2，它包含了 `ID` 的前两个字符。这是一个许多 SAS 程序员使用的“技巧”。相对于 `SUBSTR` 函数是因为函数会消耗计算机资源（CPU 时间），而这种技巧避免了使用函数。（再次，作者的强迫症倾向又出来了。）

以下是结果数据集的列表：

# 图 12.14：数据集 `Extract` 的列表

| ID | State | Gender | Last | Number |
|---|---|---|---|---|
| NJ12M99 | NJ | M | 99 | 12 |
| NJ764512 | NY | F | 4512 | 76 |
| TX91M5 | TX | M | 5 | 91 |

程序中，使用 `LENGTH` 语句来定义 `State`、`Gender` 和 `Last` 的长度。如果没有这个语句，这字符变量的长度将等于 10，即 `ID` 的长度。理解这一点非常重要。

SAS 在读取阶段阶段之前为所有字符变量分配长度。通常，子字符串的起始位置和长度可以从数据中读取，也可以在 `DATA` 步中计算。因此，如果没有 `LENGTH` 语句，SAS 应该为 `State`、`Gender` 和 `Last` 分配什么长度？从长度为 n 的字符串中提取的最长子字符串是长度为 n 的字符串，所以如果你不定义长度，SAS 正是这样做。

# 196 实例式学习 SAS：程序员指南，第二版

## 12.14 将字符串分为单词

`SCAN` 函数通常用于从字符串中提取单词。然而，正如你将在后面的示例中看到的，它也可以用于解析（分离）由空格以外的分隔符分隔子字符串。让我们从常见的例子开始——将姓和名分离到一个包含两者的变量中：

# 程序 12.13：演示 `SCAN` 函数

```sas

data Original;

  input Name $ 30;

  datalines;

  Jeffrey Smith

  Ron Cody

  Alan Wilson

  Alfred E. Newman

data First_Last;

  set Original Last $ 15;

  First = scan(Name,1, ' ');

  Last = scan(Name,2, ' ');

run;

```

`SCAN` 函数从以空格和非标点字符作为默认分隔符的字符串中提取第 n 个单词。分隔符在 ASCII 和 EBCDIC 字符集中不同。（它们分别是 (<+!*$); ^,/ % (+&*);~/%。）指定要使用的作为 `SCAN` 函数参数的分隔符通常是一个好主意。程序中，指定了空格作为分隔符。

# 图 12.15：数据集 `First_Last` 的列表

| Name | First | Last |
|---|---|---|
| Jeffrey Smith | Jeffrey | Smith |
| Ron Cody | Ron | Cody |
| Alan Wilson | Alan | Wilson |
| Alfred E. Newman | Alfred | E. |

注意 `Newman` 先生的中间名被读成了姓氏，你如何解决这个问题呢？你可以在这个程序中使用 `SCAN` 函数查找第三个单词。如果你在只有两个单词时请求第三个，`SCAN` 返回缺失的字符值。你可以教 `Name` 为

第三个单词。如果找到了它，你就可以假设第二个单词是首字母。然而，有一种更简单的方法。

这是一个程序，它可以从 `Name` 值中提取姓（Last Name），并生成按字母顺序排序的姓名列表：

## 程序 12.14：使用 `SCAN` 函数提取姓

```sas

data Last;

  set Original;

  length Last_Name = $ 15;

  Last_Name = scan(Name,-1, ' ');

run;

proc sort data=Last;

  by Last_Name;

title "Alphabetical List of Names";

proc print data=Last noobs;

  var Name Last_Name;

run;

```

这里的技巧是使用一个**负值**作为 `SCAN` 函数的第二个参数。负值会使扫描从右向左进行，点点从字符串的末尾开始。以下是结果：

## 程序 12.16：程序 12.14 的输出

| Name | Last_Name |
| --- | --- |
| Ron Cody | Cody |
| Alfred E. Newman | Newman |
| Jeffrey Smith | Smith |
| Alan Wilson | Wilson |

注意，姓名是按姓字母字母排序的。

## 12.15 执行模糊匹配

`SPEDIS` 函数（代表拼写距离 spelling distance）用于模糊匹配，即比较可能拼写不同的字符值。虽然其逻辑有点复杂，但使用这个函数非常简单。例如，假设你想搜索一个姓名列表，查看 **Friedman** 这个名字是否在列表中。你想寻找精确匹配或相似的名称。以下是程序：

## 程序 12.15：使用 `SPEDIS` 函数执行模糊匹配

```sas

data Fuzzy;

  input Name = $20;

  Value = spedis(Name, 'Friedman');

datalines;

Friedman
