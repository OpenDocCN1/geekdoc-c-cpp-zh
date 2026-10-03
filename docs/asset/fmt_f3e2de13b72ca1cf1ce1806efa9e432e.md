
```sas
proc print data=orion.nonsales
var Employee_ID Job Title Salary Gender
format Salary salrange Gender $gender;
title1 'Distribution of Salary and Gender Values';
title2 'For Non-Sales Employees';
run;
```

e. 提交程序。

# 9. 创建嵌套格式定义

a. 获取初始程序。

b. 创建一个自定义格式。

```sas
proc format;
value dategrp
  ='None'
  low-'31dec2006'd=[year4]
  '01jan2007'-d-high=[monyy7].
run;
```

11.7 解决方案

11-97

```sas
proc freq data=orion.employee_payroll;
tables Employee_Term_Date / missing;
format Employee_Term_Date dategrp.;
title 'Employee Status Report';
```

c. 应用新格式。

d. 提交程序。

# 11. 子集提取与观测分组

a. 获取初始程序。

b. 添加一个 `PROC SORT` 步骤。

```sas
proc sort data=orion.order_fact out=order_sorted;
by order_type;
run;
```

c. 限制 `PROC MEANS` 分析。

```sas
proc means data=order_sorted;
where order_type in (2,3);
var Total Retail Price;
title 'Orion Star Sales Summary';
run;
```

d. 修改 `PROC MEANS` 步骤。

```sas
proc means data=order_sorted;
by order_type;
where order_type in (2,3);
var Total Retail Price;
title 'Orion Star Sales Summary';
run;
```

e. 提交程序。

# 11. 按多个变量进行子集提取与分组

a. 获取初始程序。

b. 排序数据集。

```sas
proc sort data=orion.order_fact out=order_sorted;
by Order_Type descending Order_Date;
run;
```

c. 分割 `PROC PRINT` 报告。

```sas
proc print data=order_sorted;
by Order_Type;
var Order_ID Order Date Delivery Date;
title 'Orion Star Sales Details';
run;
```

d. 限制 `PROC PRINT` 报告中的观测值。

```sas
proc print data=order_sorted;
by Order_Type;
var Order_ID Order Date Delivery_Date;
where Delivery_Date - Order_Date = 2
and Order_Date between '01jan2005'd and '30apr2005'd;
titlel 'Orion Star Sales Details';
run;
```

e. 添加第二个标题。

```sas
proc print data=order_sorted;
by Order_Type;
var Order_ID Order Date Delivery_Date;
where Delivery_Date - Order_Date = 2
and Order_Date between '01jan2005'd and '30apr2005'd;
titlel 'Orion Star Sales Details';
title2 '2-Day Deliveries from January to April 2005';
run;
```

f. 提交程序。

# 12. 添加子集条件

a. 获取初始程序。

b. 重新排序 `PROC PRINT` 步骤中的变量。

```sas
proc format;
value $country
"CA"="Canada"
"DK"="Denmark"
"ES"="Spain"
"GB"="Great Britain"
"NL"="Netherlands"
"SE"="Sweden"
"US"="United States";
run;
```

```sas
proc sort data=orion.shoe_vendors out=vendors_by_country;
by Supplier_Country;
run;
```

```sas
proc print data=vendors_by_country;
where Product_ID=21;
by Supplier_Country notsorted;
var Product_ID Name;
titlel 'Orion Star Products: Children';
run;
```

c. 增强现有标准。

```sas
proc format;
value $country
"CA"="Canada"
"DK"="Denmark"
"ES"="Spain"
"GB"="Great Britain"
"NL"="Netherlands"
"SE"="Sweden"
"US"="United States";
run;
```

```sas
proc sort data=orion.shoe_vendors out=vendors_by_country;
by Supplier_Country;
run;
```

```sas
proc print data=vendors_by_country;
where Product_ID=21;
and Product_Name = 'Street'; /* 根据上下文修正 */
and Product_Name = 'Running'; /* 根据上下文修正 */
by Supplier_Country notsorted;
var Product_ID Name;
title 'Orion Star Products: Children';
run;
```

