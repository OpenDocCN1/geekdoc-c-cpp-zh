# 15.4 DateTimePicker Control

| MonthCalendar properties and an event | Description |
|---|---|
| Common MonthCalendar Event | |
 DateChanged | Generated when a date is selected in the calendar. |

**Fig. 15.9** | MonthCalendar properties and an event. (Part 2 of 2)

# 15.4 DateTimePicker Control

The DateTimePicker control (see output of 15.11) is similar to the MonthCalendar control but displays the calendar when a down arrow is selected. The DateTimePicker can be used to retrieve date and time information from the source. A DateTimePicker Value property stores both date and time information. You can retrieve the date information from the DateTime object by using Date, and can retrieve only the time information using TimeOfDay.

The DateTimePicker is also more customizable than a MonthCalendar control—more properties are provided to edit the look and feel of the dropdown calendar. Format specifies the user's selection options using the DateTimePickerFormat enumeration. The values in this enumeration are Long (displays the date in long format, as in Thursday, July 10, 2013), Time (displays a time value, as at 5:31:02 PM) and Custom (indicates that a custom format will be used). If Custom is used, the date in the DateTimePicker is specified by property CustomFormat. The default event for this control is ValueChanged, which occurs when the selected value (whether a date or a time) is changed. DateTimePicker properties and a common event are summarized in Fig. 15.10.

| DateTimePicker properties and an event | Description |
|---|---|
 DateTimePicker Properties | |
 CalendarForeColor Sets the text color for the calendar.
 CalendarMonthBackground Sets the background color.
 CustomFormat Sets the custom format string for the date and/or time displayed in the control.
 Format Sets the format of the date and/or time used for the date and/or time displayed in the control.
 MaxDate The maximum date and time that can be selected.
 MinDate The minimum date and time that can be selected.
 ShowCheckBox Indicates that a CheckBox should be displayed to the left of the selected date and time. |

**Fig. 15.10** | DateTimePicker properties and an event. (Part I of 2)