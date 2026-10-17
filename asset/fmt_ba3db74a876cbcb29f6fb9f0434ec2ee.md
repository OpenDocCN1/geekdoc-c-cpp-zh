
# PROC SQL 示例

## 产品分类查询

```sql
PROC SQL;
    SELECT *
        FROM
            (SELECT PRODNAME,
                    PRODNUM,
                    CASE SUBSTR(PUT(PRODNUM,4.),1,1)
                        WHEN '1' THEN 'Laptop/Workstation'
                        WHEN '2' THEN 'Phone'
                        WHEN '5' THEN 'Software'
                        ELSE 'Unknown'
                    END AS Product_Classification
             FROM PRODUCTS
            )
    WHERE Product_Classification = 'Software';
QUIT;
```

## Results

| Product Name | Product Number | Product_Classification |

|---|---|---|

| Spreadsheet Software | 5001 | Software |

| Database Software | 5002 | Software |

| Wordprocessor Software | 5003 | Software |

| Graphics Software | 5004 | Software |

## Simple CASE Expression in a WHERE Clause

在上一节中，我们研究了 SELECT 子句中简单 CASE 表达式的语法和应用。在本节中，我们将探讨 WHERE 子句中简单 CASE 表达式的语法和应用。由于 SQL 过程支持在任何可以使用表达式的地方使用 CASE 表达式，我们将了解到查询可以通过将 CASE 表达式的结果值直接传递给 WHERE 子句来代替硬编码值而受益。

## SQL Code

```sql
PROC SQL;
    SELECT MANUNAME,
        MANUSTAT
    FROM MANUFACTURERS
    WHERE CASE MANUSTAT
        WHEN 'CA' THEN 1
        ELSE 0
    END;
QUIT;
```

## Results

| Manufacturer Name | Manufacturer State |

|---|---|

| Global Comm Corp | CA |

| Storage Devices Inc | CA |

| KPL Enterprises | CA |

| San Diego PC Planet | CA |

## Creating a Customized List with a Simple CASE Expression

可以使用 SELECT 和 ORDER BY 子句中的简单 CASE 表达式对显示和顺序进行自定义编码。以下示例说明了通过为 PRODUCTS 表中的每个产品编码单独的 Case 逻辑来创建产品和可用性列表的独特方法。生成的输出显示值为 “1” 以指示其对输出列表有贡献，或值为 “0” 以指示其未对输出列表有贡献。

## SQL Code

```sql
OPTIONS LS=120;
PROC SQL;
SELECT PRODNAME,
    PRODCOST,
    CASE PRODTYPE WHEN 'Laptop'      THEN 1 ELSE 0 END
        AS LaptopRequest,
    CASE PRODTYPE WHEN 'Workstation' THEN 1 ELSE 0 END
        AS WorkstationRequest,
    CASE PRODTYPE WHEN 'Phone'       THEN 1 ELSE 0 END
        AS PhoneRequest,
    CASE PRODTYPE WHEN 'Software'    THEN 1 ELSE 0 END
        AS SoftwareRequest
FROM PRODUCTS
ORDER BY CASE PRODTYPE WHEN 'Laptop'      THEN 1 ELSE 0 END,
    CASE PRODTYPE WHEN 'Workstation' THEN 1 ELSE 0 END,
    CASE PRODTYPE WHEN 'Phone'       THEN 1 ELSE 0 END,
    CASE PRODTYPE WHEN 'Software'    THEN 1 ELSE 0 END;
QUIT;
```

## Results

| Product Name | Product Cost | LaptopRequest | WorkstationRequest | PhoneRequest | SoftwareRequest |

|---|---:|---:|---:|---:|---:|

| Wordprocessor Software | $299.00 | 0 | 0 | 0 | 1 |

| Graphics Software | $299.00 | 0 | 0 | 0 | 1 |

| Spreadsheet Software | $299.00 | 0 | 0 | 0 | 1 |

| Database Software | $399.00 | 0 | 0 | 0 | 1 |

| Office Phone | $130.00 | 0 | 0 | 1 | 0 |

| Digital Cell Phone | $175.00 | 0 | 0 | 1 | 0 |

| Analog Cell Phone | $35.00 | 0 | 0 | 1 | 0 |

| Dream Machine | $3,200.00 | 0 | 1 | 0 | 0 |

| Business Machine | $3,300.00 | 0 | 1 | 0 | 0 |

| Travel Laptop | $3,400.00 | 1 | 0 | 0 | 0 |

## Simple CASE Expression in a HAVING Clause

