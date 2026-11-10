
### Listing 5.22 Control Break Example

```abap
START-OF-SELECTION.
*Select Header Data
SELECT VBELN FKDAT NETWR KUNRG FROM VBRK
                                  INTO TABLE it_vbrk
                                  WHERE VBELN in s_vbeln.

  "Select Item Data
  SELECT VBELN POSNR ARKTX FKIMG VRKME NETWR MATNR MWSBP
         FROM vbrp INTO TABLE it_vbrp WHERE vbeln in s_vbeln.

END-OF-SELECTION.
*The SORT statement ensures the control break is consistent if
the table is not a sorted table.
SORT it_vbrp BY vbeln.
LOOP AT it_vbrp INTO wa_vbrp.
    AT FIRST. "Print Column Headings
    WRITE AT: /05 'ITEM',
              15 'DESCRIPTION',
              60 'BILLED QUANTITY',
              80 'UNITS',
             105 'NET VALUE',
             130 'MATERIAL NUMBER',
             150 'TAX AMOUNT'.

        WRITE SY-ULINE.
    ENDAT.

    AT NEW VBELN. " To print header data once per new document
      READ TABLE it_vbrk into wa_vbrk WITH KEY
                                      VBELN = wa_vbrp-vbeln.
      WRITE AT : /5 'Billing Document' LEFT-JUSTIFIED.
      WRITE AT : 30 wa_vbrk-vbeln  LEFT-JUSTIFIED COLOR 2.
      WRITE AT : /5 'Payer' LEFT-JUSTIFIED.
      WRITE AT : 30 wa_vbrk-kunrg LEFT-JUSTIFIED COLOR 3.
      WRITE AT : /5 'BILLING DATE' LEFT-JUSTIFIED.
      WRITE AT : 30  wa_vbrk-fkdat LEFT-JUSTIFIED COLOR 5.
      WRITE AT : /5 'NET VALUE' LEFT-JUSTIFIED.
      WRITE AT : 30 wa_vbrk-netwr LEFT-JUSTIFIED COLOR 6.
    ENDAT.
*Print Item details
      WRITE : /5 wa_vbrp-posnr LEFT-JUSTIFIED,
             15 wa_vbrp-arktx LEFT-JUSTIFIED,
             60 wa_vbrp-fkimg LEFT-JUSTIFIED,
             80 wa_vbrp-vrkme LEFT-JUSTIFIED,
            105 wa_vbrp-netwr LEFT-JUSTIFIED,
            130 wa_vbrp-matnr LEFT-JUSTIFIED,
            150 wa_vbrp-mwsbp LEFT-JUSTIFIED.

*To print document total netvalue at the end of last item in the
*document. The code in AT END OF will execute before the next new
*document.
    AT END OF vbeln.
*The keyword SUM can be used within a control break to
*automatically add up the column.
    SUM.
*Prints total Sum for document
    WRITE : / 105 WA_VBRP-NETWR LEFT-JUSTIFIED.
    ENDAT.
*To identify the last record in the table
    AT LAST.
        WRITE : / 'END OF REPORT'.
    ENDAT.
ENDLOOP.
```

Listing 5.22 processes the header and item data of a billing document. The header data is fetched from the database table `VBRK` and the item data is fetched from the database table `VBRP`. We're providing a selection screen to the user via the `SELECT-OPTIONS` statement. The `SELECT-OPTIONS` statement allows the user to input multiple document numbers that should be processed by the program. You'll learn more about `SELECT-OPTIONS` in Chapter 6.

Based on the user's input, we fetch the relevant records from the database table and process the records to print in the output using the `WRITE` statement. We're using the control break statements within the `LOOP` statement of the item table `IT_VBRP` to format the output.

For example, we're using the `AT FIRST` statement to identify the first loop pass to print the column heading. `AT NEW` is used to identify a new document to read and print the header record. `AT END OF` is used to identify the last item of the current document to print the total sum for the document. Finally, we used the `AT LAST` statement to identify the last record of the internal table to print a report closing statement.

The `WRITE` statement supports various formatting techniques, such as specifying the position on the screen to print the record, using the `WRITE AT` addition, using `/` to print the record in a new line, and so on. We'll explore the `WRITE` statement further in Chapter 13.

The following rules are applicable while using control break statements:

- The internal table fields should be sorted by the fields used in the control break.
- The internal table can't be modified within the loop.
- The content of a work area specified in the `LOOP` statement after the `INTO` addition can't be modified.

When the `AT-ENDAT` control structure is entered, the contents of the work area are modified as follows:

