
将数据集从宽结构转换为窄结构可以简化此任务。

![](img/d3bde6e6ab06b1fc622215d982111742_352_0.png)

![](img/d3bde6e6ab06b1fc622215d982111742_352_1.png)

![](img/d3bde6e6ab06b1fc622215d982111742_352_2.png)

![](img/d3bde6e6ab06b1fc622215d982111742_352_3.png)

# 业务场景：考虑因素

重构输入数据集，并为每个非空的季度捐款创建一个单独的观测。

| Employee_ID | Qtr1 | Qtr2 | Qtr4 | 支付方式 |
|---|---|---|---|---|
| 120265 | - | - | 25 | 现金或支票 |
| 120267 | 18 | 15 | 15 | 工资扣款 |
| 120269 | 20 | 15 | 20 | 工资扣款 |

| Employee_ID | 周期 | 金额 |
|---|---|---|
| 120265 | Qtr4 | 25 |
| 120267 | Qtr1 | 15 |
| 120267 | Qtr2 | 15 |
| 120267 | Qtr3 | 15 |
| 120269 | Qtr1 | 20 |
| 120269 | Qtr2 | 20 |
| 120269 | Qtr3 | 20 |
| 120269 | Qtr4 | 20 |

- 输出数据集 `rotate` 应该只包含 `Employee_ID`、`Period` 和 `Amount`。

# 旋转 SAS 数据集

下面的 `DATA` 步骤旋转输入数据集，并且如果某个季度有捐款，则输出一个观测值。

```sas
data rotate (keep=Employee_Id Period Amount);
set orion.employee_donations
  (drop=recipients paid_by);
  array contrib(4) qtr1-qtr4;
  do i=1 to 4;
  if contrib(i) != . then do;
    Period=cats("Qtr",i);
    Amount=contrib(i);
    output;
  end;
run;
```

## 执行：旋转 SAS 数据集

```sas
data rotate (Keep=Employee_Id Period Amount);
set orion.employee_donations
  (drop=recipients paid by);
  array contrib(4) qtr1-qtr4;
  do i=1 to 4;
    if contrib{i} != . then do;
      Period=cats("Qtr",i);
      Amount=contrib{i};
      output;
    end;
end;
```

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 | i | Period | Amount |
|---|---|---|---|---|---|---|---|
| 120265 | . | . | . | . | 25 | 3 | . |

## 执行：旋转 SAS 数据集

```sas
data rotate (Keep=Employee_Id Period Amount);
set orion.employee_donations
  (drop=recipients paid by);
  array contrib(4) qtr1-qtr4;
  do i=1 to 4;
    if contrib{i} != . then do;
      Period=cats("Qtr",i);
      Amount=contrib{i};
      output;
    end;
end;
```

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 | i | Period | Amount |
|---|---|---|---|---|---|---|---|
| 120265 | . | . | . | . | 25 | 4 | . |

## 执行：旋转 SAS 数据集

```sas
data rotate (keep=Employee_Id Period Amount);
set orion.employee_donations
  (drop=recipients paid by);
  array contrib{4} qtr1-qtr4;
  do i=1 to 4;
    if contrib(i) ne . then do;
      Period=cats("Qtr",i);
      Amount=contrib(i);
      output;
    end;
run;
```

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 | Period |
|---|---|---|---|---|---|
| 120265 | | | | | 25 | 4 |

work.rotate

Employee_ID | Period | Amount

## 执行：旋转 SAS 数据集

```sas
data rotate (keep=Employee_Id Period Amount);
set orion.employee_donations
  (drop=recipients paid by);
  array contrib{4} qtr1-qtr4;
  do i=1 to 4;
    if contrib(i) ne . then do;
      Period=cats("Qtr",i);
      Amount=contrib(i);
      output;
    end;
run;
```

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 | Period |
|---|---|---|---|---|---|
| 120265 | | | | | 25 | 4 |

work.rotate

Employee_ID | Period | Amount

## 执行：旋转 SAS 数据集

```sas
data rotate (keep=Employee_Id Period Amount);
set orion.employee_donations
  (drop=recipients paid_by);
  array contrib(4) qtr1-qtr4;
do i=1 to 4;
  if contrib(i) ne . then do;
    Period=cats("Qtr",i);
    Amount=contrib(i);
    output;
  end;
end;
```

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 | i | Period | Amount |
|---|---|---|---|---|---|---|---|
| 120265 | . | . | 25 | 4 | Qtr4 | | |

当你在字符上下文中中使用数值值时，会发生自动转换。`CAT` 系列的函数会在将数值值格式化为 `BEST12` 格式后，移除数值参数开头和末尾的空格。

## 执行：旋转 SAS 数据集

```sas
data rotate (keep=Employee_Id Period Amount);
set orion.employee_donations
  (drop=recipients paid_by);
  array contrib(4) qtr1-qtr4;
do i=1 to 4;
  if contrib(i) ne . then do;
    Period=cats("Qtr",i);
    Amount=contrib(i);
    output;
  end;
end;
```

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 | i | Period | Amount |
|---|---|---|---|---|---|---|---|
| 120265 | . | . | 25 | 4 | Qtr4 | | 25 |

## 执行：旋转 SAS 数据集

```sas
data rotate (keep=Employee_Id Period amount);
set orion.employee_donations
  (drop=recipients paid by);
  array contrib(4) qtr1-qtr4;
do i=1 to 4
  if contrib{i} ne . then do;
    Period=cats("Qtr",i);
    Amount=contrib(i);
    output;
  end;
```

![](img/d3bde6e6ab06b1fc622215d982111742_362_0.png)

| Employee_ID | Period | Amount |
|---|---|---|
| 120265 | Qtr4 | |

## 执行：旋转 SAS 数据集

```sas
data rotate (keep=Employee_Id Period Amount);
set orion.employee_donations
  (drop=recipients paid by);
  array contrib(4) qtr1-qtr4;
do i=1 to 4
  if contrib{i} ne . then do;
    Period=cats("Qtr",i);
    Amount=contrib(i);
    output;
  end;
end;
```

![](img/d3bde6e6ab06b1fc622215d982111742_362.png)

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 | i | Period | Amount |
|---|---|---|---|---|---|---|---|
| 120265 | | | | | 25 | 4 |

Employee_ID | Period | Amount |
|---|---|---|
| 120265 | Qtr4 | |

## 执行：旋转 SAS 数据集

```sas
data rotate (keep=Employee_Id Period Amount);
set orion.employee_donations
  (drop=recipients paid_by);
  array contrib(4) qtr1-qtr4;
do i=1 to 4
  if{{i} . then do do

    =cats("Qtr",i);
    Amount=contrib(i);
    output;
  end;

;
```

|__ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 | i | Period | Amount |
|---|---|---|---|---|---|---|---|
| 120265 | | | | | 25 | Q4 | |

Employee_ID | Period | Amount |
|---|---|---|
| 120265 | Qtr4 | |

## 执行：旋转 SAS 数据集

```sas
data rotate (keep=Employee_Id Period Amount);
set orion.employee_donations
  (drop=recipients paid_by);
  array contrib(4) qtr1-qtr4;
do i=1 to 4
  if contrib(i) ne . then do;
    Period=cats("Qtr",i);
    Amount=contrib(i);
    output;
  end;
end;
```

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 | i | Period | Amount |
|---|---|---|---|---|---|---|---|
| 120265 | | | | | 25 | Q4 | |

Employee_ID | Period | Amount |
|---|---|---|
| 120265 | Qtr4 | |
