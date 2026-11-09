| Table 11.1: Controls in Silverlight 4.0 |  |  |
|---|---|---|
| **Control** | **Description** | **XAML Element Example** |
| CheckBox | Allows you to provide check boxes that facilitate the selection of options. Check boxes can be checked, unchecked, or can have indeterminate state at a time. | `<CheckBox ClickMode="Press" IsChecked="False" Content="Apple" />` |
| ComboBox | Allows you to display a list of items with a drop-down list. | `<ComboBox x:Name="selectFontSize" Width="80" Height="23">`<br>`<ComboBoxItem Content="1" />`<br>`<ComboBoxItem Content="2"`<br>`IsSelected="True" />`<br>`<ComboBoxItem Content="3" />`<br>`<ComboBoxItem Content="4" />`<br>`</ComboBox>` |
| ContentControl | Refers to a control that contains content. Several controls are derived from the ContentControl class. | `<ContentControl Content="Silverlight" />` |
| DataGrid | Allows you to display data in the form of a grid with several rows and columns. | `<sdk:DataGrid ItemsSource="Silverlight" AutoGenerateColumns="true" ColumnHeaderHeight="30" AlternatingRowBackground="Orchid" />` |
| DataPager | Provides a UI that helps in displaying a large collection of data in the form of multiple pages. | `<sdk:DataPager x:Name="DP1" PageSize="5" AutoEllipsis="True" NumericButtonCount="3" DisplayMode="PreviousNext" />` |
| DatePicker | Allows you to select a particular date from a given calendar or type the desired date. | `<sdk:DatePicker IsTodayHighlighted="True" SelectedDateFormat="Short" />` |
| Ellipse | Allows you to provide an elliptical shape. | `<Ellipse Fill="Red" Height="50" Width="100" />` |
| Grid | Allows you to arrange the containing controls in rows and columns. | `<Grid Background="Yellow" ShowGridLines="True">`<br>`<Grid.RowDefinitions>`<br>`<RowDefinition Height="50" />`<br>`<RowDefinition Height="50" />`<br>`</Grid.RowDefinitions>`<br>`<Button Content="Silverlight" Grid.Row="0" />`<br>`</Grid>` |
| GridSplitter | Allows you to provide a UI element that can be moved to adjust the space between the rows and columns of a grid. | `<sdk:GridSplitter Grid.Row="1" ShowsPreview="True" Height="10" Width="300" />` |
| HyperlinkButton | Allows you to display a button with hyperlink. | `<HyperlinkButton Content="URL for Google" NavigateUri="http://www.google.com/" />` |