

## 使用 SET 子句向表中添加数据

您使用 INSERT INTO 语句向表中填充数据。INSERT INTO 语句指定三个参数：表名、要插入值的列名以及值本身。通过 SET 子句向表中插入一行或多行数据。假设您想要向 CUSTOMERS 表中插入（或添加）一行数据，该行由三列组成（客户编号、客户姓名和家庭城市）。

### SQL 代码

```
PROC SQL;
    INSERT INTO CUSTOMERS
        SET CUSTNUM=702,
            CUSTNAME='Mission Valley Computing',
            CUSTCITY='San Diego';
QUIT;
```

SAS 日志显示以下消息，指出已向 CUSTOMERS 表中插入了一行。

### SAS 日志结果

```
PROC SQL;
    INSERT INTO CUSTOMERS
        SET CUSTNUM=702,
            CUSTNAME='Mission Valley Computing',
            CUSTCITY='San Diego';
NOTE: 1 row was inserted into WORK.CUSTOMERS.
    QUIT;
NOTE: PROCEDURE SQL used:
        real time            0.08 seconds
```

来自 INSERT INTO 语句和 SET 子句的插入数据行被添加到 CUSTOMERS 表的末尾。

|  | Customer Number | Customer Name | Customer's Home City |
|---|---|---|---|
| 1 | 101 La Mesa Computer Land | La Mesa |
| 2 | 201 Vista Tech Center | Vista |
| 3 | 301 Coronado Internet Zone | Coronado |
| 4 | 401 La Jolla Computing | La Jolla |
| 5 | 501 Alpine Technical Center | Alpine |
| 6 | 601 Oceanside Computer Land | Oceanside |
| 7 | 701 San Diego Byte Store | San Diego |
| 8 | 801 Jamul Hardware & Software | Jamul |
| 9 | 901 Del Mar Tech Center | Del Mar |
| 10 | 1001 Lakeside Software Center | Lakeside |
| 11 | 1101 Bonsall Network Store | Bonsall |
| 12 | 1201 Rancho Santa Fe Tech | Rancho Santa Fe |
| 13 | 1301 Spring Valley Byte Center | Spring Valley |
| 14 | 1401 Poway Central | Poway |
| 15 | 1501 Valley Center Tech Center | Valley Center |
| 16 | 1601 Fairbanks Tech USA | Fairbanks Ranch |
| 17 | 1701 Blossom Valley Tech | Blossom Valley |
| 18 | 1801 Chula Vista Networks |  |
| 19 | 702 Mission Valley Computing | San Diego |

向包含索引的表中输入新行会自动将该值添加到索引中（有关索引的更多信息，请参阅第 6 章“修改和更新表和索引”）。以下示例说明了使用 SET 子句添加三行数据。

### SQL 代码

```
PROC SQL;
    INSERT INTO CUSTOMERS
        SET CUSTNUM=402,
            CUSTNAME='La Jolla Tech Center',
            CUSTCITY='La Jolla'
        SET CUSTNUM=502,
            CUSTNAME='Alpine Byte Center',
            CUSTCITY='Alpine'
        SET CUSTNUM=1702,
            CUSTNAME='Rancho San Diego Tech',
            CUSTCITY='Rancho San Diego';
    QUIT;
```

SAS 日志显示已向 CUSTOMERS 表中插入了三行数据。

### SAS 日志结果

```
PROC SQL;
    INSERT INTO CUSTOMERS
        SET CUSTNUM=402,
            CUSTNAME='La Jolla Tech Center',
            CUSTCITY='La Jolla'
        SET CUSTNUM=502,
            CUSTNAME='Alpine Byte Center',
            CUSTCITY='Alpine'
        SET CUSTNUM=1701,
            CUSTNAME='Rancho San Diego Tech',
            CUSTCITY='Rancho San Diego';
NOTE: 3 rows were inserted into WORK.CUSTOMERS.
QUIT;
NOTE: PROCEDURE SQL used:
      real time          0.01 seconds
```

来自 INSERT INTO 语句和 SET 子句的插入数据行被添加到 CUSTOMERS 表的末尾。

|  | Customer Number | Customer Name | Customer's Home City |
|---|---|---|---|
| 1 | 101 La Mesa Computer Land | La Mesa |
| 2 | 201 Vista Tech Center | Vista |
| 3 | 301 Coronado Internet Zone | Coronado |
| 4 | 401 La Jolla Computing | La Jolla |
| 5 | 501 Alpine Technical Center | Alpine |
| 6 | 601 Oceanside Computer Land | Oceanside |
| 7 | 701 San Diego Byte Store | San Diego |
| 8 | 801 Jamul Hardware & Software | Jamul |
| 9 | 901 Del Mar Tech Center | Del Mar |
| 10 | 1001 Lakeside Software Center | Lakeside |
| 11 | 1101 Bonsall Network Store | Bonsall |
| 12 | 1201 Rancho Santa Fe Tech | Rancho Santa Fe |
| 13 | 1301 Spring Valley Byte Center | Spring Valley |
| 14 | 1401 Poway Central | Poway |
| 15 | 1501 Valley Center Tech Center | Valley Center |
| 16 | 1601 Fairbanks Tech USA | Fairbanks Ranch |
| 17 | 1701 Blossom Valley Tech | Blossom Valley |
| 18 | 1801 Chula Vista Networks |  |
| 19 | 702 Mission Valley Computing | San Diego |
| 20 | 402 La Jolla Tech Center | La Jolla |
| 21 | 502 Alpine Byte Center | Alpine |
| 22 | 1702 Rancho San Diego Tech | Rancho San Diego |

