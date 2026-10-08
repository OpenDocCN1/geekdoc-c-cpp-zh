
# LISTING 8-7 (continued)

```c
{
  if (PropertyChanged != null)
    PropertyChanged(this, new PropertyChangedEventArgs(propertyName));
  }

  public DateTime CurrentTime
{
    get { return DateTime.Now; }
  }

  public event PropertyEventHandler PropertyChanged;
}
```

Code file [ViewModel.cs] available for download at Wrox.

At first, the Clock sample application seems to be a bit overcomplicated. After all, you could have simply created a timer in the code-behind, and updated the context of the TextBlock whenever the timer fires. However, with complex master-detail relationships and multiple objects, the advantages of the separate data object and data binding become obvious.

> There is also a popular architecture pattern, called Model-View-ViewModel (MVVM) that relies heavily on data binding. MVVM allows for UI logic testing and complete separation of the UI and the application logic. Discussing MVVM in depth is beyond the scope of this book. If you are planning to develop serious applications with Silverlight or WPF, you should definitely get yourself acquainted with the pattern.

Using XAML is how we describe an object hierarchy; Here, you use XAML feature to create an instance of the ClockViewModel class, and assign it to the DataContext property of the UserControl. The XML namespace local refers to the assembly that contains the ClockViewModel. When the XAML is executed by the Silverlight runtime, the ClockViewModel object is created, which, in turn, starts its timer.

The Data property is inherited down the visual tree (but it can be changed on any element). This means that the LayoutRoot grid and all children have their DataContext set to the same ClockViewModel instance. The DataContext is also inherited by the TextBlock that is used to display the time.

The Text property of the TextBlock contains a data binding: Text="Binding Path=CurrentTime"; This connects the Text property to the CurrentTime property of the DataContext. At every tick of the timer, the PropertyChanged event is fired. The INotifyPropertyChanged interface (which only defines the PropertyChanged event) is how Silverlight run-time learns changes in the data binding source. Firing the PropertyChanged event instructs the Silverlight run-time to update all properties that have been bound to the data object in question. From this point, the display is automatic and handled by the Silverlight run-time.

The Binding' clause has several additional options to make data binding more powerful. Some of the most important ones:

- Converter: This allows you to create custom display logic and to convert any entered data to something a backing field more easily. (For example, if you want to display and enter a property of size "24x48" in a TextBox, you can implement the IValueConverter and write the code.)
- Mode: This can be set to OneTime (does not further updates), OneWay (default), and TwoWay.
- Source: This specifies the data source for the binding. Source can be omitted, and in this case, the DataContext will be the source object, just like the Clock sample.
- Path: This can be omitted shorthand. The binding expression in the Clock sample can also be written as Text="{Binding CurrentTime}".

# Data Binding Between Two Elements

You can bind two UI elements. Here is a small sample that binds a TextBox to a Slider:

```xml
<Slider HorizontalAlignment="Center" xName="slider1" Width="100"
  Margin="0,109,0,0" VerticalAlignment="Top" />
<TextBox HorizontalAlignment="Center" VerticalAlignment="Center"
  Binding="Path=Value, Mode=TwoWay, ElementName=slider1, ValidatesOnError=True" Width="40" />
```

As you can see, you move the Slider, and the TextBox automatically updates. Similarly, you can enter a number in the TextBox, and the Slider updates. This automatic binding is done via dependency properties instead of the INotifyPropertyChanged interface, which is used for business objects. Dependency properties are essentially control properties that can participate in data binding, styling, and animation, and are managed by the Silverlight (or WPF) run-time.

The binding is triggered when the TextBox loses focus. You can use the Tab key for this.) The input controls in Silverlight are prepared to display validation errors. If the value entered in the TextBox is invalid (for example, it contains an exception) an exception will be raised. Use the ValidatesOnExceptions property of the Binding to True, the exception actually appears as a user-friendly notification, as shown in Figure 8-15. Further binding validation options include ValidatesOnDataErrors and ValidatesOnNotifyErrors.

![](img/b5597c749e848b27b0d305153ae1610_366_0.png)

FIGURE 8-15: TextBox showing a Validation Error

# Data Binding to a List of Objects

Most of the time, the task is to display multiple objects at the same time — for example, in a ListBox, DataGrid, or even a DropDownList. Suppose the application has to list the authors of this book. The Author object is very simple:

```c
public class Author
{
    public string Name { get; set; }
    public string Chapters { get; set; }
}
```

To display a list of Author objects in DataGrid, simply declare a DataGrid in XAML:

```xml
<DataGrid Name="myGrid" />
```

And, in the code-behind, assign the ItemsSource property of the DataGrid like:

```csharp
myGrid.ItemsSource = authors;
```

If authors is of type IEnumerable<Author> (or something similar, like List<Author>), and it has any data, the objects will be displayed as shown in Figure 8-16.

![](img/b5597c749e848b27b0d305153ae161_367_0.png)

FIGURE 8-16: Displaying Authors in DataGrid
