```
```csharp
public partial class StyledListBoxWindow1 : Window
{
    public StyledListBoxWindow1()
    {
        InitializeComponent();
        this.DataContext = Countries.GetCountries();
    }
}
```
```

*code snippet TemplateDemo/StyledListBoxWindow1.xaml.cs*

Within the XAML code, the ListBox named countryList1 is defined. countryList1 doesn't have a different style. It uses the default look from the ListBox element. The property ItemsSource is set to the Binding markup extension, which is used by data binding. From the code-behind, you have seen that the binding is done to an array of Country objects. Figure 35-25 shows the default look of the ListBox. By default, just the names of the countries returned by the ToString() method are displayed in a simple list:

```
```xml
<Window x:Class="TemplateDemo.StyledListBoxWindow1"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:src="clr-namespace:TemplateDemo"
    Title="StyledListBoxWindow1" Height="300" Width="300">
    <Grid>
        <ListBox ItemsSource="{Binding}" Margin="10" />
    </Grid>
</Window>
```
```

*code snippet TemplateDemo/StyledListBoxWindow1.xaml*

# ItemTemplate

The Country objects do have both the name and the flag in the object. Of course, you can also display both values in the list box. To do this, you need to define a template.

The ListBox element contains ListBoxItem elements. You can define the content for an item with the ItemTemplate. The style ListBoxStyle1 defines an ItemTemplate with a value of a DataTemplate. A DataTemplate is used to bind data to elements. You can use the Binding markup extension with DataTemplate elements.

The DataTemplate contains a grid with three columns. The first column contains the string Country:. The second column contains the name of the country. The third column contains the flag for the country. Because the country names have different lengths, but the view should be the same size for every country name, the SharedSizeGroup property is set with the second column definition. This shared size information for the column is used only because the property Grid.IsSharedSizeScope is also set.

After the column and row definitions, you can see two TextBlock elements. The first TextBlock element contains the text Country:. The second TextBlock element binds to the Name property that is defined in the Country class.

The content for the third column is a Border element containing a Grid. The Grid contains a Rectangle with a linear gradient brush and an Image element that is bound to the ImagePath property of the Country class. Figure 35-26 shows the countries in a ListBox with completely different output than before:

![](bbox=[0.78, 0.7, 0.95, 0.82])

FIGURE 35-25

![](bbox=[0.7, 0.8, 0.92, 0.95])

FIGURE 35-26

```
```xml
<Style x:Key="ListBoxStyle1" TargetType="{x:Type ListBox}">
  <Setter Property="ItemTemplate">
    <Setter.Value>
      <DataTemplate>
```
```