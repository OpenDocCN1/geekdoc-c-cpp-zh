
# 9.04 投票

当 `DROP` 语句置于 `SET` 语句之后，生成的运行是否正确？

- 是
- 否

## 处理 DROP 和 KEEP 语句

`DROP` 和 `KEEP` 语句在变量被引入程序数据向量 (PDV) 之后进行选择。

![](img/1698e3a97543d6895ff5297aae8fd042_395_0.png)

## 编译

```sas
data work.sales;
  set orion.sales;
  drop Gender Salary Job Title;
  Country Birth Date Hire_Date;
  Bonus=500;
  Compensation=sum(Salary,Bonus);
  BonusMonth=month(Hire_Date);
run;
```

## 编译

```sas
data work.comp;
set orion.sales;
drop Gender Salary Job Title
Country Birth_Date Hire_Date;
Bonus=100;
Compensation=sum(Salary, Bonus);
BonusMonth=month(Hire_Date);
run;
```

| 员工 ID (Employee_ID) | 名字 (First Name) | 姓 (Last Name) | 性别 (Gender) | 薪资 (Salary) | 职位 (Job_Title) |
|---|---|---|---|---|---|
| N 8 | $12 | $18 | N 8 | $25 |

| 国家 (Country) | 出生日期 (Birth_Date) | 入职日期 (Hire_Date) |
|---|---|---|
| $ 2 | N 8 | N 8 |

```sas
data work.comp;
set orion.sales;
drop Gender Salary Job Title
Country Birth_Date Hire_Date;
Bonus=500;
Compensation=sum(Salary, Bonus);
BonusMonth=month(Hire_Date);
run;
```

| 员工 ID (Employee ID) | 名字 (First Name) | 姓 (Last Name) | 性别 (Gender) | 薪资 (Salary) | 职位 (Job_Title) |
|---|---|---|---|---|---|
| N 8 | $12 | $18 | $1 | N 8 | $25 |

| 国家 (Country) | 出生日期 (Birth Date) | 入职日期 (Hire Date) | Bonus |
|---|---|---|---|
| $ 2 | N 8 | N 8 | 8 |

```sas
data work.comp;
set orion.sales;
drop Gender Salary Job Title
Country Birth_Date Hire Date;
Bonus=500;
Compensation=sum(Salary, Bonus);
BonusMonth=month(Hire_Date);
run;
```

| 员工 ID (Employee ID) | 名字 (First Name) | 姓 (Last Name) | 性别 (Gender) | 薪资 (Salary) | 职位 (Title) |
|---|---|---|---|---|---|
| N 8 | $12 | $18 | $1 | N 8 | $25 |

| 国家 (Country) | 出生日期 (Birth Date) | 入职日期 (Hire Date) | Bonus |
|---|---|---|---|
| $ 2 | N 8 | N 8 | N 8 |

```sas
data work.comp;
set orion.sales;
drop Gender Salary Job Title
Country Birth-Date Hire Date;
Bonus=500;
Compensation=sum(Salary,Bonus);
BonusMonth=month(Hire_Date);
run;
```

| 员工 ID (Employee ID) | 名字 (First Name) | 姓 (Last Name) | 性别 (Gender) | 薪资 (Salary) | 职位 (Title) |
|---|---|---|---|---|---|
| N 8 | $12 | $18 | $1 | N 8 | $25 |

| 国家 (Country) | 出生日期 (Birth Date) | 入职日期 (Hire Date) | Bonus |
|---|---|---|---|
| $ 2 | N 8 | N 8 | N 8 |

```sas
data work.comp;
set orion.sales;
drop Gender Salary Job Title
Country Birth Date Hire Date;
Bonus=500;
Compensation=sum(Salary,Bonus);
BonusMonth=month(Hire_Date);
run;
```

| 员工 ID (Employee ID) | 名字 (First Name) | 姓 (Last Name) | 性别 (Gender) | 薪资 (Salary) | 职位 (Title) |
|---|---|---|---|---|---|
| N 8 | $12 | $18 | $1 | N 8 | $25 |

| 国家 (Country) | 出生日期 (Birth Date) | 入职日期 (Hire Date) | Bonus | Compensation |
|---|---|---|---|---|
| $ 2 | N 8 | N 8 | N 8 |

```sas
data work.comp;
set orion.sales;
drop Gender Salary Job Title
Country Birth Date Hire Date;
Bonus=500;
Compensation=sum(Salary,Bonus);
BonusMonth=month(Hire_Date);
run;
```

| 员工 ID (Employee ID) | 名字 (First Name) | 姓 (Last Name) | 性别 (Gender) | 薪资 (Salary) | 职位 (Title) |
|---|---|---|---|---|---|
| N 8 | $12 | $18 | $1 | N 8 | $25 |

| 国家 (Country) | 出生日期 (Birth Date) | 入职日期 (Hire Date) | Bonus | Compensation |
|---|---|---|---|---|
| $ 2 | N 8 | N 8 | N 8 |

```sas
data work.comp;
set orion.sales;
drop Gender Salary Job Title
Country Birth_Date Hire Date;
Bonus=500;
Compensation=sum(Salary, Bonus);
BonusMonth=month(Hire_Date);
run;
```

