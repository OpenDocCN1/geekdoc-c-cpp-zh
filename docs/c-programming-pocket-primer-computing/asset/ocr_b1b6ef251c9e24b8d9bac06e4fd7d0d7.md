# CHECKING FOR LEAP YEARS

As a quick reminder, a *leap year* is a positive (integer-valued) year that satisfies the following two conditions:

+   - the year is a multiple of four, and
+   - if the year is a century then the year must be a multiple of 400

Examples of leap years include: 400, 1492, 1776, 2000, 2012, and 2472 (note that the centuries are multiples of 400). Examples of years that are not leap years include: 100, 1370, 1510, 1900, and 2011 (note that the centuries are *not* multiples of 400).

Listing 3.3 displays the contents of `LeapYear.c` that illustrates how to use if-else logic in a C program to determine if a particular year is a leap year.

# **LISTING 3.3: LeapYear.c**

```
```c
#include <stdio.h>

int main()
{
    int years[6] = {1900, 1953, 1958, 2000, 2004, 2006};
    int year=0, leapyear=0;

    int len = sizeof(years)/sizeof(years[0]);

    for(int i=0; i<len; i++)
    {
        year = years[i];

        if( year % 4 == 0)
        {
            leapyear = 1;
```
```