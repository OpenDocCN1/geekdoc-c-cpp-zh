# 242 Learning SAS by Example: A Programmermer's Guide, Second Edition

Figure 15.6: Output from Program 15.6

| Clinic | Average Heart Rate | Average Weight |
| HMC | 69 | 218 |
| Mayo Clinic | 67 | 170 |

The figures in the report show the average heart rate and average weight for each of the two clinics.

# 15.6 Demonstrating the FLOW Option of PROC REPORT

One of the nice features of PROC REPORT is its ability to wrap lines of text within a column when you have long values. To demonstrate this feature, here is a report that includes a variable called Comment that is 50 characters long. Because a value would take up most of the width of a page, you can use the FLOW option to improve the appearance of your report.

> Note: This option affects only the listing output. It has no effect on other ODS destinations as HTML or PDF. For other ODS destinations, long text fields will wrap automatically.

Here is the code to accomplish this:

Program 15.7: Demonstrating the FLOW Option with PROC REPORT

```
title "Demonstrating the FLOW Option;
proc report data=Medical headline
split="is=74;
column Patno VisitDate DX HR Weight Comment
def Patno /"Patient Name" width=7;
def VisitDate /width=9 format=date9;
def DX /"DX Code" width=4;
def HR /"Heart Date" width=6;
def Weight /width=6;
def Comment /width=30 flow;
run;
```

This program has several new features. First, the FLOW option was added to the DEFINE statement for the Comment variable. This wraps the comment defined within the column width of 30. The SPLIT option is required to tell the program that you want to split the comments between words (blanks). Without this option, PROC REPORT would use other characters like the slashes as possible line breaks. The LS= option allows you to select a line size.

The option RIGHT, used for the DX variable, right-aligns the DX values. The default alignment for character variables is LEFT. Alignment options are LEFT, RIGHT, CENTER. Here is the report: