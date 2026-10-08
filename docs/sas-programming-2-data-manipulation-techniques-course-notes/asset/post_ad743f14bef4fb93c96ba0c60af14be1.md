
# 10.01 Multiple Choice Poll

Which program should be more efficient?

- a. Program 1
- b. Program 2
- c. They should be equally efficient.

## Using the LIBRARY= Option

Use the LIBRARY= option to control where the format is stored.

```
proc format library=orion.MyFmts
   cntlin=country;
run;
LIBRARY=libref.catalog
```

## Where Formats Are Stored

By default, formats are stored in the work.formats catalog and exist only for the duration of the SAS session.

![](img/d3bde6e6ab06b1fc622215d982111742_409_0.png)

Catalog entries have four-level names: libref.catalog.entry-name.type.

The type for character formats is format. The type for numeric formats is format.

## Using the LIBRARY= Option

Use the LIBRARY= option to control where the format is stored.

```
proc format library=orion.MyFmts
   cntlin=country;

LIBRARY=libref.catalog
```

## Using the LIBRARY= Option

If the LIBRARY= option specifies only libref, formats are stored permanently in a catalog named formats, referenced by libref.formats.

```
proc format library=orion;
PROC FORMAT LIBRARY=libref;
```

![](img/d3bde6e6ab06b1fc622215d982111742_410_0.png)

## Using the LIBRARY= Option

If the LIBRARY= option specifies libref.catalog, formats are stored permanently in that catalog.

```
proc format library=orion.MyFmts;
PROC FORMAT LIBRARY=libref.catalog;
```

- Store frequently used formats in permanent catalogs.

## Viewing Formats

You can use the SAS Explorer window to view formats stored in a catalog.

![](img/d3bde6e6ab06b1fc622215d982111742_411_0.png)

You need the SAS Catalog Explorer Add-in for Enterprise Guide to view formats stored in a catalog. For more information see: http://blogs.sas.com/content/sasdummy/2010/05/10/viewing-sas-catalogs-from-sas-enterprise-guide/

## CATALOG Procedure

The CATALOG procedure manages entries in SAS catalogs.

```
proc catalog cat=orion.MyFmts;
  contents;
quit;
```

| # | Name | Type | Create Date | Modified Date |
|---|---|---|---|---|
| 1 | DATES | FORMAT | 20Jan08:16:26:39 | |
| 2 | COUNTRY | FORMATC | 20Jan08:16:33:30 | 29Jan08:16:33:30 |
| 3 | COUNTRY_NAME | FORMAT | 20Apr09:15:30:14 | 20Apr09:15:30:14 |
| 4 | EXTRA | FORMAT | 20Apr09:15:30:14 | 20Apr09:15:30:14 |

## Documenting Formats

You can use the FMTLIB option in the PROC FORMAT statement to document the format.

```
proc format library=orion.MyFmts fmtlib;
  select $country;
run;
```

| FORMAT NAME: SCOUNTRY LENGTH: 13 NUMBER OF VALUES: 7 |
| MIN LENGTH: 1 MAX LENGTH: 40 DEFAULT LENGTH 13 FUZZ: 0 |
| START | END | LABEL (VER. T7|VB) OSMAY2009:12:34:42 |
| AU | AU | Australia |
| CA | CA | Canada |
| DE | DE | Germany |
| IL | IL | Israel |
| TR | TR | Turkey |
| US | US | United States |
| ZA | ZA | South Africa |

![](img/d3bde6e6ab06b1fc622215d982111742_412_0.png)

You can use either the SELECT or EXCLUDE statement to process specific formats rather than an entire catalog.

## Nesting Formats

In the VALUE statement, you can specify that the format use a second format as the formatted value.

Enclose the format name in square brackets:

```
proc format library=orion.MyFmts;
  value $extra = 'Unknown'
    other=[$country30];
run;
  value=[existing-format];
```

![](img/d3bde6e6ab06b1fc622215d982111742_412_1.png)

Avoid nesting formats for more than one level. The resource requirements can increase dramatically with each additional level.

10-12 Chapter 10 Creating and Maintaining Permanent Formats

## Using a Control Data Set to Create a Format

p210d01

This demonstration illustrates how to create a permanent format from a SAS data set, and start values.

