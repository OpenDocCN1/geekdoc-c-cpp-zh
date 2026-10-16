

FROM PRODUCTS
    WHERE UPCASE(PRODTYPE) IN ('SOFTWARE', 'LAPTOP');
QUIT;

## SAS 日志结果

```
OPTIONS FULLSTIMER;
PROC SQL;
    SELECT DISTINCT *
        FROM PRODUCTS
            WHERE UPCASE(PRODTYPE) IN ('SOFTWARE', 'LAPTOP');
QUIT;
NOTE: PROCEDURE SQL used (Total process time):
    real time            0.07 seconds
    user cpu time        0.01 seconds
    system cpu time      0.04 seconds
    memory               561.41k
    OS Memory            6768.00k
    Timestamp            06/03/2012 05:12:56 PM
```

另一种可以改善使用 SET 操作符的查询性能的方法是指定 ALL 关键字，只要重复项不是问题或表中的行都是唯一的即可。因为 ALL 关键字阻止 SQL 两次处理数据并且不删除重复行，所以 CPU 资源可能会得到改善。下一个示例显示了 UNION ALL 编码构造被用来执行相当于追加操作的操作，从而完全绕过了排序，因为重复行不会被删除。

## SQL 代码（效率较低）

```
OPTIONS FULLSTIMER;
PROC SQL;
    SELECT *
        FROM PRODUCTS
            WHERE UPCASE(PRODTYPE) = 'LAPTOP'

    UNION ALL

    SELECT *
        FROM PRODUCTS
            WHERE UPCASE(PRODTYPE) = 'SOFTWARE';
QUIT;
```

## SAS 日志结果

```
OPTIONS FULLSTIMER;
PROC SQL;
    SELECT *
        FROM PRODUCTS
            WHERE UPCASE(PRODTYPE) = 'LAPTOP'

UNION ALL
SELECT *
    FROM PRODUCTS
        WHERE UPCASE(PRODTYPE) = 'SOFTWARE';
QUIT;
NOTE: PROCEDURE SQL used (Total process time):
    real time            0.06 seconds
    user cpu time        0.00 seconds
    system cpu time      0.04 seconds
    memory               226.42k
    OS Memory            6768.00k
    Timestamp            06/03/2012 05:22:14 PM
```

## 摘要

- 1. 性能调优涉及测量、评估和修改查询的执行，以在相互竞争的计算机资源之间实现最佳平衡（参见“理解性能调优”部分）。
- 2. 在创建表或视图时避免指定 ORDER BY 子句（参见“排序与性能”部分）。
- 3. 当排序是必要的时，指定 SORTPGM= 系统选项以指示 SAS 系统根据数据库环境的大小使用最佳可能的排序实用程序（参见“用户指定的排序”部分）。
- 4. 建议将 GROUP BY 子句中的分组列数量保持在尽可能小的范围内（参见“拆分表”部分）。
- 5. 应谨慎地将索引分配给表中的那些区分变量，并避免创建过多的索引（参见“索引与性能”部分）。
- 6. 当表相对较小时（通常少于三页），创建或使用索引没有任何优势（参见“查看 CONTENTS 输出和系统消息”部分）。
- 7. 将 MSGLEVEL= 系统选项设置为“I”允许 SAS 显示有关一个或多个索引存在与否以优化 WHERE 子句处理的重要信息（如果可用）（参见“查看 CONTENTS 输出和系统消息”部分）。
- 8. 应用 WHERE 子句处理以限制结果表的行数（参见“使用索引优化 WHERE 子句处理”部分）。
- 9. 在 WHERE 子句中构造 AND 条件链时，先指定最严格的条件值（参见“构造高效的逻辑条件”部分）。

## 索引

A
ADD 子句 210–211
加法 (+) 操作符 38–40
ad-hoc 查询 280
_AGGR 选项 342
聚合函数
  使用聚合函数创建宏变量 152–153
  指定 257–258
ALL 关键字 268
ALTER TABLE 语句 193–202, 207, 210–211, 214–219, 338–340
模糊引用，列错误 347
AND 操作符 36–38
ANSI（美国国家标准学会） 7–8
APPEND 过程 276
算术数据 29–32
算术操作符 38–40
AS 关键字 32–34
_ASGN 选项 342
星号 (*) 通配符 59
使用自动宏变量控制处理 156–158
自动排序 353
AVG 函数 59

B
BEST 选项 353
BETWEEN 谓词 63–65
B-tree 223
错误 324
从 Microsoft Excel 批量加载数据 186–191
Burlew, Michele M.
  Output Delivery System: The Basics and Beyond 114

SAS Macro Programming Guide Made Easy, Second Edition 148
BY 语句 144

C
计算列视图 298
计算列 299
基数 225
Carpenter, Art
  Carpenter's Complete Guide to the SAS Macro Language, Second Edition 148
Carpenter's Complete Guide to the SAS Macro Language, Second Edition (Carpenter) 148
笛卡尔积连接 242
笛卡尔积查询 237
CASE 表达式
  关于 123–124
  分配标签和分组数据 143–146
  案例逻辑与 COALESCE 表达式 142–143
  逻辑和空值 146–148
  搜索的 137–142
  简单的 124–136
