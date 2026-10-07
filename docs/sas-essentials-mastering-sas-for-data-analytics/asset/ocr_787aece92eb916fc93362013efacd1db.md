# USING DATA IN PERMANENT SAS DATA SETS

In the previous example, the MYLIB2 library nickname continues to be active and available for use until you exit the SAS program. However, the library nickname MYASLIB, created with the dialog box, using the Enable at startup option, is remembered by SAS each time you enter the SAS environment.

# 3.6 USING DATA IN PERMANENT SAS DATA SETS

After you created a SAS library (either a permanent or a temporary one), you can access data in that library within SAS procedures or as input into other DATA steps. In previous examples, you created a permanent library named MYASLIB and a temporary library named MYLIB2. They both refer to the folder location C:\SASDATA. Suppose there is a SAS data set in that folder named SOMEDATA. SAS7BDAT. To access that data set in SAS in a PROC statement, you can use either the Full path or either of the library prefixes. For example, the following three different statements that all access the same data set:

```
PROC MEANS DATA='C:\SASDATA\SOMEDATA'; RUN;
Or
PROC MEANS DATA=MYASLIB.SOMEDATA; RUN;
Or
PROC MEANS DATA=MYLIB2.SOMEDATA; RUN;
```

HANDS-ON EXAMPLE
In this example, you will read data from an existing SAS data set.
1. Open the program file READFILE.SAS. The entire program consists of a single line of code:

PROC MEANS DATA=':c:\sasdata\somedata'; RUN;

Note that the DATA=set includes the information

DATA='c:\sasdata\somedata';
2. Run this program and observe the output, a table of descriptive statistics created by the PROC MEANS statement. The data used in that procedure is from the SAS data file named SOMEDATA. SAS7BDAT (This method of reading SAS data sets works only in the Windows environment).
3. Change the statement in PROC MEANS DATA=MYASLIB.SOMEDATA. Note that you will no longer put the data set designation name in quotes. Re-run the program to verify that the new data set designation produces the same results as those created in Step 2.
4. Change the file reference to DATA= MYLIB2.SOMEDATA and re-run the program. Again you should get the same results (as long as you do not exit SAS and lose the MYLIB2 library nickname).