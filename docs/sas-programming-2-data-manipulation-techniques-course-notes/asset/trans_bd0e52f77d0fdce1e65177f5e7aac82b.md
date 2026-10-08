

## 3.3 答案 3-41

```sas
title '零售销售额达到 $100 或以上的客户';
proc print data=work.discount1 noobs;
format TotSales dollar11.2;
run;
title;
```

## 7 识别每组数据中的极值

```sas
proc sort data=orion.customer_dim out=work.customers;
  by Customer_Type;
run;

data work.agecheck;
  set work.customers;
  by Customer_ID;
  retain oldest youngest o_ID y_ID;
  if first.Customer_Type=1 then do
    oldest=Customer BirthDate;
    youngest=Customer BirthDate;
    o_ID=Customer_ID;
    y_ID=Customer_ID;
  end;
  if Customer BirthDate < oldest then do
    o_ID=Customer_ID;
    oldest=Customer BirthDate;
  end;
  else if Customer BirthDate > youngest then do
    y_ID=Customer_ID;
    youngest=Customer BirthDate;
  end;
  if last.Customer_Type=1 then do
    age=(youngest-oldest)/365.25;
    output;
  end;
  keep Customer_Type oldest youngest o_ID y_ID ageange;
```

```sas
title '每个客户类型最老和最的客户';
proc print data=work.agecheck noobs;
format youngest date9. ageange 5.1;
ntitle;
```

### 替代方案

```sas
proc sort data=orion.customer_dim out=work.customers;
  by Customer_Type Customer_BirthDate;
run;

data work.agecheck;
  set work.customers;
  by Customer_Type;
  /* 可以缩进而不是使用：by Customer_Type Customer_BirthDate;
     在这个 DATA 步中，任何 BY 语句均有效。 */
  retain oldest youngest o_ID y_ID;
  if first.Customer_Type=1 then do
    o_ID=Customer_ID;
    oldest=Customer_BirthDate;
  end;
  /* 由于已经按 Customer_BirthDate 排序，我们知道
     每个 BY 组中的第一个客户是最老的（具有
     最小的 SAS 生日日期值）。 */
  if last.Customer_Type=1 then do
    y_ID=Customer_ID;
    youngest=Customer_BirthDate;
    agerange=(youngest-oldest)/365.25;
    output;
  end;
  /* 类似的情况：每个 BY 组中的最后一个将是最年轻的。 */
  keep Customer_Type oldest youngest o_ID y_ID agarange;
run;

title '每个客户类型最老和最的客户';
proc print data=work.agecheck noobs;
format oldest youngest date9. agarange 5.1;
run;
title;
```

## 学生活动答案（投票/测验）

### 3.01 简答式问答 – 正确答案

打开并提交 p203a1 中的程序。这会为 MthDte 创建正确的值吗？

```sas
data mnthDte;
  set orion.apales;
  MthDte=MthDte+SaleAmt;
run;
```

部分 orion.apales：

| SaleDate | Sale Amt | MthDte |
|---|---|---|
| 01APR2011 | 49.49 | 49.49 |
| 02APR2011 | 96.50 | 145.99 |
| 03APR2011 | 94.97 | 240.96 |
| 04APR2011 | 56.59 | 297.55 |

不，该程序创建 MthDte 带有缺失值。

### 3.02 多选题投票 – 正确答案

SaleAmt 的缺失值对 MthDte 产生了什么影响？

- a. 缺失值被忽略，MthDte 值不受影响。
- b. 缺失值导致 DATA 步停止。
- c. 缺失值导致 MthDte 的后续值被设置为缺失值。

### 3.03 简答式问答 – 正确答案

当 DATA 步按箭头方向处理观测值时，First.Dept 和 Last.Dept 的值是多少？

| Dept | Salary |
|---|---|
| ADMIN | 20000 |
| ADMIN | 10000 |
| ADMIN | 50000 |
| ENGINR | 25000 |
| FINANC | 10000 |
| FINANC | 12000 |

First.Dept 和 Last.Dept 均为 1。这当一个组仅包含一个观测值时发生。

### 3.04 多选题投票 – 正确答案

在 DATA 步中必须发生什么才能按分组汇总数据？（选择所有适用项。）

- b. 在每个 BY 组开始时将累积变量设置为零。
（注意：选项 a 不适用，因为排序是通过 PROC SORT 完成的，而不是在 DATA 步中。）

### 3.05 简答式问答 – 正确答案

当 DATA 步按箭头方向处理观测值时，First.Proj 和 Last. 变量的值是多少？

| Proj | Dept | First.Proj |
|---|---|---|
| A | ADMIN | |
| A | ADMIN | |
| A | ADMIN | |
| B | ENGINR | |
| C | FINANC | |
| C | FINANC | |

