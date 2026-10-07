# Chapter 9: Working with Dates

Figure 9.7: Listing of Data Set Substitute

# Listing of Data Set Substitute

| Obs | Month | Day | Year | Date |
|---|---|---|---|---|
| 1 | 10 | 21 | 1950 | 10/21/1950 |
| 2 | | 3 | 2005 | 03/15/2005 |
| 3 | 5 | 7 | 2000 | 05/07/2000 |

# 9.10 Using Date Interval Functions

Two functions, INTCK and INTNX, deal with date intervals (such as months, quarters, years). The INTCK function computes the number of interval boundaries that are crossed from one date to another date; the INTNX function computes a date after a given number of intervals.

First of all, nobody knows how to pronounce either of these two functions—you're on your own. Next, these functions can be very complicated. For a more complete treatment of these functions, please see SAS Functions by Example, 2nd edition (Cody – published by SAS Press 2010) or SAS Help Center at http://go.documentation.sas.com.

To understand the most basic use of these two functions, you must both deal with interval boundaries. For example, an interval boundary for the YEAR is January 1, the boundary for WEEK is Sunday. A few examples make this clear. Look at the following table:

| Expression | Value Returned |
|---|---|
| INTCK('year','01Jan2005d','31Dec2005d') | 0 |
| INTCK('year','31Dec2005d','01Jan2006d') | 1 |
| INTCK('month','01Jan2005d','31Jan2005d') | 0 |
| INTCK('month','31Jan2005d','01Feb2005d') | 1 |
| INTCK('qtr','25Mar2005d','15Apr2005d') | 1 |

The INTCK function takes three arguments. The first is the desired starting a starting date and an ending date. The function returns the number of interval boundaries that have been crossed by going from the first date to the second date. The first entry in the table starts at January 1, 2005, and ends at December 31, 2005. The value returned is 0 because a boundary (January 1) was not crossed from the first date to the second. The next entry, from December 31, 2005, to January 1, 2006, returns a 1 because a boundary was crossed (even though this represents only one day).

The same logic holds for the two INTCK functions with MONTH as the interval. A month boundary is the first of any month. The last table entry counts how many months are crossed from March 25, 2005 to April 15, 2005. Because the boundaries for quarters are January 1, April 1, July 1, and October 1, this expression returns a 1 (the boundary of April 1 was crossed).