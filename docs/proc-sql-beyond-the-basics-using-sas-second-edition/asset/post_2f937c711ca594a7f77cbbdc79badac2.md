
In the next example, both phones and software products are selected from the PRODUCTS table. To avoid having to specify two OR conditions, the IN predicate is specified.

## SQL Code

```
PROC SQL;
    SELECT PRODNAME,
            PRODTYPE,
            PRODCOST
    FROM PRODUCTS
        WHERE UPCASE(PRODTYPE) IN ('PHONE', 'SOFTWARE');
QUIT;
```

## Results

| Product Name | Product Type | Product Cost |
|---|---|---|
| AnalogPhone | Phone | $35.00 |
| DigitalPhone | Phone | $175.00 |
| OfficePhone | Phone | $130.00 |
| SpreadsheetSoftware | Software | $299.00 |
| DatabaseSoftware | Software | $399.00 |
| WordprocessorSoftware | Software | $299.00 |
| GraphicsSoftware | Software | $299.00 |

## Testing for NULL or MISSING Values

The IS NULL predicate is the ANSI approach of selecting one or more rows by evaluating whether a column value is missing or null (see the “Missing Values and Null section). The next example selects products from the INVENTORY table that are out-of-stock in inventory.

## SQL Code

```
PROC SQL;
    SELECT PRODNUM,
            INVENQTY,
            INVENCST
    FROM INVENTORY
        WHERE INVENQTY IS NULL;
QUIT;
```

## SAS Log Results

```
PROC SQL;
    SELECT PRODNUM,
        INVENQTY,
        INVENCST
        FROM INVENTORY
        WHERE INVENQTY IS NULL;
NOTE: No rows were selected.
    QUIT;
NOTE: PROCEDURE SQL used:
    real time          0.05 seconds
```

The next example selects products from the INVENTORY table that are currently stocked in inventory. Note that the predicates NOT IS NULL or IS NOT NULL can be specified to produce the same results.

## SQL Code

```
PROC SQL;
    SELECT PRODNUM,
        INVENQTY,
        INVENCST
        FROM INVENTORY
        WHERE INVENQTY IS NOT NULL;
QUIT;
```

## Results

| Product Number | Inventory Quantity | Inventory Cost |
|---|---|---|
| 1110 | 20 | $45,000.00 |
| 1700 | 10 | $28,000.00 |
| 5001 | 5 | $1,000.00 |
| 5002 | 3 | $900.00 |
| 5003 | 10 | $2,000.00 |
| 5004 | 20 | $1,400.00 |
| 5001 | 2 | $1,200.00 |

The IS MISSING predicate performs identically to the IS NULL predicate by selecting one or more rows containing a missing value (null). The only difference is that specifying IS NULL is the ANSI standard way of expressing the predicate and IS MISSING is commonly used in SAS. The

When a pattern search for a specific number of characters is needed, using the LIKE predicate with the underscore (_) provides a way to pattern match character-by-character. Thus, a single underscore (_) in a specific position acts as a wildcard placement holder for that position only. Two consecutive underscores (__) act as a wildcard placement holder for those two positions. Three consecutive underscores act as a wildcard placement holder for those three positions. And so forth. In the next example, the first position used to search product type contains the character “P”, and the next five positions (represented with five underscores) act as a placeholder for any value.

## SQL Code

```
PROC SQL;
    SELECT PRODNAME,
            PRODTYPE,
            PRODCOST
      FROM PRODUCTS
     WHERE UPCASE(PRODTYPE) LIKE 'P_____';
QUIT;
```

## Results

| Product Name | Product Type | Product Cost |
|---|---|---|
| AnalogPhone | Phone | $35.00 |
| DigitalPhone | Phone | $175.00 |
| OfficePhone | Phone | $130.00 |

The next example illustrates a pattern search of product name (PRODNAME) where the first three positions are represented as a wildcard; the fourth position contains the lowercase character “a”, followed by any combination of uppercase or lowercase characters.

## SQL Code

```
PROC SQL;
    SELECT PRODNAME
      FROM PRODUCTS
     WHERE PRODNAME LIKE '___a%';
QUIT;
```

## Results

| Product Name |
|---|
| Dream Machine |
| Database Software |

## Testing for the Existence of a Value

The EXISTS predicate is used to test for the existence of a set of values. In the next example, a subquery is used to check for the existence of customers in the CUSTOMERS table with purchases from the PURCHASES table. More details on subqueries will be presented in Chapter 7, “Coding Complex Queries.”

## SQL Code

```
PROC SQL;
    SELECT CUSTNUM,
            CUSTNAME,
            CUSTCITY
    FROM CUSTOMERS C
    WHERE EXISTS
        (SELECT *
         FROM PURCHASES P
         WHERE C.CUSTNUM = P.CUSTNUM);
QUIT;
```

