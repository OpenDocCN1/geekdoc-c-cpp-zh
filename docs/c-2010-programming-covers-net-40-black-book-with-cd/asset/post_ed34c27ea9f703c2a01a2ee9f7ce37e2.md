
The inheritance hierarchy of the Button class is as follows:

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Media.Visual
        System.Windows.UIElement
          System.Windows.FrameworkElement
            System.Windows.Controls.Control
              System.Windows.Controls.ContentControl
                System.Windows.Controls.Primitives.ButtonBase
                  System.Windows.Controls.Button
```

You can add a Button control to a WPF application by using the following code snippet:

```
<Button>
  <!-- Content -->
</Button>
```

Table 10.17: Showing the Noteworthy Properties of the Button Class

| Property | Description |
|---|---|
| IsCancel | Gets or sets a value that indicates whether a button is a Cancel button |
| IsDefault | Gets or sets a value that indicates whether a button is the Default button |
| IsDefaulted | Retrieves a value to activate a Button control at the time of pressing the ENTER key |

Figure 10.13 shows the Button control added to a WPF application:

![](img/e073a4882197be4ab61103cbe0bcb394_425_0.png)

Figure 10.13: Showing the Button Control

## The Label Control

The Label control in WPF is similar to the Label control of Windows Forms, the only difference being that the Label control in a WPF application can contain text or other controls in it. The Label control allows you to add as well as display the text in the Design view.

The Label control in WPF also provides support for access keys. You can access a Label control by pressing the appropriate access keys from the keyboard. This control is generally used to set the Target property of a control.

The inheritance hierarchy of the Label class is as follows:

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Media.Visual
        System.Windows.UIElement
          System.Windows.FrameworkElement
            System.Windows.Controls.Control
              System.Windows.Controls.ContentControl
                System.Windows.Controls.Label
```

You can add a Label control to a WPF application by using the following code snippet:

```
<Label>
  <!-- Content -->
</Label>
```

Table 10.18: Showing the Noteworthy Property of the Label Class

| Property | Description |
|---|---|
| Target | Gets or sets a control that receives focus when the user presses the Label control access key |

Figure 10.14 shows the Label control added to a WPF application:

![](img/e073a4882197be4ab61103cbe0bcb394_426_0.png)

Figure 10.14: Showing the Label Control

## The RadioButton Control

The RadioButton control in WPF is used to select an option from a given list of options. The functioning of the RadioButton control in WPF and Windows Forms is similar. You can select only one RadioButton control at a time. A RadioButton control can be selected but not cleared. You can clear the RadioButton control only when you select another RadioButton control on the window.

The inheritance hierarchy of the RadioButton class is as follows:

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Media.Visual
        System.Windows.UIElement
          System.Windows.FrameworkElement
            System.Windows.Controls.Control
              System.Windows.Controls.ContentControl
                System.Windows.Controls.Primitives.ButtonBase
                  System.Windows.Controls.Primitives.ToggleButton
                    System.Windows.Controls.RadioButton
```

You can add a RadioButton control to a WPF application by using the following code snippet:

```
<RadioButton>
<!-- Content -->
</RadioButton>
```

Table 10.19: Showing the Noteworthy Property of the RadioButton Class

| Property | Description |
|---|---|
| GroupName | Gets or sets the name that specifies which controls are mutually exclusive |

Figure 10.15 shows the RadioButton control added to a WPF application:

![](img/e073a4882197be4ab61103cbe0bcb394_427_0.png)

## The CheckBox Control

In WPF, the CheckBox control represents the options that a user can select or clear. You can use a single CheckBox control or group multiple CheckBox controls. The CheckBox control in a WPF application and Windows Forms is the same. The CheckBox control is inherited from the ToggleButton class and can have three states: Checked, Unchecked, and Indeterminate.

The inheritance hierarchy of the CheckBox class is as follows:

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Media.Visual
        System.Windows.UIElement
          System.Windows.FrameworkElement
            System.Windows.Controls.Control
              System.Windows.Controls.ContentControl
                System.Windows.Controls.Primitives.ButtonBase
                  System.Windows.Controls.Primitives.ToggleButton
                    System.Windows.Controls.CheckBox
```

You can add a CheckBox control to a WPF application by using the following code snippet:

```
<CheckBox>
<!-- Content -->
</CheckBox>
```

