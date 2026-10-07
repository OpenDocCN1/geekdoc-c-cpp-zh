# METHODS OF READING DATA INTO SAS 37

# 2.5.6 Using the SAS INFORMAT Statement

There is a SAS statement named INFORMAT that you could use in the freeform data entry case. For example,

```
DATA PEOPLE;
  INFORMAT LASTNAME FIRSTNAME $12. AGE 3. SCORE 4;
  INPUT LASTNAME FIRSTNAME AGE SCORE;
DATALINES;
Lincoln    35 3.45
Ryan      Lacy      33 5.5
;
PROC PRINT DATA=PEOPLE;
RUN;
```

In this case, the INFORMAT statement can specify that a freeform input text value is longer than the default eight characters. You still cannot have blanks in the string variables (LASTNAME and FIRSTNAME). However, we will not use the INFORMAT statement in any future examples. We will prefer instead to specify informats in the INPUT statement when needed. (The code for this example is found within the program DINFORMAT3.SAS).

# 2.5.7 Reading External Data INFILE

In the examples so far, the DATALINES statement has been used to tell SAS that data records follow in the same file as your SAS code. If your data are already stored in certain types of computer file, you can instruct SAS to read the records from the file using the INFILE statement.

For this example, we use data, where data sets are available by download from a number of sources. Data are often in a text (raw data) file where the values are in fixed columns. (Typical file extensions for such files are DAT, TXT, or ASC.) In these situations, you can use either the column or formatted input technique to read the data into SAS. In practice, because these data sets may contain hundreds or thousands of rows (making it difficult to embed them into your SAS code), it is useful to read the data from these files using the INFILE technique.

The INFILE statement is used to identify the filename of an ASCII (text) file. When you use the INFILE statement, you do not have to use a DATALINES statement. The INFILE statement takes the place of the DATALINES statement. The general form for the INFILE statement is as follows:

INFILE specification options;

For example, the file EXAMPLE.TXT contains 50 lines of data in ASCII format. You can look at this data file using Notepad or any text editor or word processor.) The first few lines are as follows:

```
101 A 12 22.3 25.3 28.2 30.6 5 0
102 A 12 22.8 27.5 33.3 35.8 5 0
104 B 12 22.8 30.0 32.8 31.0 4 0
110 A 12 18.5 26.0 27.9 29.7 5 1
```