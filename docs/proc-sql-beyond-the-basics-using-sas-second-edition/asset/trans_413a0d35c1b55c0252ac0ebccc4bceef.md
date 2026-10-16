
由于其中一行包含重复的 CUSTNUM 值，因此具有已定义 UNIQUE 约束的行无法填充到 CUSTOMER_CITY 表中。

### SQL 代码

```
PROC SQL;
    INSERT INTO CUSTOMER_CITY
    VALUES (101,'La Mesa Computer Land')
    VALUES (1301,'Spring Valley Byte Center')
    VALUES (1301,'Chula Vista Networks');
QUIT;
```

SAS 日志显示，UNIQUE 约束阻止了这三行数据填充到 CUSTOMER_CITY 表中。该违规行为产生了一条错误消息，导致添加/更新操作失败。

### SAS 日志结果

```
PROC SQL;
    INSERT INTO CUSTOMER_CITY
    VALUES (101,'La Mesa Computer Land')
    VALUES (1301,'Spring Valley Byte Center')
    VALUES (1301,'Chula Vista Networks');
ERROR: Add/Update failed for data set WORK.CUSTOMER_CITY because data value(s) do not comply with integrity constraint _UNO001_.
NOTE: This insert failed while attempting to add data from VALUES clause 3 to the data set.
NOTE: Deleting the successful inserts before error noted above to restore table to a consistent state.
QUIT;
NOTE: The SAS System stopped processing this step because of errors.
NOTE: PROCEDURE SQL used:
    real time          1.12 seconds
    cpu time           0.06 seconds
```

## 使用 CHECK 约束验证列值

CHECK 约束在填充表之前，会根据值列表、最小值和最大值以及值范围来验证数据值。使用 CREATE TABLE 或 ALTER TABLE 语句，你可以对任何需要执行数据验证的列应用 CHECK 约束。在下一个示例中，假设你想验证 PRODUCTS 表中 PRODTYPE（产品类型）列的数据值。当你使用 ALTER TABLE 语句对 PRODTYPE 列指定 CHECK 约束时，产品类型值必须首先匹配定义的值列表，否则相应的行将被拒绝。

### SQL 代码

```
PROC SQL;
    ALTER TABLE PRODUCTS
        ADD CONSTRAINT CHECK_PRODUCT_TYPE
        CHECK (PRODTYPE IN ('Laptop',
            'Phone',
            'Software',
            'Workstation'));
QUIT;
```

定义了 CHECK 约束后，在表填充之前，每一行都必须满足为列指定的验证规则。如果任何行未通过基于既定验证规则的验证检查，则添加/更新操作失败，且表会自动恢复到操作发生之前的状态。在下一个示例中，将根据为 PRODTYPE 列定义的 CHECK 约束对三行数据进行验证。

### SQL 代码

```
PROC SQL;
    INSERT INTO PRODUCTS
        VALUES (5005,'Internet Software',500,'Software',99.)
        VALUES (1701,'Elite Laptop',170,'Laptop',3900.)
        VALUES (2103,'Digital Cell Phone',210,'Fone',199.);
QUIT;
```

SAS 日志显示了尝试添加这三行数据后的结果。由于其中一行包含“Fone”值，违反了 CHECK 约束，因此这些行不会被添加到 PRODUCTS 表中。该违规行为产生一条错误消息，导致添加/更新操作失败。

### SAS 日志结果

```
PROC SQL;
    INSERT INTO PRODUCTS
        VALUES (5005,'Internet Software',500,'Software',99.)
        VALUES (1701,'Elite Laptop',170,'Laptop',3900.)
        VALUES (2103,'Digital Cell Phone',210,'Fone',199.);
ERROR: Add/Update failed for data set WORK.PRODUCTS because data value(s) do not comply with integrity constraint CHECK_PRODUCT_TYPE.
NOTE: This insert failed while attempting to add data from VALUES clause 3 to the data set.
NOTE: Deleting the successful inserts before error noted above to restore table to a consistent state.
QUIT;
NOTE: The SAS System stopped processing this step because of errors.
NOTE: PROCEDURE SQL used:
    real time          0.09 seconds
    cpu time           0.02 seconds
```