## 向行的所有列中添加数据

另一种填充表数据的方法是使用 VALUES 子句与 INSERT INTO 语句一起使用。如前一节所述，使用 INSERT INTO 语句和 VALUES 子句指定三个参数：表名、要插入值的列名以及值本身。通过 VALUES 子句向表中插入数据值。假设您想要向 CUSTOMERS 表中插入（或添加）一行数据，该行由三列组成（客户编号、客户姓名和家庭城市）。

### SQL 代码

```
PROC SQL;
    INSERT INTO CUSTOMERS (CUSTNUM, CUSTNAME, CUSTCITY)
        VALUES (703, 'Sonic Boom Analytics', 'Spring Valley');
QUIT;
```

SAS 日志显示以下消息，指出已向 CUSTOMERS 表中插入了一行。

### SAS 日志结果

```
PROC SQL;
    INSERT INTO CUSTOMERS
        (CUSTNUM, CUSTNAME, CUSTCITY)
        VALUES (703, 'Sonic Boom Analytics', 'Spring Valley');
NOTE: 1 row was inserted into WORK.CUSTOMERS.
QUIT;
NOTE: PROCEDURE SQL used:
    real time          0.54 seconds
```

来自之前的 INSERT INTO 语句的插入数据行被添加到 CUSTOMERS 表的末尾。

|  | Customer Number | Customer Name | Customer's Home City |
|---|---|---|---|
| 1 | 101 La Mesa Computer Land | La Mesa |
| 2 | 201 Vista Tech Center | Vista |
| 3 | 301 Coronado Internet Zone | Coronado |
| 4 | 401 La Jolla Computing | La Jolla |
| 5 | 501 Alpine Technical Center | Alpine |
| 6 | 601 Oceanside Computer Land | Oceanside |
| 7 | 701 San Diego Byte Store | San Diego |
| 8 | 801 Jamul Hardware & Software | Jamul |
| 9 | 901 Del Mar Tech Center | Del Mar |
| 10 | 1001 Lakeside Software Center | Lakeside |
| 11 | 1101 Bonsall Network Store | Bonsall |
| 12 | 1201 Rancho Santa Fe Tech | Rancho Santa Fe |
| 13 | 1301 Spring Valley Byte Center | Spring Valley |
| 14 | 1401 Poway Central | Poway |
| 15 | 1501 Valley Center Tech Center | Valley Center |
| 16 | 1601 Fairbanks Tech USA | Fairbanks Ranch |
| 17 | 1701 Blossom Valley Tech | Blossom Valley |
| 18 | 1801 Chula Vista Networks |  |
| 19 | 702 Mission Valley Computing | San Diego |
| 20 | 402 La Jolla Tech Center | La Jolla |
| 21 | 502 Alpine Byte Center | Alpine |
| 22 | 1702 Rancho San Diego Tech | Rancho San Diego |
| 23 | 703 Sonic Boom Analytics | Spring Valley |

向包含索引的表中输入新行会自动将该值添加到索引中（有关索引的更多信息，请参阅第 6 章“修改和更新表和索引”）。INSERT INTO 语句还可以向表中添加多行数据。以下示例说明了使用 VALUES 子句添加三行数据。

### SQL 代码

```
PROC SQL;
    INSERT INTO CUSTOMERS
        (CUSTNUM, CUSTNAME, CUSTCITY)
    VALUES (402, 'La Jolla Tech Center', 'La Jolla')
    VALUES (502, 'Alpine Byte Center', 'Alpine')
    VALUES (1702, 'Rancho San Diego Tech', 'Rancho San Diego');

    SELECT *
        FROM CUSTOMERS
        ORDER BY CUSTNUM;
QUIT;
```

SAS 日志显示已向 CUSTOMERS 表中插入了三行数据。

### SAS 日志结果

```
PROC SQL;
    INSERT INTO CUSTOMERS
        (CUSTNUM, CUSTNAME, CUSTCITY)
        VALUES (402, 'La Jolla Tech Center', 'La Jolla')
        VALUES (502, 'Alpine Byte Center', 'Alpine')
        VALUES (1701,'Rancho San Diego Tech','Rancho San Diego');
NOTE: 3 rows were inserted into WORK.CUSTOMERS.

    SELECT *
        FROM CUSTOMERS
            ORDER BY CUSTNUM;
QUIT;
NOTE: PROCEDURE SQL used:
    real time                1.03 seconds
```