- The content of the components to which the control break is applied remain unchanged.
- All components with a character-like flat data type that are after the current control key are set to character * in every position.
- All the other components that are after the current control key are set to their initial values.

Figure 5.12 and Figure 5.13 display the contents of a work area before entering the control break and after entering the control break, respectively.

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_185_0.png)

**Figure 5.12** Contents of Work Area before Control Break Is Applied, Viewed in Debugger

![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_186_0.png)

**Figure 5.13** Contents of Work Area after Control Break Is Applied, Viewed in Debugger

When the `AT-ENDAT` control structure is exited, the content of the current table row is assigned to the entire work area.

## 5.3 Introduction to Open SQL Statements

SAP supports different relational database management systems (RDBMSs) like Oracle, Microsoft SQL, and SAP HANA. Structured Query Language (SQL) is a programming language designed for working with data in a relational database management system.

ABAP supports two types of SQL:

- **Open SQL**
  Open SQL allows you to access database tables and perform certain actions independent of the underlying database that the SAP ERP system is using. When executing an Open SQL statement, the database interface of the work process will take care of converting the Open SQL statement to a Native SQL statement—that is, native to the underlying database. This ensures your ABAP code is portable and will work irrespective of the underlying database.
- **Native SQL**
  Native SQL allows you to use database-specific SQL statements in an ABAP program. With a Native SQL statement, you can use database tables that are not part of ABAP Data Dictionary. This allows you to integrate data that is not part of the SAP ERP system. To use a Native SQL statement in an ABAP program, precede the statement with the `EXEC SQL` keyword and close it with the `END-EXEC` statement—for example:

  ```abap
  EXEC SQL.
  <Native sql statement>.
  END-EXEC.
  ```

SQL statements are categorized into the following languages:

- **Data Definition Language (DDL)**
  DDL statements are used to define the database structure or schema. Using a DDL statement, you can perform actions such as creating a table, dropping a table, changing the structure of the database table, and so on.
  The following are some examples of DDL statements:
  - `CREATE`: Creates objects in the database
  - `ALTER`: Alters the structure of the database
  - `DROP`: Deletes objects from the database
  - `TRUNCATE`: Removes all records from a table, including all spaces allocated for the records
  - `RENAME`: Renames an object

- **Data Manipulation Language (DML)**
  DML statements manage data within schema objects. Using DML statements, you can't alter the database schema but you can manipulate the data. For example, you can fetch the data from a database table, modify the records of the database table, delete records from the database table, and so on.
  The following are some examples of DML statements:
  - `SELECT`: Retrieves data from a database
  - `INSERT`: Inserts data into a table
  - `UPDATE`: Updates existing data within a table
  - `DELETE`: Deletes all records from a table, leaving the spaces for the records in place

With Open SQL, you can use DML statements. With Native SQL, you can use DDL statements. We generally use ABAP Data Dictionary to perform tasks that require using DDL statements with Native SQL.

In this section, we’ll discuss various key concepts of an RDBMS, such as database design, tables and keys, foreign key relationships, and normalization. We’ll also provide an introduction to Open SQL statements used to fetch data from database tables.

### 5.3.1 Database Overview

As discussed in Chapter 2, the database is managed by an RDBMS. A relational database consists of multiple tables that store particular sets of data, and an RDBMS standardizes how the data is stored and processed. In a relational database, data is stored in multiple tables, with a relationship between the tables.

The relational database model was first conceived by E. F. Codd in 1969. The model is based on set theory and predicate logic (branches of mathematics). The idea behind the relational model is that the database consists of a series of tables that can be manipulated using a declarative approach (nonprocedural operations).

It’s commonly thought that the word *relational* in a relational database pertains to the fact that you *relate* the tables in the database to one another. However, a table is also known as a *relation*, and the word *relational* takes its root from this. In fact, Codd and other database theorists use the terms *relations, attributes,* and *tuples* to refer to what developers call *tables, columns (fields),* and *rows* (or what we’d call *files, fields,* and *records* in a physical sense).

In the following subsections, we’ll explain how a database is modeled. We’ll start by discussing the use of database tables and the significance of table keys. We’ll then explore the concept of foreign key relationships to establish relationships between different tables of the database. We’ll also discuss the concept of normalization, which helps to simplify database design and avoid redundancy. We’ll conclude this section with an introduction to SAP HANA and the many benefits this database provides.

### Relational Database Design

A database model to reflect a real-world system takes time and effort to conceive, build, and refine. You need to make decisions about the tables you need to create, what fields they’ll contain, and how the tables can be related to each other.