HAVING 子句用于在 SQL 查询中过滤 GROUP BY 子句中指定的聚合。在此示例中，SELECT 子句返回 MANUFACTURERS 表中的制造商名称及其居住州。HAVING 子句中的 CASE 表达式将 SELECT 子句返回的内容限制为仅居住在加利福尼亚州的制造商。

## SQL Code

```sql
PROC SQL;
    SELECT MANUNAME,
           MANUSTAT
    FROM MANUFACTURERS
    HAVING CASE MANUSTAT
           WHEN 'CA' THEN 1
           ELSE 0
           END;
QUIT;
```

## Results

The SAS System

| Manufacturer Name | Manufacturer State |

|---|---|

| Global Comm Corp | CA |

| Storage Devices Inc | CA |

| KPL Enterprises | CA |

| San Diego PC Planet | CA |

在下一个示例中，SELECT 子句返回 PRODUCTS 表中最昂贵的产品（s），并且 HAVING 子句中的 CASE 表达式将结果限制为成本超过 $300.00 的软件产品。

## SQL Code

```sql
PROC SQL;
    SELECT PRODNAME,
            PRODTYPE,
            MAX(PRODCOST) AS Product_Cost FORMAT=DOLLAR10.2
    FROM PRODUCTS
    HAVING CASE PRODTYPE
            WHEN 'Software' THEN PRODCOST
            ELSE 0
        END > 300;
QUIT;
```

## Results

The SAS System

| Product Name | Product Type | Product_Cost |

|---|---|---|

| Database Software | Software | $3,400.00 |

## Simple CASE Expression in a Join Construct

可以在 JOIN 构造中指定 CASE 表达式以过滤 GROUP BY 子句中指定的聚合。在此示例中，SELECT 子句返回 MANUFACTURERS 表中的制造商名称及其居住州。CASE 表达式在 HAVING 子句中将 SELECT 子句返回的内容限制为仅居住在加利福尼亚州的制造商。

## SQL Code

```sql
PROC SQL;
    SELECT PRODNAME,
           PRODTYPE,
           MANUNAME
    FROM PRODUCTS P,
         MANUFACTURERS M
    WHERE P.MANUNUM = M.MANUNUM AND
          CASE PRODTYPE
            WHEN 'Software' THEN 1
            ELSE 0
          END;
QUIT;
```

## Results

![](img/9d3e4d8fa063e50a0c9985e34cf9d6e8_154_0.png)

## Preventing Division by Zero with a Simple CASE Expression

除零错误可能导致查询出现许多问题，包括严重的性能下降。在下一个示例中，在 SELECT 子句中指定了一个简单的 CASE 表达式以防止除零错误。使用 INVENTORY 表，CASE 表达式告诉 SAS 忽略对 INVENQTY 值为零的产品执行任何计算（通过分配布尔值 false）。否则，将计算方程 INVENCST / INVENQTY，并且 WHERE 子句将选择成本超过 $1,000.00 的产品。使用 AS 关键字为新列分配名为 Average_Cost 的列标题。

## SQL Code

```sql
PROC SQL;
    SELECT PRODNUM,
           INVENQTY,
           INVENCST,
           CASE INVENQTY
               WHEN 0 THEN 0
               ELSE INVENCST / INVENQTY
           END AS Average_Cost FORMAT=DOLLAR10.2
    FROM INVENTORY
    WHERE INVENCST / INVENQTY > 1000;
QUIT;
```

### 结果

| 产品编号 | 库存数量 | 库存成本 | 平均成本 |

|---:|---:|---:|---:|

| 1110 | 20 | $45,000.00 | $2,250.00 |

| 1700 | 10 | $28,000.00 | $2,800.00 |

在下一个示例中，一个简单的 CASE 表达式在 WHERE 子句中实现，以防止除零错误。与之前一样，CASE 表达式的 WHEN 条件告诉 SAS 忽略对 INVENQTY 值为零的产品执行任何计算（通过分配布尔值 false）。否则，计算等式 INVENCST / INVENQTY，并由 WHERE 子句选择成本超过 $1,000.00 的产品。

### SQL 代码

```sql
PROC SQL;
    SELECT PRODNUM,
           INVENQTY,
           INVENCST
    FROM INVENTORY
    WHERE CASE INVENQTY
          WHEN 0 THEN 0
          ELSE INVENCST / INVENQTY
          END > 1000;
QUIT;
```

### 结果

| 产品编号 | 库存数量 | 库存成本 |

|---:|---:|---:|

| 1110 | 20 | $45,000.00 |

| 1700 | 10 | $28,000.00 |

### 嵌套简单 CASE 表达式

