![](bbox=[0.35, 0.19, 0.58, 0.29])

Fig.C#7.30

In Fig.C#7.30, data is displayed inside the DataGrid control under the Student_ID, Name of Student, and Age of Student columns. Next, let's discuss about the Calendar control.

# Using the Calendar Control

The Calendar control is a new control that has been introduced with the latest version of WPF. It is a visual calendar, in which a user can select a particular date. Whenever a date is selected on a Calendar control, an event is fired on the selected date. The Calendar control is found in the System.Windows.Controls namespace, which is present in the PresentationFramework assembly. The Calendar control inherits the Control class. Table 7.12 lists some of important properties of the Control class:

Table 7.12: Noteworthy Properties of Calendar Control

| Property | Description |
|---|---|
| BlackOutDates | Retrieves a collection of dates that are marked as not selectable in a Calendar control |
| DisplayDate | Retrieves or sets the date to display in a Calendar control |
| DisplayDateEnd | Retrieves or sets the last date in the date range that is available in a Calendar control |
| DisplayDateStart | Retrieves or sets the first date that is available in a Calendar control |
| DisplayMode | Retrieves or sets a value that indicates whether a Calendar control displays a month, year, or decade |
| FirstDayOfWeek | Retrieves or sets the day that is considered the beginning of the week in a Calendar control |
| SelectedDate | Retrieves or sets the currently selected date in a Calendar control |
| SelectedDates | Retrieves a collection of selected dates in a Calendar control |
| SelectionMode | Retrieves or sets a value that indicates what kind of selections are allowed in a Calendar control |

Let's create a standalone WPF application named CalendarDemo to show the use the Calendar control. For this, perform the following steps:

+   1. Repeat steps 1 to 3 as followed earlier while creating the GridDemo application in the Using the Grid Control section of this chapter.
+   2. Enter the name CalendarDemo in the Name text box and specify an appropriate location for the application in the Location combo box.
+   3. Click the OK button. The CalendarDemo application is created.
+   4. Add the highlighted code given in Listing 7.15, in the MainWindow.xaml file:

Listing 7.15: Using the Calendar Control

```
<Window x:Class="CalendarDemo.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="CalendarDemo" Height="300" Width="300">
```