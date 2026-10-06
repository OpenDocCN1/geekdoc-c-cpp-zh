# CHAPTER 12 Using Controls

Several useful methods can be applied to the SelectionStart and SelectionEnd properties of MonthCalendar, including the following:

+   * ToShortString(), which displays the date in the format of 1/21/2019
* ToLongDateString(), which displays the date in the format of Monday, January 21, 2019
* AddDays(), which takes a double argument and adds a specified number of days to the date
* AddMonths(), which takes an int argument and adds a specified number of months to the date
* AddYears(), which takes an int argument and adds a specified number of years to the date

The format in which dates are depends on the operating system's regional settings. For example, using United Kingdom settings, the short string would use the day, followed by the month, as in 21/01/2019 for January 21. The examples in the list above use United States. To change your regional setting in Windows, you can go to Control Panel, click Region, and choose a region from the drop down list.

> AddDays() method accepts a double argument because you can add fractional days to SelectionStart and SelectionEnd.

> SelectionStart and SelectionEnd are structures of the DateTime type. The chapter "Files and Streams" contains additional information about DateTime objects to determine when files were created, modified, or accessed.

Many business and financial applications use AddDays(), AddMonths(), and AddYears() to calculate dates for events, such as a payment for a bill (perhaps in 10 days from an order) or scheduling a salesperson's call to a customer (perhaps two months after initial contact). The default event for MonthCalendar is Changed(). For example, Figure 12-26 shows a method that executes when the user clicks a MonthCalendar named monthCalendar. Days are added to a selected date and the result is displayed on a Label that has been named messageLabel. Figure 12-27 shows the output when the user selects April 26, 2019. The date that is 10 days in the future is correctly calculated as May 6.

```
private void MonthCalendar1_Changed(object sender,
    DateEventArgs e) {
    const int DAYS_TO_ADD = 10;
    messageLabel.Text = "Date " + DAYS_TO_ADD +
        " days after selection is " +
        monthCalendar1.SelectionStart.AddDays(
        (DAYS_TO_ADD)).ToShortDateString());
}
```

Figure 12-26 The Calendar_Changed() method