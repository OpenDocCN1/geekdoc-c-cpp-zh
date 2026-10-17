
### 示例 6：在存储的编译 DATA 步程序中使用密码

第一个 DATA 步创建了一个名为 `STORED.ITEMS` 的存储编译 DATA 步。该程序包含了 `ALTER` 密码，它限制了对程序的访问。

```sas
data sample;
input Name $ TotalItems $;
datalines;
Lin 328
Susan 433
Ken 156
Pat 340

proc print data=sample;
run;
libname stored 'SAS-library';

data employees / pgm=stored.items (alter=klondike);
set sample;
if TotalItems > 200 then output;
run;
```

此 DATA 步执行存储的编译 DATA 步程序 `STORED.ITEMS`。它使用 `DESCRIBE` 语句将源代码打印到 SAS 日志中。因为程序在创建时使用了 `ALTER` 密码，所以当你在使用 `DESCRIBE` 语句时必须使用密码。如果不输入密码，SAS 将提示你输入。

```sas
data pgm=stored.items (alter=klondike);
describe;
execute;
run;
```

### 示例 7：显示嵌套层

以下程序有两个嵌套层。SAS 将生成四条日志消息，每个嵌套层各一个开始和结束消息。

```sas
data _null_ /nesting;
do i = 1 to 10;
  do j = 1 to 5;
    put i = j;
  end;
run;
```

#### 日志 2.2 嵌套层调试（部分 SAS 日志）

| 行号 | 内容 |
| :--- | :--- |
| 6 | data _null_ /nesting; |
| 7 | do i = 1 to 10; |
| | 719 |
| | NOTE 719-185: *** DO begin level 1 *** |
| | do j = 1 to 5; |
| 8 | 719 |
| | NOTE 719-185: *** DO begin level 2 *** |
| | put i = j; |
| 9 | end; |
| 10 | 720 |
| | NOTE 720-185: *** DO end level 2 *** |
| | NOTE 720-185: *** DO end level 1 *** |
| | end; |
| | run; |

*(注：日志内容是根据标准 SAS 日志行为重的，因为 OCR 文本是碎片化的)*

# DESCRIBE 语句

## 不带参数

当执行 `DELETE` 时，当前观测值不会被写入数据集，SAS 会立即返回到 DATA 步的开始进行下一次迭代。

## 详细

`DELETE` 语句通常用于 `IF-THEN` 语句的 THEN 子句中，或作为条件执行的 DO 组的一部分。

## 比较

- 当更容易指定一个排除数据集中观测值的条件时，或者当没有继续处理当前观测值的 DATA 步语句的需要时，请使用 `DELETE` 语句。
- 当更容易指定一个包含观测值的条件时，请使用子集 `IF` 语句（subsetting IF）。
- 不要将 `DROP` 语句与 `DELETE` 语句混淆。`DROP` 语句从输出数据集中排除变量；而 `DELETE` 语句排除观测值。

## 示例

示例 1：将 `DELETE` 语句作为 `IF-THEN` 语句的一部分

当 `LEAFWT` 的值为缺失值时，删除当前观测值：

```
if leaftw= then delete;
```

示例 2：使用 `DELETE` 语句对原始数据进行子集处理

```
data tops;
infile file-specification;
input region office product yrsales;
if yrsales<10000 then delete;
run;
```

## 另另

语句：
- 第 63 页的“`DO` 语句”
- 第 71 页的“`DROP` 语句”
- 第 155 页的“`IF-THEN`, 子集”
- 第 157 页的“`IF-THEN/ELSE` 语句”

# DESCRIBE 语句

从存储的编译 DATA 程序或 DATA 步视图中检索源代码。

有效位置：`DATA` 步

类别：操作

## 可执行

**类型：** 可执行

**限制：** 仅对存储的编译 DATA 步程序和 DATA 步视图使用 `DESCRIBE`。

**要求：** 你必须在 `DATA` 语句中指定 `PGM=` 或 `VIEW=` 。

## 语法

`DESCRIBE:` 

## 不带参数

使用 `DESCRIBE` 语句从存储的编译 DATA 步程序或 DATA 步视图中检索程序源代码。SAS 将源语句写入日志。

## 详细

在不使用 `EXECUTE` 语句的情况下使用 `DESCRIBE` 语句从存储的编译 DATA 步程序或 DATA 步视图中检索源代码。带有 `EXECUTE` 语句的 `DESCRIBE` 语句用于检索源代码并执行存储的编译 DATA 步程序。有关如何将这些语句与 `DATA` 语句配合的信息，请参见第 48 页的“`DATA` 语句”。

