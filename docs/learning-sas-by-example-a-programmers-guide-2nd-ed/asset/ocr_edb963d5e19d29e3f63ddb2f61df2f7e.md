# Chapter 6: Reading and Writing Data from an Excel Spreadsheet 79

Figure 6.13: Output from Program 6.3

| Variable | Label | Mean |
|---|---|--|
| Wage | Wage | 2568.40 |
| Hours_Worked | Hours Worked | 37.2000000 |

Once you have created the appropriate LIBNAME statement, you can treat your spreadsheets as if they were SAS data sets.

# 6.5 Using the SAS Output Delivery System to Convert a SAS Data Set to an Excel Spreadsheet

You can use the Output Delivery System (ODS) to create CSV files that Excel can open directly. For more information on ODS, refer to Chapter 19.

As an example, you want to send the contents of the permanent SAS data set Survey to Excel. Program 6.4 creates a CSV file from the SAS data set:

# Program 6.4: Using ODS to Convert a SAS Data Set into a CSV File (To Be Read by Excel)

```
libname Learn 'C:\books\learning\';

ods csv file='C:\books\learning\ODS_Example.csv'

proc print data=Learn.Survey noobs;
run;

ods close;
```

The ODS CLOSE statement removes the CSV file as an output destination. Notice that the NOOBS option of PROC PRINT removes the OBS from the output. It is important to close the file with an ODS CLOSE statement following the PROC PRINT. Here is a listing of the file with C:\books\learning\ODS_Example.csv:

"ID","Gender","Age","Salary","Ques1","Ques2","Ques3","Ques4","Ques5"
001,"M",23,28800,1,2,1,2,3
002,"F",55,76123,4,5,2,1,1
003,"M",38,36500,2,2,2,1,1
004,"F",67,128000,5,3,2,2,4
005,"M",22,23060,3,3,4,2
006,"M",63,90000,2,3,5,4,3
007,"F",45,76100,5,3,4,3,3