
```
CultureInfo culture)
{
    throw new NotImplementedException();
}
}
```

code snippet BooksDemo/Utilities/Information.cs

In the XAML code, the StringArrayConverter class can be declared as a resource for referencing it from the Binding markup extension:

```
<UserControl x:Class="Wrox.ProcSharp.WPF.BooksUC"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:local="clr-namespace:Wrox.ProcSharp.WPF.Data"
    xmlns:utils="clr-namespace:Wrox.ProcSharp.WPF.Utilities"
    mc:Ignorable="d"
    d:DesignHeight="300" d:DesignWidth="300">
    <UserControl.Resources>
        <utils:StringArrayConverter x:Key="stringArrayConverter" />
        <ObjectDataProvider x:Key="books" ObjectType="{x:Type local:BookFactory}"
            MethodName="GetBooks" />
    </UserControl.Resources>
    <!-- -->
</UserControl>
```

code snippet BooksDemo/Books/UC.xaml

For multiline output, a TextBlock element is declared with the TextWrapping property set to Wrap to make it possible to display multiple authors. In the Binding markup extension the Path is set to Authors, which is defined as a property returning a string array. The string array is converted from the resource stringArrayConverter as defined by the Converter property. The Convert method of the converter implementation receives the ConverterParameter ',', as input to separate the authors:

```
<TextBlock Text="{Binding Authors,
    Converter={StaticResource stringArrayConverter},
    ConverterParameter=', '}"
    Grid.Row="1" Grid.Column="1" Margin="5"
    VerticalAlignment="Center" TextWrapping="Wrap" />
```

Figure 36-8 shows the book details, including authors.

![](img/d7d2ffa0a76feaab821930e95daace93_1113_0.png)

FIGURE 36-8

```
<Author>Morgan Skinner</Author>
</Book>
<Book isbn="978-0-7645-4182-1">
<Title>Beginning Visual C# 2008</Title>
<Publisher>Wrox Press</Publisher>
<Author>Karli Watson</Author>
<Author>David Espinosa</Author>
<Author>Zach Greenwoss</Author>
<Author>Jacob Hammer Pedersen</Author>
<Author>Christian Nagel</Author>
<Author>John D. Reid</Author>
<Author>Matthew Reynolds</Author>
<Author>Morgan Skinner</Author>
<Author>Eric White</Author>
</Book>
</Books>
```

code snippet XmlBindingDemo/Books.xml

Similarly to defining an object data provider, you can define an XML data provider. Both ObjectDataProvider and XmlDataProvider are derived from the same base class, DataSourceProvider. With the XmlDataProvider in the example, the Source property is set to reference the XML file books.xml. The XPath property defines an XPath expression to reference the XML root element Books. The Grid element references the XML data source with the DataContext property. With the data context for the grid, all Book elements are required for a list binding, so the XPath expression is set to Book. Inside the grid, you can find the ListBox element that binds to the default data context and uses the DataTemplate to include the title in TextBlock elements as items of the ListBox. Inside the grid, you can also see three Label elements with data binding set to XPath expressions to display the title, publisher, and ISBN numbers:

```
<Window x:Class="XmlBindingDemo.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="Main Window" Height="240" Width="500">
<Window.Resources>
<XmlDataProvider x:Key="books" Source="Books.xml" XPath="Books" />
<DataTemplate x:Key="listTemplate">
<TextBlock Text="{Binding XPath=Title}" />
</DataTemplate>

<Style x:Key="labelStyle" TargetType="{x:Type Label}">
<Setter Property="Width" Value="190" />
<Setter Property="Height" Value="40" />
<Setter Property="Margin" Value="5" />
</Style>
</Window.Resources>

<Grid DataContext="{Binding Source={StaticResource books}, XPath=Book}">
<Grid.RowDefinitions>
<RowDefinition />
<RowDefinition />
<RowDefinition />
<RowDefinition />
</Grid.RowDefinitions>
<Grid.ColumnDefinitions>
<ColumnDefinition />
<ColumnDefinition />
<ColumnDefinition />
</Grid.ColumnDefinitions>
<ListBox IsSynchronizedWithCurrentItem="True" Margin="5"
Grid.Column="0" Grid.RowSpan="4" ItemsSource="{Binding}"
ItemTemplate="{StaticResource listTemplate}" />

<Label Style="{StaticResource labelStyle}" Content="{Binding XPath=Title}"
Grid.Row="0" Grid.Column="1" />
<Label Style="{StaticResource labelStyle}" Content="{Binding XPath=Publisher}" Grid.Row="1" Grid.Column="1" />
<Label Style="{StaticResource labelStyle}" Content="{Binding XPath=@isbn}" Grid.Row="2" Grid.Column="1" />

</Grid>
</Window>
```

