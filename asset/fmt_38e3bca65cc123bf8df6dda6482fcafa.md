
运行 `PROC MEANS` 时，它会显示所有数值变量的均值。通过进一步检查，发现 `AGE` 是字符类型变量（从 Excel 或 CSV 文件导入时的常见问题）。将此转换为数值的方法是使用 `INPUT()` 函数（见附录 B）。还需要注意最大值的问题。通过进一步检查，决定：
- 将 `EDUCATION` 的 99 设置为缺失。
- 有些温度被视为摄氏度，有些是华氏度。它们都应该是华氏度。咨询医生后，决定低于 45 的温度应被视为摄氏度并转换。
- 通过查看记录，发现编码为 108 的温度应该是 101.8。
- 将 `SATISCTION` 的 -99 设置为缺失。
- 忽略 Subject ID 变量。

## 表 6.12 多个变量的均值检查

| Variable (变量) | Label (标签) | N | Mean (均值) | Std Dev (标准差) | Minimum (最小值) | Maximum (最大值) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Subject | Subject ID | 79 | 39.99 | 22.96 | 1.00 | 79.00 |
| Education | Years of School | 79 | 0.46 | 0.50 | 0.00 | 1.00 |
| Satisfaction | Satisfaction Score | 78 | 14.64 | 17.16 | 6.00 | 99.00 |
| TEMP | Arrival Temperature | 79 | 77.92 | 21.70 | -99.00 | 94.10 |

- 2. 为了修复这些问题，打开 `MESSY4.SAS`。观察代码第 4 部分列出的每项修复代码。提交代码并观察输出。

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

- 3. 为了验证更改已完成，重新运行 `DISCOVER2.SAS` 中的代码。现在 `AGEN` 是数值变量，你注意到最小值和最大值是 0 和 22。与研究人员核实后，得出年龄应在 10 到 99 之间。

- 4. 返回 `MESSY4.SAS` 进行此额外修复。注意你现在使用的是数值变量 `AGEN` 而不是之前的字符 `AGE`。

```
IF AGEN LT 10 OR AGEN GT 99 THEN AGEN=;
```

运行 `MESSY4.SAS` 代码，然后运行 `DISCOVER2.SAS` 代码以确保修复已发生。

## 深入探讨：清理混乱数据集

### 6.4.5 修正日期和时间值

需要到达诊所的日期和时间来计算服务每个患者所需。然而，这些值是字符类型。以下示例说明了如何将字符变量转换为日期时间。例如，转换 `DATEARRIVED`：

```
DATEARRIVED=INPUT(TRIM (DATEARRIVED),MMDDYY10.)
```

新的（转换后的）值必须有一个新名称。在这种情况下，对于 `DATEARR2`，你不能将值转换为不同类型并保持相同名称。在这个版本中，`DATEARRIVED` 值首先使用 `TRIM()` 函数进行修整。`TIME` 值稍微复杂，因为 `TIME` 的文本值包含 AM 或 PM，这些信息在转换之前需要剥离。为了做到，使用 `FIND()` 函数定位 AM 或 PM 之前的空格：

```
I= FIND(TIMEARRIVE, " ");
```

然而，你想知道 `TIME` 是 AM 还是 PM，因为需要将 `TIME` 转换为 24 小时制（军事类型）时间。因此，执行第二次 `FIND` 并查找 `P`，因为它将唯一指示 PM。使用此代码：

```
P= FIND(TIMEARRIVE,"p ");
```

如果 `P` 大于 0，则语句中存在 `P`，你知道该时间代表午后值。否则，时间代表午前（AM）。
这两个 `FIND()` 函数的结果是 `I` 代表 AM 或 PM 之前空格的位置，`P` 代表时间是在午前还是午后。使用 `I` 配合 `SUBSTR()` 函数提取仅包含时间信息的子字符串：

```
TIMEARRIVE=SUBSTR(TIMEARRIVE,1,I-1);
```

使用 `INPUT()` 函数将生成的 `TIMEARRIVE` 值转换为新的日期类型变量 `TIMEARRIVET`，并应用时间格式 `TIME8`。

```
TIMEARRIVET=INPUT(TRIM (TIMEARRIVE),TIME8.)
```

你还没有完成！时间是以 AM（上午）或 PM（下午）记录的，你可能需要调整时间。如果时间在下午（如果 `P=1`），你需要给记录的时间值加上 12 小时。由于时间值是以秒为单位的，计算 12 小时的秒数为 12×60×60=43200，因此转换语句为：

```
IF P>0 THEN TIMELEFT=TIMELEFT+43200;
```

最后，使用 `DHMS()` 函数通过以下代码合并日期和时间值：

```
ARRIVEDT=DHMS(DATEARRIVED2,0,0,TIMEARRIVET)
```

`DHMS()` 函数的参数是 DATE、HOUR、MINUTE 和 SECONDS。在这种情况下，我们：
- 使用 `DATEARRIVED2` 作为 DATE 值
- 使用 `TIMEARRIVET` 作为 SECONDS 值
- 因为秒数已经包含了小时和分钟，因此我们在 HOUR 和 MINUTE 参数中输入 0。

