
`BASE=` 指定要添加观测值的数据集。
`DATA=` 指定包含要添加到基础数据集中的观测值的数据集。

# APPEND 过程

要求：

- 每一步中同时只能使用两个数据集。
- 不读取基础数据集中的观测值。
- 基础数据集描述部分中的变量信息不能发生更改。

## 10.2 追加数据集（自学）

### 业务场景

`Emps` 是一个主数据集，包含了在 2006 年和 2007 年入职的员工。

### Emps

| First | Gender | HireYear |
|---|---|---|
| Stacey | F | 2006 |
| Gloria | F | 2007 |
| James | M | 2007 |

### 业务场景

`Emps` 是一个主数据集，包含了 2006 年和 2007 年入职的员工。

### Emps2008

| First | Gender | HireYear |
|---|---|---|
| Brett | M | 2008 |
| Renee | F | 2008 |

### Emps

| First | Gender | HireYear |
|---|---|---|
| Stacey | F | 2006 |
| Gloria | F | 2007 |
| James | M | 2007 |

### Emps2009

| First | HireYear |
|---|---|
| Sara | 2009 |
| Dennis | 2009 |

### Emps2010

需要追加 2008 年、2009 年和 2010 年入职的员工。

| First | HireYear | Country |
|---|---|---|
| Rose | 2010 | Spain |
| Eric | 2010 | Spain |

## 10.02 测验

在追加三个数据集后，`Emps` 中会有多少个观测值？

| Emps2008 |
| First | Gender | HireYear |
|---|---|---|
| Brett | M | 2008 |
| Renee | F | |

| Emps |
| First | Gender | HireYear |
|---|---|---|
| Stacey | F | 2006 |
| Gloria | F | 2007 |
| James | M | 2007 |

| Emps2009 |
| First | HireYear |
|---|---|
| Sara | 2009 |
| Dennis | 2009 |

| Emps2010 |
| First | HireYear | Country |
|---|---|---|
| Rose | 2010 | Spain |
| Eric | 2010 | Spain |

## 10.03 测验

在追加三个数据集后，`Emps` 中会有多少个变量？

| Emps2008 |
| First | Gender | HireYear |
|---|---|---|
| Brett | M | 2008 |
| Renee | F | |

| Emps |
| First | Gender | HireYear |
|---|---|---|
| Stacey | F | 2006 |
| Gloria | F | 2007 |
| James | M | 2007 |

| Emps2009 |
| First | HireYear |
|---|---|
| Sara | 2009 |
| Dennis | 2009 |

| Emps2010 |
| First | HireYear | Country |
|---|---|---|
| Rose | 2010 | Spain |
| Eric | 2010 | Spain |

## 结构相似的数据集

| First | Gender | HireYear | First | Gender | HireYear |
|---|---|---|---|---|---|
| Stacey | F | 2006 | Brett | M | 2008 |
| Gloria | F | 2007 | Renee | F | 2008 |
| James | M | 2007 | | | |

数据集包含相同的变量。

```
proc append base=Emps
data=Emps2008;
run;
```

# 结构相似的数据集

```
84 proc append base=Emps
85 data=Emps2008;
86 run;
```

NOTE: 将 `WORK.EMPS2008` 追加到 `WORK.EMPS`。
NOTE: 从数据集 `WORK.EMPS2008` 读取了 2 个观测值。
NOTE: 添加了 2 个观测值。
NOTE: 数据集 `WORK.EMPS` 有 5 个观测值和 3 个变量。

| First | Gender | HireYear |
|---|---|---|
| Stacey | F | 2006 |
| Gloria | F | 2007 |
| James | M | 2007 |
| Brett | M | 2008 |
| Renee | F | 2008 |

## 结构相似的数据集

| First | Gender | HireYear | First | HireYear |
|---|---|---|---|---|
| Stacey | F | 2006 | Sara | 2009 |
| Gloria | F | 2007 | Dennis | 2009 |
| James | M | 2007 | | |
| Brett | M | 2008 | | |
| Renee | F | 2008 | | |

`BASE=` 数据集包含一个在 `DATA=` 数据集中不包含的变量。

```
proc append base=Emps
data=Emps2009;
run;
```

# 结构相似的数据集

```
90 proc append base=Emps
91 data=Emps2009;
92 run;
```

NOTE: 将 `WORK.EMPS2009` 追加到 `WORK.EMPS`。
WARNING: 在 `DATA` 中未找到变量 `Gender`。
NOTE: 从数据集 `WORK.EMPS2009` 读取了 2 个观测值。
NOTE: 添加了 2 个观测值。
NOTE: 数据集 `WORK.EMPS` 有 7 个观测值和 3 个变量。

| First | Gender | HireYear |
|---|---|---|
| Stacey | F | 2006 |
| Gloria | F | 2007 |
| James | M | 2007 |
| Brett | M | 2008 |
| Renee | F | 2008 |
| Sara | | 2009 |
| Dennis | | 2009 |

