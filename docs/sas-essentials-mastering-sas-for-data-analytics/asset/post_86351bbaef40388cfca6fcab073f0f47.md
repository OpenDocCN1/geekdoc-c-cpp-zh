
# 40 CHAPTER 2: GETTING DATA INTO SAS®

INPUT ID $ SEX $ AGE WT $ SBP DBP BLDCH #3 OBS1 OBS2 OBS3;

or in another order:

INPUT #2 SBP DBP BLDCH #1 ID $ SEX $ AGE WT #3 OBS1 OBS2 OBS3

An advantage of this technique is that you can read the data lines in SAS in any order, specified by the #n. Note that all of these methods require that there be the same number of records for each subject. If there are differing numbers of records per subject, SAS can still read in the data, but that technique is beyond the scope of this book.

An example of a program (DMULTINE.SAS) to read multiple-line data into SAS as the following:

```sas
DATA MYDATA;
INPUT ID $ SEX $ AGE WT/ SBP DBP BLDCHL/ OBS1 OBS2 OBS3;
DATALINES;
10011 M 15 115
120 80 254
15 65 102
10012 F 25 180
130 70 240
34 120 132
10013 M 89 170
140 100 279
19 89 111
;
PROC PRINT DATA=MYDATA;
RUN;
```

In this case, we use the / indicator technique to read the three data lines per person. The output for this program is given in Table 2.11. Note that even though there are nine lines of data, the DATA steps reads in the data as three records.

# TABLE 2.11 Multiline Entry

| Obs | ID | AGE WT | SBP | DBP | BLDCHL | OBS1 | OBS2 | OBS3 |
|---|---|---|---|---|---|---|---|---|
| 1 | 10011 M | 15 115 | 120 | 80 | 254 | 15 | 65 | 102 |
| 2 | 10012 F | 25 180 | 130 | 240 | 34 | 120 | 132 |
| 3 | 10013 M | 89 170 | 140 | 100 | 279 | 19 | 89 | 111 |

# HANDS-ON EXAMPLE

1. Open the program file DMULTINE.SAS. Change the INPUT line to read in data using each of the three different INPUT statements technique.
2. Change in the INPUT line to read in data using line number technique, but read in first first line #1, then line #3, and finally line two #2. Submit the code and observe the output.

# GOING DEEPER: MORE TECHNIQUES FOR ENTERING DATA

A number of examples given used INPUT column pointer control as @5 to move the pointer to column 5. Table 2.12 lists commonly used INPUT pointer controls and arguments.

# TABLE 2.12 INPUT Pointer Control Commands

| INPUT Pointer Control or Arguments | Meaning |
|---|---|
| @N | Moves the pointer to the Nth column (N can be a numeric variable or a numeric expression) |
| +N | Moves the pointer ahead of N columns (N can be a numeric variable or a numeric expression) |
| @ | Holds the exact of the next INPUT item and allows you to specify some conditional input criteria |
| @@ | Must be the last item in an INPUT line, Reads data for multiple records within a single line of data |
| #N | Moves the pointer to record N (N can be a numeric variable or a numeric expression) |
| / | Advances to the next record |

# TABLE 2.13 INFILE Options

| INFILE Option | Meaning |
|---|---|
| DLM='char' | Allows you to define a delimiter to something other than a blank. For example, if data are separated by commas, include the option DLM=',' in the INFILE statement |
| DLSTR='string' | Allows you to define a string as a delimiter in the INFILE statement. For example, DLSTR='~/~' Instructs SAS to recognize two consecutive delimiters as a missing value. For example, the information M,15,,115 would be read as M, 15, Missing, 115. Moreover, this option uses the delimiter within quoted strings. For example, the data value "Robert Downey," would be read properly, meaning that SAS would interpret the comma in the name as signaling a new value |
| MISOVER | Indicates to SAS that, when reading a data line, if it encounters the end of a data line without finding enough data to match all of the variables in the statement, it should continue reading data from the next input line |
| TRUNCOVER | Forces the INPUT statement to stop reading data when it gets to the end of a short line |
| PAD and LRECL=n | This option pads short lines with extra blanks. It is used in conjunction with the LRECL= option that specifies the length of the input line |

