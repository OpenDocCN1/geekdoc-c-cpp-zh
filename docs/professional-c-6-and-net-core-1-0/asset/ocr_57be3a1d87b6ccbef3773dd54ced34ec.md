```
```xml
</ListBoxItem>
<ListBoxItem>
<Hyperlink Command="local:ShowCommands.ShowBooksList">
Show Books List</Hyperlink>
</ListBoxItem>
</ListBox>
```
```

The implementation of the event handler adds a new TabItem control to the TabControl, assigns the Content to the user control BooksUC,and sets the selection of the TabControl to the newly created TabItem (code file BooksDemoRibbon/MainWindow.xaml.cs):

```
```csharp
private void OnShowBooksList(object sender, ExecutedRoutedEventArgs e)
{
	var booksUI = new BooksUC();
	this.tabControl1.SelectedIndex =
	this.tabControl1.Items.Add(
	new TabItem { Header="Books List", Content=booksUI});
}
```
```

Because the DockPanel has the Book array assigned to the DataContext, and the ListBox is placed within the DockPanel, the ListBox shows all books with the default template, as illustrated in Figure 34.20.

![](bbox=[0.05, 0.52, 0.95, 0.82])

# Figure 34.20

For a more flexible layout of the ListBox, you have to define a template, as discussed in Chapter 33, “Advanced Windows Apps,” for ListBox styling. The ItemTemplate of the ListBox defines a DataTemplate with a Label element. The content of the label is bound to the Title. The item template is repeated for every item in the list. Of course, you can also add the item template to a style within resources:

```
```xml
<ListBox DockPanel.Dock="Left" ItemsSource="{Binding}" Margin="5">
```
```