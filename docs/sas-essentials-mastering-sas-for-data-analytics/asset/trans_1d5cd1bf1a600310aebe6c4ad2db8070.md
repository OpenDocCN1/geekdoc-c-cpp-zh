

经过进一步检查，你向调查协调员核实，种族（race）的答案 "MEX" 或 "M" 应修正为 "H"，"W" 应修正为 "C"，而 "A" 应修正为 "AA"。如果 RACE 为 "X"、NA" 或 ""则将其设为空（缺失）。用于修正其中两项内容的代码（必须出现在 UPCASE 分句之后、IN () 函数之前）修复了以下问题：

```
IF RACE="MEX" OR RACE="M" then RACE="H";
IF RACE="X" OR RACE="NA" then RACE="";
```

输入这些文件。提交代码并验证修复是否有效（包括检查日志中的错误消息）。

## 6.4.3 检查并修复错误类别，修复重复变量

有两个变量 MARRIED（已婚）和 SINGLE（单身）。调查询问了受访者的婚姻状况，数据集中记录的信息中，1 表示是，0 表示否。从技术上讲，这两个变量应该是互相反的，你只需要在数据集中保留其中一个。然而，如果你查看每个 PROC FREQ 的频率分布，你会发现它们提供的信息并不相同。
要检查和其他分类变量，请使用 PROC FREQ 过程。如下例所示。

## 动手操作示例

此示例使用 PROC FREQ 检查错误输入并修复问题。

- 1. 打开程序文件 DISCOVER1.SAS。

```
PROC FREQ data=MYSASLIB_cleaned;
TABLES MARRIED SINGLE TOP_REASON RACE GENDER HOW_ARRIVED;
run;
```

提交代码并观察表 6.11 中的结果。（此处仅显示了部分输出）。注意你发现的内容：

- MARRIED 的某些代码存在错误。
- MARRIED 和 SINGLE 两个变量并不如你预期的那样互相反。通常情况下，你只需要其中一个表。在这种情况下，研究人员选择使用 SINGLE 表，因此可以删除 MARRIED 变量。
- TOP_REASON 的几个值是错误的。
- RACE 仍然包含一些错误值。（之前的修复没有解决所有问题。）

| 表 6.11 几个分类变量的频率分布 | | | | | |
| :--- | :--- | :--- | :--- | :--- |
| Married (已婚) | Frequency (频率) | Percent (百分比) | Cumulative Frequency (累计频率) | Cumulative Percent (累计百分比) |
| 0 | 38 | 48.10 | 38 | 48.10 |
| 1 | 39 | 49.37 | 77 | 97.47 |
| 9 | 1 | 1.27 | 78 | 98.73 |
| 11 | 1 | 1.27 | 79 | 100.00 |
| Single? (单身?) | | | | |
| Single (单身) | Frequency (频率) | Percent (百分比) | Cumulative Frequency (累计频率) | Cumulative Percent (累计百分比) |
| 0 | 43 | 54.43 | 43 | 54.43 |
| 1 | 36 | 45.57 | 79 | 100.00 |
| Top Reason for Coming (就主要原因) | | | | |
| Top_Reason | Frequency (频率) | Percent (百分比) | Cumulative Frequency (累计频率) | Cumulative Percent (累计百分比) |
| 1 | | 44 | 55.70 | 44 | 55.70 |
| 1,2,3 | | 1 | 1.27 | 45 | 56.96 |
| 1,3 | | 1 | 1.27 | 46 | 58.23 |
| 1.5 | | 1 | 1.27 | 47 | 59.49 |
| 2 | | 19 | 24.05 | 66 | 83.54 |
| 3 | | 12 | 15.19 | 78 | 98.73 |
| 3&1 | | 1 | 1.27 | 79 | 100.00 |
| Race (种族) | | | | | |
| Race (种族) | Frequency (频率) | Percent (百分比) | Cumulative Frequency (累计频率) | Cumulative Percent (累计百分比) |
| A | | 1 | 1.32 | 1 | 1.32 |
| AA | | 37 | 48.68 | 38 | 50.00 |
| C | | 5 | 6.58 | 43 | 56.58 |
| H | | 32 | 42.11 | 75 | 98.68 |
| W | | 1 | 1.32 | 76 | 100.00 |
| Frequency Missing (缺失频率) = 3 | | | | |

- GENDER（性别）现在看起来正常。注意，由于上一个示例中的修复，它包含了缺失值。（此处未显示此表。）
- HOW_ARRIVED（到达方式）的所有类别都是正确的。（此处未显示此表。）

有了这些信息，你可以继续清理数据集。

2. 打开程序文件 MESSY3.SAS。观察步骤 3 下列出的代码。代码已经包含了以下修复：
- MARRIED 变量已被删除。
- 包含了额外的 RACE 修复。

```
DROP MARRIED;
IF RACE NOT IN ('AA', 'H', 'C') THEN RACE="";
IF TOP_REASON ="1" or TOP_REASON="2" then TOP_REASON="";
```

提交代码并观察结果。