| 员工 ID (Employee ID) | 名字 (First Name) | 姓 (Last Name) | 性别 (Gender) | 薪资 (Salary) | 职位 (Job_Title) |
|---|---|---|---|---|---|
| N 8 | $12 | $18 | $1 | N 8 | $25 |

| 国家 (Country) | 出生日期 (Birth Date) | 入职日期 (Hire Date) | Bonus | Compensation |
|---|---|---|---|---|
| $ 2 | N 8 | N 8 | N 8 |

```sas
data work.comp;
set orion.sales;
drop Gender Salary Job Title
Country Birth_Date Hire Date;
Bonus=500;
Compensation=sum(Salary, Bonus);
BonusMonth=month(Hire_Date);
run;
```

| 员工 ID (Employee ID) | 名字 (First Name) | 姓 (Last Name) | 性别 (Gender) | 薪资 (Salary) | 职位 (Job_Title) |
|---|---|---|---|---|---|
| N 8 | $12 | $18 | $1 | N 8 | $25 |

| 国家 (Country) | 出生日期 (Birth Date) | 入职日期 (Hire Date) | Bonus | Compensation |
|---|---|---|---|---|
| $ 2 | N 8 | N 8 | N 8 |

| 员工 ID (Employee ID) | 名字 (First Name) | 姓 (Last Name) | 奖金 (Bonus) | 薪酬 (Compensation) | 奖金月份 (BonusMonth) |
|---|---|---|---|---|---|
| N 9 | $12 | $18 | $9 | N 8 | N 8 |

## 执行

部分 `orion.sales`

| 员工 ID (Employee ID) | 入职日期 (Hire Date) |
|---|---|
| 120102 | 10744 |
| 120103 | 5114 |
| 120121 | 5114 |
| 120122 | 6756 |

```sas
data work.comp;
set orion.sales;
drop Gender Salary Job Title
Country Birth Date
Bonus=500;
Compensation=sum(Salary, Bonus);
BonusMonth=month(Hire_Date);
run;
```

## 执行

部分 `orion.sales`

| 员工 ID | 入职日期 |
|---|--|
| 120102 | 10744 |
| 120103 | 5114 |
| 120121 | 5114 |
| 120122 | 6756 |

```sas
data work.comp;
set orion.sales;
drop Gender Salary Job Title
Country Birth Date
Hire_Date;
Bonus=500;
Compensation=sum(Salary,Bonus);
BonusMonth=month(Hire_Date);
run;
```

## PDV (程序数据变量)

| 员工 ID | 性别 | 入职日期 | 奖金 | 薪酬 | 奖金月份 |
|---|---|---|---|---|---|
| 120102 | M | | | | |

## Work.comp

| 员工 ID | 名字 | 姓 | 奖金 | 薪酬 | 奖金月份 |
|---|---|---|---|---|---|
| 120102 | Tom | Zhou | 500 | 108755 | 6 |

SAS 在每个 `DATA` 步迭代开始时会调整 PDV 中变量的大小。通过赋值语句创建的变量会被重置为缺失值，但通过 `SET` 语句读取的变量不会重置为缺失值。

## 执行

部分 `orion.sales`

| 员工 ID | 入职日期 |
|---|--|
| 120102 | 10744 |
| 120103 | 5114 |
| 120121 | 5114 |
| 120122 | 6756 |

```sas
data work.comp;
set orion.sales;
drop Gender Salary Job Title
Country Birth Date
Hire_Date;
Bonus=500;
Compensation=sum(Salary,Bonus);
BonusMonth=month(Hire_Date);
run;
```

## PDV

| 员工 ID | 性别 | 入职日期 | 奖金 | 薪酬 | 奖金月份 |
|---|---|---|---|---|---|
| 120103 | M | | 5114 | | |

## Work.comp

| 员工 ID | 名字 | 姓 | 奖金 | 薪酬 | 奖金月份 |
|---|---|---|---|---|---|
| 120102 | Tom | Zhou | 500 | 108755 | 6 |

## 执行

部分 `orion.sales`

| 员工 ID | 入职日期 |
|---|---||
| 120102 | 10744 |
| 120103 | 5114 |
| 120121 | 5114 |
| 120122 | 6756 |

```sas
data work.comp;
set orion.sales;
drop Gender Salary Job Title
Country Birth Date
Hire Date;
Bonus=500;
Compensation=sum(Salary,Bonus);
BonusMonth=month(Hire Date);
run;
```

## PDV

| 员工 ID | 性别 | 日期 | 奖金 | 薪酬 | 奖金月份 |
|---|---|---|---|---|---|
| 120103 | M | | 5114 | 500 | |

## Work.comp

| 员工 ID | 名字 | 姓_Name | 奖金 | 薪酬 | 奖金月份 |
|---|---|---|---|---|---|
| 120102 | Tom | Zhou | 500 | 108755 | 6 |

...

50

## 执行

部分 `orion.sales`

| 员工 ID | 入职日期 |
|---|---||
| 120102 | 10744 |
| 120103 | 5114 |
| 120121 | 5114 |
| 120122 | 6756 |

```sas
data work.comp;
set orion.sales;
drop Gender Salary Job Title
Country Birth Date
Hire Date;
Bonus=500;
Compensation=sum(Salary,Bonus);
BonusMonth=month(Hire Date);
run;
```
