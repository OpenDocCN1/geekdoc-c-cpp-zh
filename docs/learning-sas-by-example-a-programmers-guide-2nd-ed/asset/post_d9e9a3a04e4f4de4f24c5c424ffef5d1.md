
## 74 Learning SAS by Example: A Programmer's Guide, Second Edition

Figure 6.5: Select a Worksheet if More than One

![](img/e9e15d853989558188e1c83b0ae655b0_88_0.png)

Once you have selected the worksheet you want to import, click Next. You are presented with a screen where you can enter a library (Work, if you want a temporary SAS data set, or a libref created with a LIBNAME statement) and the name of the SAS data set (labeled Member in the destination screen). See the following:

Figure 6.6: Choose a Library and File Name

![](img/e9e15d853989558188e1c83b0ae655b0_88_1.png)

If you then select Finish, SAS imports your spreadsheet. If you select Next, you can choose to save the conversion program (PROC IMPORT). If you save this program (you will be prompted for the name of a file to save the program), you can run it later to perform your conversion.

You are done. That's all there is to it. In this example, you chose the Work library and your SAS data set Wages_Permanent. It is a good idea to list the contents of this data set using the SAS viewer or PROC PRINT before to use it for reports or further analysis. If the data set is large, you can list the first few observations in the data set using the OBS=n data option to limit the number of observations you want to process. For example, to see the first four observations in data set Wages_Permanent, you could run the following program:

## Chapter 6: Reading and Writing Data from an Excel Spreadsheet

### Program 6.1: Using PROC PRINT to List the First Four Observations in a Data Set

```sas
title "The First Four Observations of Wages_Permanent";
proc print data=Wages_Permanent (obs=4);
run;
```

Here is the output:

Figure 6.7: Output from Program 6.1

| Obs | Subject | Date | Hours | Rate_Per_Hour | Wage |
|---|---|---|---|---|---|
| 1 | M75 | 04APR2006 | | 54 | $1,782.00 |
| 2 | F399 | 23AUG2006 | | 56 | $7,250.00 |
| 3 | M766 | 11MAY2006 | | 12 | $900.00 |
| 4 | M287 | 28FEB2006 | | 40 | 50 | $2,000.00 |

SAS has created variable names from the Excel column headings. It replaces invalid characters in column headings with an underscore (_). It is also a good idea to use the SAS Explorer or PROC CONTENTS to view the type (character or number) and length of each variable in this data set. You may need to use PROC DATASETS to change the format of one or more variables or to write a short DATA step to perform a character-to-numeric conversion for variables that you want to be numeric, but for one reason or other, as character.

Using the OBS=n data set option is a very useful way to check the data values of very large data sets. By this way, while we are on, you can combine the OBS=n data set option with the FIRSTOBS=m option. The value defines the first observation you want to process; the LASTOBS defines the last observation you want to process. It is a good idea to use OBS=LASTOBS. Perhaps you want to list observations 100 through 110 in a very large SAS data set called a library of Verbig. You could combine the FIRSTOBS=m and OBS=n options like this:

### Program 6.2: Using the FIRSTOBS and OBS= Options Today

```sas
title "Observations 100 through 110 in VERBIG";
proc print data=Project.Verbig (firstobs=100 obs=110);
run;
```

Program 6.2 results in a listing containing 11 observations (observation 100 through observation 110).

Importing Excel Worksheets using either Enterprise Guide or SAS Studio. For example, when using SAS Studio, you do not have to select a file format—it looks at the file extension (for example, XLS or XLSX) and automatically selects the correct import method.

## 76 Learning SAS by Example: A Programmer's Guide, Second Edition

### Program 6.3 Creating an Excel Spreadsheet from a SAS Data Set

Before we leave this, let's see how you can use the Export Wizard to convert a SAS data set into an Excel spreadsheet. From the File menu, select Export Data and then select Microsoft Excel.

