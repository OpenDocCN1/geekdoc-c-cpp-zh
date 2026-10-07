# CHAPTER 19: CREATING CUSTOM REPORTS

(continued)

+   2. To see what the SUPPRESS option does in the BREAK statement, delete SUPRESS and rerun the code. Observe that without SUPPRESS, the name of the BRAND is repeated over the subtotal line.

# 19.2.1 Writing Reports in a Data Statement

Another way to create reports from a SAS data set is to use the PUT statement within a DATA step. Typically, this is done using the following technique:

+   1. Specify the name _NULL_ as the data name in a DATA step to be able to use the features of the DATA step without creating a SAS data output. (Because you are interested in creating a report rather than creating a SAS data set.)
2. Define a destination (output file) for the report using a FILE statement. The statement FILE prints the report output to the SAS Results Viewer. When you use FILE "file-specification," the report output is sent to the specified text file location.
3. Use PUT statements in the DATA step to create lines of output for the report.

# HANDS-ON EXAMPLE

The heart of a DATA statement report is the PUT statement. By default, a PUT statement displays information for each record in a data set in the SAS Log. For example, open the program file APUT_REPORT1.SAS

```
DATA _NULL_; SET MYSASLIB.SOMEDATA;
    PUT AGE;
RUN;
```

This simple program lists the values of AGE for each record in the specified SAS data set. In this case, when no FILE option is used, the report output is sent to the SAS Log.

+   1. Run this program and observe the output in the log. Note that there are 50 lines of ages listed there.
2. You typically want to display the results of your report in the Results Viewer or capture the results in a File. To display the output in the Results Viewer, include the statement FILE PRINT; in the code:

```
DATA _NULL_; SET MYSASLIB.SOMEDATA;
    FILE PRINT;
    PUT AGE;
RUN;
```

Rerun the code and observe the output. This time the values of AGE are displayed in the SAS Results Viewer.