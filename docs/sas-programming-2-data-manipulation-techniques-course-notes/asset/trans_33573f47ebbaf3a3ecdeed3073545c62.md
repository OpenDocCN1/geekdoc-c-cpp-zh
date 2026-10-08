

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

当你在字符上下文中中使用数值值时，会发生自动转换。CAT 系列的函数会在将数值值格式化为 BEST12 格式后，移除数值参数开头和末尾的空格。

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
|---|---|---|---|---|---|

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

(注：由于原文中存在大量重复的块，译文已将核心标题翻译为“执行：旋转 SAS 数据集”并保持结构)

--- **由于您提供的文本中包含大量重复的 SAS 代码块和表格，我已按照您的要求，对其中的非代码部分进行了翻译，并完整保留了所有代码、表格结构和原始格式。**

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

当你在字符上下文中中使用数值值时，会发生自动转换。CAT 系列的函数会在将数值值格式化为 BEST12 格式后，移除数值参数开头和末尾的空格。

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
|---|---|---|---|---|---|---|

  120265 | | | | | 25 | |44 | |

__ | Period | Amount |
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

## 执行：旋转 SAS 数据集

```sas
data rotate (keep=Employee_Id Period Amount);
set orion.employee_donations
  (drop=recipients paid_by);
  array contrib{4} qtr1-qtr4;
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
| 120265 | | | | | 25 | Q4 | |

Employee_ID | Period | Amount |
|---|---|---|
| 120265 | Qtr4 | |

## 执行：旋转 SAS 数据集

```sas
data rotate (keep=Employee_Id Period Amount);
set orion.employee_donations
  (drop=recipients paid_by);
  array contrib{4} qtr1-qtr4;
do i=1 to 4;
  if contrib(i) ne . then do;
    Period=cats("Qtr",i);
    Amount=contrib(i);
    output;
  end;
end;
```

## 执行：旋转 SAS 数据集

```sas
data rotate (keep=Employee_Id Period Amount);
set orion.employee_donations
  (drop=recipients paid_by);
  array contrib{4} qtr1-qtr4;
do i=1 to 4;
  if contrib{i} ne . then do;
    Period=cats("Qtr",i);
    Amount=contrib(i);
    output;
  end;
end;
```

|

_ID | Qtr1 | Amounttr2 | Qtr3 |
tr4 | | |
 | Amount |

 |
| 120265 | | | | | 25 | |44 | |

Employee_ | | Period | Amount |
|---|


| 120265 | Qtr4 | |

## 执行：旋转 SAS 数据集

```sas
data rotate (keep=Employee_Id Period Amount);
set orion.employee_donations
  (drop=recipients paid by);
  array contrib(4) qtr1-qtr4;
do i=1 to 4;
  if contrib(i) ne . then do;
    Period=cats("Qtr",i);
    Amount=contrib(i);
    output;
  end;
run;
```

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 | i | Period | Amount |
|---|---|---|---|---|---|---|---|
| 120265 | 15 | 15 | 15 | 15 | 1 | Qtr1 | 15 |

Employee_ID | Period | Amount |
|---|---|---|
| 120265 | Qtr4 | 25 |

## 执行：旋转 SAS 数据集

```sas
data rotate (keep=Employee_Id Period Amount);
set orion.employee_donations
  (drop=recipients paid by);
  array contrib(4) qtr1-qtr4;
do i=1 to 4;
  if contrib(i) ne . then do;
    Period=cats("Qtr",i);
    Amount=contrib(i);
    output;
  end;
run;
```

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 | i | Period | Amount |
|---|---|---|---|---|---|---|---|
| 120265 | 15 | 15 | 15 | 15 | 1 | Qtr1 | 15 |

Employee_ID | Period | Amount |
|---|---|---|
| 120265 | Qtr4 | 25 |

## 执行：旋转 SAS 数据集

```sas
data rotate (keep=Employee_Id Period Amount);
set orion.employee_donations
  (drop=recipients paid by);
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
| 120265 | . | . | 25 | 4 | Qtr4 | | | | |__ | | | Amount |



---|


  1222 |5 | | |4 | |

## 执行：旋转 SAS 数据集

```sas
data rotate (keep=Employee_Id Period Amount);
set orion.employee_donations
  (drop=recipients paid by);
  array contrib(4) qtr1-qtr4;
do i=1 to 4;
  if contrib(i) ne . then do;
    Period=cats("Qtr",i);
    Amount=contrib(i);
    output;
  end;
end;
```

```

_ Employee_ID | Qtr1 | Qtr2 | Q |3 | Q |4 | i | Period |
 |
---|---|---|---|---|---|---|


1 120265 | | | | | 25 | 4 | |

Employee_ID | Period | Amount |
|---|---|---|
| 120265 | Qtr4 | |

## 执行：旋转 SAS 数据集

```sas
data rotate (keep=Employee_Id Period Amount);
set orion.employee_donations
  (drop=recipients paid by);
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
| 120265 | | | | | 25 | 4 | |

Employee_ID | Period | Amount |
|---|---|---|
| 120265 | Qtr4 | |

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
| 120265 | | | | | 25 | 4 | |

Employee_ID | Period | Amount |
|---|---|---|
| 120265 | Qtr4 | 25

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

