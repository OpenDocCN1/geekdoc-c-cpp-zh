
> NOTE: LOST CARD.
> sex=M fname=Adam lname=_ERROR_=1 _N_=6
> NOTE: 12 records were read from the infile PATLIST.
>       The minimum record length was 13.
>       The maximum record length was 26.
> NOTE: SAS went to a new line when INPUT statement reached past the end of a line.

The resulting data set has a number of data problems. Even a quick inspection of the data shows that the data fields have become confused.

### 1.3.4a Varying Length Records

| Obs | sex | fname | lname |
|---:|:---:|:---|:---|
| 1 | F | Linda | M Ronald |
| 2 | F | M Mat | M David |
| 3 | F | Merrie | F June |
| 4 | M | Mery | M Matthew |
| 5 | M | Robert | M Arthur |

Our INPUT statement requests SAS to read 15 spaces starting in column 18; however, there are never 15 columns available (the longest record is the last – Robertson – with a last name of 9 characters). To fill our request, it skips to column 1 of the next physical record to read the last name. When this happens, the notes mentioned in the LOG are generated.

## INFILE Statement Options (TRUNCOVER, MISSOVER)

Two INFILE statement options can be especially useful in controlling how SAS handles *short* records.

- **MISSOVER** — Assigns missing values to variables beyond the end of the physical record. Partial variables are set to missing.
- **TRUNCOVER** — Assigns missing values to variables beyond the end of the physical record. Partial variables are truncated, but not necessarily set to missing.
- **FLOWOVER** — SAS finishes the logical record using the next physical record. This is the default.

```
title '1.3.4b Varying Length Records';
title2 'Using TRUNCOVER';
data patients(keep=sex fname lname);
    infile patlist truncover;
    input @2  sex $1.
          @8  fname $10.
          @18 lname $15.;
run;
```

The TRUNCOVER option is specified and as much information as possible is gathered from each record; however, SAS does not go to the next physical record to complete the observation.

### 1.3.4b Varying Length Records
Using TRUNCOVER

| Obs | sex | Fname | lname |
|---:|:---:|:---|:---|
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

Generally, the TRUNCOVER option is easier to apply than the $VARYING informat, and there is no penalty for including a TRUNCOVER option on the INFILE statement even when you think that you will not need it.

By including the TRUNCOVER option on the INFILE statement, we have now correctly read the data without skipping a record, while correctly assigning a missing value to Rachel’s last name.

## Using the $VARYING Informat

The $VARYING informat was created to be used with variable-length records. This informat allows us to determine the record length and then use that length for calculating how many columns to read. As a general rule, you should first attempt to use the more flexible and easier to apply TRUNCOVER option on the INFILE statement, before attempting to use the $VARYING informat.

Unlike other informats, $VARYING utilizes a secondary value to determine how many bytes to read. Very often this value depends on the overall length of the record. The record length can be retrieved with the LENGTH= option ❶ and a portion of the overall record length is used to read the field with a varying width.

The classic use of the $VARYING informat is shown in the following example, where the last field on the record has an inconsistent width from record to record. This is also the type of data read for which the TRUNCOVER option was designed.

```
title2 'Using the $VARYING Informat';
data patients(keep=sex fname lname);
    infile patlist lrecl=10; ❶
    input @; ❷
    namewidth = len - 17; ❸
    input @2 sex $1.
          @8 fname $10.
          @18 lname $varying15. namewidth ❹;
run;
```

- ❶ The LENGTH= option on the INFILE statement specifies a temporary variable (LEN) which holds the length of the current record.
- ❷ An INPUT statement with just a trailing @ is used to load the record into the input buffer. Here the length is determined and loaded into the variable LEN. The trailing @ holds the record so that it can be read again.

### 1.3.4c Varying Length Records
Using the $VARYING Informat

| Obs | sex | Fname | lname |
|---:|:---:|:---|:---|
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

