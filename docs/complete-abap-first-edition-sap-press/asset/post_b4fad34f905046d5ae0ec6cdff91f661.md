
from the database after successful execution of the `SELECT` statement. If no data is read, the `SY-SUBRC` system field is updated with 4. The `SY-DBCNT` system field is updated with the number of records read.

The `WHERE` clause condition specifies the conditions under which the data is read. The system performs a lookup on the database table based on the condition specified in the `WHERE` clause. If no `WHERE` clause is specified, all the data from the database table specified in the `FROM` clause will be read to the data object specified in the `INTO` clause. Executing `SELECT` without a `WHERE` clause should always be avoided, because it can result in huge data transfer and cause memory overflow under certain conditions.

In addition to these basic clauses, the `SELECT` statement can contain three other clauses:

- `GROUP BY` — Used to aggregate several rows and import to a single row.
- `HAVING` — Used to specify conditions for aggregated rows.
- `ORDER BY` — Used to sort the rows of the result set.

Now, let’s discuss the different clauses of the `SELECT` statement and the different additions that are supported.

## SELECT Clause

The `SELECT` clause determines if one or several rows are read from a database table and what columns are read. If the `SINGLE` addition is used, only one record is read. If the `SINGLE` addition isn't specified, the `SELECT` statement should be closed with an `ENDSELECT` statement (or the target variable should be an internal table), and the system will assume that the result set contains multiple rows. The system loops between the `SELECT` and `ENDSELECT` statements, transferring one record at a time to the data object specified in the `INTO` clause.

The `SELECT...ENDSELECT` statement allows you to evaluate each row as it’s transferred to the program. When using the `SINGLE` addition, the `WHERE` clause should use the complete key of the database table to uniquely identify the row; otherwise, the first matching row is fetched into the program. To ignore duplicates when using a non-unique WHERE clause with SELECT...ENDSELECT, you can use the DISTINCT addition.

You can specify the columns that should be selected by listing the field names separated by spaces, or use * to select all the fields of the table. The following statement shows an example of using SELECT SINGLE to select certain fields of table SPFLI:

```abap
SELECT SINGLE carrid connid FROM spfli INTO st_spfli WHERE carrid EQ 'AA' AND connid EQ '0017'.
```

The following statement shows an example of using SELECT SINGLE to select all the fields of table SPFLI:

```abap
SELECT SINGLE * FROM spfli INTO st_spfli WHERE carrid EQ 'AA' AND connid EQ '0017'.
```

**Listing 11.2** shows an example of how to use the SELECT...ENDSELECT statement to fetch certain fields from table SPFLI. The system loops between SELECT and ENDSELECT, transferring one record at a time.

```abap
SELECT carrid connid FROM sflight INTO st_sflight WHERE carrid EQ 'AA' AND connid EQ '0017'.
*Code to process the record
ENDSELECT.
```

**Listing 11.2**  Fetching Particular Fields from Table SPFLI

**Listing 11.3** shows an example of using the SELECT...ENDSELECT statement to fetch all fields from table SPFLI. The system loops between SELECT and ENDSELECT, transferring one record at a time.

```abap
SELECT * FROM sflight INTO st_sflight WHERE carrid EQ 'AA' AND connid EQ '0017'.
*Code to process the record
ENDSELECT.
```

**Listing 11.3** Fetching All Fields from Table SPFLI

*Aggregate functions* can be used with the SELECT clause, which then calculates the value in the database system and returns a single value. This is especially useful with CDS views, in which calculations can be pushed to a database, such as SAP HANA, which performs the aggregations much faster than fetching the records into the ABAP program and then performing aggregations. Aggregate functions also reduce the data transfer between the database and the ABAP program by returning just the result. Aggregate functions bypass the buffer.

The following aggregation functions are supported:

- **Average (AVG)**

  Returns the average value for the specified column field of the result set. The AVG function can only be applied to numeric fields.

  ```abap
  SELECT AVG( netwr ) FROM vbrp INTO lv_avg_netwr WHERE vbeln EQ p_vbeln.
  ```

  In the preceding example, the lv_avg_netwr variable should be of type F (floating point).

- **Minimum (MIN)**

  Returns the smallest value for the specified column in the result set. NULL values are ignored unless all the rows in the column contain NULL values.

  ```abap
  SELECT MIN( fkimg ) FROM vbrp INTO lv_min_fkimg WHERE vbeln EQ p_vbeln.
  ```