关于软件构建相关的技术，尤其是与程序和/或代码设计相关的方面，已经有很多论述。当讨论程序复杂性时，人们普遍认为，通过将解决方案分解为更小的部分，可以降低程序的复杂程度。这种思维规则在 Steve McConnell 的《代码大全：软件构建的实用手册》第二版（2004）中得到了最好的讨论：“人类往往更容易理解几个简单的信息片段，而不是一个复杂的信息片段。”

尽管存在许多改善程序设计过程的设计策略，但经常被提及的一种策略是嵌套过程。嵌套涉及将复杂和/或繁琐的逻辑场景转换为两个（或更多）更简单的逻辑条件。其主要目标是提高程序的可维护性和可读性。SQL 过程支持使用 CASE 表达式结构进行嵌套，进一步强化了这一思维规律。

嵌套是一种有用的技术，因为它为 SQL 用户提供了一种处理复杂代码的有效方式。但是，不必要的嵌套或仅为嵌套而嵌套实际上会使代码更难理解和维护。根据我的经验，嵌套绝不应超过三到四层。超过这个深度，复杂程度会显著增加。一般规则是编写不仅易于理解，而且希望包含更少错误的代码。为了说明嵌套过程，一个简单的 CASE 表达式被嵌套两层，用于识别 PRODUCTS 表中成本低于 $300.00 的软件产品。

### SQL 代码

```sql
PROC SQL;
    SELECT PRODNAME,
            PRODTYPE,
            PRODCOST,
            CASE PRODTYPE
                WHEN 'Software' THEN
                    CASE
                        WHEN PRODCOST < 300 THEN 'Match'
                        ELSE 'No Match'
                    END
                ELSE 'Not Software'
            END AS Product_Type_Cost
    FROM PRODUCTS;
QUIT;
```

### 结果

### SAS 系统

| 产品名称 | 产品类型 | 产品成本 | 产品类型成本 |

|---|---|---|---|

| 梦想机器 | 工作站 | $3,200.00 | 非软件 |

| 商务机器 | 工作站 | $3,300.00 | 非软件 |

| 旅行笔记本电脑 | 笔记本电脑 | $3,400.00 | 非软件 |

| 模拟手机 | 手机 | $35.00 | 非软件 |

| 数字手机 | 手机 | $175.00 | 非软件 |

| 办公电话 | 手机 | $130.00 | 非软件 |

| 电子表格软件 | 软件 | $299.00 | 匹配 |

| 数据库软件 | 软件 | $399.00 | 不匹配 |

| 文字处理软件 | 软件 | $299.00 | 匹配 |

| 图形软件 | 软件 | $299.00 | 匹配 |

### 使用简单 CASE 表达式条件性更新表

可以指定 CASE 表达式来条件性更新表的内容。有关更新表中数据的更多信息，请参阅第 6 章“修改和更新表与索引”。该示例说明了使用 UPDATE 语句和简单 CASE 表达式条件性更新表中数据的过程，将 PURCHASES 表中“Chair”的单位成本（UNITCOST）从 $179.00 增加 $10.00 至 $189.00。

注意：表必须以更新模式打开才能更新其内容。

### SQL 代码

```sql
PROC SQL;
    TITLE1 'Before Update Operation';
    SELECT *
        FROM PURCHASES2;
    UPDATE PURCHASES2
        SET UNITCOST = UNITCOST +
            CASE ITEM
                WHEN 'Chair' THEN 10.00
                ELSE 0
            END;
    TITLE1 'After Update Operation';
    SELECT *
    FROM PURCHASES2;
QUIT;
```

### 结果

### 更新操作前

| 客户编号 | 项目 | 单位数量 | 单位成本 |

|---|---|---|---|

| 1 | 椅子 | 1 | $179.00 |

| 1 | 笔 | 12 | $0.89 |

| 1 | 纸 | 4 | $6.95 |

| 1 | 订书机 | 1 | $8.95 |

| 7 | 鼠标垫 | 1 | $11.79 |

| 7 | 笔 | 24 | $1.59 |

| 13 | 马克笔 | . | $0.99 |

### 更新操作后

| 客户编号 | 项目 | 单位数量 | 单位成本 |

|---|---|---|---|

| 1 | 椅子 | 1 | $189.00 |

| 1 | 笔 | 12 | $0.89 |

| 1 | 纸 | 4 | $6.95 |

| 1 | 订书机 | 1 | $8.95 |

| 7 | 鼠标垫 | 1 | $11.79 |

| 7 | 笔 | 24 | $1.59 |

| 13 | 马克笔 | . | $0.99 |
