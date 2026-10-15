

在本章中，您将了解到一种可在 DATA 步中使用的数据结构（数组）。数组可以存储一组相似类型的元素。提供了涉及这些数据结构的各种操作。一系列示例说明了数组的强大功能和灵活性。默认情况下，SAS 逐条处理数据，忘记前一条记录中变量的值。（抱歉拟人化了 SAS。我知道它实际上并没有忘记值，但这是一个有用的形象。）然而，保留值以便处理未来的记录通常很重要。RETAIN 语句解决了这一需求。对 ARRAY 和 RETAIN 的描述和基本说明辅以案例研究，强调了它们的强大功能。

## 9.1 用于存储值集合的存储箱

数组是一种临时数据结构，包含一组变量或值。数组常用于存储变量列表。可以将数组概念化为一个被划分为许多隔间的盒子，每个隔间包含信息。定义数组中变量及其值的方式有很多。那么，如何告诉 SAS 您想要设置一个用于存储值的数组呢？以下是基本语法：

```
ARRAY arrayname{number of array elements} variable-list;
```

（符号 { }、[ ] 和 ( ) 都可以在数组定义中使用。）如果您想直接定义变量的值，可以在变量列表之后进行定义。

### 9.1.1 在变量列表中定义值

在此示例中，一个数组（tempF）用四个华氏温度初始化。该数组被循环遍历一个摄氏温度数组（tempC），以计算对应于华氏值的数值。

# Display 9.1 使用数组转换温度尺度

```
data temps;
  array tempF(4) tempF1-tempF4 (32,50,68,86);
  array tempC(4) tempC1-tempC4;

  do itemp = 1 to 4;
    tempC(itemp) = 5/9*(tempF(itemp)-32);
  end;
  drop itemp;
end;
run;

proc print data=temps;
run;
```

Display 9.1 的打印输出包括以下输出行：

| Obs | temp F1 | temp F2 | temp F3 | temp F4 | temp C1 | temp C2 | temp C3 | temp C4 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 32 | 50 | 68 | 86 | 0 | 10 | 20 | 30 |

### 9.1.2 在变量列表中输入值

您可以从数据行或外部文件中读取变量值到数组中。假设每位养老院居民在连续七个季度中能够进行的日常生活活动（ADL）数量被测量。很自然地将每位居民的数据视为分组。在下图中，一个七元素数组包含一位居民的数据，其前两个 ADL 测量值为 6，其后三个 ADL 测量值为 5，其后一个 ADL 测量值为 4，最后一个 ADL 测量值为 3。

| ADL[1] | ADL[2] | ADL[3] | ADL[4] | ADL[5] | ADL[6] | ADL[7] |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 6 | 5 | 5 | 5 | 4 | 3 |

对于此示例，以下代码可用于将这些数据读入数组：

```
data D1;
ARRAY ADL{7} ADL1-ADL7;
    input ADL1-ADL7;
    datalines;
6 6 5 5 5 4 3
;
run;
```

在此代码段中，数组名为 ADL，元素名为 ADL1 至 ADL7。通过在数组名 ADL 声明后使用 {7}，显式声明数组的大小为 7 个元素。您可以通过使用星号，如 { * }，来定义数组的大小，而无需计算数组中的元素数。这在下一段代码中进行了说明：

```
data D2;
ARRAY ADL{*} ADL1-ADL7;
    input ADL1-ADL7;
    datalines;
6 6 5 5 5 4 3
;
run;
```

此数组中的变量定义为 ADL1 至 ADL7。您可以基于一组变量名定义数组。例如：

```
data D3;
ARRAY ADL{*} t1 t2 t3 t4 t5 time6 time_7;
input t1 t2 t3 t4 t5 time6 time_7;
datalines;
6 6 5 5 5 4 3
;
run;
```

数组常用于处理变量列表。也许数组最常见的用途是将缺失值代码重新分配为 SAS 内部表示。要处理数组的所有元素，请使用带 DO-END 语句对和索引的循环结构。下一节中的示例说明了这种策略。

### 9.1.3 重新编码数值变量的缺失值代码 “.”

