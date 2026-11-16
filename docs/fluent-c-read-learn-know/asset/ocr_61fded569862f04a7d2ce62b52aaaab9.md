![](bbox=[0.09, 0.05, 0.2, 0.21])

# HOW'D YOU DO?

I asked you to implement sorting either in XAML or code. Here's the version if you chose an all-XAML approach:

```
<Window x:Class="_20app02__Binding_Collections.MainWindow"
    ...
    xmlns:src="clr-namespace:_20app02__Binding_Collections"
    xmlns:scm="clr-namespace:System.ComponentModel;assembly=WindowsBase"
    ...>
    <Window.Resources>
    <src:CountToItemConverter x:Key="ItemsConverter" />
    <src:SampleIngredients x:Key="ResourceIngredients" />
    <CollectionViewSource Source="{StaticResource ResourceIngredients}"
        x:Key="cvs">
    <CollectionViewSource.SortDescriptions>
    <scm:SortDescription PropertyName="Name" Direction="Ascending" />
    </CollectionViewSource.SortDescriptions>
    </CollectionViewSource>
    </Window.Resources>
    <Window.DataContext>
    <StaticResource ResourceKey="cvs" />
    </Window.DataContext>
    ...
    </Window>
```

> The XAML version really is getting pretty verbose, isn't it? But most people think it's easier to read, and that's always the trade-off: verbosity against clarity.

And here's the version if you used code.

```
public MainWindow()
{
    InitializeComponent();

    SampleIngredients Ingredients = new SampleIngredients();
    this.DataContext = Ingredients;
    view = (CollectionView) CollectionViewSource.GetDefaultView(this.DataContext);
    view.SortDescriptions.Add(new SortDescription("Name", ListSortDirection.
    Ascending));
}
```