code snippet XmlBindingDemo/MainWindow.xaml

Figure 36-10 shows the result of the XML binding.

![](img/d7d2ffa0a76feaab821930e95daace93_1118_0.png)

FIGURE 36-10

> If XML data should be shown hierarchically, you can use the TreeView control.

## Binding Validation

Several options are available to validate data from the user before it is used with the .NET objects. These options are:

- Handling exceptions
- Data error information
- Custom validation rules

## Handling Exceptions

One of the options demonstrated here is that the .NET class throws an exception if an invalid value is set as shown in the class SomeData. The property Value1 accepts only values larger or equal to 5 and smaller than 12:

```
public class SomeData
{
    private int value1;
    public int Value1 {
        get
        {
            return value1;
        }
        set
        {
            if (value < 5 || value > 12)
                throw new ArgumentException(
                    "value must not be less than 5 or greater than 12");
            value1 = value;
        }
    }
}
```

code snippet ValidationDemo/SomeData.cs

In the constructor of the MainWindow class, a new object of the class SomeData is initialized and passed to the DataContext for data binding:

```
public partial class MainWindow: Window
{
    private SomeData p1 = new SomeData { Value1 = 11 };

    public MainWindow()
    {
        InitializeComponent();
        this.DataContext = p1;
    }
}
```

code snippet ValidationDemo/MainWindow.xaml.cs

The event handler method OnShowValue displays a message box to show the actual value of the SomeData instance:

```
private void OnShowValue(object sender, RoutedEventArgs e)
{
    MessageBox.Show(p1.Value1.ToString());
}
```

With simple data binding, here the Text property of a TextBox is bound to the Value1 property. If you run the application now and try to change the value to one that is not valid, you can verify that the value never changed by clicking the Submit button. WPF catches and ignores the exception thrown by the set accessor of the property Value1:

```
<Label Margin="5" Grid.Row="0" Grid.Column="0">Value1:</Label>
<TextBox Margin="5" Grid.Row="0" Grid.Column="1" Text="{Binding Path=Value1}" />
```

code snippet ValidationDemo/MainWindow.xaml

To display an error as soon as the context of the input changes, you can set the ValidatesOnExceptions property of the Binding markup extension to True. With an invalid value (as soon as the exception is thrown when the value should be set), the TextBox is surrounded by a red line, as shown in Figure 36-11.

```
<Label Margin="5" Grid.Row="0" Grid.Column="0">Value1:</Label>
<TextBox Margin="5" Grid.Row="0" Grid.Column="1" Text="{Binding Path=Value1, ValidatesOnExceptions=True}" />
```

![](img/d7d2ffa0a76feaab821930e95daace93_1119_0.png)

To return the error information in a different way to the user, you can assign the attached property ErrorTemplate that is defined by the Validation class to a template defining the UI for errors. The new template to mark the error is shown here with the key validationTemplate. The ControlTemplate puts a red exclamation point in front of the existing control content:

```
<ControlTemplate x:Key="validationTemplate">
    <DockPanel>
        <TextBlock Foreground="Red" FontSize="20">!</TextBlock>
        <AdornedElementPlaceholder/>
    </DockPanel>
</ControlTemplate>
```

Setting the validationTemplate with the Validation.ErrorTemplate attached property activates the template with the TextBox:

```
<Label Margin="5" Grid.Row="0" Grid.Column="0">Value1:</Label>
<TextBox Margin="5" Grid.Row="0" Grid.Column="1" Text="{Binding Path=Value1, ValidatesOnExceptions=True}" Validation.ErrorTemplate="{StaticResource validationTemplate}" />
```

The new look of the application is shown in Figure 36-12.

![](img/d7d2ffa0a76feaab821930e95daace93_1119_1.png)
