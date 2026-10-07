
# TABLE B.6 (Continued)

| Function | Description |
| --- | --- |
| INDEX (text, texttofind) | Searches for specified texttofind string and returns a number where the text begins, or 0 |
| LEFT (text) | Left-aligns a character string |
| LENGTH (text) | Returns the length of a text string |
| LOWCASE (text) | Converts all to lowercase |
| QUOTE (text) | Adds double quotation marks to text |
| REPEAT (text, n) | Repeats text n times. For example, R=repeat("ABC", 3); Results in R="ABCABC" |
| REVERSE (argument) | Reverses a text expression |
| RIGHT (argument) | Right-aligns a text |
| SCAN (text, n,<delimiters>) | Returns the nth word from a text expression. For example, FIRST-SCAN("JOHN SMITH", 1, ''); returns JOHN and LAST-SCAN("JOHN SMITH", 2, ' '); returns SMITH |
| SOUNDEX (text) | Turns text into a sounds-like argument for example, SOUNDEX("ALLEN")=SOUNDEX("ALAN") matches and SOUNDEX("ALLEN")=SOUNDEX("MELON") does not |
| SUBSTR (text, start,<n>) | Searches and replaces text. For example, VAR=SUBSTR("LINCOLN", 3, 2) returns VAR="NC" and SUBSTR("LINCOLN", 3, 2)="XX" returns XX |
| TRANSLATE (text, to, from) | Replaces characters with specified new characters. For example, TRANSLATE('LINCOLN','X','C') returns LINCOXN |
| TRWRD (source, target, replacement) | Replaces or removes all occurrences of a word in a text string. For example, TRANWRD('SPECIAL WED MEAL', 'WED', 'MON') returns 'SPECIAL MON MEAL' |
| TRIM (text) | Removes blanks from the text. (Returns a null if the expression is missing) |
| TRIMN (text) | Removes trailing blanks from the text. Returns a null if the expression is missing. |
| UPCASE (text) | Converts text to uppercase |
| VERIFY (source, excerpt-1,< ...excerpt-n) | Searches for text and returns the position of the first non-matched character in the first argument. VERIFY("12345","54301") returns 2 because the second character doesn't match any character in the second argument |

# HANDS-ON EXAMPLE

- 1. Open the program file FUNC_CHAR.SAS . This program illustrates how you could separate two numeric values from a text value. In this case, systolic and diastolic blood pressures were recorded as a single text value as 120/80. Run this code and observe how the two values are extracted and made into two numeric values SBP and DBP.

```sas
DATA BP;
INPUT BP $10;
I=FIND(BP,"/");
SBP=SUBSTR(BP, 1, I-1); * get number before the /;
DBP=SUBSTR(BP, I+1); *get number after the /;
DROP I;
DATALINES;
120/80
140/90
110/70

PROC PRINT DATA=BP;RUN;
```

- 2. Note the code I=FIND(BP,"/"). What value is the variable I set to on the first record?

- 3. What does the code SUBSTR(BP, 1, I-1) do?

- 4. What does the code SUBSTR(BP, I+1) do?

# HANDS-ON EXAMPLE

- 1. Open the program file FUNC_SCAN.SAS. The goal of this program is to separate a series of names into first and last names. In this case, we don't care about middle initials. Run the program and observe the results in Table B.7.

```sas
DATA NAMES;
FORMAT FIRST LAST NAME $20;
INPUT @1 NAME $30;
FIRST=SCAN(NAME, 1, " ");
LAST=SCAN(NAME, -1);
MAYBE=SCAN(NAME, -2);
IF MAYBE=FIRST THEN MAYBE=""
IF LENGTH(MAYBE)=1 THEN MAYBE=""
LASTNAME=CAT(MAYBE, LAST);
FULLNAME=CAT(FIRST, TRIM(LASTNAME));
DATALINES;
Alfred J. Prufrock
Benjamin Harrison
George H. W. Bush
Vincent Van Gogh
A. C. Elliott;;
RUN;
PROC PRINT DATA=NAMES; RUN;
```

- 2. Put your name in the data segment as first name, initial, and last name. Run the program to see if it separates them correctly.

- 3. Look at the three uses of the SCAN function

```sas
FIRST=SCAN(NAME, 1, " ");
LAST = SCAN(NAME, -1);
MAYBE=SCAN(NAME,-2);
```

What does each do? What do the negative numbers as arguments mean?

- 4. What does the LENGTH function do? How is it used to tell if there is a middle name?

- 5. What does the CAT function do? Replace it with a CAT function when creating FULLNAME, rerun the code. What changes? Finally, note the TRIM function used in the FULLNAME statement. It is needed to trim off any blanks in LASTNAME.

# **TABLE B.7 SCAN, LENGTH, and CAT Functions**