## 引用完整性约束

SQL 过程中可用的第二种约束类型称为引用完整性约束。引用完整性约束通过两个或多个表之间的主键和外键来强制实施，内置于数据库环境中，以防止发生数据完整性问题。使用特定类型的引用完整性约束和约束操作子句来强制执行更新和删除操作，具体包括以下内容：

### 引用完整性约束

- 主键
- 外键

### 引用完整性约束操作子句

- RESTRICT（默认）
- SET NULL
- CASCADE

操作子句将在本章的“建立外键”一节中讨论。

### 建立主键

主键由一个或多个具有唯一值的列组成，用于标识表中的各个行。根据所用列的性质，可能只需要一个列即可标识特定行。而在其他情况下，可能需要两个或更多列才能充分标识被引用表中的一行。假设你需要唯一标识 MANUFACTURERS 表中的特定行。通过将制造商编号（MANUNUM）建立为行的唯一标识符，就建立了一个键。下一个示例指定 ALTER TABLE 语句，使用 MANUFACTURERS 表中的 MANUNUM 创建主键。

### SQL 代码

```
PROC SQL;
  ALTER TABLE MANUFACTURERS
    ADD CONSTRAINT PRIM_KEY PRIMARY KEY (MANUNUM);
QUIT;
```

SAS 日志显示，使用 MANUNUM 列创建主键后，MANUFACTURERS 表已成功修改。

### SAS 日志结果

```
PROC SQL;
  ALTER TABLE MANUFACTURERS
    ADD CONSTRAINT PRIM_KEY PRIMARY KEY (MANUNUM);
NOTE: Table WORK.MANUFACTURERS has been modified, with 4 columns.
QUIT;
NOTE: PROCEDURE SQL used:
  real time          0.07 seconds
  cpu time           0.01 seconds
```

假设你还需要唯一标识 PRODUCTS 表中的特定行。通过将 PRODNUM（产品编号）指定为主键，下一个示例指定 ALTER TABLE 语句来创建表中行的唯一标识符。

### SQL 代码

```
PROC SQL;
    ALTER TABLE PRODUCTS
        ADD CONSTRAINT PRIM_PRODUCT_KEY PRIMARY KEY (PRODNUM);
QUIT;
```

SAS 日志显示，使用 PRODNUM 列建立主键后，PRODUCTS 表已成功修改。

### SAS 日志结果

```
PROC SQL;
    ALTER TABLE PRODUCTS
        ADD CONSTRAINT PRIM_PRODUCT_KEY PRIMARY KEY (PRODNUM);
NOTE: Table WORK.PRODUCTS has been modified, with 5 columns.
    QUIT;
NOTE: PROCEDURE SQL used:
        real time           0.03 seconds
        cpu time            0.01 seconds
```

### 建立外键

外键由表中的一个或多个列组成，这些列引用或关联另一个表中的值。用作外键的列必须与被引用表中的列匹配。外键的目的是确保一个表中的数据行存在于另一个表中，从而防止表之间丢失或缺失链接的可能性。引用完整性规则的执行对数据可靠性问题具有积极而直接的影响。

假设你想确保 INVENTORY 表中的数据值与 PRODUCTS 表中有对应且匹配的数据值。通过将 PRODNUM（产品编号）建立为 INVENTORY 表中的外键，你可以确保两个表之间具有高水平的数据完整性。这实质上验证了 INVENTORY 表中的关键数据存在于 PRODUCTS 表中。在下一个示例中，通过指定 ALTER TABLE 语句，使用 INVENTORY 表中的 PRODNUM 列创建外键。

### SQL 代码

```
PROC SQL;
    ALTER TABLE INVENTORY
        ADD CONSTRAINT FOREIGN_PRODUCT_KEY FOREIGN KEY (PRODNUM)
            REFERENCES PRODUCTS
                ON DELETE RESTRICT
                ON UPDATE RESTRICT;
QUIT;
```