- ❸ The width of the last name is calculated (total length less the number of characters to the left of the name). The variable NAMEWIDTH holds this value for use by the $VARYING informat.

The width of the last name field for this particular record follows the `$VARYING15.` informat. Here the width used with the `$VARYING` informat is the widest possible value for `LNAME` and also establishes the variable’s length.

Inspection of the resulting data shows that we are now reading the correct last name; however, we still have a data issue for the third and fourth input lines. Since the third data line has no last name, the `$VARYING` informat jumps to the next data record. The `TRUNCOVER` option on the `INFILE` statement discussed above addresses this issue successfully.

In fact, for the third record the variable `FNAME`, which uses a `$10.` informat, reaches beyond the end of the record and causes the data to be misread.

```
data patients(keep=sex fname lname namewidth);
    length sex $1 fname $10 lname $15;
    infile patients length=len;
    input @;
    if len lt 8 then do;
        input @2 sex $;
    end;
    else if len le 17 then do;
        namewidth = len-7;
        input @2 sex $
              @8 fname $varying. namewidth;
    end;
    else do;
        namewidth = len-17;
        input @2 sex $
              @8 fname $
              @18 lname $varying. namewidth;
    end;
    run;
```

Using a `LENGTH` statement to declare the variable lengths avoids the need to add a width to the informats.

Neither a first or last name is included. This code assumes that a gender (SEX) is always present.

The record is too short to have a last name, but must contain a first name of at least one letter.

The last name must have at least one letter.

The variable `NAMEWIDTH` will contain the width of the rightmost variable. The value of this variable is generally of no interest, but it is kept here so that you can see its values change for each observation.

It is easy to see that the `$VARYING` informat is more difficult to use than either the `TRUNCOVER` or the `MISSOVER` options. However, the `$VARYING` informat can still be helpful. In the following simplified example suggested by John King, there is no delimiter and yet the columns are not of constant width. To make things more interesting, the variable with the inconsistent width is not on the end of the input string.

```
data datacodes;
    length dataname $15;
    input @1 width 2.
          dataname $varying. width
          datacode :2.;
    datalines;
5 Demog43
2 AE65
13lab_chemistry32
    run;
```

The first field (WIDTH) contains the number of characters in the second field (DATANAME). This value is used with the $VARYING informat to correctly read the data set name while not reading past the name and into the next field (DATACODE).

## SEE ALSO

Cates (2001) discusses the differences between MISSOVER and TRUNCOVER. A good comparison of these options can also be found in the SAS documentation http://support.sas.com/documentation/cdl/en/basics/58133/HTML/default/viewer.htm#a002645812.htm.

SAS Technical Support example #37763 uses the $VARYING. informat to write a zero-length string in a REPORT example http://support.sas.com/kb/37/763.html.

## 1.4 Writing Delimited Files

Most modern database systems utilize metadata to make the data itself more useful. When transferring data to and from Excel, for instance, SAS can take advantage of this metadata. Flat files do not have the advantage of metadata and consequently more information must be transferred through the program itself. For this reason delimited data files should not be our first choice for transferring information from one database system to another. That said, we do not always have that choice. We saw in Section 1.3 a number of techniques for reading delimited data.

Since SAS already knows all about a given SAS data set (it has access to the metadata), it is much more straightforward to write delimited files.

## MORE INFORMATION

Much of the discussion on reading delimited data also applies when writing delimited data (see Section 1.3).

### 1.4.1 Using the DATA Step with DLM= Option

When reading delimited data using the DATA step, the INFILE statement is used to specify a number of controlling options. Writing the delimited file is similar; however, the FILE statement is used. Many of the same options that appear on the INFILE statement can also be used on the FILE statement. These include:

- DLM=
- DLMSTR=
- DSD

While the DSD option by default implies a comma as the delimiter, there are differences between the uses of these two options. The DSD option will cause values which contain an embedded delimiter character to be double quoted. The DSD option also causes missing values to appear as two consecutive delimiters, while the DLM= alone writes the missing as either a period or a blank.
