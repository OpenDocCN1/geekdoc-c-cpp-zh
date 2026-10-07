

# 第 7 章：执行条件处理

有几种方法可以防止缺失值被包含在 AgeGroup 1 中。以下是可选方案：

```
if Age lt 20 and Age ne . then AgeGroup = 1;
if Age ge 0 and Age lt 20 then AgeGroup = 1;
if 0 le Age lt 20 then AgeGroup = 1;
if Age lt 20 and not missing (Age) then AgeGroup = 1;
```

这些语句都能为 AgeGroup 得到正确的值。Age 为缺失的受试者其 AgeGroup 也会是缺失值。

第一个 IF 语句使用句号 `.` 来在 DATA 步中引用数值型缺失值。最后一个 IF 语句使用了 `MISSING` 函数。如果参数（括号中的变量）为缺失，该函数返回 `TRUE`；如果参数缺失，则返回 `FALSE`。`MISSING` 函数也适用于字符数据。

这个程序可以进行改进。如果某人的年龄小于 20 岁，第一个 IF 语句将被执行并将 AgeGroup 设置为 1。其余所有的 IF 语句仍然会执行（尽管它们的结果为假且 AgeGroup 保持为 1）。编写此程序的更好方法是将第一个语句之后的所有 IF 语句改为 `ELSE IF` 语句。

以下是修正后的程序：

## 程序 7.2：将年龄分组到年龄组的修正程序

```sas
data Conditional;
  length Gender $ 1
  Quiz $ 2;
  input Age Gender Midterm Quiz FinalExam;
  if Age lt 20 and not missing (age) then AgeGroup = 1;
  else if Age ge 20 and Age lt 40 then AgeGroup = 2;
  else if Age ge 40 and Age lt 60 then AgeGroup = 3;
  else if Age ge 60 then AgeGroup = 4;
datalines;
```

使用这种逻辑，当任何一个 IF 语句为真时，后续的 `ELSE` 语句就不会被评估。

编写此程序的另一种方法是在第一个 IF 语句中测试缺失值，并使用 `ELSE` 语句继续执行，如下：

## 程序 7.3：程序 7.2 的替代方案

```sas
data Conditional;
  length Gender $ 1
  Quiz $ 2;
  input Age Gender Midterm Quiz FinalExam;
  if missing (Age) then AgeGroup = .;
  else if Age lt 20 then AgeGroup = 1;
  else if Age lt 40 then AgeGroup = 2;
  else if Age lt 60 then AgeGroup = 3;
  else if Age ge 60 then AgeGroup = 4;
datalines;
```

《通过实例学习 SAS：程序员指南》，第二版

当你编写像这样的程序时，你需要“模拟计算机运行”并确保你的逻辑是正确的。例如，如果某人 25 岁呢？第一个 IF 语句为假，因为 Age 不缺失。下一个 `ELSE IF` 语句被评估并发现为假。最后，第三个 IF 语句被评估，AgeGroup 被设置为 2。因为这个 IF 语句为真，所有的 `ELSE IF` 语句都会被跳过。

如果你正在处理大型数据集并想榨取每一分效率，你应该将 IF 语句按顺序排列，将最可能为真的条件放在前面，最不可能为真的条件放在后面。这增加了效率，因为当之前的 IF 条件为真时，SAS 会跳过所有的 `ELSE` 条件。使用这种技术的缺点是它让程序更难读。得于现代计算机的速度，你应该只对在在大型数据集上的程序考虑这些努力。

## 7.3 子集 IF 语句

如果你想从原始文件或现有的 SAS 数据集中创建子集，可以使用特殊的 IF 语句形式称为子集 IF（subsetting IF）。例如，让我们使用 7.1 中的原始数据，但将数据集限制为女性。以下是程序：

### 示例 7.4：演示子集 IF

```sas
data Females;
  length Gender $ 1
  Quiz $ 2;
  input Age Gender Midterm Quiz FinalExam;
  if Gender = 'F';
datalines;
21 M 80 B-
22 F 90 A
35 M 87 B+
48 F 76
59 F 95 A+
15 M 88 93
67 F 90 A 91
M 62 F 67
35 F 77 C-
49 M 59 C 81
title "Listing of Females";
proc print data=Females;
run;
```

注意，此程序中 IF 后面没有 `THEN`。如果条件为真，程序继续执行下一条语句；如果条件为假，控制返回到 DATA 步的开头。在这种情况下，紧随子集 IF 之后的唯一语句是 `DATALINES` 语句。如果 Gender 的值为 F，则到达 DATA 步的结束并发生自动输出。如果 Gender 的值不等于 F，控制返回 DATA 步的开头且不会发生自动输出。以下是输出：

![](img/e9e15d8539855118e183005555103_0.png)

) 图 7.1：程序 7.4 的输出

# 女性列表

| Gender | Quiz | Age | Midterm | FinalExam |
| :--- | :--- | :--- | :--- | :--- |
| F | | 22 | | A |
| F | | 48 | | |
| F | | 59 | | A+ |
| F | | 67 | | A 91 |
| F | | 62 | | 67 |
| F | | 35 | | C- |

（子集 IF 之后的唯一语句是 `DATALINES` 语句。如果 Gender 的值为 F，则到达 DATA 步的结束并发生自动输出。如果 Gender 的值不等于 F，控制返回 DATA 步的开头且不会发生自动输出。）

# 女性列表

| 性别 | 测验 | 年龄 | 中期考试 | 期末考试 |
| :--- | :--- | :--- | :--- | :--- |
| F | | 22 | | A |
| F | | 48 | | |
| F | | 59 | | A+ |
| F | | 67 | | A 91 |
| F | | 62 | | 67 |
| F | | 35 | | C- |

（子集 IF 之后的唯一语句是 `DATALINES` 语句。如果 Gender 的值为 F，则到达 DATA 步的结束并发生自动输出。如果 Gender 的值不等于 F，控制返回 DATA 步的开头且不会发生自动输出。）

## 7.4 IN 运算符

另一种方法是在第一个 IF 语句中测试缺失值，并使用 `ELSE` 语句继续执行，如下：

（注：此处对应原文的逻辑描述，已根据翻译要求处理并保持结构）

（注：由于提供的原文中存在大量重复的逻辑和断裂的文本块，如 7.4 标题和  ..  内部的重复描述，译文已按照文档工程师逻辑进行了整合。）