## Results

| Customer Number | Customer Name | Customer's Home City |
|---|---|---|
| 101 | La Mesa Computer Land | La Mesa |
| 201 | Vista Tech Center | Vista |
| 301 | Coronado Internet Zone | Coronado |
| 401 | La Jolla Computing | La Jolla |
| 501 | Alpine Technical Center | Alpine |
| 701 | San Diego Byte Store | San Diego |
| 801 | Jamul Hardware & Software | Jamul |
| 901 | Del Mar Tech Center | Del Mar |
| 1001 | Lakeside Software Center | Lakeside |
| 1101 | Bonsall Network Store | Bonsall |
| 1201 | Rancho Santa Fe Tech | Rancho Santa Fe |
| 1301 | Spring Valley Byte Center | Spring Valley |
| 1401 | Poway Central | Poway |
| 1601 | Fairbanks Tech USA | Fairbanks Ranch |
| 1701 | Blossom Valley Tech | Blossom Valley |
| 1801 | Chula Vista Networks |  |

## Dictionary Tables

SAS generates and maintains valuable runtime information (metadata) about SAS libraries, data sets, catalogs, indexes, macros, system options, titles, views, and other content in a collection of read-only tables called *dictionary tables*. Although called tables, dictionary tables are not real tables at all. Dictionary tables and their contents permit a SAS session’s activities to be easily accessed and monitored. Information is automatically produced and the tables contents are made available at the time a SAS session begins.

Table 2.1: Available Dictionary Tables and Their Contents

| Dictionary Table Name | Contents |
|---|---|
| DICTIONARY.CATALOGS | SAS catalogs |
| DICTIONARY.COLUMNS | Data set columns and attributes |
| DICTIONARY.EXTFILES | Allocated filerefs and external physical path |
| DICTIONARY.INDEXES | Data set indexes |
| DICTIONARY.MACROS | Global and automatic macro variables |
| DICTIONARY.MEMBERS | SAS data sets and other member types |
| DICTIONARY.OPTIONS | Current SAS system option settings |
| DICTIONARY.TABLES | SAS data sets and views |
| DICTIONARY.TITLES | Title and footnote definitions |
| DICTIONARY.VIEWS | SAS data views |

## Dictionary Tables and Metadata

SAS collects and populates valuable information (“metadata” or data about data) on SAS libraries, data sets (tables), catalogs, indexes, macros, system options, titles, views, and a collection of other read-only tables called *dictionary tables*. Dictionary tables serve a special purpose by providing system-related information about the current SAS session’s SAS databases and applications. When a query is requested against a dictionary table, SAS automatically launches a discovery process at runtime to collect information pertinent to that table. This information is made available any time after a SAS session is started.

While earlier versions of SAS software had 22 dictionary tables and SASHELP views, there are 29 “known” dictionary tables and SASHELP views in SAS 9.2, and 30 “known” dictionary tables and SASHELP views in SAS 9.3, with the name of each DICTIONARY table and SASHELP view illustrated below.

## Table 2.2: DICTIONARY Tables and SASHELP Views

| DICTIONARY Table | SASHELP View | Purpose |
|---|---|---|
| CATALOGS | VCATALG | Provides information about SAS catalogs. |
| CHECK_CONSTRAINTS | VCHKCON | Provides check constraints information. |
| COLUMNS | VCOLUMN | Provides information about column in tables. |
| CONSTRAINT_COLUMN_USAGE | VCNCOLU | Provides column integrity constraints information. |
| CONSTRAINT_TABLE_USAGE | VCNTABU | Provides information related to tables with integrity constraints defined. |
| DATAITEMS | VDATAIT | Provides information about known data items. |
| DESTINATIONS | VDEST | Provides information about known ODS destinations. |
| DICTIONARIES | VDCTNRY | Provides information about all the DICTIONARY tables. |
| ENGINES | VENGINE | Provides information about known SAS engines available to the session. |
| EXTFILES | VEXTFL | Provides information related to external files. |
| FILTERS | VFILTER | Provides information about known filters. |
| FORMATS | VFORMAT | Provides information related to defined formats and informats. |
| FUNCTIONS | VFUNC | Provides information about all known functions. |
| GOPTIONS | VGOPT | Provides information about currently defined SAS/GRAPH software graphics options. |
| INDEXES | VINDEX | Provides information related to defined indexes. |
| INFOMAPS | VINFOMP | Provides information about all known information maps. |
| LIBNAMES | VLIBNAM | Provides information related to defined SAS data libraries. |
| MACROS | VMACRO | Provides information related to any defined macros. |
| MEMBERS | VMEMBER | Provides information related to objects currently defined in SAS data libraries. |
| OPTIONS | VOPTION | Provides information related to SAS system options. |
