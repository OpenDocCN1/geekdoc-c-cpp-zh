
330 Learning SAS by Example: A Programmer's Guide, Second Edition

### Program 19.4: Using an ODS SELECT Statement to Restrict PROC UNIVARIATE Output

```sas
ods select extremeobs;

title "Extreme Values of RBC";
proc Univariate data=Learn.Blood;
  id Subject;
  var RBC;
run;
```

When you run this program, the only output is as follows:

### Program 19.5: Output from Program 19.4
Extreme Values of RBC

| Variable: RBC | |
|---|---|
| Extreme Observations | |
| Value Subject Obs | Value Subject Obs | | |
|---|---|---|---|---|---|
| 1.71 | 525 | 525 | 7.99 | 565 | 565 |
| 2.33 | 440 | 440 | 8.12 | 984 | 984 |
| 2.55 | 113 | 113 | 8.26 | 288 | 288 |
| 2.92 | 293 | 293 | 8.43 | 726 | 726 |
| 3.13 | 635 | 635 | 8.75 | 135 | 135 |

This seems simple enough, but how do you determine the name of the output objects (in this case, EXTREMEOBS?) One way is to run the procedure sandwiched between ODS TRACE ON and ODS TRACE OFF statements, like this:

### Program 19.5: Using the ODS TRACE Statement to Identify Output Objects

```sas
ods trace on;

title "Extreme Values of RBC";
proc Univariate data=Learn.Blood;
  id Subject;
  var RBC;
run;
```

# Chapter 19: Introducing the Output Delivery System 331

When you run the procedure, the names of the output objects appear in the SAS log as shown next (only selected portions are shown):

Figure 19.6: SAS Log Showing ODS Output Objects

![](img/e9e15d853989558188e1c83b0ae655b0_339_0.png)

![](img/e9e15d853989558188e1c83b0ae655b0_339_1.png)

One way to figure out the correspondence between output objects and portions of the output is to look through the output listing and the list of objects in the SAS log and make an educated guess. If you use TRACE ON/LISTING, it's usually quite obvious which object goes with each portion of output. The information on each output object is placed in the Output window, along with the listing. This is yet another way to know which output names go with each portion of the output.

For a more systematic approach, look at the Results window in the SAS windowing environment and notice the labels in the list. For example, the following display results from running Program 19.5:

332 Learning SAS by Example: A Programmer's Guide, Second Edition

Figure 19.7: The Results Window in the SAS Windowing Environment

![](img/e9e15d853989558188e1c83b0ae655b0_340_0.png)

If you then right-click on any of these labels, you will see more information, including the names of the output objects.

Below is a screen shot taken after right-clicking on Extreme Observation and selecting Preferences:

Figure 19.8: Properties of Extreme Obs*

| Attribute | Value |
|---|---|
| Type | Folder |
| Name | ExtremeObs |
| Description | Extreme Observations |
| Path | Univariate1.RBC#1.ExtremeObs#1 |
| Created | 11/26/2017 1:58 PM |

You see here that the name of this output object is ExtremeObs.

As an alternative to using the name in the ODS SELECT statement, you can also select objects by the labels instead of the names. For example, you can use the following:

```sas
ods select "Extreme Observations";
```

in place of this statement:

```sas
ods select ExtremeObs;
```

If you use the label, place it in single or double quotes.

You can include a list of output objects following the ODS SELECT statement (separated by spaces). If you want to select most of the output objects from a particular procedure, it might be easier to use an ODS EXCLUDE statement to exclude the ones you don't want.

Chapter 19: Introducing the Output Delivery System 333

Remember that ODS SELECT or EXCLUDE statements only operate on the procedure that follows. If you want the selections to remain for other procedures, you can use the PERSIST option, like this:

```sas
ods select ExtremeObs(persist);
```

## 19.7 Sending Output to a SAS Data Set

One of the possible ODS output destinations is a SAS data set. This feature of ODS allows you to capture just about any value computed by a procedure and use it in further calculations or a customized report. Prior to the development of ODS, PROC PRINTTO was used to capture SAS output from a procedure and use it as input to DATA step.

Many procedures already provide you with the ability to capture information in a SAS data set with an OUT option, usually in OUTPUT statement. Using ODS to capture output is more general—it lets you capture any value you want. Suppose you want to run a statistical procedure called t-test. This statistical test produces a t-value and a p-value (the significance of the result). These values are not available in an output data set from PROC TTEST, but you can use ODS to place these values into a SAS data set. If you are not familiar with PROC TTEST, it should be clear how to capture procedure output into SAS data sets.

