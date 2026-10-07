# 21.3 Reading Short Data Lines

Take a look at the following file Short.txt:

```
1         2         3
123456789012345678901234567890

001Josua Tyson     100 97 95
002Helen Ames      87 85
003Shouen Lu       98 98 92
004Pam Mann       100100 99
```

These lines of data represent a subject number (Columns 1–3), a name (Columns 4–19), and three scores (20–22, 23–25, and 26–28). It's important to note that Line 2 contains a short record and it is not padded with blanks (that is, the person who entered the data pressed the carriage return after the 85). Let's see what happens if you read this file with either or formatted input on a Windows or UNIX platform (flat files like this are padded in mainframe frames). Here is a program to do that:

# Program 21.3: Reading a Data File with Short Records

```
data Short;
infile 'C:\books\learning\Short.txt';
input Subject $ 1-3
       Name      $ 4-19
       Quiz1         20-22
       Quiz2         23-25
       Quiz3         26-28;

run;
```

Now look at a listing from PROC PRINT:

Figure 21.4: Listing of Data Set Short

# Listing of Data Set Short

| Subject | Name | Quiz1 | Quiz2 | Quiz3 |
|---|---|---|---|--|
| 001 | Josua Tyson | 100 | 97 | 95 |
| 002 | Helen Ames | 87 | 85 | 3 |
| 004 | Pam Mann | 100 | 100 | 99 |

Again, you see what went wrong—very wrong. Four records were read, but the data set only has three observations. Worse yet, Subject 002 has a Quiz3 score of 3.

Even though the INPUT statement instructed SAS to read a value of Quiz3 in Columns 26–28, it went to the next line when it was unable to read columns in the second record. Then it read the subject number in Line 3 as the quiz score. SAS then moved the pointer to the next record and read data for subject 4 correctly. One way to prevent this from happening is to use the PAD option in the INFILE statement. This option pads each of the input records with blanks, out to the end of the logical record. On Windows and UNIX platforms, the default logical record (abbreviated LRECL) is 32,767. You will see later how to change this length.