checks the index to locate the entry where A=10 and uses the pointer to retrieve the remaining fields of the row from the table (see Figure 10.12).

![](bbox=[0.142, 0.159, 0.624, 0.301])

**Index**

| A | Pointer |
|---|---:|
| 1 | 1 |
| 5 | 4 |
| 10 | 2 |
| 12 | 3 |

**Table XYZ**

| A | B | C | D |
|---:|---:|---:|---:|
| 1 | 20 | 30 | 40 |
| 10 | 21 | 31 | 41 |
| 12 | 22 | 32 | 42 |
| 5 | 23 | 33 | 43 |

**Figure 10.12** Index

# Secondary Index

Apart from the primary index created by default, we can create other indexes, called *secondary indexes*. These are required if we're performing a lookup on a table in which the complete primary key is not used in the WHERE clause. For example, if we're searching table XYZ where D=41, then the system can't make use of the primary index, because the primary index stores only the key fields.

In such situations in which a suitable index isn't available, the system performs a full table scan, which affects performance. To avoid a full table scan if the complete primary key can't be supplied in the WHERE clause, we can create secondary indexes.

The *database kernel* consists of an SQL optimizer, which analyzes the SQL query and optimizes access to the data by performing cost determination and analyzing table statistics. The *SQL optimizer* selects the best search strategy for accessing the data. For example, if the table contains multiple indexes, the SQL optimizer automatically selects the most suitable index for reading the data.

The SQL optimizer can also determine if performing a full table scan results in more efficient access than selecting any of the available indexes. Sometimes, the SQL optimizer may ignore an index and perform a full table scan even when a suitable index is available. This can happen if the SQL optimizer finds the cost of a full table scan to be lower than the cost of using a secondary index due to profile settings that are more favorable to full table scans. Certain databases, such as