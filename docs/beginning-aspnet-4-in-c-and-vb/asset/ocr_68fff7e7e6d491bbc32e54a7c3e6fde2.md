and UpperRoman), a graphic (Disc, Circle, Square, Box). List can only contain ListItem elements which in turn can only contain Block elements.

Defining the following list with XAML results in the output shown in Figure 37-7.

```
```xml
<List MarkerStyle="Square">
  <ListItem>
    <Paragraph>Monday</Paragraph>
  </ListItem>
  <ListItem>
    <Paragraph>Tuesday</Paragraph>
  </ListItem>
  <ListItem>
    <Paragraph>Wednesday</Paragraph>
  </ListItem>
</List>
```
```

![](bbox=[0.82, 0.12, 0.95, 0.24])

code snippet FlowDocumentsDemo/ListDemo.xaml

# Tables

The Table class is very similar to the Grid class that was presented in Chapter 35 to define rows and columns.

The following example demonstrates creating a FlowDocument with a Table. To create tables you can add TableColumn objects to the Columns property. With TableColumn you can specify the width and background.

The Table also contains TableRowGroup objects. The TableRowGroup has a Rows property where TableRow objects can be added. The TableRow class defines a Cells property where TableCell objects can be added. TableCell objects can contain any Block element. Here a Paragraph is used that contains the Inline element Run:

```
```csharp
var doc = new FlowDocument();
var t1 = new Table();
t1.Columns.Add(new TableColumn
{ Width = new GridLength(50, GridUnitType.Pixel) });
t1.Columns.Add(new TableColumn
{ Width = new GridLength(1, GridUnitType.Auto) });
t1.Columns.Add(new TableColumn
{ Width = new GridLength(1, GridUnitType.Auto) });

var titleRow = new TableRow();
titleRow.Background = new SolidColorBrush(Colors.LightBlue);
var titleCell = new TableCell
{ ColumnSpan = 3, TextAlignment = TextAlignment.Center };
titleCell.Blocks.Add(
new Paragraph(new Run("Formula 1 Championship 2009")
{ FontSize=24, FontWeight = FontWeights.Bold }));
titleRow.Cells.Add(titleCell);

var headerRow = new TableRow
{ Background = new SolidColorBrush(Colors.LightGoldenrodYellow) };
headerRow.Cells.Add(new TableCell(new Paragraph(new Run("Pos"))
{ FontSize = 14, FontWeight=FontWeights.Bold}));
headerRow.Cells.Add(new TableCell(new Paragraph(new Run("Name"))
{ FontSize = 14, FontWeight=FontWeights.Bold }));
headerRow.Cells.Add(new TableCell(new Paragraph(new Run("Points"))
{ FontSize = 14, FontWeight=FontWeights.Bold }));

var row1 = new TableRow();
row1.Cells.Add(new TableCell(new Paragraph(new Run("1."))));
row1.Cells.Add(new TableCell(new Paragraph
new Run("Jenson Button"))));
row1.Cells.Add(new TableCell(new Paragraph(new Run("95"))));

var row2 = new TableRow / Background =
```
```