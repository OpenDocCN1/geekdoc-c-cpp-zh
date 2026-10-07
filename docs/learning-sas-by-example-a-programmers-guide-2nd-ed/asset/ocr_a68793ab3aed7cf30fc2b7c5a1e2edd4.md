# Chapter 10: Subsetting and Combining SAS Data Sets 139

> **Note:** If you use a KEEP statement listing the eight variables instead of the KEEP= data set option, all of the variables, including Salary would be in the PDV but not written out to the Females data set. If the input data set contains a large number of variables and you want only a few of these in the new data set, using the KEEP= data set option is more efficient than a KEEP statement.

You must remember when you use the KEEP= data set option, the variables not in the keep list are also not available in the DATA step.

# 10.3 Creating More Than One Subset Set in One DATA Step

You can create multiple SAS data sets from one input data set (something SQL cannot). Following the previous example, you can create a data set containing only on females and one containing only on males, in one step like:

Program 10.3: Creating Two Data sets in One DATA Step

```
data Males;
set Learn.Survey;
if Gender = 'F' then output Females;
else if Gender = 'M' then output Males;
run;
```

Notice that you must name the data set following the OUTPUT statement. If you do not, SAS outputs the observation to all the data sets listed in the DATA statement.

# 10.4 Adding Observations to a SAS Data Set

Suppose you want to create a single data set from several similar data sets. For example, your company may collect data each month into separate data sets and you want to analyze a year's worth of data. You can list as many data sets as you want on a SET statement and SAS will add all the observations together to form a single data set. For example, look at the listings of data sets One and Two here:

Figure 10.2: Listing of Data Sets One and Two

| Data Set One | | | | Data Set Two | | | |
|---|---|---|---|---|---|---||
| Obs | ID | Name | Weight | Obs | ID | Name | Weight |
| 1 | 7 | Adams | 210 | 1 | 9 | Shea | 120 |
| 2 | 1 | Smith | 190 | 2 | 3 | O'Brien | 180 |
| 3 | 2 | Schneider | 110 | 3 | 5 | Bessler | 207 |
| 4 | 4 | Gregory | 90 | | | | |