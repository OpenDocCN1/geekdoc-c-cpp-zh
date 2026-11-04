
## Using the Grid Control

When you create a WPF application, you may notice that a Grid control is automatically added to the default window or page in the application. Every window or page in a WPF application (standalone or XBAP) contains a Grid control by default.

The Grid control is one of the most common and flexible container controls. A container control refers to a control that encompasses other controls and provides a predefined layout for these controls. The controls that are encompassed or contained within a container control are known as child controls or elements. In a Grid control, the child elements are contained in the cells of a grid. By default, a Grid control consists of a single cell, that is, one row and one column. However, you can create additional cells (rows and columns) in the Grid control by using the properties of the control.

The Grid control is an instance of the Grid class, which has various properties that allow you to work with the control. Table 7.2 lists the noteworthy properties of the Grid class:

Table 7.2: Noteworthy Properties of the Grid Class

| Property | Description |
|---|---|
| ColumnDefinitions | Retrieves an ordered collection of columns defined in a Grid control |
| RowDefinitions | Retrieves an ordered collection of rows defined in a Grid control |
| ShowGridLines | Retrieves or sets a value that indicates whether or not the grid lines between the cells of a Grid control are visible |
| Column | Retrieves or sets a value that indicates the column in which a child element of a Grid control appears |
| ColumnSpan | Retrieves or sets a value that indicates the number of columns that a child element of a Grid control spans |
| Row | Retrieves or sets a value that indicates the row in which a child element appears in a Grid control |
| RowSpan | Retrieves the number of rows that a child element spans in a Grid control |

> **Note**
> The Column, ColumnSpan, Row, and RowSpan properties listed in Table 7.2 are attached properties of the Grid control. An attached property is a property of a control that can be accessed and set by other controls. For instance, the Column, ColumnSpan, Row, and RowSpan properties of the Grid control can be accessed by its child elements.

Now, let's create a standalone WPF application named GridDemo to show the use of the Grid control. For this, perform the following steps:

- 1. Click Start→All Programs→Microsoft Visual Studio 2010→Microsoft Visual Studio 2010 to open the Visual Studio 2010 IDE.
- 2. Select File→New→Project from the menu bar in the Visual Studio 2010 IDE to open the New Project dialog box.
- 3. Select Visual C#→Windows in the Installed Templates pane and the WPF Application option from the middle pane of the New Project dialog box.
- 4. Enter the name GridDemo in the Name text box and specify an appropriate location for the application in the Location combo box.
- 5. Click the OK button. The GridDemo application is created.
- 6. Now, add the highlighted code given in Listing 7.3 in the MainWindow.xaml file:

### Listing 7.3: Adding Rows and Columns in a Grid Control

```xml
<Window x:Class="GridDemo.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="Demo Grid" Height="300" Width="300">
<Grid ShowGridLines="True" Background="Cornsilk">
<Grid.RowDefinitions>
<RowDefinition Height="68"/>
<RowDefinition Height="68"/>
<RowDefinition Height="68"/>
<RowDefinition Height="68"/>
</Grid.RowDefinitions>
<Grid.ColumnDefinitions>
<ColumnDefinition Width="139"/>
<ColumnDefinition Width="139"/>
</Grid.ColumnDefinitions>
</Grid>
</Window>
```

In Listing 7.3, the ShowGridLines property of the Grid control is set to True, which implies that straight lines are visible between the rows and columns of the grid. The grid has two child elements, Grid.RowDefinitions and Grid.ColumnDefinitions. The Grid.RowDefinitions element refers to the RowDefinitions property of the grid, which allows you to define a collection of rows in the grid. The Grid.ColumnDefinitions element refers to the ColumnDefinitions property, which allows you to define a collection of columns in the grid. The Grid.RowDefinitions element has four RowDefinition elements, each corresponding to a row. Similarly, the Grid.ColumnDefinitions element has two ColumnDefinition elements, each of which corresponds to a column.

- 7. Press the F5 key to run the application. The output appears, as shown in Fig. 7.18:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_236_0.png)

Fig. 7.18 shows the grid lines between the rows and columns of a Grid control.

## Using the Button Control

The Button control in WPF is similar to the one available for Windows Forms applications. It allows you to perform an action when a user clicks it. The Button control in WPF is a basic UI component that can contain text as well as an image.

The Button control is an instance of the Button class. Table 7.3 lists the noteworthy properties of the Button class:

Table 7.3: Noteworthy Properties of the Button Class

