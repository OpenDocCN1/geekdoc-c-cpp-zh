
## 5.2 Reordering Variables on the PDV

**The CONTENTS Procedure**

**Variables in Creation Order**

| # | Variable | Type | Len | Format | Label |
|---:|---|---|---:|---|---|
| 1 | subject | Num | 8 |  |  |
| 2 | clinnum | Char | 6 |  | clinic number |
| 3 | lname | Char | 10 |  | last name |
| 4 | fname | Char | 6 |  | first name |
| 5 | ssn | Char | 9 |  | social security number |
| 6 | sex | Char | 1 |  | patient sex |
| 7 | dob | Num | 8 | DATE7. | date of birth |
| 8 | death | Num | 8 | DATE7. | date of death |
| 9 | race | Char | 1 |  | race |
| 10 | edu | Num | 8 |  | years of education |
| 11 | wt | Num | 8 |  | weight in pounds |
| 12 | ht | Num | 8 |  | height in inches |
| 13 | symp | Char | 2 |  | symptom code |
| 14 | death2 | Num | 8 | DATE9. |  |

In the example that follows, only a few of the variables from ADVRPT.DEMOG flow through to the new data set, and the order of these variables is changed by the use of the LENGTH statement.

```sas
data demog2(keep=subject lname fname sex ht wt dob symp);
   length lname $10 fname $6 sex $1 symp $2;
   set advrpt.demog(keep=subject lname fname sex edu
                    death ht wt dob symp);
   where death and edu>15;
run;
```

❶ The KEEP and DROP statements/options do not change or affect the order of variables on the PDV.

❷ The LENGTH statement is used not only to assign the length attribute to these four variables, but it also adds them to the PDV. Since the LENGTH statement appears before the SET statement these variables and their associated attributes are added to the PDV before any variables or attributes are contributed by the SET statement. Attributes for these variables that have not been specified, for example formats or labels, will be picked up from the metadata of the incoming data set named on the SET statement.

❸ Although the variables DEATH and EDU are not to be included on the new data set, they must be available on the PDV for use by the WHERE statement.

| Obs | lname | fname | sex | symp | subject | dob | wt | ht |
|---:|---|---|---|---:|---:|---|---:|---:|
| 1 | James | Debra | F | 05 | 232 | 19JUN42 | 163 | 63 |
| 2 | Manley | Debra | F | 05 | 241 | 19JAN42 | 163 | 63 |

Notice that while the order has changed for the variables in the LENGTH statement, the order for the remaining variables is the same as it was on the incoming data.

The ARRAY, FORMAT, INFORMAT, RETAIN, and ATTRIB statements can also be used in a similar manner to reorder variables on the PDV. The KEEP, DROP, and RENAME statements cannot be used to change variable order. Generally the recommended choice of statements for reordering the variables is the RETAIN statement as it does not require any other attributes and does not otherwise change behavior of variables that are being brought into the DATA step via the SET or MERGE statements.

In the previous example the LENGTH statement ❷ could have been replaced with a RETAIN statement, which does not require additional knowledge of the attributes of the variables that are to be reordered.

```sas
retain lname fname sex symp;
```

It is also possible to reorder variables using an SQL step. Here the SELECT statement ❶ is used to specify the new variable order. Notice that unlike the DATA step a full list of variables must be specified unless you use the asterisk (*) ❷ to specify all variables, in which case you will see them in PDV order.

```sas
proc sql ;
create table demog4 as
❶ select lname, fname, sex, symp, subject, dob, wt, ht
  from advrpt.demog(keep=subject lname fname sex
  edu death ht wt dob symp)
  where death and edu>15;
  select * ❷
  from demog4;
quit;
```

When you read more than one data set in a step, the order of variables is determined to some extent by the order that the data sets are read in. Variables are added to the PDV in the order that they are encountered by the compiler. The order of the variables taken from the first data set seen by the compiler will be written to the PDV first. Variables not already on the PDV will be added to the PDV in the order that they are encountered on subsequent data sets. This means that you may have some control of variable order by controlling the order in which your incoming data sets are first seen.

### MORE INFORMATION

Although I do not necessarily recommend their use, some of the variable list abbreviations require you to have specific knowledge of the order of the variables (see Section 2.6.1).

### SEE ALSO

SAS Usage Note 8395 discusses the reordering of variables at http://support.sas.com/kb/8/395.html.

## 5.3 Building and Maintaining Indexes

