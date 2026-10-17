
| ID | Type | Units | ID | Code | Units |
|---|---|---|---|---|---|
| 2304 | O | 16 | 6488 | 65 | 27 |
| 1129 | A | 48 | 1129 | 63 | 32 |
| 1129 | A | 50 | 5438 | 62 | 39 |
| 1129 | A | 57 | 2304 | 61 | 45 |
| 2486 | B | 63 | 1387 | | |

- a. 数据集包含某些缺失值，因为并不是所有观测值在另一个数据集中都有匹配的观测值。
- b. 合并的数据集包含 8 个观测值。
- c. DATA 步产生错误。
- d. `Cert.Dors2` 中的值覆盖了 `Cert.Dors1` 中的值。

- 9. 如果通过 `ID` 合并下面的 `Cert.Staff1` 和 `Cert.Staff2`，新数据集有多少个观测值？

| CertStaff1 | | | | CertStaff2 | | | |
|---|---|---|---|---|---|---|---|
| ID | 姓名 | Dept | | ID | 姓名 | 小时 | |
| 000 | Miguel | Project | | | | | 35 | |
| 111 | Diana | B45 | | | | | 0 | |
| 222 | Steve | A12 | | | | | 7 | |
| 888 | Vien | D03 | | | | | 9 | |

- a. 4
- b. 5
- c. 6
- d. 9

## 第 11 章 使用 DO 循环处理数据

语法，DO 组：

```sas
DO;
  SAS statements
END;
```

- `DO` 语句开始 DO 组处理。
- `DO` 语句和 `END` 语句之间的 SAS 语句被称为 DO 组，并作为一个单元执行。
- `END` 语句终止 DO 组处理。

> 提示：你可以在 DO 组中嵌套 `DO` 语句。

你可以在 `IF-THEN/ELSE` 语句和 `SELECT` 组中使用 DO 组，以根据条件操作执行多条语句。

## 示例：DO 和 END 语句

在这个 DO 组中，只有当 `TotalTime` 大于 800 时，`DO` 和 `END` 之间的语句才会执行。如果 `TotalTime` 小于或等于 800，则 DO 组中的语句将不会执行，程序将继续执行跟在相应的 `ELSE` 语句之后的赋值语句。

```sas
data work.ststest;
  set cert.tests;
  TotalTime=(timemin*60)+timesec;
  retain SumSec 5400;
  sumsec+totaltime;
  length TestLength$6 Message $20;
  if totaltime>800 then
    do;
      TestLength='Long';
      message='Run blood panel';
    end
  else if 750<totaltime<=800 then TestLength='Normal';
  else if totaltime<750 then TestLength='Short';
run;

proc print data=work.ststest;
run;
```

## DO 循环的基础

输出 11.1 PROC PRINT Work.StressTest (部分输出)

| Obs | ID | Name | TimeSec | Tolerance | TotalTime | SumSec | TestLength | Message |
|---|---|---|---|---|---|---|---|---|
| 1 | 2458 | Murray, W | | 38 D | | 758 | 6158 | Normal | |
| | | | | more observations. | | | | |
| 7 | 2552 | Reberson, P | | 41 D | | | 9041 | Long | Run blood panel |
| | | | | more observations. | | | | |
| 10 | 2568 | Eberhardt, S | | 49 N | | 1009 | 12835 | Long | Run blood panel |
| 11 | 2571 | Nunnelly, A | | 2 I | | 902 | 13737 | Long | Run blood panel |
| | | | | more observations. | | | | | |
| 13 | 2574 | Peterson, V | | 9 D | | 849 | 15317 | Long | Run blood panel |
| | | | | more observations. | | | | | |
| 15 | 2578 | Cameron, L | | 27 I | | 867 | 16870 | Long | Run blood panel |
| | | | | more observations. | | | | | |
| 17 | 2584 | Takashi, Y | | 7 D | | 967 | 18636 | Long | Run blood panel |
| 18 | 2586 | Decker, B | | 35 N | | 1055 | 19691 | Long | Run blood panel |
| 19 | 2588 | Ivan, H | | 41 N | | 941 | 20632 | Long | Run blood panel |
| 20 | 2589 | Wilcox, E | | 57 I | | 897 | 21529 | Long | Run blood panel |

## DO 语句，迭代语法

迭代 `DO` 语句根据索引变量的值，重复执行 `DO` 和 `END` 语句之间的语句。

语法，`DO` 语句，迭代：

```sas
DO index-variable=specification-1 <, ...specification-n>;
...more SAS statements...
END;
```

- `index-variable`（索引变量）：其值控制 DO 组执行的变量名。

