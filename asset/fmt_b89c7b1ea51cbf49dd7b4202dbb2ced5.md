
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

定义了 `CHECK` 约束后，在表填充之前，每一行都必须满足为列指定的验证规则。如果任何行未通过基于既定验证规则的验证检查，则添加/更新操作失败，且表会自动恢复到操作发生之前的状态。在下一个示例中，将根据为 `PRODTYPE` 列定义的 `CHECK` 约束对三行数据进行验证。

### SQL 代码

```
PROC SQL;
    INSERT INTO PRODUCTS
        VALUES (5005,'Internet Software',500,'Software',99.)
        VALUES (1701,'Elite Laptop',170,'Laptop',3900.)
        VALUES (2103,'Digital Cell Phone',210,'Fone',199.);
QUIT;
```

SAS 日志显示了尝试添加这三行数据后的结果。由于其中一行包含“Fone”值，违反了 `CHECK` 约束，因此这些行不会被添加到 `PRODUCTS` 表中。该违规行为产生一条错误消息，导致添加/更新操作失败。

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

- `RESTRICT`（默认）

- `SET NULL`

- `CASCADE`

操作子句将在本章的“建立外键”一节中讨论。

### 建立主键

主键由一个或多个具有唯一值的列组成，用于标识表中的各个行。根据所用列的性质，可能只需要一个列即可标识特定行。而在其他情况下，可能需要两个或更多列才能充分标识被引用表中的一行。假设你需要唯一标识 `MANUFACTURERS` 表中的特定行。通过将制造商编号（`MANUNUM`）建立为行的唯一标识符，就建立了一个键。下一个示例指定 `ALTER TABLE` 语句，使用 `MANUFACTURERS` 表中的 `MANUNUM` 创建主键。

### SQL 代码

```
PROC SQL;
  ALTER TABLE MANUFACTURERS
    ADD CONSTRAINT PRIM_KEY PRIMARY KEY (MANUNUM);
QUIT;
```

SAS 日志显示，使用 `MANUNUM` 列创建主键后，`MANUFACTURERS` 表已成功修改。

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

假设你还需要唯一标识 `PRODUCTS` 表中的特定行。通过将 `PRODNUM`（产品编号）指定为主键，下一个示例指定 `ALTER TABLE` 语句来创建表中行的唯一标识符。

### SQL 代码

```
PROC SQL;
    ALTER TABLE PRODUCTS
        ADD CONSTRAINT PRIM_PRODUCT_KEY PRIMARY KEY (PRODNUM);
QUIT;
```

SAS 日志显示，使用 `PRODNUM` 列建立主键后，`PRODUCTS` 表已成功修改。

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

假设你想确保 `INVENTORY` 表中的数据值与 `PRODUCTS` 表中有对应且匹配的数据值。通过将 `PRODNUM`（产品编号）建立为 `INVENTORY` 表中的外键，你可以确保两个表之间具有高水平的数据完整性。这实质上验证了 `INVENTORY` 表中的关键数据存在于 `PRODUCTS` 表中。在下一个示例中，通过指定 `ALTER TABLE` 语句，使用 `INVENTORY` 表中的 `PRODNUM` 列创建外键。

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

SAS 日志显示 `PRODNUM` 列已成功作为外键创建在 `INVENTORY` 表中。通过指定默认值的 `ON DELETE RESTRICT` 和 `ON UPDATE RESTRICT` 子句，当在外键中找到匹配值时，你限制了更改主键数据值的能力。在 SQL 处理期间，任何可能违反这些引用完整性规则的 SQL 语句的执行都会被阻止。

## SAS 日志结果

```
PROC SQL;
    ALTER TABLE INVENTORY
    ADD CONSTRAINT FOREIGN_PRODUCT_KEY FOREIGN KEY (PRODNUM)
        REFERENCES PRODUCTS
        ON DELETE RESTRICT
        ON UPDATE RESTRICT;
NOTE: Table WORK.INVENTORY has been modified, with 5 columns.
    QUIT;
NOTE: PROCEDURE SQL used:
      real time           0.01 seconds
      cpu time            0.01 seconds
```

假设某个制造商的某种产品不再供应并且已被停产。为了处理这种情况，当产品从 `PRODUCTS` 表中删除时，`INVENTORY` 表中的数据值应设为缺失。下一个示例使用 `INVENTORY` 表中的 `PRODNUM` 列建立外键，并使用 `ON DELETE` 子句将值设为 null。

### SQL 代码

```
PROC SQL;
    ALTER TABLE INVENTORY
    ADD CONSTRAINT FOREIGN_MISSING_PRODUCT_KEY FOREIGN KEY (PRODNUM)
        REFERENCES PRODUCTS
        ON DELETE SET NULL;
QUIT;
```

SAS 日志显示 `PRODNUM` 列已成功作为外键创建在 `INVENTORY` 表中，以及 `ON DELETE SET NULL` 子句的效果。指定此子句会将外键值更改为缺失或 null，适用于在主键中找到匹配值的所有行。在 SQL 处理期间，任何可能违反这些引用完整性规则的 SQL 语句的执行都会被阻止。

## SAS 日志结果

```
PROC SQL;
    ALTER TABLE INVENTORY
    ADD CONSTRAINT FOREIGN_MISSING_PRODUCT_KEY FOREIGN KEY (PRODNUM)
        REFERENCES PRODUCTS
        ON DELETE SET NULL;
NOTE: Table WORK.INVENTORY has been modified, with 5 columns.
    QUIT;
NOTE: PROCEDURE SQL used:
    real time          0.02 seconds
    cpu time           0.02 seconds
```

