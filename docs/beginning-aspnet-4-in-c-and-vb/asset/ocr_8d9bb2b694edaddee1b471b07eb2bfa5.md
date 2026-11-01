To show some issues with localization, this program has a picture, some text, a date, and a number. The picture shows a flag that is also localized. Figure 22-8 shows this form of the application as seen in the Windows Forms Designer.

The following table lists the values for the Name and Text properties of the Windows Forms elements.

| NAME | TEXT |
|---|---|
| labelBookOfTheDay | Book of the day |
| labelItemsSold | Books sold |
| textDate | Date |
| textTitle | Professional C# |
| textItemsSold | 30000 |
| pictureFlag |  |

![](bbox=[0.75, 0.15, 0.95, 0.45])

# FIGURE 22-8

In addition to this form, you might want a message box that displays a welcome message; this message might change depending on the current time of day. This example demonstrates that the localization for dynamically created dialogs must be done differently. In the method WelcomeMessage(), display a message box using MessageBox.Show(). Call the method WelcomeMessage() in the constructor of the form class BookOfTheDayForm, before the call to InitializeComponent().

Here is the code for the method WelcomeMessage():

```
public void WelcomeMessage()
{
    DateTime now = DateTime.Now;
    string message;
    if (now.Hour <= 12)
    {
        message = "Good Morning";
    }
    else if (now.Hour <= 19)
    {
        message = "Good Afternoon";
    }
    else
    {
        message = "Good Evening";
    }
    MessageBox.Show(String.Format("{0}\nThis is a localization sample", message));
}
```

The number and date in the form should be set by using formatting options. Add a new method, SetDateAndNumber(), to set the values with the format option. In a real application, these values could be received from a Web service or a database, but this example is just concentrating on localization. The date is formatted using the D option (to display the long date name). The number is displayed using the picture number format string #,##,###,##, where # represents a digit and ',' is the group separator.

```
public void SetDateAndNumber()
{
    DateTime today = DateTime.Today;
    textDate.Text = today.ToString("D");
    int itemsSold = 32744;
    textItemsSold.Text = itemsSold.ToString("#,##,###,##");
}
```