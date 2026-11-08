| 1.3.4b Varying Length Records |  |  |  |
|---|---|---|---|
| Using TRUNCOVER |  |  |  |
| Obs | sex | Fname | lname |
| 1 | F | Linda | Maxwell |
| 2 | M | Ronald | Mercy |
| 3 | F | Rachel |  |
| 4 | M | Mat | Most |
| 5 | M | David | Nabers |
| 6 | F | Terrie | Nolan |
| 7 | F | June | Olsen |
| 8 | M | Merv | Panda |
| 9 | M | Mathew | Perez |
| 10 | M | Robert | Pope |
| 11 | M | Arthur | Reilly |
| 12 | M | Adam | Robertson |

Generally the TRUNCOVER option is easier to apply than the $VARYING informat, and there is no penalty for including a TRUNCOVER option on the INFILE statement even when you think that you will not need it.

By including the TRUNCOVER option on the INFILE statement, we have now correctly read the data without skipping a record, while correctly assigning a missing value to Rachel’s last name.

# Using the $VARYING Informat

The $VARYING informat was created to be used with variable-length records. This informat allows us to determine the record length and then use that length for calculating how many columns to read. As a general rule, you should first attempt to use the more flexible and easier to apply TRUNCOVER option on the INFILE statement, before attempting to use the $VARYING informat.

Unlike other informats $VARYING utilizes a secondary value to determine how many bytes to read. Very often this value depends on the overall length of the record. The record length can be retrieved with the LENGTH= option ❶ and a portion of the overall record length is used to read the field with a varying width.

The classic use of the $VARYING informat is shown in the following example, where the last field on the record has an inconsistent width from record to record. This is also the type of data

read for which the TRUNCOVER option was designed.

```
title2 'Using the $VARYING Informat';
data patients(keep=sex fname lname);
    infile patlist lrecl=10; ❶
    input @; ❷
    namewidth + len=17; ❸
    input @2 sex $1.
          @8 fname $10.
          @18 lname $varying15. namewidth ❹;
run;
```

+   ❶ The LENGTH= option on the INFILE statement specifies a temporary variable (LEN) which holds the length of the current record.

+   ❷ An INPUT statement with just a trailing @ is used to load the record into the input buffer. Here the length is determined and loaded into the variable LEN. The trailing @ holds the record so that it can be read again.

| 1.3.4c Varying Length Records |  |  |  |
|---|---|---|---|
| Using the $VARYING Informat |  |  |  |
| Obs | sex | Fname | lname |
| 1 | F | Linda | Maxwell |
| 2 | M | Ronald | Mercy |
| 3 | F | M | Mat ❺ |
| 4 | M | David | Nabers |
| 5 | F | Terrie | Nolan |
| 6 | F | June | Olsen |
| 7 | M | Merv | Panda |
| 8 | M | Mathew | Perez |
| 9 | M | Robert | Pope |
| 10 | M | Arthur | Reilly |
| 11 | M | Adam | Robertson |

+   ❸ The width of the last name is calculated (total length less the number of characters to the left of the name). The variable NAMEWIDTH holds this value for use by the $VARYING informat.