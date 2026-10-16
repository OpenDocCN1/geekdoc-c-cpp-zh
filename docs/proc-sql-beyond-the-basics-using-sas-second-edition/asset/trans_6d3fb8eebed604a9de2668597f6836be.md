

## 表 9.1：调试流程步骤与任务

| 调试步骤 | 任务描述 |
|---|---|
| 问题识别 | 1. 确定代码中是否存在 bug。<br>2. 通过扮演侦探来确定问题是什么。<br>3. 描述为什么该问题是一个 bug。<br>4. 确定代码应该做什么。<br>5. 确定代码正在做什么。 |
| 信息收集 | 1. 收集用户评论和反馈。<br>6. 收集个人观察和症状。<br>7. 查看 SAS 日志信息。<br>8. 收集突出问题的测试用例。<br>9. 捕获环境信息（例如，系统设置、运行环境、外部元素等）。 |
| 问题评估与分类 | 1. 提出关于问题原因的理论。<br>10. 查看代码。<br>11. 将问题分类为以下类别之一：<br>- 需求问题<br>- 语法错误<br>- CPU 问题<br>- 内存问题<br>- 存储问题<br>- I/O 问题<br>- 逻辑问题 |
| 问题解决 | 1. 提出解决方案。<br>12. 描述为什么该解决方案能修复问题。<br>13. 验证该解决方案不会导致额外问题。<br>14. 通过实施解决方案修复问题。 |
| 验证解决方案 | 1. 验证问题是否仍然存在。<br>15. 验证问题是否可以重新创建或重现。<br>16. 确定是否其他方法会导致相同问题发生。<br>17. 验证解决方案不会导致其他问题。 |

## 问题类型

SQL 编程问题的常见原因包括误用语言语法；错误引用数据，尤其是列数据；忽略或错误指定系统参数；以及构建语法正确但逻辑不良的代码，导致结果不符合预期。

使用错误可能导致 SAS 停止处理、产生警告或产生意外结果。表 9.2 说明了四种使用错误类型并简要描述了每种类型。

## 表 9.2：使用错误类型

| 问题 | 描述 |
|---|---|
| 语法 | 语法问题是由于违反了一个或多个 SQL 过程语言结构造成的。这些问题可能阻止程序处理，直到您做出必要的更改。例如，在 SELECT 语句中引用的变量在引用表中找不到，会导致程序停止。 |
| 数据 | 数据问题是由于数据与程序规范不一致造成的。这些问题可能阻止程序处理，但也可能允许处理继续并导致分配缺失、不完整或不可靠的数据。例如，当字符数据被错误引用为数值数据时，列中可能会生成缺失值。 |
| 系统相关 | 系统相关问题通常是由于指定不兼容的系统选项或选择错误的系统选项值造成的。这些问题可能阻止程序处理，但最常见的是允许处理以不令人满意的结果进行。例如，忘记指定标题语句对输出的产生影响很小，但可能会迫使程序在添加一个或多个标题后重新运行。 |
| 逻辑 | 逻辑问题通常是由于未正确指定编码条件造成的。例如，当需要 AND 条件时指定 OR 条件，可能会在没有任何警告、错误或注释的情况下产生错误结果。 |

其他问题来源可能因多种原因出现在程序中。表 9.3 说明了这些其他问题来源并简要描述了每个来源。

## 表 9.3：其他错误类型

| 问题 | 描述 |
|---|---|
| 功能蔓延 | 在设计、实施或测试阶段，额外的功能可能会渗入程序或应用程序。这会增加出现问题的可能性。 |
| 解决方案复杂性 | 更复杂或晦涩的解决方案也可能转化为问题。难以维护的程序可能会因此产生。 |
| 需求 | 需求可能陈述不充分、被误解或被遗漏。在这些情况下，程序可能无法满足用户社区的需求并被归类为 bug。 |
| 测试环境 | 不充分的测试环境、不良的测试计划或测试时间不足通常会导致 bug 众多的程序。在这些情况下，bug 可能在测试阶段溜走并进入生产环境。 |

## 故障排除和调试技术

PROC SQL 为从业者提供了众多故障排除和调试功能可供选择。从语句到选项再到宏变量，您可以使用各种技术快速轻松地控制查找和收集 SQL 过程编码问题信息的过程。

## 使用 VALIDATE 语句验证查询

