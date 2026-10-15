

## 代码清单 17.3：显示 MainPage.xaml 文件的代码隐藏文件代码

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

在代码清单 17.3 中，可以看到 BookTicketCalendarAppCS 应用程序中的 MainPage 类有一个名为 checkTicket 的 Boolean 变量。checkTicket 变量用于检查票务的可用性，并且在应用程序中被设置为 true 以简化操作。在 MainPage 构造函数中，text2 TextBlock 控件的 Text 属性被设置为 DateTime.Today，即当前日期。此外，toIconButton 和 selectIconButton 按钮的 IsEnabled 属性被设置为 false，以防止用户点击它们。三个 Calendar 控件 fromCal、toCal 和 selectCal 的 Visibility 属性也被设置为 Visibility.Collapsed。这意味着最初，这些 Calendar 控件处于折叠或收起状态。

- 4. 现在，如代码清单 17.4 所示，在代码隐藏文件中添加以下代码，以完成 BookTicketCalendarAppCS 应用程序：

## 代码清单 17.4：显示 BookTicketCalendarAppCS 应用程序的 MainPage.xaml 文件的代码隐藏文件代码

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

在代码清单 17.4 中，当你点击 fromIconButton 按钮时，会调用 fromIconClick() 方法，并且 fromCal 日历出现。fromCal Calendar 控件的 DisplayDateStart 属性被设置为 DateTime 类的新实例。该属性被设置为 2010.01.01，其中 2010 为年份，其后为月份，最后为日期。因此，你在 fromCal 日历中可以选择的第一个日期是 2010 年 1 月 1 日。同样，fromCal 日历的 DisplayDateEnd 属性被设置为 2011.12.31，这意味着你在 fromCal 日历中可以选择的最后一个日期是 2011 年 12 月 31 日。这意味着你只能选择从 2010 年 1 月 1 日到 2011 年 12 月 31 日之间的日期。当你在 fromCal

日历中选择一个日期时，会调用 fromCalDateSelected() 方法，该方法是从 fromCal 日历控件的 SelectedDatesChanged 事件的处理程序。当此方法执行时，日历中选择的日期会被分配给 fromDateBox TextBox 控件。此外，fromCal 日历再次折叠起来，并且 toIconButton 按钮被启用。

toIconButton 按钮的 Click 事件处理程序为 toIconClick() 方法。因此，当你点击 toIconButton 按钮时，toCal 日历会出现。请注意，toCal 日历中可见且可选择的日期范围在 fromCal 日历中选择的日期与 fromCal 日历中显示的最后日期之间。当用户在 toCal 日历中选择一个日期时，所选日期会显示在 toDateBox TextBox 控件中，之后 toCal 日历会折叠。

- 5. 通过点击 Check Availability 按钮来检查票务的可用性，该按钮在你在 toCal 日历中选择日期后会被启用。在这种情况下，当你点击 Check Availability 按钮时，isTicketAvailable() 方法会执行。

TicketAvailable() 方法检查代码隐藏文件中之前声明的 checkTicket 变量是否评估为 true。由于 checkTicket 变量评估为 true，selectIconButton 按钮现在显示为已启用。当你点击 selectIconButton 按钮时，selectCal 日历会展开并允许你在 fromCal 和 toCal 日历中选择的日期所定义的持续时间内选择一个日期。在你选择预订日期后，会调用 selectCalDateSelected() 方法。此方法被调用以在 selectDateBox 文本框中显示所选日期、隐藏 selectCal 日历并启用 confirmButton 按钮。当你点击 confirmButton 按钮时，Silverlight 应用程序的一些 XAML 元素会通过将 Opacity 属性设置为零而被隐藏，并且 text1 文本块会显示 Thank You 消息。

- 6. 按键盘上的 F5 键运行 BookTicketCalendarAppCS 应用程序。输出显示如下所示，如图 17.23 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_908_0.png)

图 17.23：运行 BookTicketCalendarAppCS 应用程序

7. 点击 Calendar 按钮以查看日历。日历显示如下所示，如图 17.24 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_909_0.png)

# 图 17.24：显示日历

8. 从日历中点击所需的月份，如图 17.25 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_909_1.png)

# 图 17.25：在日历中选择月份

9. 从你之前选择的月份中选择一个期望的日期。在此情况下，我们选择了日期 2010 年 7 月 11 日。一旦你选择一个日期，toCal 日历就会被启用。你可以以相同的方式在 toCal 日历中选择日期，如图 17.26 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_910_0.png)

# 图 17.26：从 toCal 日历控件中选择日期

在你从 fromCal 日历中选择日期 2010 年 7 月 11 日后，你会注意到 toCal 日历中 7 月之前的月份和 2010 年 7 月 11 日之前的日期不可见，因此不可选择。我们在 toCal 日历中选择了日期 2010 年 11 月 16 日。所选日期显示在相应的文本框中，并且 Check Availability 按钮被启用。

- 10. 点击 Check Availability 按钮，如果票务可用，则 selectCal 日历会被启用。点击日历图标以显示 selectCal 日历，然后从日历中选择一个日期（图 17.27）。

- 11. 选择预订票的日期。在此情况下，我们选择了日期 2010 年 7 月 26 日，如图 17.27 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_910_1.png)

# 图 17.27：在 BookTicketCalendarAppCS 应用程序中选择预订日期

