

# 在日志中显示消息和变量值

```
PUTLOG 'text';
PUTLOG variable-name=;
PUTLOG variable-format-name=;
PUTLOG ALL;
```

# 使用 PROC SQL 查询表

```
PROC SQL;
SELECT var-1, var-2...
FROM SAS-table-1
<WHERE where-expression>
```

# 久化格式和控制数据集

```
PROC FORMAT LIBRARY=output-sas-catalog
FMTLIB CNTLININ=input-sas-data-set
CNLOUT=input-sas-data-set;
```

```
RUN;
```

# PROC CATALOG

```
PROC CATALOG CATALOG=libref.catalog;
CONTENTS;
```

```
RUN;
```

# 使用 PROC SQL 创建表

```
PROC SQL;
CREATE TABLE table-name AS
SELECT var-1, var-2...
FROM SAS-table-1
<WHERE where-expression>
```

```
QUIT;
```

# 用于格式设置的系统选项

```
OPTIONS FMTERR; NOFMTERR;
OPTIONS FMTSEARCH=
(item-1 item-2...,item-n);
```

# 使用 PROC SQL 合并表

```
PROC SQL;
SELECT var-1, var-2...
FROM SAS-table-1, SAS-table-2
<WHERE join-condition(s)>
```

```
QUIT;
```

# 迭代 DO 循环

```
DO index-variable=start TO stop <increment>;
iterated SAS statements
```

# PROC TRANSPOSE

```
PROC TRANSPOSE DATA=input-data-set
<OUT=output-data-set>
<NAME=variable-name>;
<BY <DESCENDING> variable-1
<DESCENDING> var-n
<NORTSORTED>;
<VAR variable(s);
<ID variable>;
```

```
END;
```

```
RUN;
```

```
DO index-variable=item-1, ...,item-n;
iterated SAS statements
```

```
END;
```

# 条件 DO 循环

```
DO WHILE (expression);
<additional SAS statements>
```

```
END;
```

```
DO UNTIL (expression);
<additional SAS statements>
```

```
END;
```

# 创建宏变量

```
%LET variable=value;
```

# 带有条件语句迭代 DO 循环

# 显示自动宏变量

```
DO index-variable=start TO stop <increment>
WHILE UNTIL (expression);
<additional SAS statements>
```

```
%PUT _user_;
%PUT _all_;
%PUT automatic;
```

```
END;
```

# 引用宏变量

```
&macro-variable-name.
```

# ARRAY 语句

```
ARRAY array-name {subscript} $<length>
<array-elements><initial-value-list>};
```

SAS 是商业分析软件和服务的领导者，也是商业智能市场最大的独立供应商。通过创新解决方案，SAS 帮助全球超过70,000个地的客户通过更快做出决策来提高性能并交付价值。自1976年以来，SAS 一直为全球客户提供**认知的力量**（THE POWER TO KNOW）。

![](img/d3bde6e6ab06b1fc622215d982111742_477_0.png)

SAS Institute Inc. 世界总部 +1 919 677 6000
如需联系当地 SAS 办公室，请访问：sas.com/offices
SAS 以及所有其他 SAS Institute Inc. 产品或服务名称均为美国及其他国家 SAS Institute Inc. 的注册商标或商标。
SAS 以及所有其他品牌和产品名称为各自公司的商标。版权所有 © 2014, SAS Institute Inc.
保留所有权利。MB63998, IK 14

![](img/d3bde6e6ab06b1fc622215d982111742_477_1.png)

访问 support.sas.com/training 了解 SAS 教育

