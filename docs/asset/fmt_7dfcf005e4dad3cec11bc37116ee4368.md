
INNER JOIN dbo.EmployeesNS AS C
  ON P.emid = 3
  AND C.lft BETWEEN P.lft AND P.rgt
ORDER BY C.lft;

| empid | empname |
|---|---|
| 3 | Ina |
| 7 | Aaron |
| 11 | Gabriel |
| 9 | Rita |
| 14 | Didi |
| 12 | Emilia |
| 13 | Michael |

查询连接 `EmployeesNS`。一个代表父节点 (`P`)，并通过指定的根进行过滤；另一个代表子节点 (`C`)，根据子节点的左和右值连接。你可能想使用 `C.lft >= P.lft AND C.rgt` 而不是 `C.lft BETWEEN P.lft AND P.rgt`。在嵌套集合模型中，后者的含义相同，但由于后者仅基于一个范围而不是两个，在索引访问方面的效率更高。输出的缩进通过从子级别减去父级别并重复 `'|'` 字符串来实现。输出按子节点的左值排序，这定义了拓扑排序，即兄弟节点的排序。此子树查询是大多数后续查询的基础。

### 返回限制根节点下节点数量的子树

```sql
SELECT C.emid, REPLICATE(' | ', C.lvl - P.lvl) + C.empname
FROM dbo.EmployeesNS AS P
INNER JOIN dbo.EmployeesNS AS C
  ON P.emid = 3
  AND C.lft BETWEEN P.lft AND P.rgt
WHERE C.lvl - P.lvl <= 2
ORDER BY C.lft;
```

| empid | empname |
|---|---|
| 3 | Ina |
| 7 | Aaron |
| 11 | Gabriel |
| 9 | Rita |

### 返回给定根节点的叶子节点

```sql
SELECT C.emid, C.empname
FROM dbo.EmployeesNS AS P
INNER JOIN dbo.EmployeesNS AS C
  ON P.emid = 3
  AND C.lft BETWEEN P.lft AND P.rgt
WHERE C.rgt - C.lft = 1;
```

| empid | empname |
|---|---|
| 11 | Gabriel |
| 14 | Didi |
| 12 | Emilia |
| 13 | Michael |

叶子节点是右值比左值大 1 的节点（没有下属）。将此过滤器添加到子树查询的 `WHERE` 子句中。你可以看到，嵌套集合识别叶子节点的速度比使用 `NOT EXISTS` 谓词的解决方案快得多。

### 返回每个节点的下属数量

```sql
SELECT empid, (rgt - lft - 1) / 2 AS cnt, REPLICATE(' | ', lvl) + empname
FROM dbo.EmployeesNS
ORDER BY lft;
```

| empid | cnt | empname |
|---|---|---|
| 1 | 13 | David |
| 2 | 5 | Eitan |
| 5 | | Jiru |
| 8 | 0 | Lilach |
| 10 | 0 | Sean |
| 4 | | Seraph |
| 6 | | Steve |
| 3 | | Ina |
| 7 | 5 | Aaron |
| 11 | | Gabriel |
| 9 | 3 | Rita |
| 14 | 0 | Didi |
| 12 | 0 | Emilia |
| 13 | 0 | Michael |

因为每个节点恰好对应两个 `lft` 和 `rgt` 值，在我们的实现中不存在间隙，你可以通过访问子树的根节点来计算下属数量。数量是 `(rgt - lft - 1) / 2`。

### 返回节点的所有祖先

```sql
SELECT P.empid, P.empname, P.lvl
FROM dbo.EmployeesNS AS P
INNER JOIN dbo.EmployeesNS AS C
  ON C.empid = 14
  AND C.lft BETWEEN P.lft AND P.rgt;
```

| empid | empname | lvl |
|---|---|---|
| 1 | David | 0 |
| 3 | Ina | 1 |
| 7 | Aaron | 2 |
| 9 | Rita | 3 |
| 14 | Didi | 4 |

