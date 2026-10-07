

# 第 5 章：预定义包 77

此 DCL PACKAGE 语句根据定义的键和数据参数实例化了一个名为 h1 的哈希对象。

```
dcl package hash h1(
[SupplierID],[SupplierName SupplierAddress Country]);
```

- 1. **keys**（键）参数接受一个变量列表，并定义了用作查找数据键的变量。
- 2. **data**（数据）参数接受一个变量列表，指示成功查找后将返回的值。在示例中，**SupplierID** 是键，而 SupplierName、SupplierAddress 和 Country 是数据。
- 3. 第三个参数 **hashash**（哈希表达式）接受一个指数值 (n)，它定义哈希包的表大小为 2ⁿ。哈希表的大小并不等同于要存储的项目数量——每个容器实际上可以容无限数量的项目。对于较大的数据，使用较多的容器可以提高哈希表查找程序的的效率。你可能需要尝试不同的值，以找到你特定哈希对象性能的平衡点。*n* 的最大值为 16，可产生 64K 个容器。我们示例中的数据很小，因此我们将使用表达式为 1 的哈希表达式：

```
dcl package hash h1(
[SupplierID],[SupplierName SupplierAddress Country],1);
```

- 4. 第四个参数 **datasrc** 提供了加载到哈希对象中的数据集名称。你可以不提供数据集名称，而是选择提供一个基于 bases 的 FedEx 查询。这些哈希声明是等效的：

```
dcl package hash h1(
[SupplierID],[SupplierName SupplierAddress Country],1
,'crs.supplier');
```

```
dcl package hash h2(
[SupplierID],[SupplierName SupplierAddress Country],1
,'select * from crs.supplier');
```

- 5. 第五个参数 **ordered**（排序）描述了从哈希对象返回值的顺序。接受的值有 'ascending'（升序，'a' 或 'yes'）、'descending'（降序，'d'）或 'no'（此时数据返回顺序未定义）。默认值为 'no'。

```
dcl package hash h1(
[SupplierID],[SupplierName SupplierAddress Country],1
,'crs.supplier','a');
```

# 精通 SAS DS2 过程：高级数据处理技术

- 6. 第六个参数 **duplicate**（重复）决定在将表加载到哈希包时是否忽略重复键。有效值有 'add'、'replace' 和 'error'。默认值为 'add'，它存储第一个键值并忽略所有后续值。'Replace' 会重复项替换原始键值，导致只保留最后一个。'Error' 会在发现重复键时在 SAS 日志中报告错误。

```
dcl package hash h1(
  [SupplierID],[SupplierName SupplierAddress Country],1
  'crs.supplier', 'a', 'error');
```

- 7. 第七个参数 **suminc** 指定一个用于维护哈希包键汇总计数的变量。由于我们在演示中不使用此功能，因此我们只提供一个空值。

```
dcl package hash h1(
  [SupplierID],[SupplierName SupplierAddress Country],1
  'crs.supplier', 'a', 'error', 'no');
```

- 8. 最后一个参数 **multidata**（多数据）指定每个键是否允许对应多个数据项。有效值有 'multidata'/'yes'或'y'（允许键对应多个数据项），或 'singledata'/'no'或'n'（不允许键对应多个数据项）。默认值为 'no'。因为预计没有重复项，我们在示例中跳过了该参数的定义，但为了清晰起见，我们提供了 'no' 值：

```
dcl package hash h1(
  [SupplierID],[SupplierName Address Country],1
  'crs.supplier', 'a', 'error', 'no');
```

或者哈希对象可以在实例化时部分构造，并使用哈希包方法加载常量数据并定义键和值。由于这些值在使用哈希对象之前只需要设置一次，因此 INIT 方法是这些赋值的绝佳选择：

