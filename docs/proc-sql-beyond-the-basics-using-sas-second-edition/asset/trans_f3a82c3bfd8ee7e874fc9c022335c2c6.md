

新行按 CUSTNUM 升序显示。

| Customer Number | Customer Name | Customer's Home City |
|---|---|---|
| 101 | La Mesa Computer Land | La Mesa |
| 201 | Vista Tech Center | Vista |
| 301 | Coronado Internet Zone | Coronado |
| 401 | La Jolla Computing | La Jolla |
| 402 | La Jolla Tech Center | La Jolla |
| 402 | La Jolla Tech Center | La Jolla |
| 501 | Alpine Technical Center | Alpine |
| 502 | Alpine Byte Center | Alpine |
| 502 | Alpine Byte Center | Alpine |
| 601 | Oceanside Computer Land | Oceanside |
| 701 | San Diego Byte Store | San Diego |
| 702 | Mission Valley Computing | San Diego |
| 703 | Sonic Boom Analytics | Spring Valley |
| 801 | Jamul Hardware & Software | Jamul |
| 901 | Del Mar Tech Center | Del Mar |
| 1001 | Lakeside Software Center | Lakeside |
| 1101 | Bonsall Network Store | Bonsall |
| 1201 | Rancho Santa Fe Tech | Rancho Santa Fe |
| 1301 | Spring Valley Byte Center | Spring Valley |
| 1401 | Poway Central | Poway |
| 1501 | Valley Center Tech Center | Valley Center |
| 1601 | Fairbanks Tech USA | Fairbanks Ranch |
| 1701 | Blossom Valley Tech | Blossom Valley |
| 1702 | Rancho San Diego Tech | Rancho San Diego |
| 1702 | Rancho San Diego Tech | Rancho San Diego |
| 1801 | Chula Vista Networks |  |

INSERT INTO 语句也可以用于在不指定列名的情况下插入数据行，只要为表中的每一列都按表中列指定的确切顺序键入一个值即可。注意：了解表的列顺序可能需要从 CONTENTS 过程产生输出，和/或检查 Dictionary.columns 表或 SASHELP.VCOLUMNS 视图中的元数据列 VARNUM。以下示例说明了在 INSERT INTO 语句中省略表的列名的情况，使用 VALUES 子句添加了三行数据。

## SQL Code
```
PROC SQL;
    INSERT INTO CUSTOMERS
        VALUES (402, 'La Jolla Tech Center', 'La Jolla')
        VALUES (502, 'Alpine Byte Center', 'Alpine')
        VALUES (1702,'Rancho San Diego Tech','Rancho San Diego');

    SELECT *
        FROM CUSTOMERS
            ORDER BY CUSTNUM;
QUIT;
```

SAS 日志显示有三行数据被插入到 CUSTOMERS 表中。

## SAS Log Results
```
PROC SQL;
    INSERT INTO CUSTOMERS
        VALUES (402, 'La Jolla Tech Center', 'La Jolla')
        VALUES (502, 'Alpine Byte Center', 'Alpine')
        VALUES (1701,'Rancho San Diego Tech','Rancho San Diego');
NOTE: 3 rows were inserted into WORK.CUSTOMERS.

    SELECT *
        FROM CUSTOMERS
            ORDER BY CUSTNUM;
QUIT;
NOTE: PROCEDURE SQL used:
        real time            0.04 seconds
```

新行按 CUSTNUM 升序显示。