> 注意：避免在 DO 组内部更改索引变量。如果你在迭代 DO 组内部修改了索引变量，可能会导致死循环。注意：除非丢弃该变量，否则索引变量将包含在正在创建的数据集中。

- `specification`（规格）：表示一个表达式或一系列表达式，例如：

`<start <TO stop> WHILE(expression) UNTIL(expression)>`

DO 组从第一个指定的索引变量开始执行。`start` 的值在循环第一次执行之前进行求值。

- `start`：指定索引变量的初始值。
- `TO`：指定索引变量的结束值。在 DO 组内进行的任何更改都不会影响迭代次数。若要在完成前停止迭代，请更改索引变量的值或使用 `LEAVE` 语句退出循环。
- `BY increment`（增量）：指定一个正数或负数（或产生数字的表达式）来控制索引变量。增量的值在循环执行之前进行求值。如果没有指定增量，索引变量将增加 1。当指定了增量时，`start`（如果存在）必须是循环的下界。如果增量为负数，`start`（如果存在）必须是循环的上界。
- `WHILE(expression) UNTIL(expression)`：在 DO 组执行之前或之后对你指定的任何表达式进行求值。将表达式括在括号内。`WHILE` 在每次循环执行之前求值，因此组内的语句在表达式为真时会重复执行。`UNTIL` 在每次循环执行之后求值，因此组内的语句会重复执行直到表达式为真。注意：`TO` 和 `BY` 子句的顺序可以反转。当你使用多个规格时，每个规格只求值一次。这可以大大减少所需的语句数量。例如，这 12 条语句是完全相同的。

## 示例：处理迭代 DO 循环

```sas
data work.earn (drop=month);
  set cert.master;
  earned=0;
  do month=1 to 12;
    earned=(amount+earned) * (rate/12);
  end;
  Balance=Amount+Earned;
run;
```

在这个程序中，每条语句都累积计算了一个月投资所产生的利息。变量 `Earned` 在 DATA 步中创建，用于存储收益利息。投资按月复利，这意味着收益利息的值是累积的。

相比之下，`do` 循环允许你用更少的语句来实现相同的结果。在这种情况下，语句执行了 12 次，位于 `month` 循环中。

输出 11.2 PROC PRINT of Work.Earnings

| Obs | Amount | Rate | Earned | Balance |
|---|---|---|---|---|
| 1 | 1000 | 0.0625 | 0 | 1000 |
| 2 | 1000 | 0.0625 | 5.21 | 2005.21 |
| 3 | 1000 | 0.0625 | 10.4438 | 3015.6538 |
| 4 | 1000 | 0.0625 | 15.7291 | 4031.3729 |
| 5 | 1000 | 0.0625 | 21.0713 | 5052.4442 |
| 6 | 1000 | 0.0625 | 26.4028 | 6078.8470 |
| 7 | 1000 | 0.0625 | 31.8178 | 7110.6648 |
| 8 | 1000 | 0.0625 | 37.3166 | 8147.9814 |
| 9 | 1000 | 0.0625 | 42.9249 | 9190.9063 |
| 10 | 1000 | 0.0625 | 48.6307 | 10239.5370 |
| 11 | 1000 | 0.0625 | 54.4564 | 11293.9934 |
| 12 | 1000 | 0.0625 | 60.3916 | 12354.360 |

## 构建 DO 循环

### DO 循环执行

以下是 DO 循环在 DATA 步中的执行方式。此示例计算了为期一年每月产生的利息。

```sas
data work.earn;
  Amount=1000;
  Rate=.75/12;
  do month=1 to 12;
    earned=(amount+earned)*rate;
  end;
run;
```

此 DATA 步没有从外部源读取数据。提交后，它只会编译并执行一次。在编译期间，为 Work.Earnings 数据集创建了程序数据向量。

#### 程序数据向量

| | | month | Earned |
|---|---|---|---|
| * | * | * | * |

当数据步执行时，赋值了 `Amount` 和 `Rate`。

#### 程序数据向量

| Amount | Rate | month | Earned |
|---|---|---|---|
| * | | | 0 |

接下来执行 DO 循环。在 DO 循环的每次执行中，计算 `earned` 的值并将其加到之前的值。在 DO 循环的第 12 次执行中，`month` 的值增加到 12，`earned` 的值增加到 1069.83。

#### 程序数据向量

| Amount | Rate | month | Earned |
|---|---|---|---|
| 1 | 1000 | 0.0625 | 12 | 1069.83 |

在 DO 循环第 12 次执行后，`month` 的值增加到 13。因为 13 超过了迭代 `DO` 语句的停止值，DO 循环停止执行，处理继续到下一个 DATA 步语句。到达 DATA 步结束，值写入 Work.Earnings 数据，在此示例中，数据步结束。数据集中仅写入了一个观测值。

