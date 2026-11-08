
虽然尾随与号（&）可能有帮助，但它也可能引入问题。如果数据稍微更复杂一些，甚至这个解决方案也可能不起作用。以下数据还包含城市名。尽管城市未被读取，与姓氏（LNAME）一起使用的尾随 & 会导致城市名与姓氏混淆。

```sas
title '1.3.2b List Input Modifiers';
data base;
length lname $15;
input fname $ dob :mmddyy10. lname $ &;
format dob mmddyy10.;
datalines;
Sam 12/15/1945 Johnson   Seattle
Susan   10/10/1983 Mc Callister New York
;
run;
```

**1.3.2b 列表输入修饰符**

| Obs | lname | fname | dob |
|---|---|---|---|
| 1 | Johnson | Sam | 12/15/1945 |
| 2 | Mc Callister Ne | Susan | 10/10/1983 |

由于尾随 & 以及 LNAME 的长度（$15），第二个观测中城市的一部分（New York）被读入了 LNAME。在第一个观测中，姓氏是正确的，因为 Johnson 和 Seattle 之间用多个空格分隔。即使使用尾随 &，多个空格仍会被成功视为字段分隔符。

在第二个观测中，如果两个字段之间有两个或更多空格，城市就不会与姓氏混淆。

- ❶ 将 FORMAT 语句放在 DATA 步中，会使该格式在后续步骤中与变量 DOB 关联。INFORMAT 语句仅在读取数据时使用。
- ❷ DATALINES 语句使后续记录作为数据读取，直到但不包括包含分号的第一行。在前面的示例中，RUN 语句兼作数据结束标记。许多程序员使用单独的分号来完成此任务。两种风格通常都被认为可接受（只要您使用 RUN 语句结束步骤）。

当姓氏和城市之间只有一个空格时，仅靠尾随 & 不足以帮助 INPUT 语句区分这两个字段。此示例的其他变体可在第 1.3.3 节中找到。

## 更多信息

LIST 输入是一种分隔输入形式，因此这些选项也适用于第 1.3.3 节中讨论的示例。当日期格式不一致时，*任意日期*  informat 之一可能会有帮助。有关这些专用 informat 的使用的更多信息，请参见第 12.6 节。

## 另请参阅

