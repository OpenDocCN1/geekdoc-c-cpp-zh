
### TABLE C-4: Key Attached Properties of DockPanel

| PROPERTY | PURPOSE |
| --- | --- |
| DockPanel.Bottom | Makes the child fill the bottom of the DockPanel's remaining area. |
| DockPanel.Left | Makes the child fill the left side of the DockPanel's remaining area. |
| DockPanel.Right | Makes the child fill the right side of the DockPanel's remaining area. |
| DockPanel.Top | Makes the child fill the top of the DockPanel's remaining area. |

### EXAMPLE Using DockPanel

The following code makes a DockPanel that contains a Menu and a Grid. The Menu is attached to the DockPanel's top as you would normally expect. The Grid occupies the rest of the DockPanel and would contain whatever you want on the window.

```
<DockPanel LastChildFill="True">
  <Menu DockPanel.Dock="Top">
    <!-- Items omitted -->
  </Menu>
  <Grid>
    <!-- Other controls omitted. -->
  </Grid>
</DockPanel>
```

### EXPANDER

The Expander displays a header and an icon that you can click to show or hide a single child. The key properties of Expander are given in Table C-5.

### TABLE C-5: Key Properties of Expander

| PROPERTY | PURPOSE |
| --- | --- |
| Background | The color used to fill the control's interior |
| BorderBrush | The color of the control's edge |
| BorderThickness | The control edge's thickness |
| ExpandDirection | Determines the direction in which the content is expanded. It can be Down, Left, Right, or Up. |
| FontFamily | The name of the font family as in Times New Roman, Arial, or Segoe (pronounced see-go) |

446 | APPENDIX C LAYOUT CONTROLS

### TABLE C-5 (continued)

| PROPERTY | PURPOSE |
| --- | --- |
| FontSize | The text's font size. Append cm, in, px, or pt to specify centimeters, inches, pixels (the default), or points (1/72 inch) as in "0.25in" or "12pt". |
| FontStyle | Can be Normal, Italic, or Oblique (simulates italic for fonts with an italic style) |
| FontWeight | The text's boldness. This can be Thin, ExtraLight, Light, Normal, Medium, SemiBold, Bold, ExtraBold, Black, and ExtraBlack, although many fonts look the same for many of these values. |
| Foreground | The color used to draw the Expander's Header |
| Header | The text displayed at the top of the Expander beside Expand/Hide button |
| HorizontalContentAlignment | Determines how the content is aligned horizontally within the control. This can be Center, Left, Right, or Stretch. |
| IsExpanded | Determines whether the control is expanded to show its child. |
| Padding | The extra space added between the control's edges and its contents |
| VerticalContentAlignment | Determines how the content is aligned vertically within the control. This can be Bottom, Center, Stretch, or Top. |

### EXAMPLE Using Expander

The following code creates an Expander that contains a StackPanel. The StackPanel would contain other controls that the Expander could show and hide.

```
<Expander Header="Details" IsExpanded="True" BorderBrush="Blue">
<StackPanel>
  <!---- Other controls omitted. -->
</StackPanel>
</Expander>
```

### EXPRESSION BLEND EXAMPLE

Expression Blend Properties tab uses Expanders to let you show and hide different groups of properties such as Brushes, Appearance, Layout, and so forth.

### GRID

One of the more powerful and useful layout controls, Grid lets you arrange children in rows and columns. The key properties of Grid are given in Table C-6.

### TABLE C-6:

| PROPERTY | PURPOSE |
| --- | --- |
| Background | The color used to fill the control's interior |
| ColumnDefinitions | This property element ColumnDefinition objects that define column widths |
| RowDefinitions | This property element contains RowDefinition objects that define row heights |

A child can use these properties to tell the Grid how to position the child. The key attached properties of Grid are given in Table C-7.

### TABLE C-7:

| PROPERTY | PURPOSE |
| --- | --- |
| Grid.Column | The column that contains the child |
| Grid.ColumnSpan | The number of columns that the child occupies |
| Grid.Row | The row that contains the child |
| Grid.RowSpan | The number of rows that the child occupies |

### EXAMPLE Making a Data Grid

