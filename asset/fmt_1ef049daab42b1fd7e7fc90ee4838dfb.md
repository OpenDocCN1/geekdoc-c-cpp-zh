
# 9.3 观测值 9-51

## 练习

### 等级 1

#### 7. 根据两个条件筛选观测值

a. 将观测值提取到向量。
b. 在 `DATA` 步中编写语句，选择 `Hire_Date` 大于等于 2006 年 7 月 1 日的观测值。
c. 在 `DATA` 步中编写另一个语句，选择增加大于 300 的观测值。
d. 提交程序创建以下报告：

| Obs | Employee ID | Annual Salary | Increase | New Salary |
|---|---|---|---|---|
| 1 | 120128 | 30,890 | 01NOV2005 | 33,979 |
| 2 | 120144 | 30,265 | 01OCT2006 | 33,292 |
| 3 | 120161 | 30,785 | 01OCT2006 | 33,864 |
| 4 | 120264 | 37,510 | 01DEC2006 | 41,261 |
| 5 | 120761 | 30,960 | 01JUL2006 | 34,056 |
| 6 | 120995 | 34,850 | 01AUG2006 | 38,335 |
| 7 | 121055 | 30,185 | 01AUG2006 | 33,204 |
| 8 | 121062 | 30,305 | 01AUG2006 | 33,336 |
| 9 | 121185 | 32,235 | 01JAN2007 | 35,459 |
| 10 | 121107 | 31,380 | 01JUL2006 | 34,518 |

### 等级 2

#### 8. 根据三个条件筛选观测值

a. 编写一个 `DATA` 步创建 `Work.delays`。
b. 创建新变量 `Order_Month`，等于 `Order_Date` 的月份。
c. 使用 `WHERE` 语句和子集 `IF` 语句筛选出所有条件的观测值：
* `Delivery_Date` 比 `Order_Date` 晚四天
* `Employee_ID` 等于 99999
* `Order_Month` 为 8 月份
d. 编写一个 `PROC PRINT` 步创建以下报告：

| Obs | Order_ID | Type | Employee_ID | Customer_ID | Order_Date | Delivery_Date | Month |
|---|---|---|---|---|---|---|---|
| 1 | 123127910 | 2 | 99999 | 70187 | 13AUG2003 | 18AUG2003 | 8 |
| 2 | 123127067 | 3 | 99999 | | 20AUG2003 | 26AUG2003 | 8 |
| 3 | 123130552 | 2 | 99999 | 16 | 27AUG2003 | 04SEP2003 | 8 |
| 4 | 123131744 | 2 | 99999 | 61 | 29AUG2003 | 03SEP2003 | 8 |
| 5 | 123348479 | 3 | 99999 | 255 | 10AUG2004 | 15AUG2004 | 8 |
| 6 | 123351453 | 3 | 99999 | 70201 | 15AUG2004 | 20AUG2004 | 8 |
| 7 | 123667373 | 3 | 99999 | 9 | 10AUG2005 | 15AUG2005 | 8 |
| 8 | 124605145 | 2 | 99999 | 71 | 30AUG2006 | 05SEP2006 | 8 |
| 9 | 124316957 | 3 | 99999 | 70201 | 24AUG207 | 29AUG27 | 8 |

### 等级 3

#### 9. 使用 `IF-THEN DELETE` 语句筛选观测值

a. 编写一个 `DATA` 步创建 `orion.donations`。
b. 创建新变量 `Total`，等于 `Qtr1`、`Qtr2`、`Qtr3` 和 `Qtr4` 的和。
c. 创建新变量 `NoDonation`，等于 `Qtr1`、`Qtr2`、`Qtr3` 和 `Qtr4` 中缺失值的数量。使用 `MISSING` 函数。
> 关于 `MISSING` 函数的文档可以在 `SAS Help and Documentation` 的 `SAS Base 9.2 Language Reference -> Dictionary -> Language Elements -> Functions and CALL` 中找到。
d. 最终数据集应仅包含符合两个条件的观测值：
* `Total` 大于或等于 50
* `NoDonation` 等于 0
使用 `IF-THEN DELETE` 语句消除不符合条件的观测值。
> `IF-THEN DELETE` 语句在本节末的自学部分提到。
e. 编写一个带有 `VAR` 语句的 `PROC PRINT` 步创建以下报告：