# CHAPTER 2: GETTING DATA INTO SAS®

# TABLE 2.13 (Continued)

| INFILE Option | Meaning |
|---|---|
| FIRSTSTOB=n | Tells SAS on what line you want it to start reading your raw data file. This is handy if your data file contains one or more header lines or if you want to skip the first part of the data lines | Indicates which line in your raw data file should be treated as the last record to be read by SAS |
| OBS=n | These commands are not discussed but may also be used to tell SAS how to read unusual input lines. See SAS documentation for more information |
| FLOWOVER, STOPOVER, and SCANOVER | |

# 2.6.2 Using Advanced INFILE Statement Options

When you acquire a set from another source that you intend to read into SAS using an INFILE statement, the data set might not be in the format you need. To help you read external data, SAS includes a number of options you can use to customize your INFILE statement. Some of these INFILE options are listed in Table 2.13.

The purpose of the options in Table 2.12 is to give you more flexibility in reading data files into SAS using the INFILE statement. The following examples illustrate some of these.

# HANDS-ON EXAMPLE

1. Open the program file FILE2.SAS.

```sas
DATA MYDATA;
INFILE 'C:\SASDATA\EXAMPLE.CSV' DLM=',' FIRSTSTOB=2 OBS=11;
INPUT GROUP $ AGE TIME1 TIME2 Time3 Time4 SOCIO;
PROC PRINT DATA=MYDATA;
RUN;
```

This code is used to import the first 10 lines of the raw data (comma separated) The first few lines of this data file are as follows:

```
GROUP,AGE,TIME1,TIME2,TIME3,TIME4,SOCIO
A,12,22.3,25.3,28.2,30.6,5
A,11,22.8,27.5,33.3,35.8,5
B,12,22.8,30.0,32.8,31.0,4
A,12,18.5,26.0,29.0,27.9,5
B,9,19.5,25.0,25.3,26.6,5
B,11,23.5,28.8,34.2,35.6,5
```

The first line of this data file is a header. The DLM=',' tells SAS the data are comma separated.

# GOING DEEPER: MORE TECHNIQUES FOR ENTERING DATA

2. Submit the code and observe the output. Note that even though there are nine lines of data, the DATA steps reads in the data as three records.

# TABLE 2.14 Multiline Entry

| Obs | GROUP | AGE | TIME1 | TIME2 | TIME3 | TIME4 | SOCIO |
|---|---|---|---|---|---|---|---|
| 1 | A | 12 | 22.3 | 25.3 | 28.2 | 30.6 | 5 |
| 2 | A | 11 | 22.8 | 27.5 | 33.3 | 35.8 | 5 |
| 3 | B | 12 | 22.8 | 30.0 | 32.8 | 31.0 | 4 |
| 4 | A | 12 | 18.5 | 26.0 | 29.0 | 27.9 | 5 |
| 5 | B | 9 | 19.5 | 25.0 | 25.3 | 26.6 | 5 |
| 6 | B | 11 | 23.5 | 28.8 | 34.2 | 35.6 | 5 |

3. Change in the INPUT line to read in data using line number technique, but read in first line #1, then line #3, and finally line two #2. Submit the code and observe the output.

4. Suppose you want to skip the first part of the data lines. Use the FIRSTOBS=2 option.

# TABLE 2.11 Multiline Entry

| Obs | ID | AGE WT | SBP | DBP | BLDCHL | OBS1 | OBS2 | OBS3 |
|---|---|---|---|---|---|---|---|---|
| 1 | 10011 M | 15 115 | 120 | 80 | 254 | 15 | 65 | 102 |
| 2 | 10012 F | 25 180 | 130 | 240 | 34 | 120 | 132 |
| 3 | 10013 M | 89 170 | 140 | 100 | 279 | 19 | 89 | 111 |