数据集通常继承自数据收集者，或来自对其他目的的初级数据收集后的二级数据分析的某个部分。假设 -999 在 ADL 研究中用作缺失值代码。您希望在进行进一步分析之前将所有 -999 的出现替换为 .。以下代码通过循环遍历数组来实现这一点。

# Display 9.2 重新编码数值变量中的缺失值

```
data D4;
ARRAY ADL{*} t1 t2 t3 t4 t5 time6 time_7;
input t1 t2 t3 t4 t5 time6 time_7;
DO ielement = 1 to dim(ADL);
    if ADL{ielement}=-999 then ADL{ielement}=.;
END;
datalines;
6 6 5 5 5 4 3
7 -999 4 4 3 -999 2
;
run;
proc print data=D4;
title "Recoding missing values using arrays and DO loop";
run;
```

Display 9.2 的打印输出包括以下输出行：

```
Recoding missing values using arrays and DO loop
Obs    t1    t2    t3    t4    t5    time6    time_7    ielement
1      6     6     5     5     5     4        3         8
2      7     .     4     4     3     .        2         8
```

请注意输出数据集中的索引变量 ielement。该索引的值为 8，超出循环范围，这是每次观察循环停止时的情况。您可以通过使用 DROP 语句从输出数据集中消除索引变量。（例如，在前面的代码中，在 datalines 语句之前插入 drop ielement 语句）。数组中包含的变量列表可以隐式定义为所有数值变量、所有字符变量或所有变量，分别使用 _NUMERIC_、_CHARACTER_ 和 _ALL_ 选项。以下示例说明了这种构造的强大功能。

### 9.1.4 重新编码所有数值和字符变量的缺失值

假设 ADL 数据集包含居民姓名和性别的字符变量以及随时间记录的七个 ADL 测量值。以下程序将所有数值变量分组到名为 num_array 的数组中。它将所有字符变量分组到名为 char_array 的数组中。程序循环遍历每个数组，将所有缺失值更改为数值变量的 .，并将所有缺失值更改为字符变量的空白。dim 函数确定每个数组中元素的数量以供循环使用。该程序显示在 Display 9.3 中。

# Display 9.3 重新编码数值和字符变量中的缺失值

```
data D5;
    input name $ sex $ t1 t2 t3 t4 t5 time6 time_7;

ARRAY num_array{*} _NUMERIC_;
ARRAY char_array{*} _CHARACTER_;

/* recode the numeric variables */
DO inum = 1 to dim(num_array);
    if num_array{inum}==-999 then num_array{inum}=.;
END;

/* recode the character variables */
Do ichar = 1 to dim(char_array);
```

# Display 9.3 (continued)

```
if char_array{ichar}="-999" then char_array{ichar}=" ";
END;

drop inum ichar;
datalines;
MrSmith -999 6   6 5 5 5    4 3
-999      F 7 -999 4 4 3 -999 2
;
run;

proc print data=D5;
title "Recoding missing values using arrays and DO loop";
run;
```

Display 9.3 的打印输出包括以下输出行：

```
Recoding missing values using arrays and DO loop
Obs    name    sex    t1    t2    t3    t4    t5    time6    time_7
1      MrSmith         6     6     5     5     5     4        3
2                   F     7     .     4     4     3     .        2
```

### 9.1.5 从单条记录创建多个观测值

SAS 中的不同过程可能期望数据具有不同的结构。例如，一些多元过程期望所有变量在单条记录中定义。在其他情况下，例如应用于纵向数据的混合模型，不同的测量值期望在不同的记录中定义。能够将单条记录扩展为多条记录，或将多条记录压缩为单条记录非常重要。假设您的数据具有以下形式：

| Name | Sex | t1 | t2 | t3 | t4 | t5 | time6 | time_7 |
|------|-----|----|----|----|----|----|-------|--------|
| Smith | M | 6 | 6 | 5 | 5 | 5 | 4 | 3 |
| Jones | F | 7 | 5 | 4 | 4 | 3 | 2 | 1 |
| Fisher | M | 5 | 5 | 5 | 3 | 2 | 2 | 1 |