Suppose you want to convert your Sales data set (located in the C:\books\learning folder) to an Excel spreadsheet. First, you need to be sure you have a library reference to the folder. For example, issue the following statement:

```sas
libname Learn 'C:\books\learning';
```

Then, follow these steps:

- From the File menu, select Export Data.

![](img/e9e15d853989558188e1c83b0ae655b0_90_0.png)

- On the next screen, enter the LIBNAME and the name of the SAS data set you want to export (Sales in this example) and click Next.

Figure 6.9: Name the Library and Data Set Name

![](img/e9e15d853989558188e1c83b0ae655b0_90_1.png)

## Chapter 6: Reading and Writing Data from an Excel Spreadsheet 77

Next, select Microsoft Excel from the pull-down menu.

Figure 6.10: Select Microsoft Excel

![](img/e9e15d853989558188e1c83b0ae655b0_91_0.png)

You can browse or enter the name of the Excel spreadsheet.

Figure 6.11: Name the Excel Workbook

![](img/e9e15d853989558188e1c83b0ae655b0_91_1.png)

You can also name the specific table.

Figure 6.12: Supply a Table Name

![](img/e9e15d853989558188e1c83b0ae655b0_91_2.png)

## 78 Learning SAS by Example: A Programmer's Guide, Second Edition

Select Finish and SAS writes the data to a spreadsheet (or select Next to write the table name).

### 6.4 Using an Engine to Read Excel Spreadsheet

You can have SAS treat an Excel spreadsheet as a data set by using the XLS or XLSX engine. For example, in the C:\books\learning folder, issue the following statement:

```sas
libname Read 'C:\books\learning';
```

You can now access the worksheet within this file. Suppose you want to compute the mean of Wage and Hours Worked in the Permanent worksheet. Here is the following:

### Program 6.3: Using PROC MEANS to Read Spreadsheet

```sas
title "Statistics from Sales"
libname Read 'C:\books\learning';

proc means data=Read.Permanent;
    var Wage HoursWorked;
run;
```

There are several important points to notice:

- First, because the worksheet name ($$) is not allowed in SAS names, you need to use single quotes.
- Second, because the column heading Hours Worked is not a valid variable name, SAS will substitute an underscore for any space.
- Thus, for this to work, you must use the VALIDNAME=ANY option:

```sas
options validname=any;
```

## Chapter 6: Reading and Writing Data from an Excel Spreadsheet 79

Figure 6.13: Output from Program 6.3

| Variable | Label | Mean |
|---|---|---|
| Wage | | 2568.40 |
| HoursWorked | | 37.20 |

Once you have created the appropriate LIBNAME statement, you can treat your spreadsheets as data sets.

### 6.5 Using the SAS Output System to Convert a SAS Data Set to Excel

You can use the Output System (ODS) to create CSV files that Excel can open directly. For more information on ODS, refer to Chapter 19.

As an example, you want to send the contents of the SAS data set to Excel. Program 6.4 creates a CSV file from the data set:

### Program 6.4: Using ODS to Convert a SAS Data Set into a CSV File (To Be Read by Excel)

```sas
libname Learn 'C:\books\learning';

ods csv file='C:\books\learning\ODS_Example.csv';

proc print data=Learn.Survey noobs;
run;

ods close;
```

The ODS CLOSE statement removes the CSV file as an output destination. Notice that the NOOBS option of PROC PRINT removes the OBS from the output. It is important to close the file with an ODS CLOSE statement following the PROC PRINT. Here is a listing of the file with C:\books\learning\ODS_Example.csv:

"ID","Gender","Age","Salary","Ques1","Ques2","Ques3","Ques4","Ques5"
001,M,23,28800,1,2,1,2,3
002,F,55,76123,4,5,2,1,1
003,M,38,36500,2,2,2,1,1
004,F,67,128000,5,3,2,2,4
005,M,22,23060,3,3,4,2,3
006,M,63,90000,2,3,5,4,3
007,F,45,76100,5,3,4,3,3
