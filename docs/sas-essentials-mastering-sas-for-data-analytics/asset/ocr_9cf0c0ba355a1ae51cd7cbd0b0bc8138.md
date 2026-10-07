# CHAPTER 3: READING, WRITING, AND IMPORTING DATA

SAS also creates another piece of memory called a Program Data Vector (PDV), as shown in the following:

| _N | _ERROR_ | ID | AGE | TEMPC | TEMPF |
|---|---|---|---|---|--|
| 1 | 0 | | | | |

The PDV contains the names of the variables specified in the INPUT statement, plus two temporary variables, _N and _ERROR_. The variable _N is the number of the data line being entered (set to 1 in this case for the first line) to indicate if an error reading data has been encountered. It is initially set at 0 (which means no error detected).

The INPUT specification tells SAS how to move the characters in the input buffer into PDV. In this case, the freedata entry tells SAS to read characters in the buffer starting with the left and going to the right, until it sees a blank. When a blank is encountered, SAS moves data to that point into the first variable specified in the PDV. In this case, it moves the "0001" into the memory space in the PDV allocated for ID. When all the information in the first line has been read, the PDV looks like the following:

| _N | _ERROR_ | ID | AGE | TEMPC | TEMPF |
|---|---|---|---|---|--|
| 1 | | 0001 | 24 | 37.3 | |

Notice that the value of each read variable from the data line are now in the PDV. However, the TEMPF variable is set at missing. SAS continues to read the code and sees that the DATA step also includes a calculation

TEMPF=TEMPC*(9/5) +32;

Using the data already in the PDV for TEMPC (which is 37.3), it uses information to calculate TEMPF. Once the calculation is performed, that value is also placed in the PDV, and it looks like the following:

| _N | _ERROR_ | ID | AGE | TEMPC | TEMPF |
|---|---|---|---|---|--|
| 1 | 0 | 0001 | 24 | 37.3 | 99.14 |

Once all of the value for a line are read, all of the calculations specified in the DATA step have been performed, and there are no errors detected, SAS outputs the PDV to the data set. In this case,

| ID | AGE | TEMPC | TEMPF |
|---|---|---|--|
| 0001 | 24 | 37.3 | 99.14 |

At this stage, only the data values appear in the data set, and the two temporary variables, _N_ and _ERROR_, are not included. Therefore:

+   The _N_ and _ERROR_ variables are available from one iteration of the data set to the next.