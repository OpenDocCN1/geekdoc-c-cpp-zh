
9-24 第 9 章 合并 SAS® 数据集

| 120400311465 | 13 | Thomas Leitmann |
| 120400312556 | 7 | Robyn Klem |
| 120400315078 | 23 | Tonie Asmussen |
| 120400312678 | 10 | Theunis Brazier |

## 9.2 答案

练习题

- 1. 对两个数据集执行等值合并（Match-Merge）
```sas
data revenue
NotSold(keep=Price Product_ID Product_Name)
InvalidCode(keep=Product_ID Quantity Customer);
merge orion.web_products(in=InProduct)
      orion.web_orders(in=InOrders)
  by Product_ID;
  if InProduct and InOrders then do;
    Revenue=Quantity * Price;
    output revenue;
end;
  else if InProduct and not InOrders then output notold;
  else if not InProduct and InOrders then output invalidcode;
run;
```
```sas
title 'Revenue from Orders';
proc print data=revenue noobs;
run;
```
```sas
title 'Products Not Ordered';
proc print data=notsold noobs;
run;
```
```sas
title 'Invalid Orders';
proc print data=invalidcode noobs;
run;
```

- 2. 处理同名变量和不同数据类型的 BY 变量
```sas
data web_connected(drop=nProduct_ID);
  length Product_ID = $12;
  set orion.web_products2(rename=(Product_ID=nProduct_ID));
  Product_ID=put(nProduct_ID, 12.);
run;
data revenue
NotSold(keep=Price Product_ID Product_Name)
InvalidCode(keep=Product_ID Quantity Customer);
merge web_connected(in=InConv rename=(Name=Product_Name))
      orion.web_orders2(in=InOrders rename=(Name=Customer))
  by Product_ID;
```
if InConv and InOrders then do;
  Revenue=Quantity * Price;
  output revenue;
else if InConv and not InOrders then output notsold;
else if not InConv and InOrders then output invalidcode;
run;
title 'Revenue from Orders';
proc print data=revenue noobs;
run;
title 'Products Not Ordered';
proc print data=notsold noobs;
run;
title 'Invalid Orders';
proc print data=invalidcode noobs;
run;
title;

## 学生活动（调查/测验）答案

### 9.01 多项选择调查 – 正确答案

- 关于等值合并（match-merging），哪个陈述是正确的？
a. MERGE 语句必须引用永久数据集。
b. BY 语句中的变量只能存在于其中一个数据。
c. MERGE 语句中只能指定两个数据集。
d. 当结合 BY 语句使用 MERGE 语句时，数据必须按 BY 变量排序或索引。

## 9.02 简答调查 – 正确答案

编写适当的 IF 语句创建仅包含非匹配项的所需数据集。

```sas
data combine;
merge products(in=InProd) costs(in=InCost);
by ID;

if InProd=0 or InCost=0;

run;
```

| Product | ID | | ID | Cost | | Product | ID | Cost |
|---|---|---|---|---|---|---|---|
| XYZ Shoe | A123 | | B456 | 59.99 | | XYZ Shoe | A123 | |
| ABC Coat | B456 | | C789 | 35.75 | | C789 | 35.75 | |

## 9.03 简答调查 – 正确答案

由于 BY 语句创建了两个临时变量？

```sas
data orders (keep=Customer_Name Quantity Product ID Total Retail Price)
noorders (keep=Customer_Name Birth_Date);
merge orion.customer
  work.order_fact(in=order);
by Customer_ID;
if order=1 then output orders;
else output noorders;
```
First.Customer_ID 和 Last.Customer_ID

## 9.04 简答调查 – 正确答案

以下数据集是否有共同变量？不，这些数据集没有共享同一个共同变量。因此，它们不能在一个 DATA 步中合并。

