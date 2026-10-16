
list can change; thus you use the mode OneTime with data binding. For list updates, the source needs to implement INotifyCollectionChanged. You do this by using the ObservableCollection type for the books, as you’ve seen previously with the BooksService implementation. Selecting an item in the ListBox updates the SelectedBook property that in turn should make an update in the BookViewModel. The update of the other view model is currently missing because you need to implement a messaging mechanism that is shown later in this chapter in the section “Messaging Using Events.” For the display of every item in the ListBox, you use a DataTemplate where a TextBlock binds to the Title property of a Book:

```
<ListBox Grid.Row="1" ItemsSource="{Binding ViewModel.Books, Mode=OneTime}" SelectedItem="{Binding ViewModel.SelectedBook, Mode=TwoWay}">
    <ListBox.ItemTemplate>
        <DataTemplate>
            <StackPanel Orientation="Vertical">
                <TextBlock Text="{Binding Title, Mode=OneWay}" />
            </StackPanel>
        </DataTemplate>
    </ListBox.ItemTemplate>
</ListBox>
```

> NOTE XAML syntax is explained in Chapter 29. Styling XAML and data templates are covered in Chapter 30, “Styling XAML Apps.”

With the BookView there’s nothing special that hasn’t already been covered with the BooksView. Just note that the two TextBox controls are bound to the Title and Publisher properties of the Book, and the setting for the Mode is to TwoWay because the user should be able to change the values and update the Book source (code file BooksDesktopApp/Views/BookView.xaml):

```
<StackPanel Orientation="Horizontal">
    <Button Content="Save" Command="{Binding ViewModel.SaveBookCommand}" />
</StackPanel>
<StackPanel Orientation="Vertical" Grid.Row="1">
    <TextBox Text="{Binding ViewModel.Book.Title, Mode=TwoWay}" />
    <TextBox Text="{Binding ViewModel.Book.Publisher, Mode=TwoWay}" />
</StackPanel>
```

> NOTE The default mode of the binding differs between different technologies. For example, binding with the Text property of a TextBox element by default has TwoWay binding with WPF. Using the same property and element with compiled binding by default has the OneTime mode. To avoid confusion, it’s best to always define the mode explicitly.

> NOTE All the features of data binding with WPF are shown in Chapter 34, “Windows Desktop Applications with WPF.” WPF supports more binding options than the UWP has to offer. On the other side, the UWP offers compiled data binding that is not yet available with WPF. This chapter concentrates on data binding that can be easily converted between the traditional data binding used with the WPF sample and the compiled data binding with the UWP app sample.

With the current state of the application, you can run the WPF application and see the list of books populated after clicking the Load button. What’s not working yet is the filling of the BookView after selecting a book in the ListBox because the BookViewModel needs to be informed about the change. This will be done after the data binding for the UWP project is implemented in the section Messaging.

## Compiled Data Binding with UWP

With the UWP, you could use the same data binding as you use with WPF. However, the binding expression makes use of .NET reflection. Microsoft Office as well as several tools within Windows 10 make use of XAML, and the binding was too slow for the hundreds of controls used here. Setting properties directly is a lot faster. Setting the properties directly has the disadvantage that code sharing and unit testing cannot be implemented as easily as with the view models you’ve seen in this chapter. Because of this, the XAML team invented compiled data binding that is now available with the UWP but is not yet available with WPF.

When you’re using compiled data binding, you use the x:Bind markup extension instead of Binding. With the exception of the name of the markup extension element, comparing x:Bind and Binding looks very similar, as this code snippet shows:

```
<TextBox Text="{Binding ViewModel.Book.Title, Mode=TwoWay}" />
<TextBox Text="{x:Bind ViewModel.Book.Title, Mode=TwoWay}" />
```

Behind the scenes, the Text property of the TextBox is directly accessed, and the Title property from the book is retrieved on setting the TextBox. Besides being faster, compiled binding also has the advantage that you get compiler errors when you are not using the correct property names. With the traditional data binding, by default errors with binding are ignored, and you don’t see a result.

Let’s have a look at the XAML code of the BooksView. The DataContext doesn’t need to be set with compiled binding; it is not used. Instead, the binding always maps directly to the root element. That’s why in the WPF example the DataContext was set to the root element as well to make the bindings similar.

With the UserControl definition, some more .NET namespaces need to

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

## Messaging Using Events

With the current state of the application there’s the issue that the BookViewModel needs to update the current book when the book is selected with the BooksViewModel. To solve this, it is possible to define a contract where one view model invokes another one. However, this is a small scenario, and such notifications of other parts of the application will be needed in other places as well. Direct communication can become a nightmare very quickly.

One way to solve this is by using events. A generic EventAggregator is defined with the Framework project. This aggregator defines an event named Event where a handler of type Action<object, TEvent> can subscribe and unsubscribe, and a method Publish fires the event. This

aggregator is implemented as a *singleton* to make it easily accessible without needing to create an instance (code file `Framework/EventAggregator.cs`):

```
public class EventAggregator<TEvent>
    where TEvent: EventArgs
{
    private static EventAggregator<TEvent> s_eventAggregator;

    public static EventAggregator<TEvent> Instance =>
        s_eventAggregator ?? (s_eventAggregator = new
    EventAggregator<TEvent>());

    private EventAggregator()
    {
    }

    public event Action<object, TEvent> Event;

    public void Publish(object source, TEvent ev)
    {
        Event?.Invoke(source, ev);
    }
}
```

> **NOTE** *With a generic Singleton class, there’s not only one instance created; there’s one instance for every generic parameter type used. That’s fine for the `EventAggregator`, as different event types don’t need to share some data, and allows for better scalability.*

For passing the information about the book from the `BooksViewModel` to the `BooksView`, just the book identifier is needed, and thus the `BookInfoEvent` class is defined (code file `Contracts/Events/BookInfoEvent.cs`):

```
public class BookInfoEvent: EventArgs
{
    public int BookId { get; set; }
}
```

The `BookViewModel` can now subscribe to the event. With the constructor of the `BookViewModel`, the static member `Instance` is accessed to get the singleton object of the `BookInfoEvent` type, and the `LoadBook` handler method is assigned to the event `Event`. Within the handler method, the book with the requested ID is retrieved via the books service (code file `ViewModels/BookViewModel.cs`):

```
public class BookViewModel : ViewModelBase, IDisposable
{
    private IBooksService _booksService;
    public BookViewModel(IBooksService booksService)
    {
        _booksService = booksService;

        SaveBookCommand = new DelegateCommand(OnSaveBook);

        EventAggregator<BookInfoEvent>.Instance.Event += LoadBook;
    }
}
```
