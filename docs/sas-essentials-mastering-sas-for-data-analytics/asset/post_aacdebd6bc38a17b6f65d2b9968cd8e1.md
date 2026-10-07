
# 208 CHAPTER 8: CONTROLLING OUTPUT USING ODS

(continued)

```
VAR AGE GENDER INJTYPE DISSTATUS;
VAR ISS/STYLE=[FOREGROUND=FMTSEVERE.];
LABEL INC_KEY='Subject ID ' 
AGE='Age in 2014 ' 
GENDER='Gender ' 
ISS_='Injury Severity Score ' 
INJTYPE='Injury Type ' 
DISSTATUS='Discharge Status'
```

RUN;
Note the on-screen color coding in the ISS column.

## TABLE 8.8 Traffic Light Example
Trauma Data Report

| Subject ID | Age in 2014 | Gender | Injury Severity Score | Injury Type | Discharge Status |
|---|---|---|---|---|---|
| 468979 | 9.1 | Female | | Blunt | Alive |
| 468942 | 17.7 | Female | | 20 | Blunt | Alive |
| 468961 | 16.6 | Female | | 5 | Blunt | Alive |
| 468971 | 6.5 | Female | | 5 | Blunt | Alive |
| 469030 | 6.7 | Male | | -81 | | Alive |
| 469055 | 10.8 | Male | | 1 | | Alive |
| 487580 | 17.7 | Male | | 25 | Penetrating | Alive |
| 597075 | 14.6 | Male | | 9 | Blunt | Alive |
| 603091 | 5.1 | Female | | 17 | Blunt | Alive |
| 603104 | 8.3 | Male | | 5 | Blunt | Alive |

- 2. Create a second format for AGE where <13 is displayed as RED and 13 or older is displayed as black.
3. Create the following format:

```
VALUE FMTISS
LOW-<0="MISSING"
0-<10="OKAY"
10-<20="CONCERN"
20-HIGH="SEVERE";
```

Apply it to the ISS variable. Submit the code and observe that the ISS column is now displayed as different color words for each category of injury.

## 4. Add the following attributes by changing the VAR statement for ISS to

Run this new code and observe how the additional attributes change the output. Put your cursor over one of the cells and see a pop-up that says "Severity Rating." This was set up with the FLYOVER attribute. Other ODS style attributes, colors, and fonts are listed in Appendix A.

## 8.6 EXTENDED ODS FEATURES

This chapter has introduced a number of features available in SAS ODS output. However, there are many features not covered here. For example, every ODS table output by a SAS procedure uses a template to control how it is created. Using PROC TEMPLATE, you can modify these templates to customize the content and look of each output table.

You can store the contents of any ODS report in order to modify and replay them using PROC DOCUMENT. These tasks are beyond the scope of this book, and we refer you to the SAS documentation if you want to learn more about these topics.

## 8.7 SUMMARY

The ODS provides a number of ways to manipulate output from SAS procedures. Many examples in the book have used ODS results from procedures into HTML and other formats. This chapter introduced other ways to use ODS, including additional options for outputting results from SAS procedures, outputting SAS data sets, and using ODS to enhance graphic output.

## EXERCISES

## 8.1 Using ODS PDF.

Using the FIRST.SAS program file, include output to the ODS PDF format using the STATISTICAL style.

## 8.2 Using ODS TRACE.

Open the program file EX_8.2.SAS. Note the TRACE ON and TRACE OFF commands. Run this program to discover the names of the output tables (in the Log window). They are as follows:

- a. Statistics
- b. Conflicts
- c.
- d.
- e.
- f.

Use this information in an ODS SELECT statement to limit output of the procedure to the tables for statistics and t-tests only.

## 8.3 Use ODS.

Open the program file EX_8.3.SAS

```
DATA TABLE;
INPUT EXPOSURE DISEASE COUNT;
DATALINES;
0 0 24
0 1 8
1 0 9
1 1 19;
PROC FREQ DATA=TABLE; WEIGHT COUNT;
TABLES EXPOSURE*DISEASE/CHISQ;
RUN;
```

This file contains the code to analyze the 2 × 2 information in this table.

| | DISEASE | | |
| --- | YES | NO |
| EXPOSED | YES | 24 | 8 |
| | NO | 9 | 19 |

The output of this program consists of three tables: a cross-tabulation, chi-square results, and Fisher's Exact test results. Using TRACE and SELECT, modify this code so that it will display only the cross-tabulation and the Fisher's Exact test (and not display the chi-square table).

## 8.4 Use ODS to extract statistics.

Using information from Exercise 8.3, write a program that will save the contents of the Fisher's Test to a SAS data set.

```
ODS OUTPUT;
```

This code will save the contents of the Fisher's Test to a SAS data set.

## 8.5 Use ODS to select statistics.

Using information from Exercise 8.3, write a program that will save the contents of the Fisher's Test to a SAS data set.

```
ODS OUTPUT;
```

This code will save the contents of the Fisher's Test to a SAS data set.
