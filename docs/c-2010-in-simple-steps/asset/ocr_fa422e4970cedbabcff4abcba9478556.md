```
```xml
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="CalendarDemo" height="300" width="300"
<Grid>
<Calendar DisplayMode="Year" DisplayDate="4/28/2010" DisplayDateStart="4/28/2010" DisplayDateEnd="4/30/2010"/>
</Grid>
</window>
```
```

9 Press the F5 key to run the CalendarDemo application again. The output appears (Fig.C#7.33).

10 Click the Apr option on the Calendar control, as shown in Fig.C#7.33:

![](bbox=[0.35, 0.25, 0.6, 0.35])

Fig.C#7.33

The output on clicking the Apr option appears, as shown in Fig.C#7.34:

![](bbox=[0.35, 0.4, 0.6, 0.53])

Fig.C#7.34

In Fig.C#7.34, we have limited the number of dates displayed in the Calendar control to three: 28, 29, and 30.

# Using the DatePicker Control

Similar to the Calendar control, a WPF DatePicker control also enables a user to select a date. Located in the System.Windows.Controls namespace, the DatePicker control inherits the DatePicker class.

Table 7.13 lists the noteworthy properties of the DatePicker class:

Table 7.13: Noteworthy Properties of DatePicker class

| Property | Description |
|---|---|
| BlackOutDates | Retrieves or assigns a collection of dates that are marked as not selectable in a DatePicker control |
| DisplayDate | Retrieves or sets the date to display in a DatePicker control |
| DisplayDateEnd | Retrieves or sets the last date to be displayed in a DatePicker control |
| DisplayDateStart | Retrieves or sets the first date to be displayed in a DatePicker control |
| FirstDayOfWeek | Retrieves or sets the day that is considered the beginning of the week in a DatePicker control |
| SelectedDate | Retrieves or sets the currently selected date in a DatePicker control |
| SelectedDateFormat | Retrieves or sets the format used to display the selected date in a DatePicker control |