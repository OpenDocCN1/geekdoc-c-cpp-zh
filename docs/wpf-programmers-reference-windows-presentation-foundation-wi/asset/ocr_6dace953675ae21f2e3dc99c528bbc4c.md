# 322 | CHAPTER 18 DATA BINDING

The following code defines the third Label. Its binding searches for the Label's ancestor of type Grid gets its value from the Grid ColumnDefinitions[2].Width value.

```
<Label Grid.Column="*"
Content={Binding Source={RelativeSource FindAncestor,
AncestorType={x:Type Grid},
Path=ColumnDefinitions[2].Width} />
```

The RelativeSource PreviousData is useful in values and other controls that display multiple values. It is the code that displays one value to the previous.

The PreviousData example program in Figure 18-6 demonstrates the PreviousData. Each ListBox displays its value and the value of the item before it. The first item has no previous data, so it displays a blank value. (Fixing this is outside the scope of the control.)

The following code shows how the program defines the ListBox. The ItemsSource property refers to a static resource numbers that contains an array of numbers.

```
<ListBox ItemsSource='StaticResource numbers'
Background="Transparent">
  <ListBox.ItemTemplate>
    <DataTemplate>
      <StackPanel Orientation="Horizontal">
        <Label Content={Binding} Width="50"
HorizontalAlignment="Right" />
        <Label Content="/" />
        <Label Content={Binding
RelativeSource={RelativeSource PreviousData}}
Margin="-5,0,0,0" />
        <Label Content="" Margin="-10,0,0,0" />
      </StackPanel>
    </DataTemplate>
  </ListBox.ItemTemplate>
</ListBox>
```

![](bbox=[0.676, 0.287, 0.856, 0.403])

FIGURE 18-6

Don't worry about the code's details. Focus on the bindings and ignore the ItemTemplate and DataTemplate elements for now. The section "Binding Collections" later in this chapter has more to say about binding ListBoxes to other lists of data.

# DataContext

There is one additional way to specify a binding's source: by setting a control's DataContext property of its ancestors. Since controls inherit the DataContext property of their ancestors, this method provides a convenient way for several controls to share the same data source.