图 11.1 SAS 数据集 Work.Earnings

| Amount | Rate | month | Earned |
|---|---|---|---|
| 1 | 1000 | 0.0625 | 13 | 1069.889918 |

## 构建 DO 循环 213

注意，索引变量 `Month` 也存储在数据集中。在大多数情况下，索引变量仅用于处理 DO 循环，可以从数据集中删除。

## 使用显式 OUTPUT 语句

为了为 DO 循环的每次迭代创建一个观测值，请在循环内部放置 `OUTPUT` 语句。默认情况下，每个 DATA 步结束时都包含一个隐式 `OUTPUT` 语句。在 DATA 步中放置显式 `OUTPUT` 语句会覆盖自动输出，导致 SAS 只在执行显式 `OUTPUT` 语句时向数据集中添加观测值。

上一个示例创建了一个观测值，是因为在 DATA 步结束时使用了自动输出。在以下示例中，`OUTPUT` 语句覆盖了自动输出，因此 DATA 步写入了 20 个观测值。

```sas
data work.earn;
Value=200;
do Year=20;
 Interest=value*.075;
value=interest;
output;
end;

run;
proc print data=work.earn;
run;
```

![](img/4d880eb3a583bf2815ab53a244818659_224_0.png)

| Obs | Value | Interest |
|---|---|---|
| 1 | 2150.00 | 150.000 |
| 2 | 2311.25 | 161.250 |
| 3 | 2484.59 | 173.344 |
| 4 | 2670.94 | 186.345 |
| 5 | 2871.26 | 200.320 |
| ..more observations.. | | |
| 15 | 5917.75 | 412.867 |
| 16 | 6361.59 | 443.832 |
| 17 | 6838.71 | 477.119 |
| 18 | 7351.61 | 512.903 |
| 19 | 7902.98 | 551.371 |
| 20 | 8495.70 | 592.723 |

## 递减 DO 循环

你可以通过为 `BY` 子句指定负值来递减 DO 循环的索引变量。例如，此迭代 `DO` 语句中的指定使索引变量减少 1，产生值 5, 4, 3, 2 和 1。以下简短示例展示了语法。

```sas
DO index-variable=5 to 1 by -1;
...more SAS statements...
END;
```

当你使用负的 `BY` 子句时，起始值必须大于停止值，以便在每次迭代期间减少索引变量。

```sas
DO index-variable=5 to 1 by -1;
...more SAS statements...
END;
```

## 指定一系列项目

你还可以通过列出系列项目来指定 DO 循环执行的次数。

语法，带有变量列表的 DO 循环：

```sas
DO index-variable=value1, value2, value3...
...more SAS statements...
END;
```

值可以是字符型或数值。

当 DO 循环执行时，它会为系列中的每个项目执行一次。索引变量等于当前项目的值。你必须使用逗号分隔系列中的项目。

要列出系列中的项目，你必须如语法所示指定以下内容之一：

- 所有的数值。

```sas
DO index-variable=2,5,9,13,27;
...more SAS statements...
END;
```

- 所有的字符，用引号括起来。

```sas
DO index-variable='MON','TUE','WED','THR','FRI';
...more SAS statements...
END;
```

- 所有的变量名。索引变量取指定变量的值。

```sas
DO index-variable=win,place,show;
...more SAS statements...
END;
```

变量名必须代表数值或全字符。不要给变量名加引号。

## 嵌套 DO 循环

### 缩进和嵌套组

你可以将 DO 组嵌套到任何级别，就像嵌套 `IF-THEN/ELSE` 语句一样。

注意：你系统的内存能力可能会限制你可以使用的嵌套 `DO` 语句的数量。

这是一个嵌套 DO 组的示例：

```sas
do;
  ...more SAS statements...;
  do;
    ...more SAS statements...;
    do;
      ...more SAS statements...;
    end;
  end;
```

对 DO 组中的语句进行缩进是一个良好的习惯，这样它们的位置就可以指示嵌套的级别。

### 示例：嵌套 DO 循环

迭代 `DO` 语句可以在 DO 循环内执行。将一个 DO 循环放在另一个 DO 循环内部被称为嵌套。

```sas
do i=1 to 20;
  ...more SAS statements...;
  do j=1 to 10;
    ...more SAS statements...;
  end;
  ...more SAS statements...;
end;
```

下面的 DATA 步计算利率为 7.5% 的月复利投资价值。假设在 20 年内添加相同金额的资金。为了这一点，可以在执行 20 次的另一个 DO 循环中包含每月计算。

```sas
data work.earn;
  Capital=2000;
  do month=1 to 12;
    Interest=capital*(.075/12);
    capital=interest;
  end;
```

### 使用 DO 循环处理
