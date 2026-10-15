

你可以在 Display 3.10 中确认新变量的格式。

## Display 3.10 Output produced by user-defined format

| Obs | animal | conc | brood1 | brood2 | brood3 | total | cbrood3 |
|---|---|---|---|---|---|---|---|
| 31 | 31 | 235 | 4 | 13 | 6 | 23 | some |
| 32 | 32 | 235 | 6 | 10 | 5 | 21 | some |
| 33 | 33 | 235 | 2 | 5 | 0 | 7 | none |
| 34 | 34 | 235 | 6 | 0 | 6 | 12 | some |
| 35 | 35 | 235 | 6 | 13 | 8 | 27 | some |
| 36 | 36 | 235 | 6 | 0 | 10 | 16 | some |
| 37 | 37 | 235 | 7 | 0 | 6 | 13 | some |
| 38 | 38 | 235 | 4 | 2 | 9 | 15 | some |
| 39 | 39 | 235 | 6 | 8 | 7 | 21 | some |
| 40 | 40 | 235 | 7 | 0 | 10 | 17 | some |

## 3.4 Selecting or Stratifying an Analysis by Values of a Variable

BY 语句用于指定按变量水平分层的数据集分析。它通常与 SORT 过程一起使用。例如，以下代码对 nitrofen 数据集 nitro_tox 进行排序，并生成输出数据集 nitro_tox2，其中观测值已排序：

```
proc sort data=nitro_tox out=nitro_tox2;
    by conc;
run;
proc print data=nitro_tox2;
    by conc;
run;
```

你可以按一个以上的变量排序。例如，假设你想在 conc 内按 total 排序。以下代码执行排序并在 Display 3.11 中打印结果：

```
proc sort data=nitro_tox;
    by conc total;
run;
proc print data=nitro_tox;
    id animal;
    var conc total;
run;
```

## Display 3.11 Printout of nitrofen data using animal ID as an identifier and sorted by TOTAL within each CONC level

| animal | conc | total |
|---|---|---|
| 9 | 0 | 24 |
| 1 | 0 | 27 |
| 8 | 0 | 30 |
| 10 | 0 | 31 |
| 2 | 0 | 32 |
| 4 | 0 | 33 |
| 7 | 0 | 33 |
| 3 | 0 | 34 |
| 6 | 0 | 34 |
| 5 | 0 | 36 |
| 16 | 80 | 26 |
| 17 | 80 | 27 |
| ... |  |  |
| 23 | 160 | 23 |
| 28 | 160 | 26 |
| ... |  |  |
| 33 | 235 | 7 |
| 34 | 235 | 12 |
| ... |  |  |
| 44 | 310 | 0 |
| 48 | 310 | 4 |
| 46 | 310 | 5 |
| 50 | 310 | 5 |
| 41 | 310 | 6 |
| 42 | 310 | 6 |
| 47 | 310 | 6 |
| 49 | 310 | 6 |
| 43 | 310 | 7 |
| 45 | 310 | 15 |

你可以使用 WHERE 语句限制输出。例如，假设你只想打印三个窝中所有幼崽总数小于 10 的观测值。以下部分代码生成 Display 3.12 中的输出：

```
proc sort data=nitro_tox;
  by conc total;
run;

proc print data=nitro_tox;
  id animal;
  var conc total brood1 brood2 brood3;
  where total<10;
run;
```

## Display 3.12 Printout of data where total young is less than 10

| animal | conc | total | brood1 | brood2 | brood3 |
|---|---|---|---|---|---|
| 33 | 235 | 7 | 2 | 5 | 0 |
| 44 | 310 | 0 | 0 | 0 | 0 |
| 48 | 310 | 4 | 4 | 0 | 0 |
| 46 | 310 | 5 | 5 | 0 | 0 |
| 50 | 310 | 5 | 5 | 0 | 0 |
| 41 | 310 | 6 | 6 | 0 | 0 |
| 42 | 310 | 6 | 6 | 0 | 0 |
| 47 | 310 | 6 | 6 | 0 | 0 |
| 49 | 310 | 6 | 6 | 0 | 0 |
| 43 | 310 | 7 | 7 | 0 | 0 |

## 3.5 Displaying Data Set Properties and Observations

数据集的内容，包括数据集属性、变量名、类型（字符、数值）、存储长度、格式和标签，都可以使用 CONTENTS 过程显示。nitro_tox 数据集的这些详细信息可以使用以下代码生成并显示，该代码在 Display 3.13 中给出：

```
proc contents data=nitro_tox;
run;
```