| orion.customer | work.order_fact | orion.product_dim |
|---|---|---|
| Customer_ID | Customer_ID | Product_ID |
| Country | Employees ID | Product_Line |
| Gender | Street_ID | Product Category |
| Personal_ID | Order_Date | Product Group |
| Customer_Name | Delivery_Date | Product Name |
| Customer_FirstName | Order_ID | Supplier_Country |
| Customer_LastName | Order_Type | Supplier_Name |
| Birth Date | Product_ID | Supplier_ID |
| Customer_Address | Quantity | ... |

## 9.05 测验 – 正确答案

哪些陈述正确访问了 Excel 工作簿中的 Supplier 工作表？

- a.
libname bonus "BonusGift.xls";
```sas
proc print data=bonus.Supplier;
```

- b.
libname bonus "BonusGift.xls";
```sas
proc print data=bonus.Supplier;
```

![](img/d3bde6e6ab06b1fc622215d982111742_400_0.png)

## 第 10 章 创建和维护永久格式

10.1 创建永久格式 ................................................................................ 10-3
演示：使用控制数据集创建格式 ................................................................. 10-12
演示：维护永久格式 ....................................................... 10-18
练习题 ................................................................................................................ 10-19

10.2 答案 .......................................................................................................... 10-21

练习题答案 ........................................................................... 10-21
学生活动答案（调查/测验） ........................................ 10-25

## 10.1 创建永久格式

### 目标

- 从 SAS 数据集创建格式。
- 创建永久格式。
- 访问永久格式。
- 维护格式。

![](img/d3bde6e6ab06b1fc622215d982111742_404_0.png)

业务场景
管理层要求在报告中使用国家名称而非国家代码。

| Country | Population | Country_ID |
|---|---|---|
| AU | 20,000,000 | 160 |
| CA | | |
| DE | | |
| IL | | |

![](img/d3bde6e6ab06b1fc622215d982111742_404_0.png)
| Country | Population | Country_ID |
|---|---|---|
| AU | 20,000,000 | 160 |
| CA | | |
| DE | | |
| IL | | |

## 10-4 创建格式

### 创建格式（回顾）

使用 PROC FORMAT 创建格式。

```sas
proc format;
$country 'AU' = 'Australia'
            'CA' = 'Canada'
            'DE' = 'Germany'
            'IL' = 'Israel'
            'TR' = 'Turkey'
            'US' = 'United States'
            'ZA' = 'South Africa';
run;
```

### 使用控制数据集创建格式

不需要在 PROC FORMAT 中输入所有值，可以从包含代码和值的数据集创建格式。

## 使用控制数据集创建格式

| Country | Country_Name | Population | Country_ID | Continent_ID | FormerName |
|---|---|---|---|---|---|
| AU | Australia | 20,000,000 | 160 | | |
| CA | Canada | | 260 | | |
| DE | Germany | 80,000,000 | 394 | | East/West |
| IL | Israel | 5,000,000 | 475 | | |

```sas
ndata country;
keep Start Label FmtName;
retain FmtName '$country';
set orion.country (rename=(Country=Start));
run;
```
CNTLIN数据集具有以下特性：

- 如果没有找到 End，假设格式范围的结束值等于 Start 的值
- 可用于创建新格式，也可重新创建现有格式
- 必须按 FmtName 分组

### FmtName

- 长度可达32个字符
- 对于字符格式，以美元符号 ($)开头，后跟字母或下划线
- 对于数值格式，以字母或下划线开头
- 不能以数字结尾
- 不能是SAS格式的名称

## 使用控制数据集创建格式

使用 CNTLIN 选项读取数据并创建格式。

```sas
proc format cntlin=country;
run;
CNTLIN=SAS-data-set;
```

为了从 CNTLIN数据集创建格式，需要 FmtName、Start 和 Label 变量。

## 调查设置

以下 DATA 步都创建了名为 country 的 SAS 数据集。

| data country; keep Start Label FmtName; Program 1 |
| retain FmtName '$country'; |
| set orion.country (rename=(Country=Start Country_Name=Label)); |
| run; |

| data country; keep Start Label FmtName; Program 2 |
| FmtName='$country'; |
| set orion.country; start-Country; Label=Country_Name; |
| run; |