部分 `PROC PRINT` 输出（50 个观测值中的前 7 个）

| Obs | Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 | Total | No Donation |
|---|---|---|---|---|---|---|---|
| 1 | 120267 | 15 | 15 | 15 | 15 | 60 | 0 |
| 2 | 120269 | 20 | 20 | 20 | 20 | 80 | 0 |
| 3 | 120271 | 20 | 20 | 20 | 20 | 80 | 0 |
| 4 | 120275 | 15 | 15 | 15 | 15 | 60 | 0 |
| 5 | 120660 | 25 | 25 | 25 | 25 | 100 | 0 |
| 6 | 120669 | 15 | 15 | 15 | 15 | 60 | 0 |
| 7 | 120671 | 20 | 20 | 20 | 20 | 80 | 0 |

# 9.4 章节回顾

## 章节回顾

- 1. 使用 `SUM` 函数代替算术运算符有什么优势？
- 2. 在 `DATA` 步中，`DROP`/`KEEP` 语句是从输入数据集还是输出数据集中删除了变量？
- 3. 你会在什么情况下在 `DATA` 步中使用 `DO` 组语句？
- 4. 在赋值语句中创建的数值变量的默认长度是多少？

# 9.5 答案

## 练习解答

### 1. 创建两个新变量

a. 获取初始程序。
b. 创建两个新变量。

```sas
data work.increase;
set orion.staff;
Increase=Salary*0.10;
NewSalary=sum(Salary, Increase);
run;
```

```sas
proc print data=work.increase label;
run;
```

c. 仅包含四个变量。

```sas
data work.increase;
set orion.staff;
Increase=Salary*0.10;
NewSalary=sum(Salary, Increase);
keep Employee_ID Salary Increase NewSalary;
run;
```

```sas
proc print data=work.increase label;
run;
```

d. 格式化三个变量。

```sas
data work.increase;
set orion.staff;
Increase=Salary*0.10;
NewSalary=sum(Salary, Increase);
keep Employee_ID Salary Increase NewSalary;
format Salary Increase NewSalary comma10.;
run;
```

```sas
proc print data=work.increase label;
run;
```

### 2. 创建三个新变量

a. 一个 `DATA` 步。

```sas
data work.birthday;
set orion.customer;
run;
```

b. 创建三个新变量。

```sas
data work.birthday;
set orion.customer;
Bday2009=mdy(month (Birth_Date),day (Birth_Date),2009);
BdayDW2009=weekday (Bday2009);
Age2009=(Bday2009-Birth_Date)/365.25;
run;
```

c. 仅包含五个变量。

```sas
data work.birthday;
set orion.customer;
Bday2009=mdy(month (Birth_Date),day (Birth_Date),2009);
BdayDW2009=weekday (Bday2009);
Age2009=(Bday2009-Birth_Date)/365.25;
keep Customer_Name Birth_Date Bday2009 BdayDW2009 Age2009;
run;
```

d. 格式化两个变量。

```sas
data work.birthday;
set orion.customer;
Bday2009=mdy(month (Birth_Date),day (Birth_Date),2009);
BdayDW2009=weekday (Bday2009);
Age2009=(Bday2009-Birth_Date)/365.25;
keep Customer_Name Birth_Date Bday2009 BdayDW2009 Age2009;
format Bday2009 date9. Age2009 3.;
run;
```

e. 写一个 `PROC PRINT` 步。

```sas
proc print data=work.birthday;
run;
```

### 3. 使用 `CATX` 和 `INTCK` 函数创建变量

a. 写一个 `DATA` 步。

```sas
data work.employees;
set orion.sales;
run;
```

b. 创建新变量 `FullName`。

```sas
data work.employees;
set orion.sales;
FullName=catx(' ', 'First_Name', 'Last_Name');
run;
```

c. 创建新变量 `Yrs2012`。

```sas
data work.employees;
set orion.sales;
FullName=catx(' ', 'First_Name', 'Last_Name');
Yrs2012=intck('year', 'Hire_Date', '01JAN2012'd);
run;
```

