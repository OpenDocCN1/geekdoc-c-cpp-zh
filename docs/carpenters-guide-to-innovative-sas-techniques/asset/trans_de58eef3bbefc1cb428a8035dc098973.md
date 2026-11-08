

## 12.1.3 在 MEANS 和 SUMMARY 过程中使用预加载格式

与 PROC TABULATE 的情况一样（参见第 12.1.2 节），当 PRELOADFMT 和 EXCLUSIVE 选项与 MEANS 和 SUMMARY 过程一起使用时，它们出现在 CLASS 语句上。

### 将 PRELOADFMT 与 EXCLUSIVE 一起使用

使用 CLASS 语句选项 PRELOADFMT ❶ 和 EXCLUSIVE ❷ 进行预加载，会将分类变量的水平限制为既在格式中又在数据中的水平。本质上，该格式充当过滤器，而无需借助子集 IF 语句或 WHERE 子句。

```sas
title2 'Using the EXCLUSIVE option';
proc summary data=advprdt.demog;
    class symp / preloadfmt ❶
                  exclusive ❷;
    var ht;
    output out=withexclusive
           mean=meanHT;
    format symp $symp.;
    run;
proc print data=withexclusive;
    run;
```

| 观测 | symp | _TYPE_ | _FREQ_ | meanHT |
|---:|---|---:|---:|---:|
| 1 |  | 0 | 18 | 66.8889 |
| 2 | 嗜睡 | 1 | 4 | 67.5000 |
| 3 | 咳嗽 | 1 | 10 | 66.8000 |
| 4 | 跛行 | 1 | 4 | 66.5000 |

请注意，与 PROC TABULATE 不同，这种 CLASS 语句选项组合不会为数据中不存在的 SYMP 格式化值（SYMP='00'）插入一行。要使用 MEANS 和 SUMMARY 过程添加此水平，还必须包括 COMPLETETYPES 选项。

### 将 COMPLETETYPES 与 PRELOADFMT 和 EXCLUSIVE 一起使用

PROC 语句选项 COMPLETETYPES（此选项在第 7.10 节中介绍）将与 PRELOADFMT 和 EXCLUSIVE 选项交互。由于这种交互，不在数据中但在格式中的分类变量水平现在会包含在汇总中。但是，不在格式中的水平不会包含在表中。

```sas
title2 'With EXCLUSIVE and COMPLETETYPES';
proc summary data=advprdt.demog;
    class symp / preloadfmt
                  exclusive;
    var ht;
    ... code not shown . . . .
```

| 观测 | symp | _TYPE_ | _FREQ_ | meanHT |
|---:|---|---:|---:|---:|
| 1 |  | 0 | 18 | 66.8889 |
| 2 | 未指定 | 1 | 0 | . |
| 3 | 嗜睡 | 1 | 4 | 67.5000 |
| 4 | 咳嗽 | 1 | 10 | 66.8000 |
| 5 | 跛行 | 1 | 4 | 66.5000 |

现在，SYMP 的“未指定”水平会出现在报告中，即使它不在数据中（_FREQ_=0）。

### 不使用 EXCLUSIVE 而使用 COMPLETETYPES

当使用 COMPLETETYPES 选项而不使用 EXCLUSIVE 选项时，分类变量的所有水平都会出现，无论它是在数据中还是仅在预加载格式中。

```sas
title2 'Two Classification Variables';
title3 'COMPLETETYPES Without EXCLUSIVE';
proc summary data=vrpt.demo completetypes;
    class symp sex / preloadfmt ;
    var ht;
    output out=twoclass mean=ht;
    format symp $symp.
           sex $genderu.;
run;
proc print data=twoclass;
run;
```

这里显示了由两个分类变量 SYMP 和 SEX（它们具有预加载格式）生成的表格的一部分。请注意，每个不与数据关联的格式水平都会出现，未格式化水平也会出现（此部分表格仅显示 SYMP='04'）。

**12.1.3 使用预加载格式与 MEANS/SUMMARY**  
**两个分类变量**  
**不使用 EXCLUSIVE 的 COMPLETETYPES**

| 观测 | symp | sex | _TYPE_ | _FREQ_ | meanHT |
|---:|---|---|---:|---:|---:|
| 1 |  |  | 0 | 65 | 67.2000 |
| 2 |  | 女性 | 1 | 29 | 65.0690 |
| 3 |  | 男性 | 1 | 36 | 68.9167 |
| 4 |  | 未知 | 1 | 0 | . |
| 5 | 04 | 未指定 | 2 | 0 | . |
| 6 | 04 | 嗜睡 | 2 | 4 | 67.5000 |
| 7 | 04 | 咳嗽 | 2 | 10 | 66.8000 |
| 8 | 04 | 跛行 | 2 | 4 | 66.5000 |
| 9 | 04 |  | 2 | 13 | 68.6923 |

## 12.2 使用 PICTURE 格式做更多事情

尽管一般来说 PICTURE 格式只是名义上的高级主题，但它们远未被充分利用，而且 PICTURE 格式特有的一些概念常被误解。

