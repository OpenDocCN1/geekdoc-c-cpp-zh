
尽管在 SQL-92 语体内连接中 `ON` 子句是强制性的，但它并没有像外连接那样区分匹配谓词和过滤谓词。两者都被视为过滤谓词。因此，尽管从逻辑处理的角度来看，`WHERE` 子句应该在带有其所有的 `FROM` 子句之后评估，优化器完全可能在处理连接之前处理 `WHERE` 子句中的谓词。因为如果你检查这两个查询的计划，你会发现两个计划都从对 `Customers` 表聚集索引的扫描开始，并在扫描过程中应用过滤器。

我之前提到过，建议对连接使用 SQL-92 语法并避免 SQL-89 语法——我已经为这个建议提供了一个理由——对所有连接类型使用统一的风格。另一个原因是 SQL-89 语法更容易产生错误；具体来说，你更有可能漏掉连接谓词且这种错误未被察觉。在 SQL-92 语法中，你将每个连接谓词直接指定在相应的连接之后，如下：

```sql
FROM T1
INNER JOIN T2
ON T2.col1 = T1.col1
```

```sql
INNER JOIN T3
ON T3.col12 = T2.col12
INNER JOIN T4
ON T4.col13 = T3.col13
```

使用这种语法，漏掉连接谓词的概率很低，即使你漏掉了，解析器也会生成错误，因为对于内连接（以及外连接），`ON` 子句是强制性的。相反，使用 SQL-89 语法时，你在 `FROM` 子句中用逗号指定所有表名，并在 `WHERE` 子句中使用连接词指定所有谓词，如下所示：

```sql
FROM T1, T2, T3, T4
WHERE T2.col11 = T1.col01 AND T3.col12 = T2.col12 AND T4.col13 = T3.col13
```

显然，无意漏掉谓词的概率更高，导致你得到一个无意的交叉连接。

一个常见问题是使用 `INNER JOIN` 关键字和直接使用 `JOIN` 是否有区别。没有区别。标准 SQL 将内连接设置为默认连接，因为它是最常用的连接类型。以此类推，SQL 让 `OUTER` 关键字在外连接中变为可选。例如，`LEFT OUTER JOIN` 和 `LEFT JOIN` 是等价的。关于推荐使用哪种，最好使用完整语法以使其更清晰。其他人则倾向于使用简写语法，因为生成的代码更短。我认为，比使用完整语法还是简写语法更重要的是开发团队成员之间要保持一致性。当不同的人使用不同的风格时，维护彼此的代码可能会变得困难。一个好主意是在讨论完整语法与简写语法、缩进、大小写等风格时召开会议，并制定一份每个人都必须遵守的编码风格文档。有时人们根据个人偏好对某些样式方面有强烈的主张，因此当发生冲突时，可以通过投票来决定哪种方案占优。一旦大家开始使用一致的风格，人们维护相同代码就会变得容易得多。

## 外连接 (Outer join)

从逻辑查询处理的角度来看，外连接的起始步骤与内连接相同。但此外，它们还有第三个逻辑步骤，确保你标记为保留的表或表中的所有行都能被返回，即使这些行根据连接谓词在表中没有匹配项。使用关键字 `LEFT`（或 `LEFT OUTER`）、`RIGHT` 或 `FULL`，可以将左表、右表或两个表都标记为保留。表示非匹配项的输出行（作为外行）其非保留侧的列具有 `NULL`。

例如，以下查询返回了客户及其订单，包括没有订单的客户：

```sql
SELECT C.custid, C.companyname, C.country,
O.orderid, O.shipcity
FROM Sales.Customers AS C
LEFT OUTER JOIN Sales.Orders AS O
ON C.custid = O.custid;
```

在外连接中，`ON` 子句中谓词的作用与内连接不同。在后者中，它只是一个简单的过滤工具，而前者则充当一个更复杂的匹配工具。保留侧的所有行都将能够返回，无论它们是否根据谓词找到了匹配的行。如果你需要应用某些过滤器，可以在 `WHERE` 子句中指定它们。例如，识别非匹配项的一种经典方法是使用外连接并添加一个 `WHERE` 子句，只过滤出那些在非保留侧不允许 `NULL` 的列中为 `NULL` 的行。主键是此目的的良好选择。例如，以下查询仅返回下过订单的客户：

```sql
SELECT C.custid, C.companyname, C.orderid
FROM Sales.Customers AS C
LEFT OUTER JOIN Sales.Orders AS O
ON C.custid = O.custid
WHERE O.orderid IS NULL;
```

使用左连接的人比使用右连接的人多得多。大多数人倾向于在查询中先看被引用的表，通常被引用的表是那些在引用表中没有匹配项的表。确实，在单个情况下如 `T1 LEFT OUTER JOIN T2`，你可以用对称的 `T2 RIGHT JOIN T1` 相同的内容。然而，在涉及多个连接的复杂情况下，你会发现右连接比使用左连接提供了更简单的解决方案。我稍后会在“多连接查询”部分演示这种情况。

