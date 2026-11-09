# Setting the countdown

In the next stage of building Countdown Calendar you’ll create a function to count the number of days between today and your important events. You’ll also write the code to display the events on the Tkinter canvas.

# 14  Count the days

Create a function to count the number of days between two dates. The datetime module makes this easy, because it can add dates together or subtract one from another. Type the code shown here below your get_events() function. It will store the number of days as a string in the variable time_between.

```
```python
def days_between_dates(date1, date2):
    time_between = str(date1-date2)
```
```

The function is given two dates.

This variable stores the result as a string.

The dates are subtracted to give the number of days between them.

![](bbox=[0.602, 0.064, 0.984, 0.273])

# 15  Split the string

If Halloween is 27 days away, the string stored in time_between would look like this: '27 days, 0:00:00' (the zeros refer to hours, minutes, and seconds). Only the number at the beginning of the string is important, so you can use the split() command again to get to the part you need. Type the code highlighted below after the code in Step 14. It turns the string into a list of three items: '27', 'days', '0:00:00'. The list is stored in number_of_days.

```
```python
def days_between_dates(date1, date2):
    time_between = str(date1-date2)
    number_of_days = time_between.split(' ')
```
```

This time the string is split at each blank space.

![](bbox=[0.606, 0.412, 0.984, 0.643])

# 16  Return the number of days

To finish off this function, you just need to return the value stored in position 0 of the list. In the case of Halloween, that’s 27. Add this line of code to the end of the function.

```
```python
def days_between_dates(date1, date2):
    time_between = str(date1-date2)
    number_of_days = time_between.split(' ')
    return number_of_days[0]
```
```

The number of days between the dates is held at position 0 in the list.