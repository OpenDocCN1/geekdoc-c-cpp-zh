
## 5.03 Multiple Choice Poll

Which SUBSTR function can extract the group of five numbers from the middle of the Item_Code value?

| PDV Item_Code |
|---|---|
| $ 20 978-1-59994-397-8 |

- a. substr(Item_Code,5,7)
- b. substr(Item_Code,5)
- c. substr(Item_Code,7,5)
- d. substr(Item_Code,'mid',5)

The variable Acct_Code is in the output for learning purposes so that it can be easily compared to the ID variable. Otherwise, there is no need for it, and it could be dropped from the charities data set.

## Create the List of Charities: Step 1

> The last non-blank character in the Acct_Code value occurs in different positions for different observations.

| Partial orion.biz_list | Acct_Code |
|---|---|
| AEK3 | last character in position 4 |
| AQI2 | last character in position 3 |
| ATS1 | |
| CBO3 | |
| CCI2 | |
| ON12 | |
| CS1 | need some way to determine the position of the last character so that the SUBSTR function can extract it. |
| CS2 | |

## LENGTH Function

The LENGTH function returns the length of a non-blank character string, excluding trailing blanks.
General form of the LENGTH function:

```
NewVar=LENGTH(argument);
```

Example:

```
Code='ABCD' ;
Last_NonBlank=length(Code);
```

| Code | Last_NonBlank |
|---|---|
| $6 | N 8 |
| ABCD | 4 |

## Create the List of Charities: Step 1

The LENGTH function is **nested**, or used as an argument to the SUBSTR function.

```sas
data charities;
length ID $ 5;
set orion.biz_list;
if substr(Acct_Code,length(Acct_Code),1)='2';
ID=substr(Acct_Code,1,length(Acct_Code)-1);
run;
```

## Execution: Step 1

```sas
data charities;
length ID $ 5;
set orion.biz_list;
if substr(Acct_Code,length(Acct_Code),1)='2';
ID=substr(Acct_Code,1,length(Acct_Code)-1);
run;
```

| ID | Acct_Code | Name |
|---|---|---|
| $5 | $6 | $ 30 |
| AQ12 | AQUAMISSIONS INTERNATIONAL |

## Execution: Step 1

```sas
data charities;
length ID $ 5;
set orion.biz_list;
if substr(Acct_Code,length(Acct_Code),1)='2';
ID=substr(Acct_Code,1,length(Acct_Code)-1);
run;
```

| ID | Acct_Code | Name |
|---|---|---|
| $5 | $6 | $ 30 |
| AQI2 | AQUAMISSIONS INTERNATIONAL |

## Execution: Step 1

```sas
data charities;
length ID $ 5;
set orion.biz_list;
if substr(Acct_Code,length(Acct_Code),1)='2';
ID=substr(Acct_Code,1,length(Acct_Code)-1);
run;
```

| ID | Acct_Code | Name |
|---|---|---|
| $5 | $6 | $ 30 |
| AQI2 | AQUAMISSIONS INTERNATIONAL |

## Execution: Step 1

```sas
data charities;
length ID $ 5;
set orion.biz_list;
if substr(Acct_Code,length(Acct_Code),1)='2';
ID=substr(Acct_Code,1,length(Acct_Code)-1);
run;
```

| ID | Acct_Code | Name |
|---|---|---|
| $5 | $6 | $ 30 |
| AQI2 | AQUAMISSIONS INTERNATIONAL |

## Execution: Step 1

```sas
data charities;
length ID $ 5;
set orion.biz_list;
if substr(Acct_Code,length(Acct_Code),1)='2';
ID=substr(Acct_Code,1,length(Acct_Code)-1);
run;
```

| ID | Acct_Code | Name |
|---|---|---|
| $5 | $6 | $30 |
| AQI2 | AQUAMISSIONS INTERNATIONAL |

## Execution: Step 1

```sas
data charities;
length ID $ 5;
set orion.biz_list;
if substr(Acct_Code,length(Acct_Code),1)='2';
ID=substr(Acct_Code,1,length(Acct_Code)-1);
run;
```

| ID | Acct_Code | Name |
|---|---|---|
| $5 | $6 | $30 |
| AQI2 | AQUAMISSIONS INTERNATIONAL |

## Execution: Step 1

```sas
data charities;
length ID $ 5;
set orion.biz_list;
if substr(Acct_Code,length(Acct_Code),1)='2';
ID=substr(Acct_Code,1,length(Acct_Code)-1);
run;
```

| ID | Acct_Code | Name |
|---|---|---|
| $5 | $6 | $30 |
| AQI | AQUAMISSIONS INTERNATIONAL |