## 自连接 (Self join)

自连接是同一张表的多个实例之间的连接。例如，以下查询将员工与其经理（经理也是员工）进行匹配：

```sql
SELECT E.firstname + ' ' + E.lastname AS emp, M.firstname + ' ' + M.lastname AS mgr
FROM HR.Employees AS E
LEFT OUTER JOIN HR.Employees AS M
ON E.mgrid = M.empid;
```

自连接的特殊之处在于必须为表的实例分配不同的别名；否则会出现重复的列名，包括表名前缀。

从优化的角度来看，优化器将这两个实例视为两个不同的表。例如，它可以为每个实例使用不同的索引。在查询计划中，你可以识别每个物理对象代表的是分配给它的表别名的哪个实例。

## 等值连接与非等连接 (Equi and non-equi joins)

等连接和非等连接的术语指的是你在连接谓词中使用的运算符类型。当你使用相等运算符时（如大多数查询所示），该连接被称为等连接。当你使用等号以外的运算符时，该连接被称为非等连接。

有很多原因可能导致优化器选择次优的连接顺序。和其他次优选择一样，连接顺序的选择可能会受到不准确的基数估计的影响。

此外，即使表的数量较少，可能的连接顺序（或称连接树）的理论数量也可能是非常巨大的。Benjamin Nevare 在此处的“Optimizing Join Orders”中解释了这一点：http://www.benjaminnevare.com/2010/06/optimizing-join-orders/。可能树的数量为 (2N−2)! / (N−1)，其中 `!` 是阶乘。例如，如果我们有 5 张表，将产生 1,680 种可能的树。 如果有 N 张表，这个数字是 17,643,225,600! 这里的 i 表示惊叹，而不是表示阶乘，谢天谢地。正如你可能意识到的，如果优化器真的尝试探索所有可能的连接树，优化过程将花费过长时间并变得适得其反。优化器根据涉及表的大小计算基于成本和基于时间的阈值，如果达到其中一个值，就会执行优化步骤。优化器通常不考虑将连接结果再次连接的 Implementation形连接树（bushy join trees）；此类树占了其大部分比例。这意味着优化器可能无法产生真正的最优连接顺序。

如果你怀疑情况确实如此并想强制优化器使用特定顺序，可以通过按照你认为最优的顺序输入连接，并遵循 `ORDER` 查询提示来实现，如下：

```sql
SELECT DISTINCT C.companyname AS customer, S.companyname AS supplier
FROM Sales.Customers AS C
INNER JOIN Sales.Orders AS O
ON O.custid = C.custid
INNER JOIN Sales.OrderDetails AS OD
ON OD.order = O.order
INNER JOIN Production.Products AS P
ON P.productid = OD.productid
INNER JOIN Production.Suppliers AS S
ON S.supplierid = P.supplierid
OPTION (FORCE ORDER);
```

此提示无疑是一个你可以使用的故障排除工具，用来测试不同顺序的性能，并观察优化器在需要时是否选择了次优方案。在生产代码中使用此类提示的问题在于，它使优化的这部分变得静态。通常情况下，索引、数据特征和其他因素的变化会导致优化器连接顺序选择的改变，但在使用提示时显然不会。该提示适合作为故障排除工具使用，有时在关键情况下作为生产环境中的短期临时解决方案。然而，它通常不适合作为长期解决方案。例如，假设导致次优顺序选择的原因是糟糕的基数估计。当你有时间对问题进行彻底研究时，我希望你能找到帮助优化器产生更准确估计的方法，从而自然地产生更优的计划。

# 控制逻辑连接顺序

你刚刚学会了如何控制物理连接顺序。在某些情况下，你需要控制逻辑连接顺序以实现查询含义的特定变化。例如，考虑上一节中返回客户-供应商对的查询：

```sql
SELECT DISTINCT C.companyname AS customer, S.companyname AS supplier
FROM Sales.Customers AS C
INNER JOIN Sales.Orders AS O
  ON O.custid = C.custid
INNER JOIN Sales.OrderDetails AS OD
  ON OD.orderid = O.orderid
INNER JOIN Production.Products AS P
  ON P.productid = OD.productid
INNER JOIN Production.Suppliers AS S
  ON S.supplierid = P.supplierid;
```

此查询返回 1,236 行。所有的连接都是内连接。这意味着没有下过订单的客户没有返回。在我们的示例数据中，有两个这样的客户。假设你需要更改方案以包含没有订单的客户。直观的方法是将 Customers 和 Orders 之间的连接类型更改为外连接，如下：

