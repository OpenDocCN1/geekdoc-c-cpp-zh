5-12  Chapter 5 Data Transformations

# LENGTH Function

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

22

# Create the List of Charities: Step 1

The LENGTH function is **nested**, or used as an argument to the SUBSTR function.

```
data charities;
length ID $ 5;
set orion.biz_list;
if substr(Acct_Code,length(Acct_Code),1)='2';
ID=substr(Acct_Code,1,length(Acct_Code)-1);
run;
```

p205d02

23

Copyright © 2014, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED.