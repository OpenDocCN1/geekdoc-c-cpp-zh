# 5.2 Reordering Variables on the PDV

**The CONTENTS Procedure**

**Variables in Creation Order**

| # | Variable | Type | Len | Format | Label |
|---:|---|---|---:|---|---|
| 1 | subject | Num | 8 |  |  |
| 2 | clinnum | Char | 6 |  | clinic number |
| 3 | lname | Char | 10 |  | last name |
| 4 | fname | Char | 6 |  | first name |
| 5 | ssn | Char | 9 |  | social security number |
| 6 | sex | Char | 1 |  | patient sex |
| 7 | dob | Num | 8 | DATE7. | date of birth |
| 8 | death | Num | 8 | DATE7. | date of death |
| 9 | race | Char | 1 |  | race |
| 10 | edu | Num | 8 |  | years of education |
| 11 | wt | Num | 8 |  | weight in pounds |
| 12 | ht | Num | 8 |  | height in inches |
| 13 | symp | Char | 2 |  | symptom code |
| 14 | death2 | Num | 8 | DATE9. |  |

In the example that follows, only a few of the variables from ADVRTP.DEMOG flow through to the new data set, and the order of these variables is changed by the use of the LENGTH statement.

```
```sas
data demog2(keep=subject lname fname sex ht wt dob symp);
   length lname $10 fname $6 sex $1 symp $2;
   set advrtp.demog(keep=subject lname fname sex edu
                    death ht wt dob symp);
   where death and edu>15;
run;
```
```

❶ The KEEP and DROP statements/options do not change or affect the order of variables on the PDV.

❷ The LENGTH statement is used not only to assign the length attribute to these four variables, but it also adds them to the PDV. Since the LENGTH statement appears before the SET statement these variables and their associated attributes are added to the PDV before any variables or attributes are contributed by the SET statement. Attributes for these variables that have not been specified, for example formats or labels, will be picked up from the metadata of the incoming data set named on the SET statement.

❸ Although the variables DEATH and EDU are not to be included on the new data set, they must be available on the PDV for use by the WHERE statement.

# 5.2 Reordering Variables on the PDV

| Obs | lname | fname | sex | symp | subject | dob | wt | ht |
|---:|---|---|---|---:|---:|---|---:|---:|
| 1 | James | Debra | F | 05 | 232 | 19JUN42 | 163 | 63 |
| 2 | Manley | Debra | F | 05 | 241 | 19JAN42 | 163 | 63 |

Notice that while the order has changed for the variables in the LENGTH statement, the order for the remaining variables is the same as it was on the incoming data.