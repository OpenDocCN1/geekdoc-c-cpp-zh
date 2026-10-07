# 130 Learning SAS by Example: A Programmer's Guide, Second Edition

Besides YEAR, MONTH, and QUARTER, the two date functions INTCK and INTNX support several others. A partial list of intervals supported by both the INTCK and INTNX functions is displayed below

Figure 9.8: A Partial List of Intervals Supported by the INTCK and INTNX Functions

| Interval | Description |
| --- | --- |
| Week | Weekly intervals with Sunday as the first day of the week |
| Weekday | Weekdays (default Sat. and Sun. not included) |
| Month | Months (with the first of each month as the boundary) |
| Qtr | Quarters (Jan. 1, April 1, July 1, and Oct. 1) |
| Semi-year | Semi-annual intervals |
| Year | Yearly intervals |

Here is an example. Data set Hosp contains 1000 observations. Variables in this data set include a date of birth (DOB) and an admission date (Admit). You want to see a graph showing the number of admissions for each quarter starting with January 1, 2003, and ending with June 30, 2006. Without the INTCK function, this would require a lot of programming; this becomes a more straightforward problem. Here is one possible solution:

# Program 9.9: Demonstrating the INTCK Function

```
data Frequency;
  set Learn.Hosp(Keep=AdmitDate
  where=(AdmitDate) between '01Jan2003'd and
  '30Jun2006'd);
  Quarter = intck('qtr','31Dec2002'd,AdmitDate);
run;

title "Admissions from January 1, 2003 to June 30, 2006";nproc sgplot data=Frequency;
  vbar Quarter;
run;
```

The key to this program is using the INTCK function to count the number of quarters from the starting date of December 31, 2002. (This date was used so that any admission in the first quarter of 2003 would be quarter 1.) PROC SGPLOT can produce a vertical bar chart (hence the keyword VBAR) showing how many visits occurred in each quarter. The resulting chart is shown next: