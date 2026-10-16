
<Window x:Class="TriggerSamples.MultiTriggerWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="Multi Trigger" Height="300" Width="300">
<Window.Resources>
    <Style TargetType="TextBox">
        <Style.Triggers>
            <MultiTrigger>
                <MultiTrigger.Conditions>
                    <Condition Property="IsEnabled" Value="True" />
                    <Condition Property="Text" Value="Test" />
                </MultiTrigger.Conditions>
                <MultiTrigger.Setters>
                    <Setter Property="Foreground" Value="Red" />
                </MultiTrigger.Setters>
            </MultiTrigger>
        </Style.Triggers>
    </Style>
</Window.Resources>
<Grid>
    <TextBox />
</Grid>
</Window>

## Data Triggers

Data triggers fire if bound data to a control fulfills specific conditions. In the following example, a Book class is used that has different displays depending on the publisher of the book.

The Book class defines the properties Title and Publisher and has an overload of the ToString method (code file TriggerSamples/Book.cs):

```
public class Book
{
    public string Title { get; set; }
    public string Publisher { get; set; }

    public override string ToString() => Title;
}
```

In the XAML code, a style is defined for ListBoxItem elements. The style contains DataTrigger elements that are bound to the Publisher property of the class that is used with the items. If the value of the Publisher property is Wrox Press, the Background is set to Red. With the publishers Dummies and Wiley, the Background is set to Yellow and DarkGray, respectively (code file TriggerSamples/DataTriggerWindow.xaml):

```
<Window x:Class="TriggerSamples.DataTriggerWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="Data Trigger" Height="300" Width="300">
<Window.Resources>
    <Style TargetType="ListBoxItem">
        <Style.Triggers>
            <DataTrigger Binding="{Binding Publisher}" Value="Wrox Press">
        <Setter Property="Background" Value="Red" />
    </DataTrigger>
    <DataTrigger Binding="{Binding Publisher}"
Value="Dummies">
        <Setter Property="Background" Value="Yellow" />
    </DataTrigger>
    <DataTrigger Binding="{Binding Publisher}"
Value="Wiley">
        <Setter Property="Background" Value="DarkGray" />
    </DataTrigger>
</Style.Triggers>
</Style>
</Window.Resources>
<Grid>
    <ListBox x:Name="list1" />
</Grid>
</Window>
```

In the code-behind, the list with the name `list1` is initialized to contain several `Book` objects (code file `TriggerSamples/DataTriggerWindow.xaml.cs`):

```
public DataTriggerWindow()
{
    InitializeComponent();

    list1.Items.Add(new Book
    {
        Title = "Professional C# 6 and .NET Core 1.0",
        Publisher = "Wrox Press"
    });
    list1.Items.Add(new Book
    {
        Title = "C# 5 All-in-One for Dummies",
        Publisher = "For Dummies"
    });
    list1.Items.Add(new Book
    {
        Title = "HTML and CSS: Design and Build Websites",
        Publisher = "Wiley"
    });
}
```