祖先查询与子树查询几乎相同。唯一的区别是，这里你过滤一个特定的子节点 ID，而在子树查询中你过滤的是特定的父节点 ID。遗憾的是，从性能角度来看，路径/祖先查询无法像子图/后代查询那样被优化，因为祖先节点在索引叶节点中并不是连续的范围。

## 传递闭包

有向图 `G` 的传递闭包是一个与 `G` 具有相同节点的图，其中对于 `G` 中通过路径（不一定仅包含一条边）连接的每对节点，都有一条边相连。传递闭包有助于立即回答许多问题，而无需在图中遍历路径。例如，David 是 Aaron 的经理（直接或间接）吗？如果 `Employees` 图的传递闭包包含一条从 David 到 Aaron 的边，那么就是。Espresso 咖啡机包含水吗？我可以从洛杉矶开车到纽约吗？如果输入图包含边 `(a, b)` 和 `(b, c)`，且 `a` 和 `c` 之间存在传递关系，那么传递闭包包含边 `(a, b)`、`(b, c)` 以及 `(a, c)`。如果 David 是 Ina 的直接经理，而 Ina 是 Aaron 的直接经理，那么 David 就是 Aaron 的传递经理，或者说是 David 的下属。

与传递闭包的问题涉及传递关系的特殊情况。一个例子是“最短路径”问题，你试图确定两个节点之间的最短路径。例如，从洛杉矶到纽约的最短路径是什么？

在本节中，我将描述传递闭包和最短路径问题的迭代/递归解决方案。

![](img/bdc38aa36f6e2987d913ee5381474711_811_0.png)

> **注意** 我将展示的某些解决方案（特别是那些使用递归 CTE 的方案）其性能会随着输入量的增长而呈指数级下降。我展示它们是为了演示目的，因为它们非常简单且自然。它们对于小图是足够的。某些与传递闭包相关的算法（例如 Floyd 算法和 Marshall 算法）可以在“层级”（广度优先）迭代的基础上实现。关于这些细节，请参考 `http://www.nist.gov/dads/`。我将展示适用于更大图的高效解决方案。

## 有向无环图

我将讨论第一个问题是生成有向无环图 (`DAG`) 的传递闭包。稍后我还会向你展示如何处理无向图和循环图。图是有向还是无向都不会显著增加解决方案的复杂度，但处理循环图会。我在示例中使用的输入 `DAG` 是在本章节之前提到的 `BOM`，它是通过运行列表 11-2 中的代码创建的。

生成 `BOM` 传递闭的代码与子图问题（即零件展开）的解决方案类似。具体而言，你使用广度优先搜索技术遍历图。然而，这里不是只返回根节点，锚点成员（`anchor member`）返回了 `BOM` 中所有的第一级关系。在大多数情况下，这意味着任何组装/目标对，其中组装是 `BOM`。在我们的情况下，这意味着任何组装/目标对，其中组装代表下一级或父级 (`P`)，而代表原始产品 ID (`P`) 的 `BOM` 是源，代表子产品 ID (`C`) 是目标。外部查询返回不同的组装/零件对。请记住，`BOM` 中可能有多条路径指向某个零件，但你只需要返回返回每个唯一对。

运行以下代码生成 `BOM` 的传递闭包：

```sql
WITH BOMTC AS (
  -- 返回所有第一级包含关系
  SELECT assemblyid, partid
  FROM dbo.BOM
  WHERE assemblyid IS NOT NULL
  UNION ALL
  -- 返回下一级包含关系
  SELECT P.assemblyid, C.partid
  FROM BOMTC AS P
  INNER JOIN dbo.BOM AS C
    ON C.assemblyid = P.partid
)
-- 返回具有
-- 传递关系的不同对
SELECT DISTINCT assemblyid, partid
FROM BOMTC;
```

此代码生成了以下输出：