SAS 论坛帖子 [http://communities.sas.com/message/42690](http://communities.sas.com/message/42690) 讨论了列表输入修饰符的使用。

## 1.3.3 控制分隔输入

从技术上讲，LIST 输入是一种分隔输入形式，默认分隔符为空格。这意味着第 1.3.2 节中显示的修饰符适用于其他形式的分隔输入，包括逗号分隔变量文件、CSV 文件。

### INFILE 语句选项

INFILE 语句上的选项用于控制如何解释分隔符。

- DELIMITER 指定用于分隔字段的字符（默认空格除外）。此选项通常缩写为 DLM=。
- DLMSTR 指定单个多字符字符串作为分隔符。
- DLMOPT 指定 DLMSTR 选项的解析选项。
- DSD 允许使用引号包围的字符字段（通过将逗号设置为分隔符）。两个连续分隔符被解释为单独的分隔符，从而可以适当地分配缺失值。DSD 还会移除引号包围的字符值中的引号。如果逗号不是分隔符，则需要将 DLM= 选项与 DSD 选项一起使用。

某些应用程序（例如 Excel）会构建用引号包围字段的分隔变量文件。如果字段的值可能包含字段分隔符，这可能至关重要。对于默认列表输入（其中空格是分隔符），成功读取包含嵌入空格的字段可能非常困难（请参见第 1.3.2 节，其中讨论了使用尾随 & 读取嵌入空格）。DSD 选项提醒 SAS 注意带引号字符字段的*可能性*。以下示例演示了简单的逗号分隔数据。

```sas
data base;
length lname $15;
infile datalines ❶ dlm=',' dsd; ❸
*infile datalines dlm=',' ❷;
input fname $ lname $ dob :mmddyy10.;
datalines;
'Sam','Johnson',12/15/1945
'Susan','Mc Callister',10/10/1983
;
run;
```

❶ 尽管在使用 DATALINES、CARDS 或 CARDS4 语句时通常不需要 INFILE 语句，但当需要与 INFILE 语句关联的选项时，它可能非常有用。*fileref* 可以是 DATALINES 或 CARDS。

1.3.3a 分隔列表输入修饰符

| Obs | lname | fname | dob |
|---|---|---|---|
| 1 | 'Johnson' | 'Sam' | 12/15/1945 |
| 2 | 'Mc Callister' | 'Susan' | 10/10/1983 |

DLM= 选项用于指定分隔符。在此示例中，字段分隔符被指定为逗号 ❷。

包含字符数据的字段已被引号包围。由于我们实际上不希望引号成为数据字段的一部分，DSD 选项 ❸ 提醒解析器注意这种可能性，引号本身成为分隔符处理过程的一部分。

```sas
infile datalines dlm=',' dsd; ❸
```

使用 DSD 选项会得到不带引号的数据字段。

1.3.3a 分隔列表输入修饰符

| Obs | lname | fname | dob |
|---|---|---|---|
| 1 | Johnson | Sam | 12/15/1945 |
| 2 | Mc Callister | Susan | 10/10/1983 |

### 关于 INPUT 语句

波浪号（~）❶ 可用于修饰格式，与冒号（:）的作用非常相似；但是，这两个修饰符并不完全相同。

```sas
title '1.3.3b Delimited List Input Modifiers';
title2 'Using the ~ Format Modifier';
data base;
length lname $15;
infile datalines dlm=',', dsd;
input fname $ lname $ birthloc $~❶15. dob :mmddyy10. ;
datalines;
'Sam','Johnson','Fresno, CA',12/15/1945
'Susan','Mc Callister','Seattle, WA',10/10/1983
run;
```

波浪号格式修饰符能正确读取 BIRTHLOC 字段；但是，它会保留包围该字段的引号。与冒号一样，波浪号可以放在字符变量的 $ 之前或之后。顺便注意，在此示例中，第一行的数值日期值被引号包围。该字段仍会作为数值 SAS 日期值正确处理。

1.3.3b 分隔列表输入修饰符
使用 ~ 格式修饰符

| Obs | lname | fname | birthloc | dob |
|---|---|---|---|---|
| 1 | Johnson | Sam | 'Fresno, CA' | 12/15/1945 |
| 2 | Mc Callister | Susan | 'Seattle, WA' | 10/10/1983 |

将波浪号 ❶ 替换为冒号（:）会使 BIRTHLOC 值在保存时不带引号。如果我们改为为 BIRTHLOC 提供长度 ❷，则既不需要格式，也不需要波浪号。

```sas
title '1.3.3c Delimited List Input Modifiers';
title2 'BIRTHLOC without a Format Modifier';
title3 'BIRTHLOC Length Specified';
data base;
length lname birthloc $15; ❷
infile datalines dlm=',', dsd;
input fname $ lname $ birthloc $ dob :mmddyy10. ;
datalines;
'Sam','Johnson','Fresno, CA',12/15/1945
'Susan','Mc Callister','Seattle, WA',10/10/1983
run;
```

1.3.3c 分隔列表输入修饰符
BIRTHLOC 不使用格式修饰符
BIRTHLOC 长度已指定

| Obs | lname | birthloc | fname | dob |
|---|---|---|---|---|
| 1 | Johnson | Fresno, CA | Sam | 12/15/1945 |
| 2 | Mc Callister | Seattle, WA | Susan | 10/10/1983 |

### 多个分隔符

可以读取包含多个分隔符的分隔输入流。在以下小示例中，逗号和斜杠这两个分隔符都用于分隔数据值。

```sas
data imports;
infile cards dlm=',/';
input id importcode $ value;
cards;
14,1,13
25/Q9,15
6,D/20
run;
```

| Obs | id | importcode | value |
| --- | --- | --- | --- |
| 1 | 14 | 1 | 13 |
| 2 | 25 | Q9 | 15 |
| 3 | 6 | D | 20 |

请注意，DLM 选项使逗号或斜杠之一被用作字段分隔符，但不会将斜杠和逗号一起作为单个分隔符（请参见下面的 DLMSTR 选项以创建单个多字符分隔符）。

```sas
data imports;
retain dlmvar '/,'; ❶
infile cards dlm=dlmvar;
input id importcode $ value;
cards;
14,1,13
25/Q9,15
6,D/20
run;
```

- ❶ 由于 INFILE 语句针对每个观测执行，分配给 DLM 选项的值不必是常量。它也可以是变量，或可以使用 IF-THEN/ELSE 逻辑更改。在最简单的形式中，此变量可以在 retain 语句中赋值。
- ❷ 这个简单示例演示了随观测变化的分隔符。这里每行的第一个字符是该行要使用的分隔符。该分隔符被读取、存储，然后在 INFILE 语句上使用。这里我们利用了 INFILE 语句的可执行特性。

```sas
data imports;
infile cards;
input dlmvar $1. ❷;
infile cards dlm=dlmvar; ❸
input @2 id importcode $ value;
cards;
,14,1,13
/25/Q9/15
~6~D~20
run;
```

### 使用 DLMSTR

与指定一个或多个分隔符的 DLM 选项不同，DLMSTR 选项声明要用作分隔符的特定字符列表。这里分隔符是字符序列 comma-comma-slash（,,/）。请注意，在 IMPORT 数据集的 LISTING 中，多余的逗号和斜杠被读取为数据。

```sas
data imports;
infile cards dlmstr=',,/' ;
input id importcode $ value;
cards;
14,,/1/,,/13
25,,/Q9,,,/15
6,,/,D,,/20
run;
```

1.3.3g 使用分隔符字符串

| Obs | id | importcode | value |
| --- | --- | --- | --- |
| 1 | 14 | 1/ | 13 |
| 2 | 25 | Q9, | 15 |
| 3 | 6 | ,D | 20 |

