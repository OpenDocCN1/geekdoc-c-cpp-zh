
## 场景 6

### 代码片段

```sas
else if Smoking > 25 then SmokingStatus = 'Very Heavy (25+)';
else SmokingStatus = 'Error';
run;

proc freq data = work.heart AgeHDdiag_Smoking_Status / norow nocol nopercent;
```

### 步骤说明

1. SAS/ACCESS `LIBNAME` 语句创建了库引用 `certdata`，它指向 Excel 工作簿 `heart.xlsx`。
2. `DATA` 步骤创建了一个名为 `Work.Heart` 的临时数据集。
3. `SET` 语句指明要从 Excel 文件中读取哪个工作表。`SET` 语句指定了库引用（对 Excel 文件的引用）和工作表名称作为输入数据。`DROP` 数据选项排除了写入数据集的 `AgeDeath` 和 `DeathCause` 变量。也可以使用 `DROP` 语句。
4. `WHERE` 语句选择了 `Status` 变量值为 `Alive` 的观测值。
5. `IF` 语句导致 `DATA` 步骤仅继续处理符合 `IF` 语句中表达式的观测值。在示例中，如果 `AgeHDdiag` 的值缺失，则这些观测值将从数据集中删除。
6. `LENGTH` 语句指定 `Smoking_Status` 的长度为 17 且类型为字符变量。这用于避免值被截断。
7. `IF/ELSE` 语句通过设置缺失值为 `Smoking_Status` 变量创建了值。
8. `ELSE` 语句在所有其他 `IF-THEN/ELSE` 语句均未执行时提供备选操作。
9. `FREQ` 过程为 `Work.Heart` 创建了双向频数表。
10. `TABLES` 语句请求变量 `AgeChDDdiag` 和 `Smoking_Status` 的双向频数表。选项 `norow`、`nocol` 和 `nopercent` 抑制了行、列百分比和单元计数。

### 输出 A2.8 部分结果：PROC FREQ 结果

#### 频数

| AgeChDDdiag 按 Smoking_Status 分类表 |
| :--- | :---: | :---: | :---: | :---: | :---: |
| AgeChDDdiag(AgeChDDdiag) | Heavy (16-25) | Moderate (6-15) | Non-Smoker (0-5) | Very Heavy (>25) | 总计 |
| 32 | 0 | 0 | 0 | 1 | 1 |
| 33 | 0 | 1 | 0 | 1 | 2 |
| 36 | 0 | 1 | 0 | 1 | 1 |
| 37 | 0 | 0 | 0 | 2 | 2 |
| 38 | 0 | 1 | 0 | 1 | 2 |
| ...观测 | | | | | |
| 84 | 0 | 0 | 2 | 0 | 4 |
| 85 | 0 | 1 | 0 | 2 | 3 |
| 86 | 0 | 0 | 0 | 3 | 3 |
| 87 | 0 | 0 | 0 | 1 | 2 |
| 88 | 0 | 0 | 2 | 0 | 2 |
| 总计 | 0 | 102 | 56 | 350 | 404 |

### 测试你的代码解决方案

1. 正确答案：102
2. 正确答案：2
3. 正确答案：3

## 场景 7

### 代码解决方案

```sas
data work.scenario7;
  set cert.temp;
  format Date date;
  Month = day;
run;

proc freq data = work.scenario7;
  tables HighTemp;
run;

proc means data = work.scenario7;
  class Month;
  var AvgLowTemp AvgHighTemp;
run;
```

### 步骤说明

1. `DATA` 步骤创建了一个名为 `Work.Scenario7` 的临时数据集。
2. `SET` 语句从一个 SAS 数据集中读取观测值。
3. `FORMAT` 语句格式化 `Date`。
4. `day` 函数返回 `Month` 的值。
5. `FREQ` 过程创建了单向、双向和 n 向表。它还通过报告值的分布来描述数据。
6. `TABLES` 语句请求变量 `HighTemp` 的默认统计数据的单向和交叉表。
7. `MEANS` 过程用于计算 `VAR` 语句中变量的描述性统计。
8. `CLASS` 语句为每个 `Month` 值提供单独计算。
9. `VAR` 语句指定 `AvgLowTemp` 和 `AvgHighTemp` 为分析变量，并控制它们在输出中的顺序。

### 输出 A2.9 HighTemp 的 PROC FREQ 结果

| HighTemp | 频数 | 累计百分比 | 累计频数 | 累计百分比 |
| :--- | :---: | :---: | :---: | :---: |
| 21 | 2 | 2.22 | 2 | 2.22 |
| 23 | 1 | 1.11 | 3 | 3.33 |
| 26 | 2 | 2.22 | 5 | 5.56 |
| 27 | 1 | 1.11 | 6 | 6.67 |
| 28 | 1 | 1.11 | 7 | 7.78 |
| ...观测 | | | | |
| 68 | 2 | 2.22 | 85 | 94.44 |
| 74 | 1 | 1.11 | 86 | 95.56 |
| 77 | 1 | 1.11 | 87 | 96.67 |
| 78 | 2 | 2.22 | 89 | 98.89 |
| 82 | 1 | 1.11 | 90 | 100.00 |

### 输出 A2.10 PROC MEANS 结果

| Month | N 观测 | Variable | N | 平均值 | 标准差 | 最小值 | 最大值 |
| :--- | :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| 1 | 31 | AvgLowTemp | 31 | 28.612903 | 0.4951376 | 30.000000 | 34.000000 |
| | | AvgHighTemp | 31 | 43.612903 | 1.7145801 | 35.000000 | 47.000000 |
| 2 | 28 | AvgLowTemp | 28 | 31.750000 | 1.4813657 | 30.000000 | 34.000000 |
| | | AvgHighTemp | 28 | 48.2857143 | 2.0880106 | 45.000000 | 52.000000 |
| 3 | 31 | AvgLowTemp | 31 | 37.6129032 | 2.5778210 | 34.000000 | 42.000000 |
| | | AvgHighTemp | 31 | 55.837097 | 3.1738176 | 51.000000 | 61.000000 |

## 场景 8

### 代码解决方案

```sas
data work.scenario8;
  set cert.addresses;
  Zipcode = substr(State, 3, 5);
  State = substr(State, 1, 2);
run;

proc data = work.scenario8;
  where zipcode = '85069';
run;

freq data = work.scenario8 order = freq;
  tables State;
```
