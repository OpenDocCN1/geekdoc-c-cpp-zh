

# 按分组汇总数据

### 第 1 步 初始化

```sas
data deptsals(keep=Dept DeptSal);
set SalSort;
by Dept;
if First.Dept then DeptSal=0;
<additional SAS statements>
run;
```

> 当 First.Dept 的值为 1 时，该条件被视为真。

# 按分组汇总数据

### 第 2 步累加

```sas
data deptsals(keep=Dept DeptSal);
set SalSort;
by Dept;
if First.Dept then DeptSal=0;
DeptSal+Salary;
<additional SAS statements>
run;
```

# 按分组汇总数据

### 第 3 步 输出

| Dept | Salary | DeptSal |
|---|---|---|
| ADMIN | 20000 | 20000 |
| ADMIN | 100000 | 120000 |
| ADMIN | 50000 | 170000 |
| ENGINR | 25000 | 25000 |
| ENGINR | 20000 | 45000 |
| ENGINR | 23000 | 68000 |
| ENGINR | 27000 | 95000 |
| FINANC | 10000 | 10000 |
| FINANC | 12000 | 22000 |

# 按分组汇总数据

### 第 3 步 输出

```sas
data deptsals(keep=Dept DeptSal);
set SalSort;
by Dept;
if First.Dept then DeptSal=0;
DeptSal+Salary;
if Last.Dept; /* 如果 last.dept=1 则输出，
run;
```

子集 IF 语句定义了一个观测值必须满足的条件，才能被 DATA 步进一步处理。

# 按分组汇总数据

```sas
proc print data=deptsals noobs;
run;
```

PROC PRINT 输出

| Dept | DeptSal |
|---|---|
| ADMIN | 410000 |
| ENGINR | 163000 |
| FINANC | 318000 |
| HUMRES | 181000 |
| SALES | 373000 |

部分 SAS 日志

> NOTE: 从数据集 WORK.ALSORT 中读取了 39 个观测值。
NOTE: 数据集 WORK.DEPTSALS 包含 5 个观测值和 2 个变量。

# 3.04 多选题

在 DATA 步中必须发生什么操作才能按分组汇总数据？（选择所有适用项。）

- a. 对输入数据排序。
- b. 在每个 BY 组开始时将累加变量置零。
- c. 增加累加变量。
- d. 输出每个 BY 组的最后一个观测值。

# 3.2 组数据的累加总和

## 业务场景

orion.projsals 中列出的每个员工都被分配到一个特殊项目。业务分析师希望查看每个特殊项目每个部门的薪资总和。

## 部分 orion.projsals

| Employee ID | Salary | Proj | Dept |
|---|---|---|---|
| 110004 | 42000 | EZ | HUMRES |
| 110009 | 34000 | WIN | ENGINR |
| 110011 | 27000 | WIN | FINANC |
| 110036 | 20000 | WIN | ENGINR |
| 110037 | 19000 | EZ | ENGINR |
| 110045 | 19000 | EZ | FINANC |
| 110077 | 27000 | CAP1 | ADMIN |
| 110097 | 20000 | EZ | ADMIN |
| 110107 | 31000 | EZ | ENGINR |

## 业务场景：预期输出

创建一个新数据集 pdsals，显示每个特殊项目每个部门的员工人数和薪资总和。

## 部分 pdsals

| Proj | Dept | Sal | Num Emps |
|---|---|---|---|
| CAP1 | ADMIN | 70000 | 2 |
| EZ | HUMRES | 80000 | 3 |
| EZ | ENGINR | 109000 | 4 |
| EZ | FINANC | 122000 | 3 |
| EZ | HUMRES | 178000 | 5 |
| NGEN | ADMIN | 37000 | 2 |

# 按项目和部门排序

这与之前的业务场景类似，但现在数据必须按多个 BY 变量：**Proj** 和 **Dept** 进行排序。

```sas
proc sort data=orion.projsals
out=projsort;
by Proj Dept;
run;
```

![](img/d3bde6e6ab06b1fc622215d982111742_107.png)

# 按项目和部门排序

```sas
proc print data=projsort noobs;
var Proj Dept;
run;
```

部分 PROC 输出（总观测数）

| Proj | Dept | Salary |
|---|---|---|
| CAP1 | ADMIN | 27000 |
| CAP1 | ADMIN | 43000 |
| EZ | ADMIN | 20000 |
| EZ | ADMIN | 31000 |
| EZ | ENGINR | 19000 |

# 3.2 组数据的累加总和

## 方案

DATA 步必须在 BY 语句中同时包含 Proj 和 Dept。

```sas
data pdsals;
by Proj Dept;
set projsort;
if First.Dept then DeptSal=0;
DeptSal+Salary;
run;
```

当按项目分组时，DATA 步发生了什么？

![](img/d3bde6e6ab06b1fc622215d982111742_107.png)

# 第一次迭代的值

| Proj | Dept | DeptSal |
|---|---|---|
| CAP1 | ADMIN | 27000 |
| CAP1 | ADMIN | 43000 |
| EZ | ADMIN | 20000 |
| EZ | ADMIN | 31000 |
| EZ | ENGINR | 19000 |

# 第二次迭代的值

| Proj | Dept | DeptSal |
|---|---|---|
| CAP1 | ADMIN | 27000 |
| CAP1 | ADMIN | 43000 |
| EZ | ADMIN | 20000 |
| EZ | ADMIN | 31000 |
| EZ | ENGINR | 19000 |

# 第三次迭代的值

| Proj | Dept | DeptSal |
|---|---|---|
| CAP1 | ADMIN | 27000 |
| CAP1 | ADMIN | 43000 |
| EZ | ADMIN | 20000 |
| EZ | ADMIN | 31000 |
| EZ | ENGINR | 19000 |

# 第四次迭代的值

| Proj | Dept | DeptSal |
|---|---|---|
| CAP1 | ADMIN | 27000 |
| CAP1 | ADMIN | 43000 |
| EZ | ADMIN | 20000 |
| EZ | ADMIN | 31000 |
| EZ | ENGINR | 19000 |

# 第五次迭代的值

| Proj | Dept | DeptSal |
|---|---|---|
| CAP1 | ADMIN | 27000 |
| CAP1 | ADMIN | 43000 |
| EZ | ADMIN | 20000 |
| EZ | ADMIN | 31000 |
| EZ | ENGINR | 19000 |

