# Table 15-4 Members of the `DateTime` class (continued)

| DateTime members | Description |
|---|---|
| Today -- static | Gets the current date |
| Year | Gets the current year |
| +, -, ==, !=, <, >, >=, <= | Operators defined to work with `DateTime` instances |

![](bbox=[0.173, 0.251, 0.237, 0.302])

Properties are shown in Table 15-4 without ( ).

# Using a Calendar Control in Applications

To continue creating the WebControls application, a button labeled Next Meeting is added to the form. Remember, the final result of the application was shown in Figure 15-19. When the button labeled Next Meeting is clicked, the calendar changes to show the date of the next computer club meeting. Programmatically, this is set as exactly seven days from the current date. A selection statement is then used to test the meeting date to make sure the date does not fall on Sunday. If it does, the meeting date is set for the following Monday. Example 15-12 shows the event-handler method for this button.

# Example 15-12

```
protected void btnShowCalendar_Click(object sender,
                                    System.EventArgs e)
{
    Calendar1.SelectedDates.Clear();
    meetingDate = new DateTime(DateTime.Today.Year,
                               DateTime.Today.Month,
                               DateTime.Today.Day, 8, 0, 0);
    // Meeting is schedule for one week from today!
    meetingDate = meetingDate.AddDays(7);
    // Unless, of course it's Sunday - if so
    // meet on Monday.
    if (meetingDate.DayOfWeek.ToString() == "Sunday")
    {
        meetingDate = meetingDate.AddDays(1);
    }
    Calendar1.SelectedDate = meetingDate;
    this.lblMsg.Text = ("Meeting next week: " +
                        meetingDate.DayOfWeek + ", " +
                        meetingDate.Month + " " +
                        meetingDate.Day + " at " +
                        meetingDate.Hour + " P.M.");
}
```