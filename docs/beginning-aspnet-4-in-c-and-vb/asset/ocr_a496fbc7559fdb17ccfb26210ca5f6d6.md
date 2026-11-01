# Master Details Binding

Instead of just showing all the elements inside a list, you might want or need to show detail information about the selected item. It doesn't require a lot of work to do this. The Label and TextBox controls are already defined; currently they only show the first element in the list.

There's one important change you have to make to the ListBox. By default, the labels are bound to just the first element of the list. By setting the ListBox property IsSynchronizedWithCurrentItem="True", the selection of the list box is set to the current item. In Figure 36-7 you can see the result; the selected item is shown in the detail section labels:

![](bbox=[0.52, 0.17, 0.9, 0.48])

FIGURE 36-7

```
<ListBox DockPanel.Dock="Left" ItemsSource="{Binding}" Margin="5" MinWidth="120" IsSynchronizedWithCurrentItem="True">
  <ListBox.ItemTemplate>
    <DataTemplate>
      <Label Content="{Binding Title}" />
    </DataTemplate>
  </ListBox.ItemTemplate>
</ListBox>
```

code snippet BooksDemo/BooksUC.xaml

# MultiBinding

Binding is one of the classes that can be used for data binding. BindingBase is the abstract base class of all bindings and has different concrete implementations. Besides Binding, there's also MultiBinding and PriorityBinding. MultiBinding allows you to bind one WPF element to multiple sources. For example, with a Person class that has LastName and FirstName properties, it is interesting to bind both properties to a single WPF element:

```
public class Person
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
}
```

code snippet MultiBindingDemo/Person.cs

For MultiBinding, a markup extension is not available — thus the binding must be specified with XAML element syntax. The child elements of MultiBinding are Binding elements that specify the binding to the various properties. Here the FirstName and LastName properties are used. The data context is set with the Grid element to reference the person1 resource.

To connect the properties together, MultiBinding uses a Converter to convert multiple values to one. This converter uses a parameter that allows for different conversions based on the parameter:

```
<Window x:Class="Wrox.ProcSharp.WPF.MainWindow" xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" xmlns:system="clr-namespace:System;assembly=mscorlib" xmlns:local="clr-namespace:Wrox.ProcSharp.WPF" Title="MainWindow" Height="240" Width="500">
  <Window.Resources>
    <local:Person x:Key="person1" FirstName="Tom" LastName="Turbo" />
```