## 结构相似的数据集

| First | Gender | HireYear | First | HireYear | Country |
|---|---|---|---|---|---|
| Stacey | F | 2006 | Rose | 2010 | Spain |
| Gloria | F | 2007 | Eric | 2010 | Spain |
| James | M | 2007 | | | |
| Brett | M | 2008 | | | |
| Renee | F | 2008 | | | |
| Sara | | 2009 | | | |
| Dennis | | 2009 | | | |

`DATA=` 数据集包含一个在 `BASE=` 数据集中不包含的变量。

```
proc append base=Emps
data=Emps2010;
run;
```

# 结构相似的数据集

- 96 `proc append base=Emps`
- 97 `data=Emps2010;`
- 98 `run;`

NOTE: 将 `WORK.EMPS` 追加到 `WORK.EMPS`。
WARNING: 在 `BASE` 文件未找到变量 `Country`。该变量将不会添加到 `BASE` 文件。
WARNING: 在 `DATA` 文件未找到变量 `Gender`。
ERROR: 由于上述异常未进行追加。使用 `FORCE` 选项追加这些文件。
NOTE: 添加了 0 个观测值。
NOTE: 数据集 `WORK.EMPS` 有 7 个观测值和 3 个变量。
NOTE: 由于上述错误未处理语句。
NOTE: SAS 系统由于错误停止此步骤。

## 结构相似的数据集

当 `DATA=` 数据集包含 `BASE=` 数据集中不包含的变量时，`FORCE` 选项强制追加观测值。
`FORCE` 选项的一般形式为：

```
PROC APPEND BASE = SAS-data-set
DATA = SAS-data-set FORCE;
RUN;
```

`FORCE` 选项会导致额外的变量删除并发出警告消息。

```
proc append base=Emps
data=Emps2010 force;
run;
```

当 `DATA=` 数据集包含以下变量时，需要 `FORCE` 选项：

- 不在 `BASE=` 数据集中
- 类型与 `BASE=` 数据集中的变量不同
- 比 `BASE=` 数据集中的变量长

如果 `DATA=` 数据集的变量长度比 `BASE=` 数据集长，SAS 将截断 `DATA=` 数据中的值以适应 `BASE=` 数据集指定的长度。

如果 `DATA=` 数据集的变量类型与 `BASE=` 数据集不同，SAS 将 `DATA=` 数据集中变量的所有值替换为缺失值，并保留 `BASE=` 数据集中指定的变量类型。

![](img/1698e3a9754d6895ff5297aae8fd042_461_0.png)

## 10.2 追加数据集（自学） 10-15

### 结构相似的数据集

```
100 proc append base=Emps
101     data=Emps2010 force;
102     run;
```

NOTE: 将 `WORK.EMPS2010` 追加到 `WORK.EMPS`。
WARNING: 在 `BASE` 文件未找到变量 `Country`。该变量将不会添加到 `BASE` 文件。
WARNING: 在 `DATA` 文件未找到变量 `Gender`。
NOTE: 指定了 `FORCE`，因此会发生删除/截断。
NOTE: 从数据集 `WORK.EMPS2010` 读取了 2 个观测值。
NOTE: 添加了 2 个观测值。
NOTE: 数据集 `WORK.EMPS` 有 9 个观测值和 3 个变量。

![](img/1698e3a9754d6895ff5297aae8fd042_462_0.png)

## 结构相似的数据集

| First | Gender | HireYear |
|---|---|---|
| Stacey | F | 2006 |
| Gloria | F | 2007 |
| James | M | 2007 |
| Brett | M | 2008 |
| Renee | F | 2008 |
| Sara | | 2009 |
| Dennis | | 2009 |
| Rose | | 2010 |
| Eric | | 2010 |

![](img/1698e3a9754d6895ff5297aae8fd042_462_1.png)

## 结构相似的数据集

| 情况 | 操作 |
| --- | --- |
| `BASE=` 数据集包含一个在 `DATA=` 数据集中不包含的变量。 | 追加观测值，但 `DATA=` 数据集的对应变量将为缺失值。在这种情况下不需要 `FORCE` 选项。 |
| `DATA=` 数据集包含一个 `BASE=` 数据集中不包含的变量。 | 在 `PROC APPEND` 语句中使用 `FORCE` 选项强制合并文件。语句会删除额外的变量并发出警告。 |

## 10.04 测验

如果再次提交该程序，`Emps` 中会有多少个观测值？

再次提交该程序将向 `Emps` 添加六个观测值，结果总共有九个观测值。

```
proc append base=Emps
  data=Emps2008; 3 obs + 2 obs = 5 obs
run;

proc append base=Emps
  data=Emps2009; 5 obs + 2 obs = 7 obs
run;

proc append base=Emps
  data=Emps2010 force; 7 obs + 2 obs = 9 obs
run;
```