When you run the application, the `ListBoxItem` elements are formatted according to the publisher value, as shown in [Figure 34.11](#).

![](img/3d365b72b289213a91ade7eb366b8f35_1314_0.png)

## Figure 34.11

With DataTrigger, multiple properties must be set for MultiDataTrigger (similar to Trigger and MultiTrigger).

> NOTE Data triggers update the user interface when the data bound changes (in case the interface INotifyPropertyChanged is implemented). The “Live Shaping” section later in this chapter includes an example.

## Menu and Ribbon Controls

Many data-driven applications contain menus and toolbars or ribbon controls to enable users to control actions. As of WPF 4.5, ribbon controls are available as well, so both menu and ribbon controls are covered here.

In this section, you create two new WPF applications named BooksDemoMenu and BooksDemoRibbon and the library BooksDemoLib to use throughout this chapter—not only with menu and ribbon controls but also with commanding and data binding. This application displays a single book, a list of books, and a grid of books. Actions are started from menu or ribbon controls to which commands are associated.

## Menu Controls

You can easily create menus with WPF using the Menu and MenuItem elements, as shown in the following code snippet that contains two main menu items, File and Edit, and a list of submenu entries. The _ in front of the characters marks the special character that users can employ to access the menu item easily without using the mouse. Using the Alt key makes these characters visible and enables access to the menu with this character. Some of these menu items have a command assigned, as discussed in the next section (code file BooksDemoMenu/MainWindow.xaml):

```
<Window x:Class="Wrox.ProCSharp.WPF.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="clr-namespace:BooksDemo"
    Title="Books Demo App" Height="400" Width="600">
<DockPanel>
    <Menu DockPanel.Dock="Top">
        <MenuItem Header="_File">
            <MenuItem Header="Show _Book" />
            <MenuItem Header="Show Book_s" />
            <Separator />
            <MenuItem Header="E_xit" />
        </MenuItem>
        <MenuItem Header="_Edit">
            <MenuItem Header="Undo" Command="Undo" />
            <Separator />
            <MenuItem Header="Cut" Command="Cut" />
            <MenuItem Header="Copy" Command="Copy" />
            <MenuItem Header="Paste" Command="Paste" />
        </MenuItem>
    </Menu>
</DockPanel>
</Window>
```

Running the application results in the menus shown in Figure 34.12. The menus are not active yet because commands are not active.

![](img/3d365b72b289213a91ade7eb366b8f35_1316_0.png)

Figure 34.12

## Ribbon Controls

An alternative to the menu controls are the ribbon controls. Microsoft Office 2007 was the first application released with Microsoft’s ribbon control. Shortly after its introduction, many users of previous versions of Office complained that they could not find the actions they wanted with the new UI. Users who hadn’t used Office prior to Office 2007 had a better experience with the new UI; they were able to easily find actions that users of previous versions found hard to detect.

Of course, nowadays the ribbon control is very common in many applications. Since Windows 8, the ribbon has been in many tools delivered with the Windows operating system—for example, Windows Explorer, Paint, and WordPad.

The WPF ribbon control is in the namespace

```
System.Windows.Controls.Ribbon
```

and requires referencing the assembly

```
System.Windows.Controls.Ribbon.
```

Figure 34.13 shows the ribbon control of the sample application. In the topmost line left of the window title is the quick access toolbar. The leftmost item in the second line is the application menu, followed by two ribbon tabs: Home and Ribbon Controls. The Home tab, which is selected, shows two groups: Clipboard and Show. Both of these groups contain some button controls.

![](img/3d365b72b289213a91ade7eb366b8f35_1317_0.png)

**Figure 34.13**

The `Ribbon` control is defined in the following code snippet. The first children of the `Ribbon` element are defined by the `QuickAccessToolBar` property. This toolbar contains two `RibbonButton` controls with small images referenced. These buttons provide users with direct access to quickly and easily fulfill actions (code file `BooksDemoRibbon/MainWindow.xaml`):

```xml
<Ribbon DockPanel.Dock="Top">
  <Ribbon.QuickAccessToolBar>
    <RibbonQuickAccessToolBar>
      <RibbonButton SmallImageSource="Assets/one.png" />
      <RibbonButton SmallImageSource="Assets/list.png" />
    </RibbonQuickAccessToolBar>
  </Ribbon.QuickAccessToolBar>
  <!-- etc. -->
</Ribbon>
```

To get these buttons from the quick access toolbar directly to the chrome of the window, the base class needs to be changed to the `RibbonWindow` class instead of the `Window` class (code file `BooksDemoRibbon/MainWindow.xaml.cs`):

```csharp
public partial class MainWindow : RibbonWindow
{
```
```

Changing the base class with the code-behind also requires a change in the XAML code to use the `RibbonWindow` element:

```xml
<RibbonWindow x:Class="Wrox.ProCSharp.WPF.MainWindow"

    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"

             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             xmlns:local="clr-namespace:Wrox.ProCSharp.WPF"
             Title="Books Demo App" Height="400" Width="600">
```

The application menu is defined by using the `ApplicationMenu` property. The application menu defines two menu entries—the first one to show a book, the second one to close the application:

```xml
<Ribbon.ApplicationMenu>
  <RibbonApplicationMenu SmallImageSource="Assets/books.png">
```