| Obs | FIRST | LAST | MAYBE | LASTNAME | FULLNAME |
|---|---|---|---|---|---|
| 1 | Alfred | J. | Pruf | rock | Alfred J. Prufrock |
| 2 | Benjamin | Harrison | | | Benjamin Harrison |
| 3 | George | H. W. | Bush | | George H. W. Bush |
| 4 | Vincent | Van | Gogh | | Vincent Van Gogh |
| 5 | A. C. | Elliott | | | A. C. Elliott |

# **B.6 TRUNCATION FUNCTIONS**

Truncation Functions are used to extract certain portions of a number such as the smallest integer, largest integer, nearest integer, and so on. are described in Table B.8.

# **B.7 FINANCIAL FUNCTIONS**

Financial functions allow you to perform common calculations on values. There are over 50 such functions available in SAS, too many to describe here. Few of the most commonly used functions are listed in Table B.9.

# **TABLE B.8 Truncation Functions**

| Function | Description |
|---|---|
| CEIL (x) | Returns the smallest integer greater than equal to the argument |
| FLOOR (x) | Returns the largest integer less than equal to the argument |
| FUZZ (x) | Returns the nearest integer if value is within x-12 |
| INT (x) | Returns the decimal portion of the argument |
| ROUND (x, roundoff) | Rounds a value to the nearest roundoff-unit. For example, ROUND(1.2345, .01) returns the value 1.23 |

# **TABLE B.9 Special Use Functions**

| Function | Description |
| --- | --- |
| IRR (period, cash, ...) (amount, rate, number) | Returns the internal rate of return as a percentage When you set the PAYMENT variable to missing. returns this payment for loan. For example, PAYMENT(30000.,.06/12, monthly) is 70.55 |
| NPV (rate, period, cash, ...) | Returns the net present value as a percentage |

# HANDS-ON EXAMPLE

- 1. Open the program file FUNC_MORT.SAS. This program uses the MORT function to calculate the payments for a loan. This example displays payment for different loan, interest, and number of payments. Run the program and observe the results in Table B.10.

```sas
DATA LOAN;
FORMAT VALUE DOLLAR12.;
INTR1-INTR3 4.
NUMBER 4;
INPUT INTR1-INTR3;
ARRAY (3) INTR1-INTR3;
DO I=1 to 3;
PAYMENT(I) = MORT(VALUE,,12);
END;
LABEL MORT="Mortage Payment"
LABEL INTR1="Int. Rate 1"
LABEL INTR2="Int. Rate 2"
LABEL INTR3="Int. Rate 3"
LABEL PAYMENT="Amount of Payment"
LABEL VALUE="Loan Amount"
LABEL NUMBER="Num. Payments";
DATALINES;
100000 .05 .04 .03 360
100000 .05 .04 .03 180
150000 .05 .04 .03 360
150000 .05 .04 .03 180;
RUN;
PROC PRINT DATA=LOAN ; RUN;
```

Add lines to the data for $200,000 loan for a 30- and 15-year mortgage with 0.05, 0.04, and 0.03 interest rates. Run the program and observe the results.

TABLE B.10 Example of MORT

| Obs | Loan Amount | Int. Rate 1 | Int. Rate 2 | Int. Rate 3 | Num. Payments | PAY1 | PAY2 | PAY3 |
|---|---|---|---|---|---|---|---|---|
| 1 | $100,000 | 0.05 | 0.04 | 0.03 | 360 | 536.82 | 477.42 | 421.60 |
| 2 | $100,000 | 0.05 | 0.04 | 0.03 | 180 | 790.79 | 739.69 | 690.58 |
| 3 | $150,000 | 0.05 | 0.04 | 0.03 | 360 | 805.23 | 716.12 | 632.41 |
| 4 | $150,000 | 0.05 | 0.04 | 0.03 | 180 | 1186.19 | 1109.53 | 1035.87 |

# **B.8 SPECIAL USE FUNCTIONS**

The "special use function" is a catch-all phrase referring to other functions that are useful in SAS. They include functions that provide ways to convert variables from one type to another, create macro variables, create lag values, and determine differences in distance using zip codes. These functions are listed in Table B.11.

# TABLE B.11 Special Use Functions

| Function | Description |
|---|---|
| INPUT(string,format) | The INPUT function converts a character variable to numeric |

![](img/6113440fee6085d6edba5f406f541c12_496_0.png)

> For example,
s="1,212"
x=input(s,comma5);
returns x=1212 (a numeric value).
Note: INPUT(string1,char-format) and PUTN(string1,num-format) are similar to INPUT(), but you can assign the format within the code

The PUT function converts variables from character or numeric to character

![](img/6113440fee6085d6edba5f406f541c12_496_1.png)
