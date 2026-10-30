# Part IV: Analyzing Data in Microsoft Access

The query shown in Figure 12.28 illustrates how the DateAdd function can be used in determining the exact date a specific benchmark is reached. You’re creating two new fields with this query: Warning Date and Overdue Date. The DateAdd function used in the Warning Date field will return the date that is three weeks from the original order date. The DateAdd function used in the Overdue Date field will return the date that is one month from the original order date.

# FIGURE 12.28

This query will give you the original order date, the date you should send a warning letter, and the date on which the order will be 30 days overdue.

![](bbox=[0.169, 0.324, 0.748, 0.521])

# Grouping dates into quarters

Why would you need to group your dates into quarters? Most databases store dates rather than quarter designations. Therefore, if you wanted to analyze data on a quarter-over-quarter basis, you would have to convert dates into quarters. Surprisingly, there is no date/time function that allows you to group dates into quarters. There is, however, the Format function.

The Format function belongs to the Text category of functions and allows you to convert a variant into a string based on formatting instructions. From the perspective of analyzing dates, there are several valid instructions you can pass to a Format function:

```
Format(#01/31/2019#, "yyyy") returns 2019.
Format(#01/31/2019#, "yy") returns 19.
Format(#01/31/2019#, "q") returns 1.
Format(#01/31/2019#, "mmm") returns Jan.
Format(#01/31/2019#, "mm") returns 01.
Format(#01/31/2019#, "d") returns 31.
Format(#01/31/2019#, "w") returns 5.
Format(#01/31/2019#, "ww") returns 5.
```