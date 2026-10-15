
## Listing 17.3: Showing the Code for the Code-Behind File of the MainPage.xaml File

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Animation;
using System.Windows.Shapes;

namespace BookTicketCalendarAppCS
{
    public partial class MainPage : UserControl
    {
        private Boolean checkTicket;
        public MainPage()
        {
            InitializeComponent();
            checkTicket = true;
            text2.Text = "Today is " + DateTime.Now;
            toIconButton.IsEnabled = false;
            selectIconButton.IsEnabled = false;
            fromCal.Visibility = Visibility.Collapsed;
            toCal.Visibility = Visibility.Collapsed;
            selectCal.Visibility = Visibility.Collapsed;
        }
    }
```

In Listing 17.3, you can see that the MainPage class in the BookTicketCalendarAppCS application has a Boolean variable named checkTicket. The checkTicket variable is used to check the availability of tickets and is set to true to keep things simple in the application. In the MainPage constructor, the Text property of the text2 TextBlock control is set to DateTime.Today, that is, the current date. In addition, the IsEnabled property of the toIconButton and selectIconButton buttons is set to false to prevent users from clicking them. The Visibility property of the three Calendar controls, fromCal, toCal, and selectCal, is also set to Visibility.Collapsed. This implies that, initially, these Calendar controls appear collapsed or folded up.

- 4. Now, add the following code in the code-behind file, as shown in Listing 17.4, to complete the BookTicketCalendarAppCS application:

## Listing 17.4: Showing the Code for the Code-Behind File of the MainPage.xaml File of the BookTicketCalendarAppCS Application

```
private void fromIconClick(object sender, RoutedEventArgs e)
{
    fromCal.Visibility = Visibility.Visible;
    fromCal.DisplayDateStart = new DateTime(2010, 1, 1);
    fromCal.DisplayDateEnd = new DateTime(2011, 12, 31);
}

private void fromCalDateSelected(object sender, SelectionChangedEventArgs e)
{
    fromDateBox.Text = fromCal.SelectedDate.ToString();
    fromCal.Visibility = Visibility.Collapsed;
    toIconButton.IsEnabled = true;
}

private void toIconClick(object sender, RoutedEventArgs e)
{
```

```
toCal.Visibility = Visibility.Visible;
toCal.DisplayDateStart = fromCal.SelectedDate;
toCal.DisplayDateEnd = fromCal.DisplayDateEnd;
}

private void toCalDateSelected(object sender, SelectionChangedEventArgs e)
{
toDateBox.Text = toCal.SelectedDate.ToString();
toCal.Visibility = Visibility.Collapsed;
checkAvailability.IsEnabled = true;
}

private void isTicketAvailable(object sender, RoutedEventArgs e)
{
if (checkTicket == true)
selectIconButton.IsEnabled = true;
}

private void selectIconClick(object sender, RoutedEventArgs e)
{
selectCal.Visibility = Visibility.Visible;
selectCal.DisplayDateStart = fromCal.SelectedDate;
selectCal.DisplayDateEnd = toCal.SelectedDate;
}

private void selectCalDateSelected(object sender, SelectionChangedEventArgs e)
{
selectDateBox.Text = selectCal.SelectedDate.ToString();
selectCal.Visibility = Visibility.Collapsed;
confirmButton.IsEnabled = true;
}

private void confirmBooking(object sender, RoutedEventArgs e)
{
text3.Opacity = 0;
text4.Opacity = 0;
text5.Opacity = 0;
text6.Opacity = 0;
fromDateBox.Opacity = 0;
fromIconButton.Opacity = 0;
toDateBox.Opacity = 0;
toIconButton.Opacity = 0;
selectDateBox.Opacity = 0;
selectIconButton.Opacity = 0;
checkAvailability.Opacity = 0;
confirmButton.Opacity = 0;
text1.Text = "Thank You";
}
}
```

In Listing 17.4, when you click the fromIconButton button, the fromIconClick() method is called, and the fromCal calendar appears. The DisplayDateStart property of the fromCal Calendar control is set to a new instance of the DateTime class. This property is set to 2010.01.01 where 2010 is the year, which is followed by the month, and eventually by the day. Therefore, the first date that you can select in the fromCal calendar is 1st January 2010. Similarly, the DisplayDateEnd property of the fromCal calendar is set to 2011.12.31, which implies that the last date that you can select in the fromCal calendar is 31st December 2011. This implies that you can select a date from 1st January 2010 to 31st December 2011 only. When you select a date in the fromCal

calendar, the fromCalDateSelected() method is called, which is the handler for the SelectedDatesChanged event of the fromCal calendar control. When this method executes, the selected date in the calendar is assigned to the fromDateBox TextBox control. In addition, the fromCal calendar again folds up and the toIconButton button is enabled.

The toIconButton button has the toIconClick() method as its handler for the Click event. Therefore, when you click the toIconButton button, the toCal calendar appears. Note that the dates that are visible and selectable in the toCal calendar ranges between the selected date in the fromCal calendar and the last date displayed in the fromCal calendar. When users select a date in the toCal calendar, the selected date is displayed in the toDateBox TextBox control after which the toCal calendar collapses.

- 5. Check the availability of the tickets by clicking the Check Availability button, which is enabled when you select a date in the toCal calendar. In this case, the isTicketAvailable() method executes when you click the Check Availability button.

The TicketAvailable() method checks whether the checkTicket variable declared earlier in the code-behind file evaluates to true. As the checkTicket variable evaluates to true, the selectIconButton button now appears enabled. When you click the selectIconButton button, the selectCal calendar expands and allows you to select a date in the duration defined by the selected dates in the fromCal and toCal calendars. After you have selected the booking date, the selectCalDateSelected() method is called. This method is invoked to display the selected date in the selectDateBox text box, to hide the selectCal calendar, and to enable the confirmButton button. When you click the confirmButton button, some of the XAML elements of the Silverlight application are hidden by setting the Opacity property to zero and the text1 text block displays the Thank You message.

- 6. Press the F5 key on the keyboard to run the BookTicketCalendarAppCS application. The output appears, as shown in Figure 17.23:

![](img/e073a4882197be4ab61103cbe0bcb394_908_0.png)

Figure 17.23: Running the BookTicketCalendarAppCS Application

7. Click the Calendar button to see the calendar. The calendar appears, as shown in Figure 17.24:

![](img/e073a4882197be4ab61103cbe0bcb394_909_0.png)

# Figure 17.24: Displaying the Calendar

8. Click the desired month from the calendar, as shown in Figure 17.25:

![](img/e073a4882197be4ab61103cbe0bcb394_909_1.png)

# Figure 17.25: Selecting a Month in the Calendar

9. Select a desired date from the month you earlier selected. In this case, we selected date, July 11, 2010. As soon as you select a date, the toCal calendar is enabled. You can then select the date in the toCal calendar in the same manner, as shown in Figure 17.26:

![](img/e073a4882197be4ab61103cbe0bcb394_910_0.png)

# Figure 17.26: Selecting a Date from the toCal Calendar Control

After you select the date, July 11, 2010, from the fromCal calendar you can notice that the months before July and the dates before July 11, 2010 are not visible and therefore, not selectable in the toCal calendar. We have selected the date, November 16, 2010, in the toCal calendar. The selected date is displayed in the corresponding text box and the Check Availability button is enabled.

- 10. Click the Check Availability button and if the tickets are available, the selectCal calendar is enabled. Click the calendar icon to display the selectCal calendar and then select a date from the calendar (Figure 17.27).

- 11. Select a date for booking the ticket. In this case, we have selected the date, July 26, 2010, as shown in Figure 17.27:

![](img/e073a4882197be4ab61103cbe0bcb394_910_1.png)

# Figure 17.27: Selecting the Booking Date in the BookTicketCalendarAppCS Application
