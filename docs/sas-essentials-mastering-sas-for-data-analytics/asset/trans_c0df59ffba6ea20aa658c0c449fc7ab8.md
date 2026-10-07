

## 日期和时间函数

年份 15 被解释为 2015 年，两位年份 20 或更高被解释为 20 世纪（例如，两位年份 21 被解释为 1921 年）。你可以在程序中使用 `YEARCUTOFF=19XX` 语句更改此默认值。例如，如果你指定 `YEARCUTOFF=1925`，则在 00 到 24 之间的两位年份将被解释为 21 世纪（例如，21 被解释为 2021），而从 25 到 99 的将被解释为 20 世纪（例如，44 被解释为 1944）：

```
DATDIF(date, edate, basis)
```

返回两个日期之间的天数。Basis（基）为 '30/360'、'ACT/ACT'、'ACT/360' 或 'ACT/365'。BASIS 选项告诉 SAS 使用哪种天数计数方法（这些是投资、会计和其他学科中使用的某些天数计算约定）。

- '30/360' 表示使用每月 30 天，每年 360 天。
- 'ACT/ACT' 表示使用实际天数。
- 'ACT/360' 表示使用每月实际天数，每年 360 天。
- 'ACT/365' 表示使用每月的实际天数，每年 365 天。

例如，

```
DAYS=DATDIF('07JUL1976d', '01JAN2013d', '30/360');
```

返回值（天数）为 13,134，而

```
DAYS=DATDIF('07JUL1976d', '01JAN2013d', 'ACT/ACT');
```

返回值（天数）为 13,327。这些整数值可以通过对变量应用如下日期格式以日期可读的方式显示：

```
FORMAT DAYS MDDDY10 ;
```

### 表 B.4 日期和时间函数

| 函数 | 描述 |
| :--- | :--- |
| DATDIF (date, edate, basis) | 使用指定的基准方法（前文描述）计算两个日期之间的差 |
| DATE () | 返回当前日期（SAS 日期值） |
| DATEPART (datetime) | 从 SAS 日时间变量中提取并仅返回日期 |
| DATETIME () | 从计算机的日期时间值返回当前的日期和时间 |
| DAY (date) | 从 SAS 日期中返回月份中的某一天（1 到 31 之间的值） |
| DAY () | 从函数中的参数日期、小时、分钟和秒返回 SAS 日时间值 |

### 表 B.4（续）