- 1. Submit step 1 to create a SAS data set that contains the format name, labels, and start values.
    - a. The DATA step creates the control set.
    - b. Use PROC PRINT to view the new data set.

```
/* Step 1 */
/* control data set containing */
/* the variables, START, and */
/* LABEL. */
data country;
  keep Start Label FmtName;
  retain Fmtname '$country'
  set orion.(rename=(Country=Start Country_Name=Label));

proc print data=country noobs;
  title 'Country';
run;
```

- 2. Submit Step 2 to use a SAS data set to create the permanent format.
    - a. The first PROC FORMAT creates the format.
    - b. Use PROC CATALOG to view the contents of the catalog.
    - c. The second PROC FORMAT augments country by creating a label for missing values.
    - d. Use PROC FORMAT with the FMTLIB option to document country.

```
/* Step 2 */
/* Use the data set to */
/* make the format $country. */
proc format library=orion.MyFmts cntlin=country;
run;

proc catalog cat=orion.MyFmts;
  contents;
run;
```

## 10.1 Creating Permanent Formats 10-13

```
****************************************************
/* If there are missing values, they can be */
/* handled by creating the $extra format. This */
/* sets missing values to the label */
/* Unknown and uses the label of the $country */
/* format for all other values. Notice that length */
/* of 30 is provided for the $country format. */
/* The default would be 40. */
****************************************************
proc format library=orion.MyFmts;
    value $extra = 'Unknown'
    other = [$country30];
run;

proc format library=orion.MyFmts fmtlib;
    select $country $extra;
run;
```

## Business Scenario

Use the permanent format $country to specify country names instead of country codes in the reports.

| Country | Population | Country_ID |
|---|---|---|
| AU | 20,000,000 | 160 |
| CA | | 260 |
| DE | 80,000,000 | 394 |
| IL | 5,000,000 | 475 |

![](img/d3bde6e6ab06b1fc622215d982111742_414_0.png)

| Country | Population | Country_ID |
|---|---|---|
| Australia | 20,000,000 | 160 |
| Canada | | 260 |
| Germany | 80,000,000 | 394 |
| Israel | 5,000,000 | 475 |

## Using Formats

By default, when a format is referenced, SAS does the following:

- searches formats supplied by SAS
- searches work.formats
- writes an error to the log if the format is not found

![](img/d3bde6e6ab06b1fc622215d982111742_415_0.png)

## 10.02 Short Answer Poll

Submit the program p210a01. What error messages do you see in the SAS log?

```
data customers;
  set orion.customer;
  Country_Name=put(Country, $country);
run;

proc freq data=orion.employee_addresses;
  tables Country;
  format Country $extra;
run;
```

> SAS can't find format

## 10.1 Creating Permanent Formats

## Using the NOFMTERR System Option

By default, the FMTERR system option is in effect. If you use a format that SAS cannot load, SAS issues an error message and stops processing the step. To prevent the default action, change the system option FMTERR to NOFMTERR.

```
OPTIONS FMTERR | NOFMTERR;
```

## 10.03 Short Answer Poll

Replace the current OPTIONS statement with the following statement and resubmit p210a01. What is the result?

```
options nofmterr;
```

![](img/d3bde6e6ab06b1fc622215d982111742_416_0.png)

## Using the FMTSEARCH= System Option

To use permanent formats or to search multiple catalogs, use the FMTSEARCH= system option to identify the catalog(s) to be searched for the format(s).

```
options fmtsearch=(orion orion.MyFmts);
OPTIONS FMTSEARCH=(item-1 item-2...item-n);
```

## Using the FMTSEARCH= System Option

```
options fmtsearch=(orion orion.MyFmts);
```

- 1 formats supplied by SAS
- 2 work.formats
- 3 library.formats
- 4 orion.formats
- 5 orion.MyFmts

Because orion is a libref without a catalog name, formats is assumed to be the catalog name.

Formats supplied by SAS are always searched first. The work.formats catalog is always searched, unless it appears in the FMTSEARCH list. If the library libref is assigned, the library.formats catalog is searched after before anything else in the FMTSEARCH list, unless it appears in the list. To assign the library libref, use the code shown below:

```
classname library 'SAS-data-library-containing-format-catalog';
```