The following code builds a fairly standard data-entry form that lets the user enter name, address, and other information:

```
<Grid.RowDefinitions>
  <RowDefinition Height="40"/>
  <RowDefinition Height="30"/>
  <RowDefinition Height="30"/>
  <!-- Other row definitions omitted -->
</Grid.RowDefinitions>
<Grid.ColumnDefinitions>
  <ColumnDefinition Width="100"/>
  <ColumnDefinition Width="*"/>
</Grid.ColumnDefinitions>

<Label Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2" Content="New Customer"
```

### SCROLLVIEWER

The ScrollViewer displays a single child inside a scrollable region. The key properties of ScrollViewer are given in Table C-8.

### TABLE C-8: Key Properties of ScrollViewer

| PROPERTY | PURPOSE |
| --- | --- |
| Background | The color used to fill the control's interior |
| HorizontalContentAlignment | Determines how the content is aligned horizontally within the control. This can be Center, Left, Right, or Stretch. |
| IsExpanded | Determines whether the control is expanded to show its child. |
| Padding | The extra space added between the control's edges and its contents |
| VerticalContentAlignment | Determines how the content is aligned vertically within the control. This can be Bottom, Center, Stretch, or Top. |
| HorizontalVisibility | Determines whether the scrollbar is displayed. This can be Auto. |
| IsExpanded | Determines whether the control is expanded to show its child. |
| Padding | The extra space added between the control's edges and its contents |
| VerticalContentAlignment | Determines how the content is aligned vertically within the control. This can be Bottom, Center, Stretch, or Top. |

The ScrollViewer also supports properties (FontFamily, FontSize, TextStyle, FontWeight). It doesn't draw any text itself, but Labels, TextBoxes, and other controls that draw text inherit these values.

For some reason, the HorizontalVisibility defaults to Disabled. You may want to set both of these properties to Auto.

### SILLY SCROLLBARS

Using ScrollViewer

The following code creates a ScrollViewer holding an Image that displays a large picture. The scrollbars appear when the window is small enough.

```
<Grid>
    <ScrollView
        HorizontalScrollBarVisibility="Auto"
        VerticalScrollBarVisibility="Auto">
        <Image Stretch="None"
               Source="http://vb-helper.com/compressed_2.jpg" />
    </ScrollView>
</Grid>
```

### STACKPANEL

The StackPanel is one of the most powerful and useful layout controls. It arranges its children either vertically or horizontally. If the control runs out of room it clips any children. The key properties of StackPanel are given in Table C-9.

### TABLE C-9: Key Properties of StackPanel

| PROPERTY | PURPOSE |
| --- | --- |
| Background | The color used to fill the control's interior |
| Orientation | Determines whether the control arranges its children in a row (Orientation = Horizontal) or a column (Orientation = Vertical) |

### EXAMPLE Using StackPanel

The following code creates three buttons arranged in a column. The StackPanel's Resource section creates an unnamed style that gives the Buttons consistent Margin, Width, and Height properties.

```
<StackPanel>
  <StackPanel.Resources>
    <Style TargetType="Button">
      <Setter Property="Margin" Value="5"/>
      <Setter Property="Width" Value="100"/>
      <Setter Property="Height" Value="40"/>
    </Style>
  </StackPanel.Resources>
  <Button Content="Add Customer"/>
  <Button Content="Find Customer"/>
  <Button Content="Delete Customer"/>
</StackPanel>
```

### STATUSBAR

StatusBar creates an area, typically at the bottom of the window, where you can give the user status information. You can place StatusBarItems, Buttons, ComboBoxes, and other controls inside the StatusBar. The key properties of StatusBar are given in Table C-10.

### TABLE C-10: Key Properties of StatusBar

| PROPERTY | PURPOSE |
| --- | --- |
| Background | The color to fill the control's interior |
| BorderBrush | The color of the control's edge |
| BorderThickness | The control's thickness |

You can place controls as Label and Button directly in the StatusBar, but you can get slightly better results if you place StatusBarItems inside the StatusBar. In that case, the StatusBar acts much like a horizontal StackPanel that stretches its last child to fill the available space. If you place controls directly inside the StatusBar, it doesn't stretch the last control.
