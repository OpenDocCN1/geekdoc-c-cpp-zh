# 648 Chapter 15 Graphical User Interfaces with Windows Forms: Part 2

Form. The event handlers for the **Bold** and *Italic* menu items (lines 139–160) use the bitwise logical exclusive OR (^) operator to combine styles, as we discussed in Chapter 14.

# 15.3 MonthCalendar Control

Many apps must perform date and time calculations. The .NET Framework provides two controls that allow an app to retrieve date and time information—MonthDatePicker (Section 15.4).
The MonthCalendar (Fig. 15.8) control displays a monthly calendar on the Form. The user can select a date from the displayed month or use the provided arrows to navigate to another month. When a date is selected, it is highlighted. Multiple dates can be selected by clicking dates on the calendar while holding down the Shift key. The default first event for this control is the DateChanged event, which is generated when a new date is selected. Properties are provided that allow you to modify the appearance of the calendar, how many dates can be selected at once, and the minimum and maximum date that may be selected. MonthCalendar properties and a common MonthCalendar event are summarized in Fig. 15.9.

![](bbox=[0.368, 0.435, 0.632, 0.584])

Fig. 15.8 | MonthCalendar control.

| MonthCalendar properties and an event | Description |
|--- |--- |
| **MonthCalendar Properties** | |
| FirstDayOfOfWeek | Sets which day of the week is the first displayed for each week in the calendar. |
| MaxDate | The last date that can be selected. |
| MaxSelectionCount | The maximum number of dates that can be selected at once. |
| MinDate | The first date that can be selected. |
| Month1BoldDates | An array of dates that will be displayed in bold in the calendar. |
| SelectionEnd | The last of the dates selected by the user. |
| SelectionRange | The dates selected by the user. |
| SelectionStart | The first of the dates selected by the user. |

Fig. 15.9 | MonthCalendar properties and an event. (Part I of 2.)