d. 提交程序。

# 13. 将输出重定向到 PDF 和 RTF 目标

a. 获取初始程序。

b. 创建 `PROC PRINT` 报告的 PDF 版本。

```sas
ods pdf file='p11ls13p.pdf';
proc print data=orion.customer;
title 'Customer Information';
run;
ods pdf close;
```

对于 z/OS (OS390), 使用以下 ODS 语句：

```sas
ods pdf file='.workshop.report();
```

d. 修改你的 ODS 语句以创建 `PROC PRINT` 报告的 RTF 版本。

```sas
ods rtf close;
```

对于 z/OS (OS390), 使用以下 ODS RTF 语句：

```sas
ods rtf file='.workshop.report(p11ls13r)' rs=none;
```

e. 抑制默认列表。

```sas
ods listing;
ods rtf file='p11ls13r.rtf';
proc print data=orion.customer;
title 'Customer Information';
run;
ods rtf close;
```

f. 提交程序。如果将 `RUN` 语句移动到程序末尾会发生什么？文件是空的。

g. 添加 `STYLE` 参数。

```sas
ods listing;
ods rtf file='p11ls13r.rtf' style=curve;
proc print data=orion.customer;
title 'Customer Information';
run;
ods rtf close;
```

h. 提交程序。

# 14. 创建兼容 Excel 的 ODS 输出

a. 获取初始程序。

b. 添加 ODS 语句将报告发送到可以在 Excel 中查看的文件。

```sas
ods csvall file='p11ls14.csv';
proc print data=orion.customer;
title 'Customer Type Definitions';
run;
```

```sas
proc print data=orion.country;
title 'Country Definitions';
run;
ods csvall close;
```

对于 z/OS (OS390), 使用以下 ODS CSVALL 语句：

```sas
ods csvall file='.workshop.report(p11ls14)' rs=none;
ods msoff2k file='p11ls14.html' style=Listing;
proc print data=orion.customer_type;
title 'Customer Type Definitions';
run;
```

```sas
proc print data=orion.country;
title 'Country Definitions';
run;
ods msoff2k close;
```

对于 z/OS (OS390), 使用以下 ODS MSSOFFICE2K 语句：

```sas
ods msoff2k file='.workshop.report(p11ls14)' rs=none;
tagsets.excelp file='p11ls14.xml' style=Listing;
proc print data=orion.customer_type;
title 'Customer Type Definitions';
run;
```

```sas
proc print data=orion.country;
title 'Country Definitions';
run;
tagsets.excelp close;
```

对于 z/OS (OS390), 使用以下 ODS TAGSETS.EXCELP 语句：

```sas
tagsets.excelp file='.workshop.report(p11ls14)' rs=none;
```

c. 提交程序。

d. 使用 Microsoft Excel 打开文件。

# 15. 在 ODS 输出中添加 HTML 特性

a. 获取初始程序。

b. 创建 `PROC PRINT` 报告的 HTML 版本。

```sas
ods html file='p11ls15.html';
proc print data=orion.customer;
title 'Customer Information';
run;
ods html close;
```

对于 z/OS (OS390), 使用以下 ODS HTML 语句：

```sas
ods html file='.workshop.report(p11ls15)' rs=none;
```

c. 自定义标题使其成为可点击超链接。

```sas
ods html file='p11ls15.html';
proc print data=orion.customer;
title link='http://www.sas.com' 'Customer Information';
run;
ods html close;
```

d. 提交程序。

# 16. 使用 ODS 实现层级样式表 (CSS)

a. 获取初始 HTML 程序。

b. 修改 ODS HTML 语句。

```sas
ods html file='p11ls16.html' stylesheet=(url='p11le16c.css');
proc print data=orion.customer_type;
title 'Customer Type Definitions';
run;
ods html close;
```

对于 z/OS (OS390), 使用以下 ODS HTML 语句：

