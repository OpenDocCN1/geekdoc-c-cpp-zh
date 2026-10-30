Here is a partial list of some useful properties and methods of the Date-Time structure:

| Property or method | Purpose |
|---|---|
| Date | Date component. |
| Day | Integer day of month; 1–31. |
| DayOfWeek | Integer day; 0 = Sunday. |
| DayOfYear | Integer day; 1–366. |
| Hour | Integer hour; 0–23. |
| Minute | Integer minutes; 0–59. |
| Second | Integer seconds; 0–59. |
| Month | Integer month; 1 = January. |
| Now (shared) | Retrieve system date and time. |
| Today (shared) | Retrieve system date. |
| Year | Year component. |
| ToLongDateString | Date formatted as long date. |
| ToLongTimeString | Date formatted as long time. |
| ToShortDateString | Date formatted as short date. |
| ToShortTimeString | Date formatted as short time. |

# Retrieving the System Date and Time

You can retrieve the system date and time from your computer's clock using the Now property or the Today property. Now retrieves both the date and time; Today retrieves only the date.

```
Dim DateAndTimeDate As Date
DateAndTimeDate = Now

Dim TodaysDate As Date
TodaysDate = Today
```

To display the values formatted:

```
DateTimeLabel1.Text = DateAndTimeDate.ToLongDateString()
DateLabel1.Text = TodaysDate.ToShortDateString()
```

# Date Variables

The Date data type may hold values of many forms that represent a date. Examples could be May 26, 2009 or 5/26/09 or 5-26-2009. When you assign a literal value to a Date variable, enclose it in # signs:

```
Dim TheDate as Date = #5/26/2009#
```