3. 返回 DISCOVER1.SAS，对 MARRIED 变量执行 TABLE 语句并重新提交以验证所有更改已生效。注意，分类变量的缺失值位于表底部，而 TOP_REASON 的缺失值列在表中。

## 6.4.4 检查超出范围的数值变量

分类变量已经清理完毕，现在该关注数值变量了：AGE、EDUCATION 和 SATISCTION。查看数值变量的方法是使用 PROC MEANS。特别是要寻找异常的最值。以下示例说明了如何使用 PROC MEANS 发现问题并修复它们。

- 1. 打开程序 DISCOVER2.SAS 并提交以创建表 6.12 所示的均值表。（取决于你之前的练习情况，答案可能不同。）

```
PROC MEANS DATA=CLEAN; RUN;
```

运行 PROC MEANS 时，它会显示所有数值变量的均值。通过进一步检查，发现 AGE 是字符类型变量（从 Excel 或 CSV 文件导入时的常见问题）。将此转换为数值的方法是使用 INPUT () 函数（见附录 B）。还需要注意最大值的问题。通过进一步检查，决定：
- 将 EDUCATION 的 99 设置为缺失。
- 有些温度被视为摄氏度，有些是华氏度。它们都应该是华氏度。咨询医生后，决定低于 45 的温度应被视为摄氏度并转换。
- 通过查看记录，发现编码为 108 的温度应该是 101.8。
- 将 SATISCTION 的 -99 设置为缺失。
- 忽略 Subject ID 变量。

## 表 6.12 多个变量的均值检查

| Variable (变量) | Label (标签) | N | Mean (均值) | Std Dev (标准差) | Minimum (最小值) | Maximum (最大值) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Subject | Subject ID | 79 | 39.99 | 22.96 | 1.00 | 79.00 |
| Education | Years of School | 79 | 0.46 | 0.50 | 0.00 | 1.00 |
| Satisfaction | Satisfaction Score | 78 | 14.64 | 17.16 | 6.00 | 99.00 |
| TEMP | Arrival Temperature | 79 | 77.92 | 21.70 | -99.00 | 94.10 |

- 2. 为了修复这些问题，打开 MESSY4.SAS。观察代码第 4 部分列出的每项修复代码。提交代码并观察输出。

```
IF EDUCATION=99 then EDUCATION=;
IF TEMP<45 then TEMP=(9/5)*TEMP+32;
IF TEMP=108 then TEMP=101.8;
IF SATISCTION=-99 then SATISCTION=;
* 将 AGE 从字符转换为数值；
AGEN=INPUT(AGE, 5.);
DROP AGE;
LABEL AGEN="Age Jan 1, 2014";
```

- 3. 为了验证更改已完成，重新运行 DISCOVER2.SAS 中的代码。现在 AGEN 是数值变量，你注意到最小值和最大值是 0 和 22。与研究人员核实后，得出年龄应在 10 到 99 之间。

- 4. 返回 MESSY4.SAS 进行此额外修复。注意你现在使用的是数值变量 AGEN 而不是之前的字符 AGE。

```
IF AGEN LT 10 OR AGEN GT 99 THEN AGEN=;
```

运行 MESSY4.SAS 代码，然后运行 DISCOVER2.SAS 代码以确保修复已发生。

## 深入探讨：清理混乱数据集

## 6.4.5 修正日期和时间值

需要到达诊所的日期和时间来计算服务每个患者所需。然而，这些值是字符类型。以下示例说明了如何将字符变量转换为日期时间。例如，转换 DATEARRIVED：

```
DATEARRIVED=INPUT(TRIM (DATEARRIVED),MMDDYY10.)
```

新的（转换后的）值必须有一个新名称。在这种情况下，对于 DATEARR2，你不能将值转换为不同类型并保持相同名称。在这个版本中，DATEARRIVED 值首先使用 TRIM () 函数进行修整。TIME 值稍微复杂，因为 TIME 的文本值包含 AM 或 PM，这些信息在转换之前需要剥离。为了做到，使用 FIND () 函数定位 AM 或 PM 之前的空格：

```
I= FIND(TIMEARRIVE, " ");
```

然而，你想知道 TIME 是 AM 还是 PM，因为需要将 TIME 转换为 24 小时制（军事类型）时间。因此，执行第二次 FIND 并查找 P，因为它将唯一指示 PM。使用此代码：

```
P= FIND(TIMEARRIVE,"p ");
```

如果 P 大于 0，则语句中存在 P，你知道该时间代表午后值。否则，时间代表午前（AM）。
这两个 FIND () 函数的结果是 I 代表 AM 或 PM 之前空格的位置，P 代表时间是在午前还是午后。使用 I 配合 SUBSTR () 函数提取仅包含时间信息的子字符串：

```
TIMEARRIVE=SUBSTR(TIMEARRIVE,1,I-1);
```

使用 INPUT () 函数将生成的 TIMEARRIVE 值转换为新的日期类型变量 TIMEARRIVET，并应用时间格式 TIME8。

```
TIMEARRIVET=INPUT(TRIM (TIMEARRIVE),TIME8.)
```