## 另另

语句：
- 第 48 页的“`DATA` 语句”
- 第 75 页的“`EXECUTE` 语句”

# DISPLAY 语句

显示用 `WINDOW` 语句创建的窗口。

| 有效位置： | DATA 步 |
| :--- | :--- |
| 类别： | 窗口显示 |
| 类型： | 可执行 |

## 语法

`DISPLAY window.<group> <NOINPUT> <BLANK> <BELL> <DELETE>;`

## 参数

`window.<group>`

指定要显示的窗口和字段组。该字段前有一个点 (.)。

**提示：** 如果窗口包含多一组字段，请提供完整的 `window.group` 规范。如果窗口包含单个未命名的组，仅使用 `window`。

## NOINPUT

指定不能向窗口中显示的字段中输入值。

**默认值：** 如果省略了 `NOINPUT`，你可以向窗口中显示的未保护字段输入值。

**限制：** 如果在 DATA 步中所有的 `DISPLAY` 语句在使用 `NOINPUT`，则必须包含一个 `STOP` 语句来停止处理 DATA 步。

**提示：** 当你想在某些时候允许向窗口输入值时，`NOINPUT` 选项非常有用。例如，你可以显示一次窗口以输入值，第二次显示以验证它们。

## BLANK

清除窗口。

**提示：** 当你想在窗口中显示不同的字段组，且不希望上一组的文本出现在当前显示中时，使用 `BLANK` 选项。

## BELL

当显示窗口时，如果你的个人电脑配备了提供声音的扬声器，则产生听力报警、哔声或铃声。

## DELETE

在处理完出现该选项的 `DISPLAY` 语句后删除窗口显示。

## 详细

你必须在显示它的同一个 DATA 步中创建一个窗口。一旦显示了窗口，窗口将保持可见，直到显示另一个窗口覆盖它或者 DATA 步结束。当你显示一个包含输入值字段的窗口时，在每个未保护字段上输入值或按回 键，以便 SAS 进入下一步。你不能跳过任何字段。

在显示窗口期间，使用命令和功能键查看其他窗口、更改当前窗口的大小等。

包含 `DISPLAY` 语句的 DATA 步将继续执行，直到 `SET`、`MERGE`、`UPDATE`、`MODIFY` 或 `INPUT` 语句读取的最后一个观测值处理完毕，直到执行 `STOP` 或 `ABORT` 语句。你也可以在窗口命令行上发出 `END` 命令来停止 DATA 步的执行。

你必须在显示之前创建窗口。请参第 381 页的“`WINDOW` 语句”如何创建窗口。用 `DISPLAY` 语句显示的窗口不会成为 SAS 日志或输出文件的一部分。

## 示例

此 DATA 步创建并显示名为 `START` 的窗口。`START` 窗口填充整个屏幕。两行文本均居中。

```
data _null;
window start;
#5 @28 'WELCOME TO THE SAS SYSTEM';
#12 @30 'PRESS ENTER TO CONTINUE';
display start;
run;
```

尽管窗口正在显示，但在窗口关闭之前，DATA 步不会结束。如果窗口关闭，DATA 步将继续执行。

## 另另

语句：
- 第 381 页的“`WINDOW` 语句”

# DM 语句

提交 SAS 程序编辑器、日志或输出。

| 有效位置： | 任意位置 |
| :--- | :--- |
| 类别： | 程序控制 |

## 语法

`DM <window>'command(s)' <CONTINUE>;`

## 参数

`window`

指定活动窗口。

默认值：如果省略窗口名称，SAS 使用编辑器窗口作为默认。

`'command(s)'`

可以是任何窗口命令或编辑器命令，且必须包含引号内。如果你想发布多个命令，请用分号分隔。

`CONTINUE`

导致 SAS 执行 `DM` 语句之后的任何 SAS 语句。例如，指定 Log 将使该窗口变为活动。

## 详细

当 `DM` 语句提交给 SAS 时就会执行。你可以使用此语句修改窗口环境。

## 示例

示例 1：使用 `DM` 语句
- `dm 'color text cyan; command red';`
- `dm log 'clear; pgm; color numbers green' output`
- `dm log 'clear' output`

示例 2：带有 `CONTINUE` 选项的 语句不激活窗口

```
af c=your-program' continue;
data temp;
more SAS statements . . .
run;
```