It is a bit surprising how few programmers actually take advantage of indexing. True the topic can be a bit complex; after all, a book has been written on the subject (Raithel, 2006). Complex or not you do not need a lot of knowledge to take advantage of them.

Indexes give us the ability to virtually sort a data table without physically sorting it. More than one index can be created for any given data table and with multiple indexes it is possible to effectively sort the data set multiple ways at the same time. Once created the index allows the use of the BY statement and other processing techniques as if the data had been sorted using PROC SORT. The index can also be very helpful in subsetting and merging situations.

### 5.3.1 Metadata for an Indexed Table

| The CONTENTS Procedure | |
|---|---|
| Data Set Name | ADVRPT.DEMOG |
| Member Type | DATA |
| Engine | V9 |
| Created | Tue, Sep 22, 2009 10:57:37 AM |
| Observations | 77 |
| Variables | 14 |
| Indexes | 3 ① |
| Observation Length | 96 |

**Alphabetic List of Indexes and Attributes**

| # | Index | # of Unique Values | Variables |
|---:|---|---:|---|
| 1 | group | 23 | sex race edu |
| 2 | ssn | 76 |  |
| 3 | subject | 77 |  |

The index definitions are also included in the data set’s metadata as can be seen by looking at the listing generated by PROC CONTENTS. The name of each index is shown under the column labeled Index ②. For composite indexes the variable list is also shown under the column labeled Variables ③.

When an index has been selected, its use will be mentioned in the LOG.

```text
66  proc print data=advrpt.demog;
67      by sex race edu;
NOTE: An index was selected to execute the BY statement.
      The observations will be returned in index order rather than
      in physical order. The selected index is for the variable(s):

sex
race
edu
```

The indexes are not actually stored in the data set itself. Instead they reside in a separate file. Under Windows the index file has the same name as the data set with which it is associated; however, the extension is different.

### 5.3.2 Creating Simple Indexes

Indexes can be created using a DATASETS step, an SQL step, or a DATA step. Each of the next three steps creates a simple index. Later in this section these indexes are used in several PROC PRINT steps.

```sas
proc datasets lib=advrpt;
  modify demog;
  index create clinnum; ② ③
quit;
```

- ❶ The data set receiving the index is named. The data set may be either permanent or temporary.
- ❷ The index to be created is named. For simple indexes the name is the same as the single variable used to form the index.
- ❸ The variable used to define the index is named (separately in the SQL step).

```sas
proc sql noprint;
  create index clinnum ②
    on advrpt.demog ❶ (clinnum) ③;
quit;
```

```sas
data demog2 ❶(index=(clinnum ②③));
  set advrpt.demog;
run;
```

The three methods for creating the index will tend to have different efficiencies based on your particular data. Each method of creating the index will read and handle the data differently.

Of these three methods of creating indexes, the DATA step is the only one that reads the entire data set. PROC SQL and PROC DATASETS don't read the data in the same way; primarily they just add the index file. This means that the generation of the index can be more costly when done with a DATA step, and its cost will grow as the volume of data grows.

When the MSGLEVEL system option is set to I ❶, a note will be written to the LOG when an index is utilized. In this PROC PRINT step the data are subsetted using the SSN variable. The LOG shows that the index for SSN was selected for use with the WHERE clause.

```sas
* Create index on ssn;
proc sql noprint;
   create index ssn
      on advrpt.demog (ssn);
   quit;

options msglevel=i; ❶

* Use the ssn index;
proc print data=advrpt.demog;
   var lname fname;
   where ssn < '3';
   id ssn;
run;
```

```text
139  proc print data=advrpt.demog;
140     var lname fname;
141     where ssn < '3';
INFO: Index ssn selected for WHERE
clause optimization. ❶
```

Once the indexes have been created, a BY statement using the indexed variable(s) will cause the index to be used. In the two PROC PRINT steps, two different BY ❷ statements are used with the same incoming data set. Since both are indexes, that data may not be sorted by either of the two BY variables; however, both steps will execute successfully.

```sas
proc print data=advrpt.demog;
   by clinnum; ❷
   id clinnum;
run;

proc print data=advrpt.demog;
   by ssn; ❸
   id ssn;
run;
```

An index can be removed from a data set through the use of PROC DATASETS. The index to be removed is identified by its name (simple or composite) on the INDEX statement along with the DELETE option. In this step the simple index CLINNUM is being removed from the ADVRPT.DEMOG data set.

```sas
proc datasets lib=advrpt;
   modify demog;
   index delete clinnum;
   quit;
```
