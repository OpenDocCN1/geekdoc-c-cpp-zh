| Document_Number | Due_Date | Created_By |
|---|---|---|
| 1003 | 20151105 | USER2 |
| 1004 | 20151106 | USER2 |

**Table 4.5** Dates Represented in Internal Format (Cont.)

Now, when the user inputs a date in your report, it's always converted to the internal format first before querying the database table to fetch the matching records. This allows the user to input the date in any of the valid external formats per his personal choice without worrying about the format the program expects.

# Output Length of Data Types

In the previous section, the external format of date included two separators (/ or -). The internal length of a date is eight characters, but to represent the date in an external format requires two extra characters to accommodate the separators. Therefore, the external length should be a minimum of ten characters. This is determined by the output length of the data type.

If you examine the data object of TYPE I in the debugger, you'll see that different lengths have been assigned for LENGTH and OUTPUT LENGTH, as shown in Figure 4.6.

![](bbox=[0.148, 0.567, 0.44, 0.712])

**Figure 4.6** Output Length

As shown in Figure 4.6, the data object F2 is of TYPE I with LENGTH 4 bytes. However, the OUTPUT LENGTH is 11 to accommodate the thousands separator for the value.

If you check the same for a data object of Type D, you'll see that the LENGTH and the OUTPUT LENGTH are the same—eight bytes—as shown in Figure 4.7.