| Property | Description |
|---|---|
| IsCancel | Retrieves or sets a value that specifies whether or not a Button control is a Cancel button |
| ClickMode | Retrieves or sets a value that indicates when the Click event of a Button control occurs, that is, when the mouse button is clicked, moved over the control, or released |
| Content | Retrieves or sets the content of a Button control |
| IsDefault | Retrieves or sets a value that specifies whether or not a Button control is the default button |
| IsDefaulted | Retrieves a value that specifies whether or not a Button control is activated when a user presses the ENTER key from the keyboard |

Now, let's create a standalone WPF application named ButtonDemo to show the use of a Button control. For this, perform the following steps:

- 1. Repeat steps 1 to 3 as followed earlier while creating the GridDemo application in the Using the Grid Control section of this chapter.
- 2. Enter the name ButtonDemo in the Name text box and specify an appropriate location for the application in the Location combo box.
- 3. Click the OK button. The ButtonDemo application is created.
- 4. Add the highlighted code given in Listing 7.4 in the MainWindow.xaml file:

### Listing 7.4: Showing the Use of the Button Control

```xml
<Window x:Class="ButtonDemo.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="Demo Button" Height="200" Width="250">
<Grid>
<Button Name="button1" Height="25" Margin="0,0,0,100" Width="75" Content="1" Background="Black" Foreground="White"/>
<Button Name="button2" Height="25" Margin="0,0,0,50" Width="100" Content="2" Background="Black" Foreground="White"/>
<Button Name="button3" Height="25" Width="125" Content="3" Background="Black" Foreground="White"/>
</Grid>
</Window>
```

In Listing 7.4, three Button controls (button1, button2, and button3) are added as child controls to the Grid control. The Content property of the three buttons are set to 1, 2, and 3, respectively.

- 5. Press the F5 key to run the application. The output appears, as shown in Fig. 7.19:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_237_0.png)

Fig. 7.19

In Fig. 7.19, the three button controls, button1, button2, and button3 are shown displaying the content 1, 2, and 3 in a Grid control.

## Using the TextBox Control

If you want to allow users of a WPF application to enter textual data, you can use the TextBox control. This control provides the facility to enter or display unformatted text. With the TextBox control, you can manipulate the input text by performing various operations, such as aligning the text, wrapping the text around the control, or specifying the casing of the text.

> **Note**
> By default, the TextBox control has a context menu, which appears when a user right-clicks in the control. The context menu allows the user to perform common editing operations such as Cut, Copy, and Paste.

The TextBox control is represented by the TextBox class, which is derived from the TextBoxBase class. The TextBox class has many properties that allow you to work with the TextBox control. Table 7.4 lists the noteworthy properties of the TextBox class:

Table 7.4: Noteworthy Properties of the TextBox Class

| Property | Description |
|---|---|
| CharacterCasing | Retrieves or sets a value that indicates the casing of the characters of the text entered in a TextBox control |
| MaxLength | Retrieves or sets the maximum number of characters that you can enter in a TextBox control |
| Text | Retrieves or sets the text contained in a TextBox control |
| TextAlignment | Retrieves or sets the horizontal alignment of the text in a TextBox control |
| TextWrapping | Retrieves or sets a value that indicates how text is wrapped in a TextBox control |

Let's create a standalone WPF application named TextBoxDemo to show the use of the TextBox control. For this, perform the following steps:

- 1. Repeat steps 1 to 3 as followed earlier while creating the GridDemo application in the Using the Grid Control section in this chapter.
- 2. Enter the name TextBoxDemo in the Name text box and specify an appropriate location for the application in the Location combo box.
- 3. Click the OK button. The TextBoxDemo application is created.
- 4. Add the highlighted code given in Listing 7.5 in the MainWindow.xaml file:

### Listing 7.5: Showing the Use of the TextBox Control

```xml
<Window x:Class="TextBoxDemo.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="Demo TextBox" Height="250" Width="300">
<Grid Background="Gray">
<TextBox Name="textBox1" Height="75" Width="175" CharacterCasing="Upper" TextWrapping="Wrap" TextAlignment="Center" Background="LavenderBlush" VerticalScrollBarVisibility="Auto"/>
<Button Height="25" Margin="100,130,100,0" Name="button1" Click="button1_Click" Background="LavenderBlush" Content="Clear textBox"/>
</Grid>
</Window>
```

In Listing 7.5, a TextBox control is added to a Grid control. The TextBox control is named textBox1 and has its CharacterCasing property set to Upper, which implies that all the characters of the text that you enter appear in uppercase. The TextWrapping and TextAlignment properties of the textBox1 control are set to Wrap and Center, respectively. This implies that the entered text is wrapped around the control and aligned at the center of the control. Note that another property, named VerticalScrollBarVisibility, of the textBox1 control is set to Auto. This property is inherited from the TextBoxBase class and retrieves or sets a value that indicates whether a vertical scroll bar appears in the control.