案例逻辑，COALESCE 表达式与 142–143
CAT 函数 41
CATALOGS 字典表 73, 79
CATS 函数 41
CATX 函数 100
Celko, Joe
  SQL for Smarties: Advanced SQL Programming 4, 47, 48, 298
变更控制，保留 202
CHECK 约束 196–197
CHECK_CONSTRAINTS 字典表 73
COALESCE 表达式，案例逻辑与 142–143
COALESCE 函数 49, 142–143
Code Complete: A Practical Handbook of Software Construction, Second Edition (McConnell) 134
编码
    参见复杂查询编码
编码逻辑
    关于 123
    CASE 表达式 123–148
    条件逻辑 122–123
    接口 PROC SQL 与宏语言 148–161
列别名，创建 32–33
列约束 192
使用列定义列表创建表 165–169
列
    向行中添加数据 176–185
    向表中添加 210–211
    计算的 299
    更改格式 218–219
    更改标签 219
    更改长度 214–218
    控制表中位置 212–214
    交叉引用 158–159
    派生的 299
    在列之间插入文本和常量 99–101
    修改包含索引的列 229
    按列排序输出 104–107
    重命名 219–221
    使用标量表达式与所选列 101–104
COLUMNS 字典表 73, 79–80
逗号分隔值 CSV 文件 116
比较操作符 35–36
The Complete Guide to Using SAS Indexes (Raithel) 224
使用搜索 CASE 表达式进行复杂比较 139–140
复杂查询编码
    关于 234–235
    笛卡尔积连接 242
    复杂查询应用 280–292
    内连接 237, 242–255
    连接 235–255
    外连接 238, 255–260
    集合操作 238, 271–280
    子查询 238, 261–271
    类型 236–239
复杂查询应用
    关于 280
    确定输入表中的行数 290–291
    识别索引最多的表 291–292
    多对多关系 237, 280–285
    多对一关系 237, 280–285
    一对多关系 237, 280–285
    一对一关系 237, 280–285
    处理 BY-and 组的第一行、最后一行和中间行 285–290
复合索引 228–229
在连接中执行计算 250–251
连接
    字符字符串 97–101
    来自两个查询的行 276–278
连接字符串 40–41
连接字符字符串操作符 (||) 97–101
概念数据库设计 2–3
条件逻辑 122–123
在列之间插入常量 99–101
CONSTRAINT_COLUMN_USAGE 字典表 73
CONSTRAINT_TABLE_USAGE 字典表 73
CONTENTS 过程 211–216, 218, 300–301, 355–358
相关子查询 238, 261, 269–271
COUNT 函数 59, 60, 160–161

CREATE TABLE 语句 74–75, 114–115, 164, 169–172, 193–197, 215–216, 219–222, 338–340
CREATE VIEW 语句 213–214, 297, 299–300
Cross Join 查询 237
交叉引用列 158–159
CSS 函数 59
CSV（逗号分隔值）文件 116
自定义查询 280
CUSTOMERS 表 9, 12, 15
自定义列表
  使用搜索 CASE 表达式创建 140–142
  使用简单 CASE 表达式创建 129–130
CV 函数 59

D
DASD（直接访问存储设备） 352
数据
  关于 24
  访问字典表的内容 78–88
  向行中的列添加数据 176–185
  使用 SET 子句向表中添加数据 173–175
  使用 SELECT 查询添加数据 185–186
  算术 29–32
  算术操作符 38–40
  从 Microsoft Excel 批量加载数据 186–191
  字符 28
  字符字符串操作符和函数 40–58
  比较操作符 35–36
  日期和时间列定义 27–28
  删除数据行 320
  字典表列名 75–78
  字典表 72–88
  显示字典表定义 74–75
  导出到 Microsoft Excel 116–118
  分组 107–110, 143–146
  使用汇总函数分组 107–109
逻辑操作符 36–38
元数据和字典表 72–74
缺失 29–32
缺失值 28–29, 66–68
NULL 值 3, 28–29, 66–68
数值 24–27
谓词 62–71
排序 109–110
SQL 关键字 32–34
SQL 操作符和函数 35–71
汇总 58–62
类型 24
更新表中的数据 230–231
更新数据行 313–320
数据定义语言 DDL 语句 210
数据完整性 8–9
数据问题 326
数据安全 307–308
DATA 步 25, 42–43, 113, 216, 217–218, 236, 305–306
数据库设计
  关于 2
  列名 7–8
  数据库的概念视图 2–3
  数据完整性 8–9
  本书中使用的数据库表 9–20
  规范化 4–7
  重复信息 3–4
  保留字 7–8
  表定义 3
数据库结构 14
数据库表
  参见表
数据库强制约束
  参见完整性约束
DATAITEMS 字典表 73
DATASETS 过程 221–222
日期列定义 26–27
DDL（数据定义语言）语句 210