There are no noteworthy properties of the CheckBox control.

Figure 10.16 shows the CheckBox control added to a WPF application:

![](img/e073a4882197be4ab61103cbe0bcb394_428_0.png)

Figure 10.16: Showing the CheckBox Control

## The ListBoxItem Control

The ListBoxItem control represents a selectable item in the ListBox control. The ListBox control contains a collection of ListBoxItem objects. You need to set the IsSelected property of the ListBoxItem control to True to select an item in the ListBox control. You can also bind a ListBoxItem control to a data source by using the ItemsSourceProperty property of the control. You can also set the horizontal and vertical alignment of the ListBoxItem control.

The ListBoxItem control is represented by the ListBoxItem class. The inheritance hierarchy of the ListBoxItem class is as follows:

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Media.Visual
        System.Windows.UIElement
          System.Windows.FrameworkElement
            System.Windows.Controls.Control
              System.Windows.Controls.ContentControl
                System.Windows.Controls.ListBoxItem
```

You can add a ListBoxItem control to a WPF application by using the following code snippet:

```
<ListBoxItem>
    <!--Content-->
</ListBoxItem>
```

Table 10.20: Showing the Noteworthy Property of the ListBoxItem Class

| Property | Description |
|---|---|
| IsSelected | Gets or sets a value that indicates whether a control is selected |

The ListBoxItem control is not available in the Toolbox and has to be added through the XAML code.

## The StatusBarItem Control

The StatusBarItem control in WPF represents an item of the StatusBar control. The Items and ItemsSource properties are used to add content to the StatusBarItem control. The StatusBarItem control defines items in the StatusBar control. The StatusBarItem control can contain complex content, such as graphics.

The inheritance hierarchy of the StatusBarItem class is as follows:

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Media.Visual
        System.Windows.UIElement
          System.Windows.FrameworkElement
            System.Windows.Controls.Control
              System.Windows.Controls.ContentControl
                System.Windows.Controls.Primitives.StatusBarItem
```

You can add the StatusBarItem control to a WPF application by using the following code snippet:

```
<StatusBarItem>
<!--Content-->
</StatusBarItem>
```

There are no noteworthy properties of the StatusBarItem control.

You cannot add the StatusBarItem control from the Toolbox. The control has to be added in the application through the XAML code.

## The ScrollViewer Control

The ScrollViewer control represents a scrollable area that can contain other visible elements. This control provides a convenient way to enable scrolling of content in a WPF application when the content in the UI is larger than the display area. There are basically two types of scrolling: physical scrolling and logical scrolling. Physical scrolling is used to scroll the content by physical increment, typically by value, which is declared in pixels. Logical scrolling is used to scroll to the next item in the logical tree of elements. Physical scrolling is the default behavior of the ScrollViewer control.

The ScrollViewer control is represented by the ScrollViewer class. The inheritance hierarchy of the ScrollViewer class is as follows:

```
System.Object
System.Windows.Threading.DispatcherObject
System.Windows.DependencyObject
System.Windows.Media.Visual
System.Windows.UIElement
System.Windows.FrameworkElement
System.Windows.Controls.Control
System.Windows.Controls.ContentControl
System.Windows.Controls.ScrollViewer
```

You can add a ScrollViewer control to your WPF application by using the following code snippet:

```
<ScrollViewer>
<!--Content-->
</ScrollViewer>
```

Table 10.21: Showing the Noteworthy Properties of the ScrollViewer Class

| Property | Description |
|---|---|
| ComputedHorizontalScrollBarVisibility | Retrieves a value that indicates whether the horizontal ScrollBar control is visible |
| ComputedVerticalScrollBarVisibility | Retrieves a value that indicates whether the vertical ScrollBar control is visible |
| ExtentHeight | Retrieves a value that contains the vertical size of the content on the control |
| ExtentWidth | Retrieves a value that contains the horizontal size of the content on the control |
| ScrollableHeight | Retrieves a value that represents the vertical size of the content control that can be scrolled |
| ScrollableWidth | Retrieves a value that represents the horizontal size of the content control that can be scrolled |
| HorizontalScrollBarVisibility | Gets or sets a value that indicates whether a horizontal ScrollBar control should be displayed |
| VerticalScrollBarVisibility | Gets or sets a value that indicates whether a vertical ScrollBar control should be displayed |