```sql
SELECT DISTINCT C.companyname AS customer, S.companyname AS supplier
FROM Sales.Customers AS C
LEFT JOIN Sales.Orders AS O
  ON O.custid = C.custid
INNER JOIN Sales.OrderDetails AS OD
  ON OD.orderid = O.orderid
INNER JOIN Production.Products AS P
  ON P.productid = OD.productid
INNER JOIN Production.Suppliers AS S
  ON S.supplierid = P.supplierid;
```

然而，如果你运行该查询，你会发现它的结果与之前相同。在逻辑上，Customers 和 Orders 之间的外连接返回了没有订单的客户（在 `O.orderid` 列中为 NULL）。当使用内连接连接结果时，这些行被删除了。这是因为与 `O.orderid` 列比较 NULL 值是未知的。你可以将其概括为：任何外连接如果随后跟着内连接或右外连接，都会导致外连接实际上变成内连接。这是假设你将外连接保留侧的元素与另一个表的元素比较。人们尝试解决问题的常用方法是将所有连接都变为左外连接，如下：

```sql
SELECT DISTINCT C.companyname AS customer, S.companyname AS supplier
FROM Sales.Customers AS C
LEFT OUTER JOIN Sales.Orders AS O
  ON O.custid = C.custid
LEFT OUTER JOIN Sales.OrderDetails AS OD
ON OD.orderid = O.orderid
LEFT OUTER JOIN Production.Products AS P
ON P.productid = OD.productid
LEFT OUTER JOIN Production.Suppliers AS S
ON S.supplierid = P.supplierid;
```

该方案有两个问题。一个问题是它实际上改变了预期的查询。Customers 和连接结果之间的剩余表不应该被保留；但在该方案中，如果它们是左的，就会被保留。另一个问题是优化器在处理外连接时改变连接顺序的灵活性较小。它唯一的灵活性是将 `T1 LEFT JOIN T2` 更改为 `T1 RIGHT JOIN T2`。

更好的解决方案是在 Customers 等表之间使用内连接，然后对 Customers 应用右外连接，如下：

```sql
SELECT DISTINCT C.companyname AS customer, S.companyname AS supplier
FROM Sales.Orders AS O
INNER JOIN Sales.OrderDetails AS OD
ON OD.orderid = O.orderid
INNER JOIN Production.Products AS P
ON P.productid = OD.productid
INNER JOIN Production.Suppliers AS S
ON S.supplierid = P.supplierid
RIGHT OUTER JOIN Customers
ON O.custid = C.custid;
```

现在方案在语义上是正确的，并返回 8 行，包含了没有下订单的客户。有一种更优雅的解决方案允许你以类似的方式表示连接。记得要在 Customers 和剩余表的结果之间应用左连接。要定义这样一个单元，只需将内连接包含在括号中，如下：

```sql
SELECT DISTINCT C.companyname AS customer, S.companyname AS supplier
FROM Sales.Customers AS C
LEFT JOIN (
    Sales.Orders AS O
    INNER JOIN Sales.OrderDetails AS OD ON OD.orderid = O.orderid
    INNER JOIN Production.Products AS P ON P.productid = OD.productid
    INNER JOIN Production.Suppliers AS S ON S.supplierid = P.supplierid
) ON O.custid = C.custid;
```

奇怪的是，括号并不是必须的。如果你移除并运行代码，你会发现它运行成功并返回正确的结果。真正产生差异的是类似括号的单元安排以及 `ON` 子句的位置。考虑到这一点，以下是单元的另一种安排方式，可以实现所需的结果：

```sql
SELECT DISTINCT C.companyname AS customer, S.companyname AS supplier
FROM Sales.Customers AS C
LEFT JOIN Sales.Orders AS O
INNER JOIN Sales.OrderDetails AS OD
INNER JOIN Production.Products AS P
INNER JOIN Production.Suppliers AS S
ON S.supplierid = P.supplierid
ON P.productid = OD.productid
ON OD.orderid = O.orderid
ON O.custid = C.custid;
```

我早提到提到，优化器用于减少优化时间的启发式算法之一是不考虑涉及结果连接的计划。如果你怀疑这种形计划（bushy plan）是最有效的，且优化器需要强制执行。你实现这一点的方法是定义两个单元，每个单元都基于带有相应 `ON` 子句的连接，然后跟一个关联这两个单元的 `ON` 子句。你还需要指定 `FORCE ORDER` 选项。

以下是强制此类形计划的示例：

```sql
SELECT DISTINCT C.companyname AS customer, S.companyname AS S
FROM Sales.Customers AS C
INNER JOIN
(Sales.Orders AS O INNER JOIN Sales.OrderDetail AS OD
ON OD.orderid = O.orderid)
INNER JOIN
(Production.Products AS P INNER JOIN Production.Suppliers AS S
ON S.supplierid = P.supplierid)
ON P.productid = OD.productid
ON O.custid = C.custid
OPTION (FORCE ORDER);
```