## Display 3.13 Details of the nitro_tox data set generated and displayed by PROC CONTENTS

The CONTENTS Procedure
Data Set Name: WORK.NITRO_TOX          Observations: 50
Member Type: DATA                      Variables: 7
Engine: V8                             Indexes: 0
Created: 10:19 Monday, September 1, 2008   Observation Length: 56
Last Modified: 10:19 Monday, September 1, 2008   Deleted Observations: 0
Protection:                            Compressed: NO
Data Set Type:                         Sorted: NO
Label:
-----Engine/Host Dependent Information-----
Data Set Page Size: 8192
Number of Data Set Pages: 1
First Data Page: 1
Max Obs per Page: 145
Obs in First Data Page: 50
Number of Data Set Repairs: 0
File Name: C:\DOCUME-1\bailera\LOCALS~1\Temp\SAS Temporary Files\_TD1220\nitro_tox.sas7bdat
Release Created: 8.0202M0
Host Created: WIN_PRO

## Display 3.13 (continued)

| # | Variable | Type | Len | Pos | Format | Label |
|---|---|---|---|---|---|---|
| 1 | animal | Num | 8 | 0 |  | animal ID number |
| 3 | brood1 | Num | 8 | 16 |  | number of young in first brood |
| 4 | brood2 | Num | 8 | 24 |  | number of young in 2nd brood |
| 5 | brood3 | Num | 8 | 32 |  | number of young in 3rd brood |
| 7 | cbrood3 | Num | 8 | 48 | TOTFMT. |  |
| 2 | conc | Num | 8 | 8 |  | Nitrofen concentration |
| 6 | total | Num | 8 | 40 |  | total young produced in three brood |

该输出顶部报告了数据集中的观测数（50）、变量数（7）以及有关数据集的其他信息。输入变量数据集和新定义的变量 cbrood3 都显示出来。此外，所有这些变量都是数值型（TYPE=NUM），为每个变量分配了 8 个字节进行存储（LEN=8）。定义的标签和格式列出。此变量列表按字母顺序排序。如果你想按变量在数据集中读取或创建的顺序查看变量名（它们在数据集中的位置），则使用 PROC CONTENTS 的 VARNUM 选项。例如：

```
proc contents data=nitro_tox varnum; run;
```

## 3.6 Using PROC PRINT to List the Observations in a Data Set

在你输入、infile 或导入数据集并定义标签和格式后，通常希望查看你构建的数据集的观测值和变量。PROC PRINT 显示 SAS 数据集中的观测值。此显示可以修改为计算简单的统计量，例如总和，并且可以使用变量来标识列表中的观测值。以下部分 SAS 代码按浓度分组打印 nitro_tox 数据集（by conc），对每个浓度条件下产生的幼崽总数求和（sum total），并使用动物 ID 标识每个观测值（id animal）：

```
proc print data=nitro_tox;
by conc;  * assumes input data sorted by this variable;
sum total;
id animal;* animal number used to ID case;
run;
```

此代码生成 Display 3.14 中的打印输出。即使 cbrood3 是一个数值变量，它也是使用分配给它的格式显示的。

## Display 3.14 Output produced by PROC PRINT

```
Nitrofen concentration=0
animal   brood1   brood2   brood3   total   cbrood3
1        3        14       10       27      some
2        5        12       15       32      some
3        6        11       17       34      some
4        6        12       15       33      some
5        6        15       15       36      some
6        5        14       15       34      some
7        6        12       15       33      some
8        5        13       12       30      some
9        3        10       11       24      some
10       6        11       14       31      some
------                           -----
conc                                 314
/* some output deleted here */

Nitrofen concentration=310
animal   brood1   brood2   brood3   total   cbrood3
41       6        0        0        6       none
42       6        0        0        6       none
43       7        0        0        7       none
44       0        0        0        0       none
45       5        10       0        15      none
46       5        0        0        5       none
47       6        0        0        6       none
48       4        0        0        4       none
49       6        0        0        6       none
50       5        0        0        5       none
------                           -----
conc                                 60
                                   ======
                                   1144
```

## 3.7 Basic Graphical Displays

探索研究数据通常从简单的图形摘要开始。讨论 SAS 中统计图形的一个好起点是 SGPLOT 过程。可以使用该过程生成大量的图形。在以下代码中，构建了一个水平条形图，其中不同浓度组的幼崽平均数分别显示。限制范围在均值 ±2 个标准差。 此外，还请求了点图来显示这些数据。Display 3.15 中的代码生成 Display 3.16 和 Display 3.17 中的输出。

