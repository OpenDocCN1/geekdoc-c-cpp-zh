# THE GRID

The Grid is the default layout root when you create a Window in Visual Studio. Like a spreadsheet, the Grid divides the available space into rows and columns. Those rows and columns are defined using the Grid.RowDefinitions and Grid.ColumnDefinitions collections.

You add one RowDefinition element for each row and a ColumnDefinition for each column in the Grid.

```
<Grid>
<Grid.RowDefinitions>
<RowDefinition Height="20"/>
<RowDefinition />
...
</Grid.RowDefinitions>
<Grid.ColumnDefinitions>
<ColumnDefinition Width="2*"/>
<ColumnDefinition Width="3*"/>
...
</Grid.ColumnDefinitions>
</Grid>
```

The Height property of a RowDefinition and the Width property of a ColumnDefinition can be specified using any of the qualified dediles, as "Auto", or as a proportional value using the star syntax.

These ColumnDefinition elements assign two-fifths of the available height to the first column, and three-fifths to the second.

# PUT ON YOUR THINKING HAT

The Grid panel defines Row and Column attached properties that allow you to assign a child element to a specific cell. In addition, it defines RowSpan and ColumnSpan attached properties that allow an element to stretch across more than one cell.

Can you re-create the diagram on the previous page using a Grid? (Hint: Like most thing in the .NET world, the rows and columns in a Grid start at zero.)