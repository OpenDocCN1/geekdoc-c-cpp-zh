# STEP 5

You can also create a program that will display all the days, weeks and months within a given year:

```
```python
import calendar
year=int(input(“Enter the year to display: “))
print(calendar.prcal(year))
```
```

We’re sure you’ll agree that’s quite a handy bit of code to have to hand.

![](bbox=[0.066, 0.245, 0.491, 0.383])

# STEP 8

You’re also able to print the individual months or days of the week:

```
```python
import calendar
for name in calendar.month_name:
    print(name)

import calendar
for name in calendar.day_name:
    print(name)
```
```

![](bbox=[0.509, 0.259, 0.934, 0.383])

# STEP 6

Interestingly we can also list the number of days in a month by using a simple for loop:

```
```python
import calendar
cal=calendar.TextCalendar(calendar.SUNDAY)
for i in cal.itermonthdays(2018, 6):
    print(i)
```
```

![](bbox=[0.066, 0.497, 0.491, 0.669])

# STEP 9

The calendar module also allows us to write the functions in HTML, so that you can display it on a website. Let’s start by creating a new file:

```
```python
import calendar
cal=open(“/home/pi/Documents/cal.html”, “w”)
c=calendar.HTMLCalendar(calendar.SUNDAY)
cal.write(c.formatmonth(2018, 1))
cal.close()
```
```

This code will create an HTML file called cal, open it with a browser and it displays the calendar for January 2018.

![](bbox=[0.509, 0.552, 0.934, 0.669])

# STEP 7

You can see that code produced some zeros at the beginning, this is due to the starting day of the week, Sunday in this case, and overlapping days from the previous month. So the counting of the days will start on Friday 1st June 2018 and will total 30 as the output correctly displays.

![](bbox=[0.066, 0.759, 0.491, 0.963])

# STEP 10

Of course, you can modify that to display a given year as a web page calendar:

```
```python
import calendar

year=int(input(“Enter the year to display as a webpage: “))
cal=open(“/home/pi/Documents/cal.html”, “w”)
cal.write(calendar.HTMLCalendar(calendar.MONDAY).formatyear(year))
cal.close()
```
```

This code asks the user for a year, then creates the necessary webpage. Remember to change your file destination.

![](bbox=[0.509, 0.847, 0.934, 0.963])