还使用了相应的格式，以便日期和时间值能够恰当显示。丢弃了不需要变量。下面的示例说明了如何操作。

## 动手实例

此示例修正了与数值变量相关的问题。

- 1. 打开程序文件 `MESSY5.SAS` 并观察 Part 5 注释后的代码。

```
FORMAT ARRIVEDETDATETIM18;

DATEARRIVED2=INPUT(TRIM (DATEARRIVED),MMDDYY10.);

I=FIND(TIMEARRIVE, " ");

P=FIND(TIMEARRIVE, "P");

TIMEARRIVE=SUBSTR(TIMEARRIVE,1,I-1);

TIMEARRIVET=INPUT(TRIM (TIMEARRIVE),TIME8.);

IF P>0 AND +43200 THEN TIMEARRIVET=TIMEARRIVET+43200;

ARRIVEDT=DHMS(DATEARRIVED2,0,0,TIMEARRIVET);

Label ARRIVEDT="Date & Time Arrived";
```

提交此代码并观察表 6.13 中的输出。
原始值在单元格中左对齐，表示是文本值；转换后的值右对齐，表示是数字/日期。`ARRIVALDT`（到达日期时间）值包含了合并后的日期和时间值。注意，第二个观测值的到达时间为 1:23 PM，已转换为 24 小时制的 13:23。

## 表 6.13 转换日期和时间值

| Obs | 受体 ID | 到达日期 | 到达时间 | DATEARRIVED2 | TIMEARRIVED2 | 到达日期时间 |
|---|---|---|---|---|---|---|
| 1 | 00001 | 2/7/2005 | 11:18:00 A | 07FEB005 | 11:18 | 07FEB05 11:18 |
| 2 | 00002 | 3/19/2005 | 1:23 PM | 10MAR005 | 13:23 | 10MAR05 13:23 |
| 3 | 00003 | 3/2/2005 | 1:08 PM | 02MAR005 | 13:08 | 02MAR05 13:08 |
| 4 | 00004 | 5/2/2005 | 11:46 A | 02MAY005 | 11:46 | 02MAY05 11:46 |
| 5 | 00005 | 1/31/2005 | 12:09 PM | 31JAN005 | 24:09 | 01FEB05 00:09 |
| 6 | 00006 | 2/1/2005 | 2:27 PM | 01FEB005 | 14:27 | 01FEB05 14:27 |
| 7 | 00007 | 2/3/2005 | 11:50 A | 03FEB005 | 11:50 | 03FEB05 11:50 |
| 8 | 00008 | 2/4/2005 | 1:47 A | 04FEB005 | 10:47 | 04FEB05 10:47 |
| 9 | 00009 | 2/5/2005 | 11:42 A | 05FEB005 | 11:42 | 05FEB05 11:42 |

- 2. 使用转换代码转换 `DATEARRIVED` 和 `TIMEARRIVE`，对 `DATELEFT` 和 `TIMELEFT` 执行类似的转换。名称将命名为 `LEFTDTD`，并添加 `LABEL` 语句将新值标记为“Date & Time Left”（离开日期时间）。提交代码并验证是否已完成修正。
- 3. 一旦有了到达和离开的时间，就可以计算受体在诊所停留多久。输入此代码，使用带有“MINUTES”参数的 `INTCK` 函数

```
STAYMINS=INTCK('MINUTES', ARRIVED, LEFTDTD )
```
并除以 60 并四舍五入，得到在诊所停留的小时数：

```
STAYHOURS=ROUND(STAYMINS/60, 1 )
```
- 4. 将 `STAYHOURS` 添加到 `PROC PRINT` 列表中。检查代码并观察表 6.14 中的结果。

| Obs | 受体 ID | 到达日期 | 到达时间 | DATEARRIVED2 | TIMEARRIVED2 | 到达日期时间 | 离开日期时间 |
|---|---|---|---|---|---|---|---|
| 1 | 00001 | 2/7/2005 | 11:18 | 07FEB005 | 11:18 | 07FEB05 11:18 | 07FEB05 14:15 |
| 2 | 00002 | 3/19/2005 | 1:23 | 10MAR005 | 13:23 | 10MAR05 13:23 | 10MAR05 12:45 |
| 3 | 00003 | 3/2/2005 | 1:08 | 02MAR005 | 13:08 | 02MAR05 13:08 | 02MAR05 17:07 |
| 4 | 00004 | 5/2/2005 | 11:46 | 02MAY005 | 11:46 | 02MAY05 11:46 | 02MAY05 21:41 |
| 5 | 00005 | 1/31/2005 | 12:09 | 31JAN005 | 24:09 | 01FEB05 00:09 | 01FEB05 14:46 |
| 6 | 00006 | 2/1/2005 | 2:27 | 01FEB005 | 14:27 | 01FEB05 14:27 | |
| 7 | 00007 | 2/3/2005 | 11:50 | 03FEB005 | 11:50 | 03FEB05 11:50 | |
| 8 | 00008 | 2/4/2005 | 1:47 | 04FEB005 | 10:47 | 04FEB05 10:47 | |
| 9 | 00009 | 2/5/2005 | 11:42 | 05FEB005 | 11:42 | 05FEB05 11:42 | |