示例 3：带有 `CONTINUE` 选项的 语句激活窗口

```
af c=your-program' continue;
proc print data=temp;
run;
```

## 语法

```sas
DO;
  ...more SAS statements...
END;
```

## 无参数

使用 `DO` 语句进行简单的 DO 组处理。

## 详细信息

`DO` 语句是 DO 组处理的最简单形式。`DO` 和 `END` 语句之间的语句被称为 DO 组。你可以在 DO 组中嵌套 `DO` 语句。

> 注意：系统的内存能力可能会限制你可以使用的嵌套 `DO` 语句的数量。

简单的 `DO` 语句通常用于 `IF-THEN/ELSE` 语句中，根据 `IF` 条件的真或假值来指定一组要执行的语句。

## 比较

`DO` 语句还有其他三种形式：
- 迭代 `DO` 语句根据索引变量的值，重复执行 `DO` 和 `END` 语句之间的语句。迭代 `DO` 语句可以包含 `WHILE` 或 `UNTIL` 子句。
- `DO UNTIL` 语句在 DO 循环中重复执行语句，直到条件为真，在在每次 DO 循环迭代后检查该条件。
- `DO WHILE` 语句在条件为真时，在 DO 循环中重复执行语句，在每次 DO 循环迭代前检查该条件。

# 示例：使用 DO 语句

在这个简单的组中，只有当 `YEARS` 小于等于 5 时才会执行 `DO` 和 `END` 之间的语句；DO 组中的语句不执行，程序继续执行 `ELSE` 语句之后的赋值语句。

```sas
if years>5 then
do;
  months=years*12;
  put years= months=;
end;
else yrshleft=5-years;
```

## 另另

语句：
- 第 65 页的“`DO Statement, Iterative`”
- 第 68 页的“`DO UNTIL Statement`”
- 第 50 页的“`DO WHILE Statement`”

# DO 语句，迭代

根据索引变量的值，重复执行 `DO` 和 `END` 语句之间的语句。

- 适用范围：`DATA` 步
- 类别：控制
- 类型：可执行

## 语法

```sas
DO index-variable=specification-1 <, ...specification-n>;
  ...more SAS statements...
END;
```

## 参数

索引变量 `Index-variable`

控制 DO 组执行的变量名称。

> 提示：除非指定丢弃它，否则索引变量将包含在创建的数据集中。
> 警告：避免在 DO 组内更改索引变量。

规格 `specification`

表示这种形式的表达式或一系列表达式

```
<TO stop> <BY increment> <WHILE(expression) | UNTIL(expression)>
```

## DO UNTIL 语句

```
DO UNTIL (expression);
...more SAS statements...
END;
```

## 参数

`(expression)`

是任何 SAS 表达式，括在括号中。你必须指定至少一个表达式。

## 详细信息

在 DO 块中的语句执行后，会在循环底部评估表达式。如果表达式为真，则 DO 循环将不再迭代。

> 注意：DO 循环始终至少迭代一次。

## 比较

`DO` 语句还有其他三种形式：
- `DO` 语句是 DO 组处理中最简单的形式
- 迭代 `DO` 语句根据索引变量的值，重复执行 `DO` 和 `END` 语句之间的语句
- `DO WHILE` 语句在条件为真时重复执行 DO 循环中的语句

## 示例：使用 DO UNTIL 语句重复循环

```sas
n=0;
do until (n>=5);
put n=;
n+1;
end;
```

## 另有所涉

语句：
- 第 63 页的“`DO` 语句”
- 第 65 页的“迭代 `DO` 语句”
- 第 70 页的“`DO WHILE` 语句”

# DO WHILE 语句

在条件为真时重复执行 DO 循环中的语句。

| 有效区域： | DATA 步 |
| 类别: | 控制 |
| 类型: | 可执行 |

## 语法

```
DO WHILE (expression);
...more SAS statements...
END;
```

## 参数

`(expression)`

是任何 SAS 表达式，括在括号中。你必须指定至少一个表达式。

## 详细信息

该表达式在 DO 循环中的语句执行之前的循环顶部评估。如果表达式为真，则 DO 循环进行迭代。如果第一次评估时表达式为假，则 DO 循环一次迭代都不进行。

## 比较

`DO` 语句还有其他三种形式：
- `DO` 语句是 DO 组处理中最简单的形式，它指定了一组语句作为单元进行执行，通常作为 `IF-THEN/ELSE` 语句的一部分。
