![](bbox=[0.19, 0.1, 0.82, 0.58])

Check if a data is valid

You can apply the `ok`-call on a calendar date. Now it's pretty easy to check if a specific calendar date is a leap day and, therefore, the corresponding year a leap year. In the worldwide used Gregorian calendar³, the following rules apply:

Each year that is exactly divisible by 4 is a leap year.

+   - Except for years that are exactly divisible by 100. They are not leap years.
+     - Except for years that are exactly divisible by 400. They are leap years.

Too complicated? The program `leapYears.cpp` exemplifies this rule.

The extended `chrono` library makes it relatively easy to ask for the time duration between calendar dates.

# ### 5.6.4.6 Query Calendar Dates

Without further ado, the following program `queryCalendarDates.cpp` queries a few calendar dates.

³https://en.wikipedia.org/wiki/Gregorian_calendar