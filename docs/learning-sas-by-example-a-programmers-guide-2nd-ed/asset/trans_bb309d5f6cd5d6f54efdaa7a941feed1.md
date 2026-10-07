
## 第 8 章：迭代处理：循环

+ 8.1 引言 .......................................................................................................... 99
+ 8.2 DO 组 ............................................................................................................ 99
+ 8.3 Sum 语句 ........................................................................................... 101
+ 8.4 迭代 DO 循环............................................................................... 106
+ 8.5 迭代 DO 循环的其他形式 ................................................................ 110
+ 8.6 DO WHILE 和 DO UNTIL 语句 ................................................................ 112
+ 8.7 使用 DO UNTIL 语句时的注意事项 ................................... 115
+ 8.8 LEAVE 和 CONTINUE 语句 ................................................................ 116
+ 8.9 问题 ................................................................................................ 117

## 8.1 引言

许多编程任务要求代码块运行多次。SAS 提供了几种方法来实现这一点。本章涵盖了 DO 组、DO 循环、DO WHILE 语句以及 DO UNTIL 语句。

## 8.2 DO 组

为了演示 DO 组，我们从一个包含学生信息的数据文件开始：他们的年龄、性别、期中成绩、测验和考试成绩。以下是数据文件 C:\books\learningGrades.txt 的列示：

```
21 M 80 B - 82
  F 90 A - 93
35 M 87 B+ - 85
48 F - 76
59 F 95 A+ 97
15 M 88 - 93
67 F 97 A - 91
  M 62 F - 61
35 F 77 C- 77
49 M 59 C - 81
```

你想从此文件中读取值并计算两个新变量——年龄组（AgeGroup）以及一个根据期中和期末考试计算出的数值（Grade）。如果年龄小于或等于 39，你想将 AgeGroup 设置为 "Younger group"（年幼组），并将成绩计算为期中成绩（40%）和期末考试（60%）的加权平均值。如果年龄大于 39，你想将 AgeGroup 设置为 "Older group"（年长组），并将成绩计算为期中和期末考试的简单平均值。

来看解决此问题的程序 8.1：

### 程序 8.1：不使用 DO 组的程序示例

```
data Grades;
  length Gender $ 1
  Quiz $ 2
  AgeGroup $ 13;
  infile 'C:\books\learning\Grades.txt' mov;
  input Age Gender Midterm Quiz FinalExam;
  if missing(Age) then delete;
  if le 39 then AgeGroup = 'Younger group';
  if le 39 then Grade = .4*Midterm + .6*FinalExam;
  if gt 39 then AgeGroup = 'Older group';
  if gt 39 then Grade = (Midterm + FinalExam)/2;
run;
```

注意前两个 IF 语句和最后两个 IF 语句测试的是同一个条件。你想测试一个条件并执行若干操作。通过使用 DO 和 END 语句，你可以做到。程序 8.2 的工作方式与程序 8.1 相同，但它使用 DO 和 END 语句使代码更高效、更易读：

### 程序 8.2：演示 DO 组

```sas
data Grades;
  length Gender $ 1
  Quiz $ 2
  AgeGroup $ 13;
  infile 'C:\books\learning\Grades.txt' mov;
  input Age Gender Midterm Quiz FinalExam;
  if missing(Age) then delete;
  if le 39 then do;
    AgeGroup = 'Younger group';
    Grade = .4*Midterm + .6*FinalExam;
  end;
  else if gt 39 then do;
    AgeGroup = 'Older group';
    Grade = (Midterm + FinalExam)/2;
  end;
run;
```

```sas
title "Listing of Grades";
proc print data=Grades noobs;
run;
```

DO 和 END 之间的语句形成了一个 DO 组。当 IF 条件成立时，组内的所有语句都会执行。一种很好的思考方式是：“如果条件成立，则执行以下语句直到结束。”将 DO 组中的所有语句缩进是标准做法。

DO 组的编码不仅比多个 IF 语句高效，而且更易读。以下是数据集的列表：

图 8.1：程序 8.2 的输出

| Gender | Quiz | AgeGrp | Age | Midterm | FinalExam | Grade |
|---|---|---|---|---|---|---|
| M | B- | Younger group | 21 | | 82 | 81.2 |
| M | B+ | Younger group | 35 | 87 | 85 | 85.8 |
| F | | | 48 | | 76 | - |
| F | A+ | Older group | 59 | 95 | 97 | 96.0 |
| M | | Younger group | 15 | 88 | 93 | 91.0 |
| F | A | Older group | 67 | 97 | 91 | 94.0 |
| F | C- | Older group | 35 | 77 | 77 | 77.0 |
| M | C | Older group | 49 | 59 | 81 | 70.0 |

你应该注意，当年龄存在缺失值时，这两个程序都能正常工作。如果参数是缺失的字符或数值，MISSING 函数会返回真值。DELETE 语句起两个作用：首先，它防止处理当前观测值。

## 8.3 Sum 语句

（注：此处后续内容原文中存在大量重复，已按要求仅翻译核心部分）

