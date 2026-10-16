```
public object Convert(object value,
    Type targetType,
    object parameter,
    string language) => value;

public object ConvertBack(object value,
    Type targetType,
    object parameter,
    string language) => value;
}
```

Using the resources of the user control, the ObjectToObjectConverter is instantiated with the same name as the key to reference the converter using the StaticResource markup extension with ItemsSource binding in the ListBox shown earlier (code file BooksUniversalApp/Views/BooksView.xaml):

```
<UserControl.Resources>
    <conv:ObjectToObjectConverter x:Key="ObjectToObjectConverter" />
</UserControl.Resources>
```

Another difference with the compiled binding is with the data template. Binding the Text property of the TextBlock to the Title property of the Book, the Book needs to be known. For this, the x:DataType was added to the DataTemplate element:

```
<ListBox.ItemTemplate>
    <DataTemplate x:DataType="model:Book">
        <StackPanel Orientation="Vertical">
            <TextBlock Text="{x:Bind Title, Mode=OneWay}" />
        </StackPanel>
    </DataTemplate>
</ListBox.ItemTemplate>
```

With the compiled data binding in place, the UWP app is in the same state as the WPF application.

> NOTE Compiled binding is also used in Chapter 32 and Chapter 33, “Advanced Windows Apps.”

# Messaging Using Events

With the current state of the application there’s the issue that the BookViewModel needs to update the current book when the book is selected with the BooksViewModel. To solve this, it is possible to define a contract where one view model invokes another one. However, this is a small scenario, and such notifications of other parts of the application will be needed in other places as well. Direct communication can become a nightmare very quickly.

One way to solve this is by using events. A generic EventAggregator is defined with the Framework project. This aggregator defines an event named Event where a handler of type Action<object, TEvent> can subscribe and unsubscribe, and a method Publish fires the event. This