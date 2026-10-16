
> **NOTE** Attached properties are explained in Chapter 29, “Core XAML.” More information about the Canvas element is in Chapter 34, “Windows Desktop Applications with WPF.”

The constructor of the MainPage initializes the Accelerometer and requests continuous reading with the minimum interval. To know the boundaries of the window, with the LayoutUpdated event of the page, MaxX and MaxY are set to the width and height of the window minus the size of the ellipse (code file RollingMarble/MainPage.xaml.cs):

```csharp
public sealed partial class MainPage : Page
{
    private Accelerometer _accelerometer;
    private double MinX = 0;
    private double MinY = 0;
    private double MaxX = 1000;
    private double MaxY = 600;
    private double currentX = 0;
    private double currentY = 0;

    public MainPage()
    {
        this.InitializeComponent();
        _accelerometer = Accelerometer.GetDefault();
        _accelerometer.ReportInterval = _accelerometer.MinimumReportInterval;
        _accelerometer.ReadingChanged += OnAccelerometerReading;
        this.DataContext = this;

        this.LayoutUpdated += (sender, e) =>
        {
            MaxX = this.ActualWidth - 100;
            MaxY = this.ActualHeight - 100;
        };
    }
}
```

With every value received from the accelerometer, the ellipse is moved within the Canvas element in the event handler method OnAccelerometerReading. Before the value is set, it is checked according to the boundaries of the window:

```csharp
private async void OnAccelerometerReading(Accelerometer sender, AccelerometerReadingChangedEventArgs args)
{
    currentX += args.Reading.AccelerationX * 80;
    if (currentX < MinX) currentX = MinX;
    if (currentX > MaxX) currentX = MaxX;

    currentY += -args.Reading.AccelerationY * 80;
    if (currentY < MinY) currentY = MinY;
    if (currentY > MaxY) currentY = MaxY;

    await this.Dispatcher.RunAsync(CoreDispatcherPriority.High, () =>
    {
        Canvas.SetLeft(ell1, currentX);
        Canvas.SetTop(ell1, currentY);
    });
}
```

## 34 Windows Desktop Applications with WPF

### What’s In This Chapter?

- WPF Controls
- Layout
- Triggers
- Menu and ribbon controls
- Using commanding for input handling
- Data binding to elements, objects, lists, and XML
- Value conversions and validation
- Using the `TreeView` to display hierarchical data
- Displaying and grouping data with the `DataGrid`
- Live shaping with the `CollectionViewSource`

### Wrox.com Code Downloads for This Chapter

The wrox.com code downloads for this chapter are found at www.wrox.com/go/professionalcsharp6 on the Download Code tab. The code for this chapter is divided into the following major examples:

- Controls Sample
- Layout Sample
- Trigger Sample
- Books
- Multi Binding Sample
- Priority Binding Sample
- XML Binding Sample
- Validation Sample
- Formula-1
- Live Shaping

### Introduction

In Chapter 29, “Core XAML,” and Chapter 30, “Styling XAML Apps,” you read about some of the core features of XAML. This chapter continues the journey through XAML using it from WPF. Here you read about important aspects for the control hierarchy, creating complete applications, using data binding and command handling, and using the `DataGrid` control. Data binding is an important concept for bringing data from .NET classes into the user interface and allowing the user to change data. WPF not only allows binding to simple entities or lists, but it also offers binding of one UI property to multiple properties of possible different types with multibinding and priority binding that are discussed in this chapter as well. It is also important to validate data entered by a user. Here, you can read about different ways to handle validation, including the interface `INotifyDataErrorInfo` that is new since .NET 4.5. Also covered in this chapter is commanding, which enables mapping events from the UI to code. In contrast to the event model, this provides a better separation between XAML and code. This chapter covers using predefined commands and creating custom commands.

The `TreeView` and `DataGrid` controls are UI controls to display bound data. This chapter explains using the `TreeView` control to display data in the tree where data is loaded dynamically depending on what the user selects. With the `DataGrid` control you find out how to use filtering, sorting, and grouping, as well as one new .NET 4.5 feature named *live shaping* that allows changing sorting or filtering options in real time.