```sas
ods html file='.workshop.report(p11ls16)' rs=none
stylesheet=(url='.workshop.report(p11le16c)');
```

c. 提交程序。

# 学生活动解答（投票/测验）

## 11.01 投票 – 正确答案

日期和/或时间变化了吗？

- 是

- 否

`DTRESET`选项使用当前日期和时间，而不是 SAS 调用的日期和时间。

```sas
options date number pageno=1 ls=100 dtreset;
```

## 11.02 测验 – 正确答案

哪个脚注出现在第二个过程输出中？

| a. 非销售部门员工 | c. 非销售部门机密 |

| --- | --- |

| b. Orion Star 非销售部门员工 | d. Orion Star 非销售部门机密 |

```sas
footnote1 'Orion Star';
proc print data=orion.sales;
footnote2 'Sales Employees';
footnote3 'Confidential';
run;
proc print data=orion.nonsales;
footnote2 'Non Sales Employees';
run;
```

## 11.03 测验 – 正确答案

关于 `Bonus` 的 `PROC PRINT` 输出，哪个陈述是正确的？

- a. Annual Bonus（年终奖金）将是标签。

- b. Mid-Year Bonus（中期奖金）将是标签。

临时标签会覆盖永久标签。

## 11.04 测验 – 正确答案

对于给定的格式，哪个显示值是错误的？

| 格式 | 存储值 | 显示值 |

| --- | --- | --- |

| $3. | Wednesday | Wed |

| 6.1 | 1234.345 | 1234,3 |

| COMMAX5. | 1234.345 | 1.234 |

| DOLLAR9. | 1234.345 | $1,234.35 |

| DDMMYY8. | 0 | 01/01/1960 |

| DATE9. | 0 | 01JAN1960 |

| YEAR4. | 0 | 1960 |

`DDMMYY8.` 产生 01/01/60。

## 11.05 多选题投票 – 正确答案

哪些用户定义的格式名称是无效的？

- a. $stfmt

- b. $3levels

- c. _4years

- d. salranges

- e. dollar

字符格式必须以美元符号作为第一个字符，以字母或下划线作为第二个字符。

用户定义的格式不能与 SAS 提供的格式相同。

## 11.06 测验 – 正确答案

如果你有一个值为 99999.87 的值，对该值应用 `TIERS` 格式后将如何显示？

- a. Tier 2

- b. Tier 3

- c. 缺失值

- d. 以上都不是

```sas
proc format;
    value tiers 20000-49999 = 'Tier 1'
                  50000-99999 = 'Tier 2'
                  100000-250000 = 'Tier 3';
run;
```

## 11.07 测验 – 正确答案

如果你有一个值为 100000 的值，对该值应用 `TIERS` 格式后将如何显示？

- a. Tier 2

- b. Tier 3

- c. 100000

- d. 缺失值

| proc format; | 20000-<50000 = 'Tier 1' |

| value tiers | 50000-100000 = 'Tier 2' |

| 100000-<250000 = 'Tier 3'; |

| run; | |

## 11.08 测验 – 正确答案

以下哪些 `WHERE` 语句是无效的？

- a. where Salary ne

- b. where Hire_Date >='01APR2008'

- c. where Country in (AU);

- d. where Salary <=10000;

- e. where Gender ne 'M'

- f. where Salary >=50000;

## 11.09 多选题 – 正确答案

关于多个 `WHERE` 语句，哪个陈述是正确的？

- a. 所有的 `WHERE` 语句都使用了。

- b. 没有一个 `WHERE` 语句被使用。

- c. 第一个 `WHERE` 语句被使用了。

- d. 最后一个 `WHERE` 语句被使用了。

```sas
1000 proc freq data=orion.sales;
1001 tables Gender;
1002 where Salary > 75000;
1003 where Country = 'US';
NOTE: Where clause has been replaced.
1004 run;
```

## 11.10 测验 – 正确答案

哪个是 `FREQ` 步骤的 `BY` 语句？

- a. by Country Gender;

- b. by Gender Last;

- c. by Country;

- d. by Gender;