PICTURE 语句用于构建本质上是由零、九和其他也要显示的字符组成的模板。零和九用作占位符。九表示该位置必须放置数字，即使该数字为零。零占位符表示如果数字非零，则在该位置放置数字（嵌入的零会显示）。

### 另请参阅

书籍 *PROC FORMAT 的力量*（Jonas Bilenas，2005）是了解一些更入门的 PICTURE 格式主题的良好来源。

PICTURE 语句的文档清晰描述了将格式应用于要格式化的值的过程。在处理小数值之前，应充分理解这一应用过程。

### 12.2.1 日期指令和 DATATYPE 选项

PICTURE 语句上的 DATATYPE= 选项可用于构建特定于日期的格式。此选项允许使用“指令”，这些指令告诉 PICTURE 语句如何相对于要解释的数据类型进一步构造或格式化该值。

指令是单个区分大小写的字母，用于指示 DATE、TIME 或 DATETIME 值的特定部分。有超过 15 个指令，并且用作指令的字母大小写很重要：

| 指令 | 含义 | 指令 | 含义 |
|---|---|---|---|
| Y | 年 | M | 分钟 |
| m | 月 | S | 秒 |
| d | 日 | b | 月份缩写 |
| H | 小时 | B | 月份名称 |

在 PICTURE 语句中，指令前面有一个百分号（%），它充当转义字符。使用单引号可防止将 % 解释为宏语言触发符。

以下格式用于以可在 DB2 中使用的格式显示 SAS 日期时间值。

```sas
proc format;
   picture dbdate
      other = '%Y-%0m-%0d:%0H:%0M:%0S' (datatype=datetime); ❶ ❷
run;

data _null_;
   now = '11sep2010:15:05:27'dt;
   put now=;
   put now= dbdate.;
   call symputx('selldate',now); ❸
run;
```

❶ 与其他 PICTURE 格式一样，零可用作占位符。

❷ DATATYPE 选项决定如何解释传入值。选项值指示该格式将用于的数据类型。这些数据类型包括：

- DATE：SAS 日期值
- TIME：SAS 时间值
- DATETIME：SAS 日期时间值
- DATETIME_UTIL：专用于公用事业行业的 SAS 日期时间值（SAS 9.3）

日志显示：

```text
now=1599836727
now=2010-09-11:15:05:27
```

在上面的 DATA 步中创建了宏变量 &SELLDATE ❸。格式化后，该宏变量可用于将此 DATETIME 值写入要传递到 DB2 服务器的 SQL 代码中。%SYSFUNC 调用 PUTN 函数，该函数将呈现格式化值。

```sas
%put %sysfunc(putn(&selldate,dbdate.));
```

由于指令种类繁多且 DATATYPE 选项可用，生成的格式具有很大灵活性。这意味着可以为三种日期时间数据值类型中的任何一种生成格式。通过为 MONNAME. 格式（只能用于 DATE 值）创建替代格式，可以展示这种灵活性。这里创建的 MONTHNAME. 和 MONTHABB. 格式用于 DATETIME 值。

```sas
proc format;
  picture monthname
    other = '%B' (datatype=datetime); ❶
  picture monthabb
    other = '%b' (datatype=datetime); ❷
run;

data _null_;
  now = '11sep2010:15:05:27'dt;
  put now=;
  put now= monthname.;
  put now= monthname3.; ❸
  put now= monthabb.;
run;
```

- ❶ %B 指令返回月份名称。定义格式时，请确保为最长的月份（September）留出足够空间，否则月份名称可能会被截断。
- ❷ 小写 %b 指令返回月份名称的前三个字母的大写形式。同样要留出三个空格（包括指令和转义字符）。
- ❸ 如果希望使用混合大小写的缩写月份名称，可以在完整名称的格式中包含宽度值。

```text
now=1599836727
now=September ❹
now=Sep ❺
now=SEP ❻
```

### SAS 9.3 日期指令增强

在 SAS 9.3 之前，小数秒会被截断（即使对 PICTURE 格式应用了 ROUND 选项）。从 SAS 9.3 开始，小数秒会被舍入。尽管通常关系不大，但这可能会改变距午夜半秒以内的时间值所对应的日期。

```sas
proc format;
  picture myDayT (round)
    low - high = '%0d%b%0Y:%0H:%0M:%0S' (datatype=datetime)
  ;
run;
```

|  | 显示值 |  |
|---|---|---|
| 日期时间常量 | MYDAYT.（SAS 9.3 之前） | MYDAYT.（SAS 9.3 及之后） |
| '01apr2011:12:34:56.7'dt | 01APR2011:12:34:56 | 01APR2011:12:34:57 |
| '01apr2011:23:59:59.7'dt | 01APR2011:23:59:59 | 02APR2011:00:00:00 |

公用事业行业通常希望将午夜日期引用为 24:00:00 而不是 00:00:00。新的 DATATYPE= 值 DATETIME_UTIL 允许这样做。

```sas
proc format;
  picture ymdtme (default=19)
    other='%Y-%0m-%0d %0H:%0M:%0S' (datatype=datetime_util);
run;
```

