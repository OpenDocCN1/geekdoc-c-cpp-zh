# Calendar Module

Beyond the time module, the calendar module can produce some interesting results when executed within your code. It does far more than simply display the date in the time module-like format, you can actually call up a wall calendar type display.

# WORKING WITH DATES

The calendar module is built into Python 3. However, if for some reason it’s not installed you can add it using `pip install calendar` as a Windows administrator or `sudo pip install calendar` for Linux and macOS.

STEP 1 — Launch Python 3 and enter: `import calendar` to call up the module and its inherent functions. Once it’s loaded into memory, start by entering:

```
sep=calendar.TextCalendar(calendar.SUNDAY)
sep.prmonth(2017, 9)
```

![](bbox=[0.066, 0.437, 0.493, 0.64])

STEP 2 — You can see that the days of September 2017 are displayed in a wall calendar fashion. Naturally you can change the 2017, 9 part of the second line to any year and month you want, a birthday for example (1973, 6). The first line configures TextCalendar to start its weeks on a Sunday; you can opt for Monday if you prefer.

![](bbox=[0.066, 0.743, 0.493, 0.947])

STEP 3 — There are numerous functions within the calendar module that may be of interest to you when forming your own code. For example, you can display the number of leap years between two specific years:

```
leaps=calendar.leapdays(1900, 2018)
print(leaps)
```

The result is 29, starting from 1904 onward.

![](bbox=[0.51, 0.468, 0.934, 0.64])

STEP 4 — You could even fashion that particular example into a piece of working, user interactive Python code:

```
import calendar
print(“>>>>>>>>Leap Year Calculator<<<<<<<<\n”)
y1=int(input(“Enter the first year: “))
y2=int(input(“Enter the second year: “))
leaps=calendar.leapdays(y1, y2)
print(“Number of leap years between”, y1, “and”, y2, “is:”, leaps)
```

![](bbox=[0.51, 0.773, 0.934, 0.947])