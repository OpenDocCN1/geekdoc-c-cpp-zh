No matter if you visually create the row and column definitions or use the Collection Editor, they both make changes to the XAML. This means that you can also edit the XAML directly to create the row and column definitions. If you have already created your rows and columns, make sure the generated XAML looks like that shown in Listing 17.5. Otherwise, add the row and column definitions shown in that listing in between the Grid element in the XAML.

# **LISTING 17.5**

Grid Row and Column Definitions

```
<Grid.RowDefinitions>
    <RowDefinition Height="Auto" />
    <RowDefinition Height="*" />
</Grid.RowDefinitions>
<Grid.ColumnDefinitions>
    <ColumnDefinition />
    <ColumnDefinition Width="250" />
</Grid.ColumnDefinitions>
```

# **By the Way**

**Height and Width Sizing**

Everything in WPF is rendered in a resolution-independent manner using pixels as the unit of measurement. Although width and height are normally thought of as just numeric values, WPF has some special values it understands as well.
By providing an actual numeric value, you are telling WPF that the width or height should be exactly that size. However, if you want WPF to automatically distribute space evenly based on content, you should enter a value of Auto.
To distribute rows or columns proportionally (using the remaining space if there are also fixed or auto-sized rows or columns), you can use what is called star sizing. To use star sizing, you specify the asterisk symbol (*) as the value. When using star sizing, you can indicate a weighting value that controls how much of the available space is given to that element. For example, a row using * for height would receive one times the available space, and a row using 2* would receive two times the available space.