## 第6 章：SAS® 高级编程主题第一部分

你还没有完成！时间是以 AM（上午）或 PM（下午）记录的，你可能需要调整时间。如果时间在下午（如果 `P=1`），你需要给记录的时间值加上 12 小时。由于时间值是以秒为单位的，计算 12 小时的秒数为 12×60×60=43200，因此转换语句为：

```
IF P>0 THEN TIMELEFT=TIMELEFT+43200;
```

最后，使用 `DHMS()` 函数通过以下代码合并日期和时间值：

```
ARRIVEDT=DHMS(DATEARRIVED2,0,0,TIMEARRIVET)
```

`DHMS()` 函数的参数是 DATE、HOUR、MINUTE 和 SECONDS。在这种情况下，我们：
- 使用 `DATEARRIVED2` 作为 DATE 值
- 使用 `TIMEARRIVET` 作为 SECONDS 值
- 因为秒数已经包含了小时和分钟，因此我们在 HOUR 和 MINUTE 参数中输入 0。

还使用了相应的格式，以便日期和时间值能够恰当显示。丢弃了不需要变量。下面的示例说明了如何操作。

## 动手实例

此示例修正了与数值变量相关的问题。

- 1. 打开程序文件 `MESSY5.SAS` 并观察 Part 5 注释后的代码。

```
FORMAT ARRIVEDETDATETIM18;

DATEARRIVED2=INPUT(TRIM (DATEARRIVED),MMDDYY10.);

I=FIND(TIMEARRIVE, " ");

P=FIND(TIMEARRIVE, "P");

TIMEARRIVE=SUBSTR(TIMEARRIVE,1,I-1);

TIMEARRIVET=INPUT(TRIM (TIMEARRIVE),TIME8.);

IF P>0 AND +43200 THEN TIMEARRIVET=TIMEARRIVET+43200;

ARRIVEDT=DHMS(DATEARRIVED2,0,0,TIMEARRIVET);

Label ARRIVEDT="Date & Time Arrived";
```

提交此代码并观察表 6.13 中的输出。
原始值在单元格中左对齐，表示是文本值；转换后的值右对齐，表示是数字/日期。`ARRIVALDT`（到达日期时间）值包含了合并后的日期和时间值。注意，第二个观测值的到达时间为 1:23 PM，已转换为 24 小时制的 13:23。

## 表 6.13 转换日期和时间值

| Obs | 受体 ID | 到达日期 | 到达时间 | DATEARRIVED2 | TIMEARRIVED2 | 到达日期时间 |
|---|---|---|---|---|---|---|
| 1 | 00001 | 2/7/2005 | 11:18:00 A | 07FEB005 | 11:18 | 07FEB05 11:18 |
| 2 | 00002 | 3/19/2005 | 1:23 PM | 10MAR005 | 13:23 | 10MAR05 13:23 |
| 3 | 00003 | 3/2/2005 | 1:08 PM | 02MAR005 | 13:08 | 02MAR05 13:08 |
| 4 | 00004 | 5/2/2005 | 11:46 A | 02MAY005 | 11:46 | 02MAY05 11:46 |
| 5 | 00005 | 1/31/2005 | 12:09 PM | 31JAN005 | 24:09 | 01FEB05 00:09 |
| 6 | 00006 | 2/1/2005 | 2:27 PM | 01FEB005 | 14:27 | 01FEB05 14:27 |
| 7 | 00007 | 2/3/2005 | 11:50 A | 03FEB005 | 11:50 | 03FEB05 11:50 |
| 8 | 00008 | 2/4/2005 | 1:47 A | 04FEB005 | 10:47 | 04FEB05 10:47 |
| 9 | 00009 | 2/5/2005 | 11:42 A | 05FEB005 | 11:42 | 05FEB05 11:42 |

- 2. 使用转换代码转换 `DATEARRIVED` 和 `TIMEARRIVE`，对 `DATELEFT` 和 `TIMELEFT` 执行类似的转换。名称将命名为 `LEFTDTD`，并添加 `LABEL` 语句将新值标记为“Date & Time Left”。提交代码并验证是否已完成修正。
- 3. 一旦有了到达和离开的时间，就可以计算受体在诊所停留多久。输入此代码，使用带有“MINUTES”参数的 `INTCK` 函数

```
STAYMINS=INTCK('MINUTES', ARRIVED, LEFTDTD )
```
并除以 60 并四舍五入，得到在诊所停留的小时数：

```
STAYHOURS=ROUND(STAYMINS/60, 1 )
```