To begin, let’s start with the `Menu` and the `Ribbon` controls. The `Ribbon` control made it into the release of .NET 4.5.

### Controls

Because you can use hundreds of controls with WPF, they are categorized into groups, each of which is described in the following sections.

#### Simple Controls

Simple controls are controls that don’t have a `Content` property. The `Button` class has come up in other chapters, where you have seen that the `Button` can contain any shape or any element you like. This is not possible with simple controls. The following table describes the simple controls.

| Simple Control | Description |
|---|---|
| TextBox | This control is used to display simple, unformatted text. |
| RichTextBox | This control supports rich text with the help of the FlowDocument class. RichTextBox and TextBox are derived from the same base class—TextBoxBase. |
| Calendar | This control displays a month, year, or decade. The user can select a date or range of dates. |
| DatePicker | This control opens a calendar onscreen for date selection by the user. |
| PasswordBox | This control is used to enter a password. It has specific properties for password input, such as PasswordChar, to define the character that should be displayed as the user enters the password, or Password, to access the password entered. The PasswordChanged event is invoked as soon as the password is changed. |
| ScrollBar | This control contains a Thumb that enables the user to select a value. A scrollbar can be used, for example, if a document doesn’t fit on the screen. Some controls contain scrollbars that are displayed if the content is too big. |
| ProgressBar | This control indicates the progress of a lengthy operation. |
| Slider | This control enables users to select a range of values by moving a Thumb. ScrollBar, ProgressBar, and Slider are derived from the same base class—RangeBase. |

> **NOTE** *Although simple controls do not have a `Content` property, you can completely customize the look of a control by defining a template. Templates are discussed later in this chapter in the section “Templates.”*

#### Content Controls

A `ContentControl` has a `Content` property, with which you can add any content to the control. The `Button` class derives from the base class `ContentControl`, so you can add any content to this control. In a previous example, you saw a `Canvas` control within the `Button`. Content controls are described in the following table.

| Content Control | Description |
|---|---|
| Button, RepeatButton, ToggleButton, CheckBox, RadioButton | The classes `Button`, `RepeatButton`, `ToggleButton`, and `GridViewColumnHeader` are derived from the same base class—`ButtonBase`. All buttons react to the `Click` event. `RepeatButton` raises the `Click` event repeatedly until the button is released. `ToggleButton` is the base class for `CheckBox` and `RadioButton`. These buttons have an on and off state. The `CheckBox` can be selected and cleared by the user; the `RadioButton` can be selected by the user. Clearing the `RadioButton` must be done programmatically. |
| Label | The `Label` class represents the text label for a control. This class also has support for access keys—for example, a menu command. |
| Frame | The `Frame` control supports navigation. You can navigate to a page’s content with the `Navigate` method. If the content is a web page, then the `WebBrowser` control is used for display. |
| ListBoxItem | An item inside a `ListBox` control. |
| StatusBarItem | An item inside a `StatusBar` control. |
| ScrollViewer | A content control that includes scrollbars. You can put any content in this control; the scrollbars are displayed as needed. |
| ToolTip | Creates a pop-up window to display additional information for a control. |
| UserControl | Using this class as a base class provides a simple way to create custom controls. However, the `UserControl` base class does not support templates. |
| Window | This class enables you to create windows and dialogs. It includes a frame with minimize/maximize/close buttons and a system menu. When showing a dialog, you can use the `ShowDialog` method; the `Show` method opens a window. |
| NavigationWindow | This class derives from the `Window` class and supports content navigation. |

Only a `Frame` control is contained within the `Window` of the following XAML code. The `Source` property is set to http://www.cninnovation.com, so the `Frame` control navigates to this website, as shown in Figure 34.1 (code file ControlsSample/FramesWindow.xaml):

```xml
<Window x:Class="ControlsSamples.FramesWindow"
```