| Customer Number | Customer Name | Customer's Home City |
|---|---|---|
| 101 | La Mesa Computer Land | La Mesa |
| 201 | Vista Tech Center | Vista |
| 301 | Coronado Internet Zone | Coronado |
| 401 | La Jolla Computing | La Jolla |
| 402 | La Jolla Tech Center | La Jolla |
| 501 | Alpine Technical Center | Alpine |
| 502 | Alpine Byte Center | Alpine |
| 601 | Oceanside Computer Land | Oceanside |
| 701 | San Diego Byte Store | San Diego |
| 702 | Mission Valley Computing | San Diego |
| 801 | Jamul Hardware & Software | Jamul |
| 901 | Del Mar Tech Center | Del Mar |
| 1001 | Lakeside Software Center | Lakeside |
| 1101 | Bonsall Network Store | Bonsall |
| 1201 | Rancho Santa Fe Tech | Rancho Santa Fe |
| 1301 | Spring Valley Byte Center | Spring Valley |
| 1401 | Poway Central | Poway |
| 1501 | Valley Center Tech Center | Valley Center |
| 1601 | Fairbanks Tech USA | Fairbanks Ranch |
| 1701 | Blossom Valley Tech | Blossom Valley |
| 1702 | Rancho San Diego Tech | Rancho San Diego |
| 1801 | Chula Vista Networks |  |

## Adding Data to Some of the Columns in a Row

在向表添加数据行时，存在一个或多个列值未分配的情况并不少见。当这种情况发生时，SQL 必须能够处理将行添加到表中，就好像所有值都存在一样。但 SQL 如何处理未指定的值呢？你将在以下示例中看到，SQL 会为未指定值的列分配缺失值。如前所述，使用 INSERT INTO 语句指定了三个参数：表的名称、要插入值的列的名称以及值本身。假设你必须向 CUSTOMERS 表中添加两行不完整的数据，其中指定了三个列中的两列（Customer Number 和 Customer Name）。

## SQL Code
```
PROC SQL;
    INSERT INTO CUSTOMERS
        (CUSTNUM, CUSTNAME)
        VALUES (102, 'La Mesa Byte & Floppy')
        VALUES (902, 'Del Mar Technology Center');
    SELECT *
        FROM CUSTOMERS
        ORDER BY CUSTNUM;
QUIT;
```

SAS 日志显示有两行数据被添加到 CUSTOMERS 表中。

## SAS Log Results
```
PROC SQL;
    INSERT INTO CUSTOMERS
        (CUSTNUM, CUSTNAME)
        VALUES (102, 'La Mesa Byte & Floppy')
        VALUES (902, 'Del Mar Technology Center');
NOTE: 2 rows were inserted into WORK.CUSTOMERS.
    SELECT *
        FROM CUSTOMERS
        ORDER BY CUSTNUM;
QUIT;
NOTE: PROCEDURE SQL used:
    real time               0.00 seconds
```

新行按 CUSTNUM 升序显示，并为字符列 CUSTCITY 分配了缺失值。

| Customer Number | Customer Name | Customer's Home City |
|---|---|---|
| 101 | La Mesa Computer Land | La Mesa |
| 102 | La Mesa Byte & Floppy |  |
| 201 | Vista Tech Center | Vista |
| 301 | Coronado Internet Zone | Coronado |
| 401 | La Jolla Computing | La Jolla |
| 402 | La Jolla Tech Center | La Jolla |
| 402 | La Jolla Tech Center | La Jolla |
| 501 | Alpine Technical Center | Alpine |
| 502 | Alpine Byte Center | Alpine |
| 502 | Alpine Byte Center | Alpine |
| 601 | Oceanside Computer Land | Oceanside |
| 701 | San Diego Byte Store | San Diego |
| 702 | Mission Valley Computing | San Diego |
| 703 | Sonic Boom Analytics | Spring Valley |
| 801 | Jamul Hardware & Software | Jamul |
| 901 | Del Mar Tech Center | Del Mar |
| 902 | Del Mar Technology Center |  |
| 1001 | Lakeside Software Center | Lakeside |
| 1101 | Bonsall Network Store | Bonsall |
| 1201 | Rancho Santa Fe Tech | Rancho Santa Fe |
| 1301 | Spring Valley Byte Center | Spring Valley |
| 1401 | Poway Central | Poway |
| 1501 | Valley Center Tech Center | Valley Center |
| 1601 | Fairbanks Tech USA | Fairbanks Ranch |
| 1701 | Blossom Valley Tech | Blossom Valley |
| 1702 | Rancho San Diego Tech | Rancho San Diego |
| 1702 | Rancho San Diego Tech | Rancho San Diego |
| 1801 | Chula Vista Networks |  |