## Create the List of Charities: Step 1 Complete

| ID | Acct_Code | Name |
|---|---|---|
| AGI | AQUAMISSIONS INTERNATIONAL |
| CCI | CANCER CURES, INC. |
| CNI | CONSERVE SURIVORS, INC. |
| CS | CHILD SURIVORS |
| QU | CUMORES LTD. |
| DAI | DISASTER ASSIST, INC. |
| ES | EARTHSAVIOR |
| FFC | FING FOR COMMUNITIES |
| MI | INTERNATIONAL |
| SBA | SAVE THE BABY ANIMALS |
| V | VICTIMS |
| YY | YES, CAN RECYCLE |

Step 2 Transform the values in Name to a mix of upper and lowercase.

## Create the List of Charities: Step 2

The name of the organization is stored as all capital letters. In the desired output, only the first letter of each word is capitalized.

| Example: Name |
|---|
| AQUAMISSIONS INTERNATIONAL |

| Change to: Name |
| Aquamissions International |

## PROPCASE Function

Example: Name='SURF&LINK SPORTS'; Pname=propcase(Name); Pname2=propcase(Name, '&');

```sas
NewVar=PROPCASE(argument,delimiter(s));
```

| Name | Pname |
|---|---|
| $16 | $16 |
| SURF&LINK SPORTS | Surf/link Sports |

| Pname2 |
|---|
| $16 |
| Surf&Link Sports |

If you omit delimiters, the default delimiters are as follows: blank, /, -, (, and tab characters

## 5.04 Short Answer Poll

This PDV shows the current value of Name:

| Name |
|---|
| HEATH*BARR*LITTLE EQUIPMENT SALES |

Write an answer statement that converts the value of Name to this:

| Name |
|---|
| Heath*Barr*Little Equipment Sales |

## Completed Business Scenario

Adding an assignment statement to convert Name to proper case completes the charities data set.

```sas
data charities;
length ID = $5;
set orion.biz_list;
if substr(Acct_Code,Acct_Code,1)='2';
ID=substr(Acct_Code,1,length(Acct_Code)-1);
Name = propcase(Name);
run;
```

## Other Useful Character Functions

| Function | Purpose |
|---|---|
| RIGHT(string) | Right-aligns a character expression. |
| LEFT(string) | Left-aligns a character expression. |
| UPCASE(string) | Converts all letters in an argument to uppercase. |
| LOWCASE(string) | Converts all letters in an argument to lowercase. |
| CHAR(string,position) | Returns a single character from a specified position in a character string. |

The CHAR function was introduced in SAS 9.2.

## 5.04 Short Answer

a. Write an answer statement that converts the value of Name to:

```sas
data shoes;
length ID $ 5;
set orion.biz_list;
if substr(Acct_Code,length(Acct_Code),1)='2';
ID=substr(Acct_Code,1,length(Acct_Code)-1);
Name = propcase(Name);
run;
```

b. How many observations are in the data set?

## 1. Extracting Characters Based on Position

The data set orion.biz_list has data for Australia.

| Employee_ID | First_Name | Last_Name |
|---|---|---|
| 1 Tom | Zhou | Sales Manager |
| 2 Wilson | Dawes | Sales Manager |
| 3 Irenie | Elvish | Sales Rep. |
| 4 Christina | Ngan | Sales Rep. |
| 5 Kimiko | Hotstone | Sales Rep. |

a. Orion wants to create ID consisting of the first letter of the first name, the final letter of the first name, and the first four letters of the last name. All letters should be lowercase. As a first step to doing this, extract these letters.

## 5.2 Manipulating Character Values (Part 1)

- Create three variables FCode1, FCode2, and LCode. As described above, variables should contain the following:

| Variable | Value | Length |
|---|---|---|
| FCode1 | First letter of First_Name | $1 |
| FCode2 | Final letter of First_Name | $1 |
| LCode | First four letters of Last_Name | $4 |

- Remember to make these new values too.

There are several ways to approach getting the final letter of First_Name. For of those ways, you need to know that the length of First_Name is 12 characters.

- Print the resulting data set.
- Include only the variables First_Name, FCode1, FCode2, Last_Name, and LCode.
- Add an appropriate title.
- Verify your output.

Partial PRINT output (63 Total Observations)

| First_Name | FCode1 | FCode2 | Last_Name | LCode |
|---|---|---|---|---|
| Tom | t | m | Zhou | zhou |
| Wilson | w | n | Dawes | dawe |
| Irenie | i | e | Elvish | elvi |
| Christina | c | a | Ngan | ngan |
| Kimiko | k | o | Hotstone | |
