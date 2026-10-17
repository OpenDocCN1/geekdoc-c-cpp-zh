
我的朋友 Laurent Martin 将此称为“竖琴函数”（harp function）。这个外号看起来可能很困惑，直到你查看图 3-13 显示的查询计划。

![](img/bdc38aa36f6e2987d913ee5381474711_242_0.png)

图 3-13 竖琴函数。

该计划的巧妙之处在于，`Top` 运算符是从右侧分支请求行的那个，一旦达到请求的行数它就会短路。分别处理行号计算和交叉连接的 `Sequence Project` 和 `Nested Loops` 算子会响应来自 `Top` 算子的行请求。一旦 `Top` 停止请求，它们也会随停止生成行。换句话说，尽管这个解决方案可能生成超过四十亿行，但在实践中它只生成请求的行数然后短路。在我的笔记本上测试该函数的性能，它在四秒钟内生成了 100,000 个数字。这还不算差。

## APPLY 算子

`APPLY` 算子是我知道的 T-SQL 最强大的工具之一，但它似乎没有被许多注意到。当我讲解 `APPLY` 时，学生只掌握了一小部分。这个算子的有趣之处在于，它可以以非常有创意的方式来解决各种任务。`APPLY` 有三种类型：

- `CROSS APPLY`
- `OUTER APPLY`
- `ER APPLY`

接下来的章节将描述这些类型。

## CROSS APPLY 算子

思考 `APPLY` 算子的一种方式将其视为交叉连接和相关子查询的混合体。想一下普通的连接（join）。输入是表或表表达式，但不允许有内部查询。`CROSS APPLY` 算子类似于交叉连接，只是右侧输入允许来自左侧输入的关联。在交叉连接中，左侧输入允许是自包含。

`T1 JOIN T2` 等同于 `T1 CROSS APPLY T2`。

为了可复用性，将解决方案封装在一个名为 `GetNums` 的内联 TVF 中，如下：

```sql
IF OBJECT_ID('dbo.GetNums', 'FN') IS NOT NULL DROP FUNCTION dbo.GetNums;

GO

CREATE FUNCTION dbo.GetNums(@low AS BIGINT, @high AS BIGINT) RETURNS TABLE
AS
RETURN
WITH
L0 AS (SELECT c FROM (VALUES(1),(1)) AS D(c)),
L1 AS (SELECT 1 AS c FROM L0 AS A CROSS JOIN L0 AS B),
L2 AS (SELECT 1 AS c FROM L1 AS A CROSS JOIN L1 AS B),
L3 AS (SELECT 1 AS c FROM L2 AS A CROSS JOIN L2 AS B),
L4 AS (SELECT 1 AS c FROM L3 AS A CROSS JOIN L3 AS B),
L5 AS (SELECT 1 AS c FROM L4 AS A CROSS JOIN L4 AS B),
Nums AS (SELECT ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS rownum FROM L5)
SELECT TOP(@high - @low + 1) @low + rownum - 1 AS n
FROM Nums
ORDER BY rownum;

GO
```

使用以下代码测试该函数：

```sql
SELECT n FROM dbo.GetNums(11, 20);
```