在前面的示例中，缺失值被分配给了字符列 CUSTCITY。假设你想向 PRODUCTS 表中添加两行部分数据，其中指定了五个列中的四列（Product Number、Product Name、Product Type 和 Product Cost），并且每行的缺失值是数值列 MANUNUM。

## SQL Code
```
PROC SQL;
    INSERT INTO PRODUCTS
        (PRODNUM, PRODNAME, PRODTYPE, PRODCOST)
    VALUES (6002,'Security Software','Software',375.00)
    VALUES (1701,'Travel Laptop SE', 'Laptop',  4200.00);
```
```
SELECT *
    FROM PRODUCTS
    ORDER BY PRODNUM;
QUIT;
```

SAS 日志显示有两行数据被添加到 PRODUCTS 表中。

## SAS Log Results
```
PROC SQL;
    INSERT INTO PRODUCTS
        (PRODNUM, PRODNAME, PRODTYPE, PRODCOST)
        VALUES (6002,'Security Software','Software',375.00)
        VALUES (1701,'Travel Laptop SE','Laptop', 4200.00);
NOTE: 2 rows were inserted into WORK.PRODUCTS.

    SELECT *
        FROM PRODUCTS
        ORDER BY PRODNUM;
QUIT;
NOTE: PROCEDURE SQL used:
      real time          0.75 seconds
```

新行按 PRODNUM 升序显示，并为数值列 MANUNUM 分配了缺失值。

| Product Number | Product Name | Manufacturer Number | Product Type | Product Cost |
|---|---|---|---|---|
| 1110 | Dream Machine | 111 | Workstation | $3,200.00 |
| 1200 | Business Machine | 120 | Workstation | $3,300.00 |
| 1700 | Travel Laptop | 170 | Laptop | $3,400.00 |
| 1701 | Travel Laptop SE | . | Laptop | $4,200.00 |
| 2101 | Analog Cell Phone | 210 | Phone | $35.00 |
| 2102 | Digital Cell Phone | 210 | Phone | $175.00 |
| 2200 | Office Phone | 220 | Phone | $130.00 |
| 5001 | Spreadsheet Software | 500 | Software | $299.00 |
| 5002 | Database Software | 500 | Software | $399.00 |
| 5003 | Wordprocessor Software | 500 | Software | $299.00 |
| 5004 | Graphics Software | 500 | Software | $299.00 |
| 6002 | Security Software | . | Software | $375.00 |

## Adding Data with a SELECT Query

你也可以使用带有 INSERT INTO 语句的 SELECT 查询向表中添加数据。查询表达式本质上是通过先创建一个临时表然后将临时表的内容插入到正在填充的目标表中来执行封闭的查询。在填充目标表的过程中，列列表中省略的任何列都会自动分配缺失值。

在下一个示例中，使用 SELECT 查询将 PRODUCTS 表中的一行数据添加到 SOFTWARE_PRODUCTS 表中。指定的查询通过使用 WHERE 子句控制将数据插入到目标 SOFTWARE_PRODUCTS 表中。

## SQL Code
```
PROC SQL;
    INSERT INTO SOFTWARE_PRODUCTS
        (PRODNUM, PRODNAME, PRODTYPE, PRODCOST)
    SELECT PRODNUM, PRODNAME, PRODTYPE, PRODCOST
        FROM PRODUCTS
        WHERE PRODTYPE IN ('Software') AND
            PRODCOST > 300;
QUIT;
```

SAS 日志显示有一行数据被添加到 SOFTWARE_PRODUCTS 表中。

