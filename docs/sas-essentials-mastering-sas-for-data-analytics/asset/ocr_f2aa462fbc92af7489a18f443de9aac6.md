# CHAPTER 4: PREPARING DATA FOR ANALYSIS

(continued)

Notice that there is a set of parentheses following the OUT= statement. Within those parentheses is a KEEP= statement that specifies variables to keep in the output file ANALYSIS. Inside these parentheses is another statement, RENAME with its own. Inside the RENAME= parentheses are two statements that rename an old variable with a name. The syntax of this RENAME statement is

```
RENAME = (oldname1=newname1 oldname2=newname2, etc...)
```

Therefore, this code renames two variables and saves four variables in the output. Submit this code and observe the (partial) results shown in Table 4.11.

However, note that the KEEP must be the original variable names, not the new names. Note that ID and AGE are kept, but in the new data set, they are named SUBJECT and GENDER.

+   2. The variable name GENDER out of the KEEP statement. Re-run the program and see that the results no longer include the GENDER column.

+   3. Re the GP to GROUP. Re-run the code and observe the changed results.

TABLE 4.11 SAS Output Showing Ascending and Descending
| Obs | SUBJECT | GP | DXAGE | GENDER |
| 1 | 101 | A | 12 | Female |
| 2 | 102 | A | 11 | Female |
| 3 | 104 | B | 12 | Female |
| 4 | 110 | A | 12 | Male |
| 5 | 103 | B | 0 | Male |

# 4.7 APPENDING AND MERGING DATA SETS

Other useful SAS data manipulation capabilities are appending and merging data sets.

+   * Adding adds records to an existing data set.
* Merging adds variables to a data set through the use of a key identifier that is present in both data sets (usually an identification code).

# 4.7.1 Appending Two Data Sets

Appending data sets combines records from two or more data sets (It is sometimes called a vertical merge.) For example, suppose that data sets are collected at two locations and you want to combine the data sets into one SAS data set for analysis. The data sets must have at least some of the same variables in common. Appending is accomplished by including multiple data set names in the SET statement. For example,