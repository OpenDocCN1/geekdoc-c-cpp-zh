# DISCOVERING THE CONTENTS OF AN SAS DATA SET

```
PROC EXPORT DATA=MYSASLIB.SOMEDATA
OUTFILE="C:\SASDATA\EXPORTED.CSV"
DBMS=CSV
REPLACE;

RUN;
```

Run this code and observe (in Windows) that the file EXPORTED. CSV was created.
2. Open EXPORTED. CSV in Notepad or Word that the first line in the file includes the variable names. The remainder of the file includes the data values, separated by commas.
3. Close the EXPORTED. CSV file. In your SAS code, add a LABELS statement before the REPLACE option. Run Exported. CSV in Excel. With this revised code, the first row contains the SAS labels for the columns rather than the variable names (Creating and using labels is introduced and discussed in Chapter 4).

# 3.8 DISCOVERING THE CONTENTS OF AN SAS DATA SET

Data can come from a number of sources. A popular way to data, by e-mail or download, is in an SAS data set. (These data sets have .SAS7BD file extension.) If you acquire an SAS data set from another source, you can find out about the contents in two ways:

+   - Copy the SAS7BDAT-type data file into a folder that is linked to an SAS library (such as C: \SASDATA). Use SAS ViewData to view the contents of the data set.
- Use PROC DATASETS to list information about the variables in the data set.

We've already illustrated how to use ViewData and PROC PRINT to see the actual contents of a data set. The PROC DATASETS technique does not show you actual data. Instead, it provides details about the variables in the data set, including their names, formats, and labels. For example, the following SAS program (CONTENTS .SAS) displays information about the SOMEDATA data set in the MYSASLIB library:

```
PROC DATASETS;
CONTENTS DATA='C:\SASDATA\SOMEDATA';
RUN;
```

When you run this program, SAS produces a listing of the contents of the data set, including variable names and other information. It is a handy way to discover what information is in a particular SAS data set. This is illustrated in the following Hands-on Example.

> HANDS-ON EXAMPLE
In this example, you will discover the contents of an SAS data file using PROC DATASETS.
1. Open the program file CONTENTS .SAS. Run the program.
(continued)