SQL 过程语法检查器在处理任何数据之前识别语法错误。语法检查在 SQL 过程中自动开启，无需指定任何语句或选项。但为了在不自动执行步骤的情况下启用语法检查，您可以在 SELECT 语句开头指定 VALIDATE 语句，或如后面将介绍的那样，指定 NOEXEC 选项。

VALIDATE 语句可供 SAS 用户控制要检查的 SELECT 语句。由于您在 SELECT 语句之前指定 VALIDATE 语句，因此您能更好地控制调试代码的过程。当代码语法有效时，SAS 日志中会自动显示表明语法正确的消息。否则，会显示错误消息以标识编码违规。在下一个示例中，在 SELECT 语句开头指定 VALIDATE 语句以启用语法检查而不执行代码。SAS 日志显示代码包含有效语法并自动显示相应消息。

## SQL 代码

```
PROC SQL;
    VALIDATE
        SELECT *
            FROM PRODUCTS
                WHERE PRODTYPE = 'Software';
QUIT;
```

## SAS 日志结果

```
PROC SQL;
    VALIDATE
        SELECT *
            FROM PRODUCTS
                WHERE PRODTYPE = 'Software';
NOTE: PROC SQL statement has valid syntax.
QUIT;
```

## 已记录的 PROC SQL 选项和语句

本节说明了广泛使用且有文档记录的故障排除和调试 SQL 选项以及 RESET 语句的示例。下面提供了每个选项和语句的描述和工作示例。

## FEEDBACK/NOFEEDBACK 选项

FEEDBACK 选项在 SELECT 查询中显示额外文档。指定时，此选项会将 SELECT *（通配符）语句扩展为其代表的列列表，通过显示底层表中的每个列名以及任何已解析的宏值和宏变量。SELECT * 语句的列显示顺序由表记录描述符中定义的顺序决定。

以下示例说明了 FEEDBACK 选项。由于 SELECT * 语句不会自动显示其代表的列，因此通过指定 FEEDBACK 选项来扩展单个列名可能很重要。这对于确定所需列是否在输出中存在并可用于文档目的特别有用。扩展列列表的结果显示在 SAS 日志中。

## SQL 代码

```
PROC SQL FEEDBACK;
    SELECT *
        FROM PRODUCTS;
QUIT;
```

## SAS 日志结果

```
PROC SQL FEEDBACK;
    SELECT *
        FROM PRODUCTS;
NOTE: Statement transforms to:
    select PRODUCTS.prodnum, PRODUCTS.prodname, PRODUCTS.manunum,
            PRODUCTS.prodtype, PRODUCTS.prodcost
        from WORK.PRODUCTS;
QUIT;
```

FEEDBACK 选项在连接两个或多个表时确定列顺序特别有帮助。下一个示例说明了在双向等值连接中 SELECT * 语句的列扩展。FEEDBACK 选项显示两个表中的所有列。

## SQL 代码

```
PROC SQL FEEDBACK;
    SELECT *
        FROM PRODUCTS, MANUFACTURERS
            WHERE PRODUCTS.MANUNUM = MANUFACTURERS.MANUNUM AND
                  MANUFACTURERS.MANUNAME = 'KPL Enterprises';
QUIT;
```

## SAS 日志结果

```
PROC SQL FEEDBACK;
    SELECT *
        FROM PRODUCTS, MANUFACTURERS
            WHERE PRODUCTS.MANUNUM = MANUFACTURERS.MANUNUM AND
                  MANUFACTURERS.MANUNAME = 'KPL Enterprises';
NOTE: Statement transforms to:
    select PRODUCTS.prodnum, PRODUCTS.prodname, PRODUCTS.manunum,
            PRODUCTS.prodtype, PRODUCTS.prodcost, MANUFACTURERS.manunum,
            MANUFACTURERS.manuname, MANUFACTURERS.manucity,
            MANUFACTURERS.manustat
        from PRODUCTS, MANUFACTURERS
        where (PRODUCTS.manunum=MANUFACTURERS.manunum) and
              (MANUFACTURERS.manuname='KPL Enterprises');
QUIT;
```

FEEDBACK 选项还可用于显示宏值和宏变量解析。下一个示例显示了宏变量 &LIB、&TABLE 和 &GROUPBY 的宏解析以用于调试目的。