假设你希望确保对 `PRODUCTS` 表中键值的更改会自动流向或级联到 `INVENTORY` 表中的行。这是通过首先使用 `ADD CONSTRAINT` 子句在 `INVENTORY` 表中创建 `PRODNUM`（产品编号）作为外键并引用 `PRODUCTS` 表来实现的。然后你指定 `ON UPDATE CASCADE` 子句，以使对 `PRODUCTS` 表所做的任何更改都能自动级联到 `INVENTORY` 表。这确保了对 `PRODUCTS` 表中产品编号值的更改也会自动发生在 `INVENTORY` 表中。

### SQL 代码

```
PROC SQL;
    ALTER TABLE INVENTORY
    ADD CONSTRAINT FOREIGN_PRODUCT_KEY FOREIGN KEY (PRODNUM)
        REFERENCES PRODUCTS
        ON UPDATE CASCADE
        ON DELETE RESTRICT  /* DEFAULT VALUE */;
QUIT;
```

SAS 日志显示 `PRODNUM` 列已成功作为外键创建在 `INVENTORY` 表中。当指定 `ON UPDATE` 和 `ON DELETE` 子句时，任何可能违反引用完整性规则的 SQL 语句的执行都被严格禁止。

## SAS 日志结果

```
PROC SQL;
ALTER TABLE INVENTORY
ADD CONSTRAINT FOREIGN_PRODUCT_KEY FOREIGN KEY (PRODNUM)
REFERENCES PRODUCTS
ON UPDATE CASCADE
ON DELETE RESTRICT  /* DEFAULT VALUE */;
NOTE: Table WORK.INVENTORY has been modified, with 5 columns.
QUIT;
NOTE: PROCEDURE SQL used:
real time          0.06 seconds
cpu time           0.01 seconds
```

## 约束与变更控制

为了保留变更控制，SAS 禁止对包含已定义引用完整性约束的表进行更改或修改。当你尝试删除、重命名或替换包含引用完整性约束的表时，会生成错误消息并且处理停止。下一个示例说明了针对包含引用完整性约束的表执行的表复制操作，该操作会生成错误消息并停止处理。

## SAS 日志结果

```
PROC COPY IN=SQLBOOK OUT=WORK;
SELECT INVENTORY;
RUN;

NOTE: Copying SQLBOOK.INVENTORY to WORK.INVENTORY (memtype=DATA).
ERROR: A rename/delete/replace attempt is not allowed for a data set involved in a referential integrity constraint. WORK.INVENTORY.DATA
ERROR: File WORK.INVENTORY.DATA has not been saved because copy could not be completed.
NOTE: Statements not processed because of errors noted above.
NOTE: PROCEDURE COPY used:
real time          0.44 seconds
cpu time           0.02 seconds
NOTE: The SAS System stopped processing this step because of errors.
```

## 显示完整性约束

使用 `DESCRIBE TABLE` 语句，SQL 过程会在 SAS 日志中与表描述一起显示完整性约束。能够捕获此类信息有助于文档过程，通过描述完整性约束的名称和类型以及它们引用的贡献列。

### SQL 代码

```
PROC SQL;
DESCRIBE TABLE MANUFACTURERS;
QUIT;
```

SAS 日志显示了用于创建 `MANUFACTURERS` 表的 SQL 语句，以及已定义的完整性约束的字母顺序列表。

## SAS 日志结果

```
PROC SQL;
    DESCRIBE TABLE MANUFACTURERS;
NOTE: SQL table WORK.MANUFACTURERS was created like:

create table WORK.MANUFACTURERS( bufsize=4096 )
(
    manunum num label='Manufacturer Number',
    manuname char(25) label='Manufacturer Name',
    manucity char(20) label='Manufacturer City',
    manustat char(2) label='Manufacturer State'
);
create unique index manunum on WORK.MANUFACTURERS(manunum);

    -----Alphabetical List of Integrity Constraints-----
                Integrity
    #   Constraint    Type            Variables
    fffffffffffffffffffffffffffffffffffffffff
    1   PRIM_KEY      Primary Key     manunum

QUIT;
NOTE: PROCEDURE SQL used:
    real time       0.19 seconds
    cpu time        0.01 seconds
```

## 删除表中的行

在数据管理的世界中，从表中删除不需要的数据行的能力与能够向表填充数据一样重要。事实上，如果没有删除数据行的能力，数据管理活动将受到严重阻碍。`DELETE` 语句和可选的 `WHERE` 子句可以根据 `WHERE` 子句中指定的内容从表中删除一行或多行不需要的行。

### 删除表中的单行

`DELETE` 语句可以指定为通过在唯一值上构造显式的 `WHERE` 子句来删除单行数据。构造 `WHERE` 子句以满足这种形式的行删除可能需要复杂的逻辑结构。因此，在将其应用于表以确定其是否按预期执行之前，请务必彻底测试表达式。以下示例说明了通过在 `WHERE` 子句中指定客户名称（`CUSTNAME`）来从 `CUSTOMERS` 表中删除单个客户。

### SQL 代码

```
PROC SQL;
    DELETE FROM CUSTOMERS2
        WHERE UPCASE(CUSTNAME) = "LAUGHLER";
QUIT;
```

## SAS 日志结果
