# Exploring Common XAML Controls 577

DataGrid: Also new in the .NET 4 (along with the DateTime and Calendar controls) is the DataGrid. (See Figure 2-21.) Conspicuously absent from the earlier versions of WPF, this control was part of the WPF Toolkit, an out-of-band release available from www.codeplex.com/wpf (still a great resource for WPF information).

The DataGrid has five base columns:

+   * DataGridColumn: For Text
* DataGridCheckBoxColumn: For Boolean
* DataGridComboBoxColumn: For ListItems
* DataGridHyperlinkColumn: For displaying Links
* DataGridTemplateColumn: For designing custom columns

The DataGrid can be set to AutoGenerate the columns based on the data it is bound to (as in the sample). It uses reflection to determine the best column type based on the data.

```
<DataGrid HorizontalAlignment="Stretch" AutoGenerateColumns="True" ItemsSource={Binding People}>
</DataGrid>
```

![](bbox=[0.135, 0.538, 0.495, 0.603])

Figure 2-21
A simple Data Grid.