d. 格式化 `Hire_Date`。

```sas
data work.employees;
set orion.sales;
FullName=catx(' ', 'First_Name', 'Last_Name');
Yrs2012=intck('year', Hire_Date, '01JAN2012'd);
format Hire_Date ddmmyy10.
run;
```

e. 添加一个标签。

```sas
data work.employees;
set orion.sales;
FullName=catx(' ', 'First_Name', 'Last_Name');
Yrs2012=intck('year', Hire_Date, '01JAN2012'd);
format Hire_Date ddmmyy10;
label Yrs2012='Years of Employment in 2012';
run;
```

f. 写一个 `PROC PRINT` 步。

```sas
proc print data=work.employees label;
var FullName Hire_Date Yrs2012;
run;
```

### 4. 条件地创建变量

a. 获取初始程序。
b. 创建三个新变量。

```sas
data work.region;
set orion.staff;
```
*(注：原文此处为 `set orion.staff;` 但根据上下文应为 `set orion.supplier;` 此处按原文翻译)*

```sas
data work.region;
set orion.staff;
```

```sas
length Region $17;
if Country in ('CA','US') then do
Discount=10;
DiscountType='Required';
Region='North America';
else do
Discount=05;
DiscountType='Optional';
Region='Not America';
end;
run;
```

```sas
proc print data=work.region;
run;
```

c. 仅包含五个变量。

```sas
data work.region;
set orion.supplier;
length Region $17;
if Country in ('CA','US') then do
Discount=10;
DiscountType='Required';
Region='North America';
else do
Discount=05;
DiscountType='Optional';
Region='Not America';
end;
keep Name Country Region;
run;
```

```sas
proc print data=work.region;
run;
```

d. 提交程序。

### 5. 无条件和有条件的创建变量

a. 写一个 `DATA` 步。

```sas
data work.ordertype;
set orion.orders;
run;
```

b. 创建新变量 `DayOfWeek`。

```sas
data work.ordertype;
set orion.orders;
DayOfWeek=weekday(Order_Date);
run;
```

c. 创建新变量 `Type`。

```sas
data work.ordertype;
set orion.orders;
length Type $13;
DayOfWeek=weekday(Order_Date);
if Order_Type=1 then do
Type='Catalog Sale';
else if Order_Type=2 then do
Type='Internet Sale';
else if Order_Type=3 then do
Type='Retail Sale';
end;
run;
```

d. 创建新变量 `SaleAds`。

```sas
data work.ordertype;
set orion.orders;
length Type $13 Ads $5;
DayOfWeek=weekday(Order_Date);
if Order_Type=1 then do
Type='Catalog Sale';
Ads='Mail';
else if Order_Type=2 then do
Type='Internet Sale';
Ads='Email';
else if Order_Type=3 then do
Type='Retail Sale';
end;
run;
```

e. 不包含三个变量。

```sas
data work.ordertype;
set orion.orders;
length Type $13 Ads $5;
DayOfWeek=weekday(Order_Date);
if Order_Type=1 then do
Type='Catalog Sale';
Ads='Mail';
else if Order_Type=2 then do
Type='Internet Sale';
Ads='Email';
else if Order_Type=3 then do
Type='Retail Sale';
end;
drop Order_Type Employee_ID Customer_ID;
run;
```

f. 写一个 `PROC PRINT` 步。

```sas
proc print data=work.ordertype;
run;
```

### 6. 在 `SELECT` 组中使用 `WHEN` 语句条件创建变量

a. 写一个 `DATA` 步。

```sas
data work.gifts;
set orion.nonsales;
run;
```

b. 创建两个新变量。

```sas
data work.gifts;
set orion.nonsales;
length Gift1 Gift2 $15;
select (Gender)
when ('F') do
Gift1='Perfume';
Gift2='Cookware';
end
when ('M') do
Gift1='Cologne';
Gift2='Lawn Equipment';
end
otherwise do
Gift1='Coffee';
Gift2='Calendar';
end;
run;
```

c. 仅包含五个变量。

```sas
data work.gifts;
```