| 函数 | 描述 |
| --- | --- |
| HMS (hour, minute, second) | 从时、分、秒创建 SAS 时间值 |
| HOUR (<time | datetime>) | 返回 SAS 时间或日期时间变量的小时值 |
| INTCK(`interval', from, to) | 返回给定时间跨度的时间间隔数，其中 interval 可以是：<br>**日期时间间隔：** DTDAY, DTWEEK, DTWEEEK, TTENDAY, SEMIMONTH, DMONTH, DTQTR, DTSEMIYEAR, DTYEAR <br>**日期间隔：** DAY, WEEKDAY, WEEK, TEND, SEMIMONTH, MONTH, QTR, SEMIYEAR, YEAR <br>**时间间隔：** HOUR, MINUTE, SECOND <br>例如：<br>WKS=INTCK('WEEK', '07JUL1976'd, '01JAN2013'd) |
| INTNX(`interval', start-from, increment,< <alignment>`) | 通过指定的间隔推进日期、时间或日期时间值，并返回日期、时间或日期时间值——参见上面的间隔 |
| MDY (month, day, year) | 从月、日、年创建并返回 SAS 日期 |
| MINUTE (<time | datetime>) | 从 SAS 时间或日期时间变量中提取并返回分钟值（1–60） |
| MONTH (date) | 从 SAS 日期值中提取并返回月份（1–12） |
| QTR (date) | 从 SAS 日期值中提取并返回年的季度（1–4） |
| SECOND (<time | datetime>) | 从 SAS 时间或日期时间值中提取并返回秒（1–60） |
| TIME () | 返回当前时间作为日期时间值（来自计算机系统钟） |
| TIMEPART (datetime) | 从 SAS 日时间变量中提取并返回时间值 |
| TODAY () | 返回当前日期作为 SAS 日期（来自计算机系统钟） |
| WEEKDAY (date) | 从 SAS 日期值中提取并返回星期（1–7） |
| YEAR (date) | 从 SAS 日期值中提取并返回年份（如 2019） |
| YRDIF (startdate, enddate, basis) | 返回两个日期之间的差。Basis 为 30/360、'ACT/CT'、'ACT/360' 或 'ACT/365。（参见上文 DTDIF 中这些值的描述） |
| YYQ (date) | 从 SAS 日期值中提取并返回年的季度（1–4） |

## 实战示例

1. 要计算两个日期之间的天数，使用 DATDIF 函数。例如，如果你想计算 1976 年 7 月 7 日到 2013 年 1 月 1 日之间的天数，使用 30/360 基准：

```
DAYS=DATDIF('07JUL1976d', '01JAN2013d', '30/360');
```

返回值（天数）为 13,134，而

```
DAYS=DATDIF('07JUL1976d', '01JAN2013d', 'ACT/ACT');
```

返回值（天数）为 13,327。这些整数值可以通过对变量应用如下日期格式以日期可读的方式显示：

```
FORMAT DAYS MDDDY10 ;
```

2. 要计算两个日期之间的周数，使用 INTCK 函数。例如，如果你想计算 1976 年 7 月 7 日到 2013 年 1 月 1 日之间的周数：

```
WKS=INTCK('WEEK', '07JUL1976'd, '01JAN2013'd);
```

3. 要从日期中提取月份和日，使用 MONTH 和 DAY 函数。例如，如果你想从 1976 年 7 月 7 日提取月份和日：

```
M=MONTH('07JUL1976d');
D=DAY('07JUL1976d');
```

## 附录 B：SAS 函数引用

### 表 B.5 使用日期和时间函数

| 观测值 | 日期 | 时间 | 日时间 | 秒 | 秒 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 11/10/2016 | 13:00 | 10NOV2016:13:00 | 48 | 48 |
| 2 | 12/12/2016 | 09:20 | 12DEC2016:09:20 | 23 | 23 |

### B.5 字符函数

字符函数允许你处理文本。当你必须从文本中提取信息、需要从多个信息片段创建新的文本值或需要“清理”文本值以便进行数据分析时，这些函数是非常关重要的。

表 B.6 列出了用于处理字符变量的一些函数。

### 表 B.6 字符函数

| 函数 | 描述 |
| :--- | :--- |
| CAT(text1, text2, ...) | 拼接文本但不移除首尾空格。CAT 移除首尾空格，CATT 移除尾部空格。例如， |
| CAT(text1, text2, ...) | RESULT=CAT("GEORGE", "WASHINGTON"); 返回 GEORGE WASHINGTON，且例如， |
| CATT(text1, text2, ...) | RESULT=CATT("GEORGE", "WASHINGTON"); 返回 GEORGEWASHINGTON |
| CATX(separator, text1, text2, ...) | 移除首尾空格并在连接的组件之间插入分隔符。例如，RESULT = CATX(":", "GEORGE", "WASHINGTON"); 返回 :WASHINGTON |
| COMPBL(text) | 移除字符串中单词之间的多个空格 |
| COMPRESS(text<characters-to-remove>) | 从字符串中移除指定的字符 |
| FIND(text, text-tofind, <modifiers>, <start>) | 从文本移除移除。在文本中查找文本的实例。Start 是可选值，modifiers 是 I 忽略大小写和 T 忽略空格。例如，RESULT=FIND("aBcDef", "DEF", "I"); 返回值 4，因为 DEF 从 ABCDEF 的字符开始（且忽略大小写）。如果未找到匹配，则返回值 0 |

