| Function | Description |
|---|---|
| displayMenu | displays selection menu and prompts user for selection |
| getCalendarDate | prompts and gets calendar date from user |
| getJulianDate | prompts and gets Julian date from user |
| toCalendar | converts Julian date into calendar date |
| toJulian | converts calendar date into Julian date |
| daysBetweenDates | calculates the number of days between two calendar dates |

Hint to compute the number of days between two calendar dates: For each date, figure out the number of days since January 1, 1900 and then subtract.

For this assignment we will define a leap year as any year that is evenly divisible by 4 but not 100, except that years divisible by 400 are leap years. Here's a function you can use to calculate leap years. Try and work through its details.

```
int isLeapYear(int year) {
       return (((year % 4) && year % 100) || !(year % 400));
}
```

Remember that the main() function should appear as the first function in the program. Be sure to use function prototypes for each of the functions that are used in your program.

Test data for the lab is given below.

**Convert Calendar Date Into Julian Date**

| 11 | 15 | 1922 | (319, 1922) |
|---|---|---|---|
| 2 | 29 | 1984 | ( 60, 1984) |
| 7 | 7 | 2000 | (189, 2000) |

**Convert Julian Date Into Calendar Date**

| 53 | 1947 | ( 2/22/1947) |
|---|---|---|
| 211 | 1995 | ( 7/30/1995) |
| 360 | 2006 | (12/26/2006) |

**Compute Number of Days Between Two Calendar Dates**

| 5 | 12 | 1949 | 8 | 16 | 1900 | (17801) |
|---|---|---|---|---|---|---|
| 12 | 15 | 1985 | 3 | 1 | 1986 | (76) |
| 1 | 1 | 1900 | 7 | 7 | 1993 | (34155) |