### 19.6: Using ODS to Send Output to a SAS Data Set

```sas
ods listing close;
ods output tests=T_Test_Data;
proc test data=Learn.Blood;
class Gender;
var RBC Chol;
run;
ods listing;
title "Listing of T_Test_Data";
proc print data=T_Test_Data;
run;
```

The first program closes the listing so that output is not sent to Output window. Note: You cannot use PRINT option on procedures that allow it. If you do, the values will not be available to send to alternate ODS destinations.

Next, the ODS OUTPUT statement is used to send the output to a data set. The keyword to the left of the equal sign is the name of the data object produced by PROCTEST. Following the equal sign is the name of the data set you want to create. You then run the procedure in the usual way. The first time you do this, you should run PROC PRINT to determine the structure of the output data set.

334 Learning SAS by Example: A Programmer's Guide, Second Edition

Figure 19.9: Output from Program 19.6

Listing of T_Test_Data
| Obs | Variable | Method | Variance | tValue | DF | Prob |
|---|---|---|---|---|---|
| 1 | RBC | Pooled | Equal | 0.41 | 914 | 0.6797 |
| 2 | RBC | Satterwaite | Unequal | 0.41 | 874 | 0.6796 |
| 3 | WBC | Pooled | Equal | 1.87 | 906 | 0.0624 |
| 4 | WBC | Satterwaite | Unequal | 1.87 | 864 | 0.0622 |
| 5 | Chol | Pooled | Equal | 0.53 | 793 | 0.5953 |
| 6 | Chol | Satterwaite | Unequal | 0.54 | 771 | 0.5918 |

The structure of these output data sets can be complicated. In this instance, you know PROCTEST produces two t-values, under the assumption of equal variance and the other under the assumption of unequal variance. What can you do with this data?

Sending computed values to a data set enables you to perform additional analyses on them. Also, you might want to see the output from a SAS procedure differently from the way SAS presents it. As an example, suppose you want to see a simple report showing the t- and p-values from your t-test, rather than the complicated output from PROC TEST. Once you know the structure of the output data set created by ODS, you can proceed like this:

### Program 19.7: Using an Output Data Set to Create a Simplified Report

```sas
title "T-Test Results - Using Equal Variance Method";
proc report data=t_Test_Data;
  where Variance = "Equal";
  columns Variable tValue ProbT / width=8;
  define tValue / display "T-Value" width=7 format=7.2;
  define ProbT / display "P-Value" width=7 format=7.5;
run;
```

Inspection of data set T_Test_Data shows that there are separate observations for the two variance assumptions. You can use a WHERE statement to select statistics using the equal variance assumption. The result of the PROC REPORT is a simple listing showing the variable name along with the t- and p-values. Here it is:

Chapter 19: Introducing the Output Delivery System 335

Figure 19.10: Output from Program 19.7

# T-Test Results – Using Equal Variance Method

| Variable | T-Value | P-Value |
|---|---|---|
| RBC | 0.41 | 0.67972 |
| WBC | 1.87 | 0.06237 |
| Chol | 0.53 | 0.59529 |

This chapter has just touched the surface of the capabilities of the Output Delivery System. However, by routing your output to destinations such as HTML or PDF files or using ODS SELECT statements, you can create output for web pages or company reports that look much more impressive than a standard listing report.

## 19.8 Problems

Solutions to odd-numbered problems are located at the back of the book. Solutions to all problems are available to professors. If you are a professor, visit the book's companion website at support.sas.com/cody for information about how to obtain the solutions to all problems.

1. Run the following program, sending the output to an HTML file. See Chapter 16, Problem 2, for the note about creating formats for this data set.

```sas
ods html file="myoutput.html";
title "Sending Output to an HTML File";
proc print data=Learn.College(obs=8) noobs;
run;
proc means data=learn.college n mean maxdec=2;
var GPA ClassRank;
run;
```

2. Run the same two procedures shown in Problem 1, except create a contents file, a body file, and a frame file.

3. Run the same two procedures as shown in Problem 1, use the JOURNAL (or FANCYPRINTER) style instead of the default style.

4. Send the results of a PROC PRINT on the data set Survey to an RTF file.

5. Run PROC ON/TRACE OFF statements to display the names of the output objects created by this procedure. Once you have done this, run PROC UNIVARIATE again, selecting only the output object that shows Quantiles.

6. Run the same PROC UNIVARIATE as in Problem 5. Issue two ODS statements: one to select the MOMENTS output object and the other to send this output to a SAS data set. Run PROC PRINT to see a listing of this data set.
