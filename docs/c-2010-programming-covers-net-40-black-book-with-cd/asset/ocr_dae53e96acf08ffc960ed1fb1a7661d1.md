```
System.Windows.Media.Visual
System.Windows.UIElement
System.Windows.FrameworkElement
System.Windows.Controls.Panel
System.Windows.Controls.VirtualizingPanel
System.Windows.Controls.VirtualizingStackPanel
```

You can add a VirtualizingStackPanel control to a WPF application by using the following code snippet:

```
<VirtualizingStackPanel>
<!--Child elements -->
</VirtualizingStackPanel>
```

Table 10.49 describes the noteworthy properties of the VirtualizingStackPanel class:

# Table 10.49: Noteworthy Properties of the VirtualizingStackPanel Class

| Property | Description |
|---|---|
| CanHorizontallyScroll | Retrieves or specifies a value that indicates whether a VirtualizingStackPanel can scroll in the horizontal dimension |
| CanVerticallyScroll | Retrieves or specifies a value that indicates whether content can scroll in the vertical direction |
| ExtentHeight | Retrieves a value that contains the vertical size of the extent |
| ExtentWidth | Retrieves a value that contains the horizontal size of the extent |
| HorizontalOffset | Retrieves a value that contains the horizontal offset of the scrolled content |
| ScrollOwner | Retrieves or specifies a value that identifies the container that controls the scrolling behavior in a VirtualizingStackPanel control |

The VirtualizingStackPanel control cannot be added from the Toolbox. You have to add this control in the application through the XAML code.

# The Calendar Control

The Calendar control of WPF is similar to the Calendar control of Windows Forms. This control allows you to select a date as well as to fire an event on the selection of the date. You can display the selected date on another control or validate the selected date. You can also customize the appearance of the Calendar control with the help of its Style property. The Calendar control also helps you to perform various tasks, such as specify the range of the date that is to be displayed by the Calendar control, select a specific range of date or multiple dates, and disable the selection of specific dates.

The inheritance hierarchy of the Calendar class is as follows:

```
System.Object
System.Windows.Threading.DispatcherObject
System.Windows.DependencyObject
System.Windows.Media.Visual
System.Windows.UIElement
System.Windows.FrameworkElement
System.Windows.Controls.Control
System.Windows.Controls.Calendar
```

You can add a Calendar control to a WPF application by using the following code snippet:

```
<sdk:Calendar .../>
```

Table 10.50 describes the noteworthy properties of the Calendar class:

# Table 10.50: Noteworthy Properties of the Calendar Class

| Property | Description |
|---|---|
| BlackoutDates | Retrieves a collection of dates that you do not want the user to select |
| DisplayDate | Retrieves or specifies the date to display on the Calendar control |