- **Maximum (MAX)**

  Returns the greatest value for the specified column in the result set. NULL values are ignored unless all the rows in the column contain NULL values.

  ```abap
  SELECT MAX( fkimg ) FROM vbrp INTO lv_max_fkimg WHERE vbeln EQ p_vbeln.
  ```

- **Total (SUM)**

  Returns the sum of all values for the specified column in the result set. SUM can only be applied to numeric fields.

  ```abap
  SELECT SUM( fkimg ) FROM vbrp INTO lv_sum_fkimg WHERE vbeln EQ p_vbeln.
  ```

- **Count (COUNT)**

  Returns the number of rows or distinct rows for the specified column in the result set. Using COUNT DISTINCT returns the number of distinct rows, whereas COUNT (*) returns the number of rows for the given selection.

## WHERE Clause

The WHERE clause allows you to restrict the data selection; it plays a crucial role in performance of the program. You can specify logical expressions with the WHERE clause, which can be combined with AND and OR, or negated with NOT. Logical expressions can form conditions by using the comparison operators =, <, >, <=, or >=, such as in the following example: WHERE carrid = 'AA'.

The left operand in the comparison must always be a field of the table specified in the FROM clause. You can also specify the predicates BETWEEN and IN in the WHERE clause—for example: WHERE col BETWEEN v_col1 AND v_col2. The IN predicate is used with selection tables (range tables).

## INSERT

The INSERT statement inserts a new record in the database table. If the primary key of the record already exists, the new record isn't inserted.

Similar to other Open SQL statements, the INSERT statement sets the value for system fields SY-SUBRC and SY-DBCNT. If the SY-SUBRC value is 0 after the statement is executed, it means the record is inserted to the database table successfully. The SY-SUBRC field will be set to 0 if an empty internal table is supplied in the source. If the SY-SUBRC value is 4, it means the record isn't inserted to the database table, because the primary key or unique secondary key already exists in the table. The SY-DBCNT system field is updated with the number of rows that are inserted.

With the INSERT statement, you can insert a single row from a structure (e.g., INSERT table_name FROM wa) or multiple rows from an internal table (e.g., INSERT table_name FROM TABLE itab).

Listing 11.4 shows an example of inserting a single row using the INSERT statement.

```abap
DATA : wa_makt TYPE makt.

wa_makt-matnr = '100'.
wa_makt-spras = 'E'.
wa_makt-maktx = 'Pen'.

INSERT makt FROM wa_makt.
IF sy-subrc IS INITIAL.
MESSAGE 'Record inserted successfully' TYPE 'I'.
ENDIF.
```

**Listing 11.4**  Inserting Single Row

Listing 11.5 shows an example of inserting multiple rows.

```abap
DATA : it_makt TYPE STANDARD TABLE OF makt,
       wa_makt TYPE makt.
wa_makt-matnr = '100'.
wa_makt-spras = 'E'.
wa_makt-maktx = 'Pen'.
APPEND wa_makt TO it_makt.

wa_makt-matnr = '200'.
wa_makt-spras = 'E'.
wa_makt-maktx = 'Pencil'.
APPEND wa_makt TO it_makt.

INSERT makt FROM TABLE it_makt.
IF sy-subrc IS INITIAL.
MESSAGE 'Records inserted successfully' TYPE 'I'.
ENDIF.
```

**Listing 11.5** Inserting Multiple Rows

## UPDATE

The UPDATE statement updates an existing record in the table. When this statement is used, the non-key fields of the existing row are updated. If the key doesn’t exist, no record is updated.

Similar to the INSERT statement, you can update a single record by supplying a structure or update multiple records by passing an internal table. The system sets the SY-SUBRC and SY-DBCNT fields, similar to the INSERT statement. These system fields can be checked to identify if the record is updated successfully and the number of records that were updated, respectively.

The syntax to use the UPDATE statement is similar to that for the INSERT statement. For example, for the code in Listing 11.4, to update a record from a work area, you can use the UPDATE statement in place of INSERT as follows:

```abap
UPDATE makt FROM wa_makt.
```

Similarly, in Listing 11.5, to update from an internal table, you can use the following statement:

```abap
UPDATE makt FROM TABLE it_makt.
```