```
dcl package hash h1();
method init();
/* 哈希对象的定义通过方法调用完成 */
h1.keys((SupplierID));
h1.data((SupplierName Address Country));
h1.hex(1);
h1.dataset('crs.supplier');
h1.ordered('a');
h1.duplicate('error');
h1.multidata('no');
end;
```

## 5.3.2.2 使用哈希对象作为查找表

我们将使用上一节的代码来实例化哈希对象，然后使用对象的 FIND 方法根据键检索数据。FIND 如果找到则返回代码 0，如果未找到则返回非零。在这里我们使用 IF 过滤表达式来仅保留匹配键值的数据行：

```
proc ds2;
title "Product Information";
data;
dcl bigint Product_ID SupplierID;
dcl varchar(55) ProductName AddressCountry;
dcl package hash h1
[SupplierID],[Country],1
'crs.supplier', 'a', 'error', 'no');
method run();
set (select Product_ID SupplierID ProductName
from crs.productlist limit 10);
if h1.find(0) output;
end;
run;
quit;
```

**图 5.4:** 使用哈希对象技术生成的报告

| Product_ID | SupplierID | ProductName | SupplierName | Address | Country |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 210201009 | 3298 | Kids Round Neck,Large | A Team Sports | 2687 Anne Ct | US |
| 210201017 | 3298 | Sweatshirt Children's O-Neck | A Team Sports | 2687 Anne Ct | US |
| 210202022 | 6153 | Sunset Swimming Tricks | Nautilus Sports Inc | 56 Bagwell Ave | US |
| 210202023 | 6153 | Stockton Swimming Trunks Jr. | Nautilus Sports Inc | 56 Bagwell Ave | US |

## 5.3.3 迭代器包示例

哈希迭代器允许按正序或反序从哈希对象检索数据。在示例中，我们将使用两个哈希对象——一个用于价格信息，另一个用于产品信息以及一个价格对象的迭代器。我们将使用的迭代器方法是 FIRST、NEXT、LAST 和 PREV，允许我们从与迭代器关联的哈希对象获取第一个、下一个、最后一个和上一个记录。所有方法都产生零返回代码，表示执行成功。

## 5.3.3.1 使用哈希对象和迭代器对象查找数据集中的值

crs.pricelist 数据集包含所有产品的 ID 和定价信息。crs.productlist 数据集包含所有产品的 ID 和描述信息。我们将为每个数据集声明一个哈希对象。

```
dcl package hash prod([Product_ID], [ProductName],1
'crs.productlist','a');
dcl package hash price([UnitsSalesPrice], [Product_ID UnitSalesPrice]
,'crs.pricelist','a');
```

我们还会声明一个迭代器来正正反序访问价格哈希对象：

```
dcl package hash prod([Product_ID],[ProductName],1
'crs.productlist','a');
dcl package hash price([UnitSalesPrice],[Product_ID UnitSalesPrice]
1,'crs.pricelist','a');
dcl package hiter GetThe('price');
```

由于对数据集的所有工作将通过哈希对象完成，我们将显式控制流和行输出。这可以在数据程序中的任何系统方法完成，因此我选择了 INIT 方法：

```
proc ds2;
title "Lowest and Highest Cost Products"
data;
dcl bigint Product_ID;
dcl varchar(55) ProductName Ranking;
dcl decimal(10,2) UnitSalesPrice;
dcl package hash prod([Product_ID],[ProductName],1
,'crs.productlist','a');
dcl package hash price([UnitSalesPrice],[Product_ID
UnitSalesPrice]);
,'crs.pricelist','a');
dcl package hiter GetThe('price');
method init(rc);
dcl int rc;
Ranking='Lowest Cost';
GetThe.first();
rc=prod.find();
output;
Ranking='Second Lowest Cost';
GetThe.next();
rc=prod.find();
output;
Ranking='Second Highest Cost';
GetThe.last();
GetThe.prev();
rc=prod.find();
output;
Ranking='Highest Cost';
GetThe.last();
rc=prod.find();
output;
end;
data;
run;
quit;
```