| assemblyid | partid |
|---|---|
| 1 | 6 |
| 1 | 7 |
| 1 | 10 |
| 1 | 13 |
| 1 | 14 |
| 2 | 6 |
| 2 | 7 |
| 2 | 10 |
| 2 | 11 |
| 2 | 13 |
| 2 | 14 |
| 3 | 6 |
| 3 | 7 |
| 3 | 11 |
| 3 | 12 |
| 3 | 14 |
| 3 | 16 |
| 3 | 17 |
| 4 | 9 |
| 4 | 12 |
| 4 | 14 |
| 4 | 16 |
| 4 | 17 |
| 5 | 9 |
| 5 | 12 |
| 5 | 14 |
| 5 | 16 |
| 5 | 17 |
| 10 | 13 |
| 10 | 14 |
| 12 | 14 |
| 12 | 16 |
| 12 | 17 |
| 16 | 17 |

此解决方案通过在外部查询中使用 `DISTINCT` 子句消除了 `BOMTC` 中发现的边。一种更高效的解决方案是在反复运行的查询中使用 `NOT EXISTS` 谓词来完全避免获取它们；该谓词会过滤掉未出现在已找到边集中的新边。然而，这种实现无法使用 CTE 中的递归成员，因为它只能访问直接的前一个层，而不是到为止获得的所有以前层。相反，你可以使用 `UDF` 或存储过程，在循环中反复调用查询并将每一层插入工作表。运行以下代码来创建 `BOMTC`，它实现了这种逻辑：

```sql
DROP FUNCTION dbo.BOMTC
CREATE FUNCTION BOMTC() RETURNS @BOMTC TABLE (
    assemblyid INT NOT NULL,
    partid INT NOT NULL,
    PRIMARY KEY (assemblyid, partid)
)
AS
BEGIN
    INSERT INTO @BOMTC(assemblyid, partid)
    SELECT assemblyid, partid
    FROM dbo.BOM
    WHERE assemblyid IS NOT NULL
    DECLARE @rowcount INT
    SELECT @rowcount = COUNT(*) FROM @BOMTC
    WHILE @rowcount > 0
    BEGIN
        INSERT INTO @BOMTC(assemblyid, partid)
        SELECT DISTINCT P.assemblyid, C.partid
        FROM @BOMTC AS P
        INNER JOIN dbo.BOM AS C ON C.assemblyid = P.partid
        WHERE NOT EXISTS (
            SELECT 1 FROM @BOMTC AS P2
            WHERE P2.assemblyid = P.assemblyid
            AND P2.partid = C.partid
        )
        SELECT @rowcount = COUNT(*) FROM @BOMTC
    END
    RETURN
```

获取 `BOM` 传递闭包的查询：`SELECT assemblyid, partid FROM BOMTC();`

如果你想返回 `BOM` 中所有路径及其距离，请使用带有距离计算的类似算法。这与子树解决方案类似：锚点为第一层分配常量 1，递归成员在每次迭代中加 1。最后，外部查询简单使用 `DISTINCT` 返回所有路径。运行以下代码生成 `BOM` 中所有可能的路径及其距离：

```sql
WITH BOMPaths AS -- 所有路径
  SELECT assemblyid, partid, 1 AS distance,
  '.' + CAST(assemblyid AS VARCHAR(MAX)) +
  '.' + CAST(partid AS VARCHAR(MAX)) + '.' AS path
  FROM dbo.BOM
  WHERE assemblyid IS NOT NULL
  UNION ALL
  SELECT P.assemblyid, C.partid, P.distance + 1,
  P.path + CAST(C.partid AS VARCHAR(MAX)) + '.'
  FROM BOMPaths AS P
  INNER JOIN dbo.BOM AS C ON C.assemblyid = P.partid
),
BOMrn AS -- 路径排名
  SELECT *, RANK() OVER(PARTITION BY assemblyid, partid ORDER BY distance) AS rnk
  FROM BOMPaths
)
-- 返回所有路径
SELECT assemblyid, partid, distance, path
FROM BOMrn
WHERE rnk = 1;
```
