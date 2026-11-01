

```
</StackPanel>
<TextBox Grid.Row="1" Grid.Column="0" Width="140"></TextBox>
</Grid>
</InlineUIContainer>
</Paragraph>
```

代码片段 FlowDocumentsDemo/FlowDocument2.xaml

## 块（Block）

Block 是块级元素的抽象基类。Block 允许对包含在特定视图中的元素进行分组。所有 Block 共有的属性是 PreviousBlock、NextBlock 和 SiblingBlocks，它们允许你在块之间导航。设置 BreakPageBefore 和 BreakColumnBefore 后，分页符和分栏符会在块开始之前插入。Block 还通过 BorderBrush 和 BorderThickness 属性定义边框。

从 Block 派生的类有 Paragraph、Section、List、Table 和 BlockUIContainer。BlockUIContainer 与 InlineUIContainer 类似，因为你可以添加从 UIElement 派生的元素。

Paragraph 和 Section 是简单的块，其中 Paragraph 包含内联元素；Section 用于对其他 Block 元素进行分组。使用 Paragraph 块，你可以确定是否允许在段落内或段落之间进行分页或分栏。KeepTogether 可用于禁止在段落内断开；KeepWithNext 则尝试将一个段落和下一个段落保持在一起。如果段落因分页或分栏而断开，MinWidowLines 定义断点后放置的最小行数，MinOrphanLines 定义断点前的最小行数。

Paragraph 块还允许使用 TextDecoration 元素修饰段落内的文本。预定义的文本修饰由 TextDecorations 定义：Baseline、Overline、Strikethrough 和 Underline。

以下 XAML 代码展示了多个 Paragraph 元素。一个带有标题的 Paragraph 元素后面跟着另一个包含该标题内容的 Paragraph 元素。这两个段落通过属性 KeepWithNext 连接。通过将 KeepTogether 设置为 True，也确保了内容段落不会被断开。结果如图 37-6 所示。

```xml
<FlowDocument xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    ColumnWidth="300" FontSize="16" FontFamily="Georgia">
    <Paragraph FontSize="36">
        <Run>Lyrics</Run>
    </Paragraph>

    <Paragraph TextIndent="10" FontSize="24" KeepWithNext="True">
        <Bold>
            <Run>Mary had a little lamb</Run>
        </Bold>
    </Paragraph>

    <Paragraph KeepTogether="True">
        <Run>
            Mary had a little lamb,
        </Run>
        <LineBreak />
        <Run>
            little lamb, little lamb,
        </Run>
        <LineBreak />
        <Run>
            Mary had a little lamb,
        </Run>
        <LineBreak />
        <Run>
            whose fleece was white as snow.
        </Run>
    <LineBreak />
<Run>
And everywhere that Mary went,
</Run>
<LineBreak />
<Run>
Mary went, Mary went,
</Run>
<LineBreak />
<Run>
and everywhere that Mary went,
</Run>
<LineBreak />
<Run>
the lamb was sure to go.
</Run>
</Paragraph>

<Paragraph TextIndent="-10" FontSize="24" KeepWithNext="True">
<Bold>
<Run>Humpty Dumpty</Run>
</Bold>
</Paragraph>
<Paragraph KeepTogether="True">
<Run>Humpty dumpty sat on a wall</Run>
<LineBreak />
<Run>
Humpty dumpty had a great fall</Run>
<LineBreak />
<Run>
All the King's horses</Run>
<LineBreak />
<Run>
And all the King's men</Run>
<LineBreak />
<Run>
Couldn't put Humpty together again
</Run>
</Paragraph>
</FlowDocument>
```

代码片段 FlowDocumentsDemo/ParagraphDemo.xaml

![](img/d7d2ffa0a76feaab821930e95daace93_1142_0.png)

图 37-6

## 列表

List 类用于创建文本的无序列表或有序列表。List 通过设置 MarkerStyle 属性来定义其项目的项目符号样式。MarkerStyle 的类型为 TextMarkerStyle，可以是数字（Decimal）、字母（LowerLatin 和 UpperLatin）、罗马数字（LowerRoman 和 UpperRoman）、图形（Disc、Circle、Square、Box）。List 只能包含 ListItem 元素，而 ListItem 又只能包含 Block 元素。

使用 XAML 定义以下列表将产生如图 37-7 所示的输出。

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

![](img/d7d2ffa0a76feaab821930e95daace93_1143_0.png)

代码片段 FlowDocumentsDemo/ListDemo.xaml

## 表格

Table 类与第 35 章中介绍的用于定义行和列的 Grid 类非常相似。

下面的示例演示了创建包含 Table 的 FlowDocument。要创建表格，你可以向 Columns 属性添加 TableColumn 对象。使用 TableColumn 可以指定宽度和背景。

Table 还包含 TableRowGroup 对象。TableRowGroup 有一个 Rows 属性，可以向其中添加 TableRow 对象。TableRow 类定义了一个 Cells 属性，可以向其中添加 TableCell 对象。TableCell 对象可以包含任何 Block 元素。这里使用了一个包含 Inline 元素 Run 的 Paragraph：

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
row1.Cells.Add(new TableCell(new Paragraph(new Run("Jenson Button"))));
row1.Cells.Add(new TableCell(new Paragraph(new Run("95"))));

var row2 = new TableRow { Background = new SolidColorBrush(Colors.LightGray) };
row2.Cells.Add(new TableCell(new Paragraph(new Run("2."))));
row2.Cells.Add(new TableCell(new Paragraph(new Run("Sebastian Vettel"))));
row2.Cells.Add(new TableCell(new Paragraph(new Run("84"))));
var row3 = new TableRow();
row3.Cells.Add(new TableCell(new Paragraph(new Run("3."))));
row3.Cells.Add(new TableCell(new Paragraph(
    new Run("Rubens Barrichello"))));
row3.Cells.Add(new TableCell(new Paragraph(new Run("77"))));
var rowGroup = new TableRowGroup();
rowGroup.Rows.Add(titleRow);
rowGroup.Rows.Add(headerRow);
rowGroup.Rows.Add(row1);
rowGroup.Rows.Add(row2);
rowGroup.Rows.Add(row3);
t1.RowGroups.Add(rowGroup);
doc.Blocks.Add(t1);
reader.Document = doc;
```

代码片段 TableDemo/MainWindow.xaml

运行应用程序，你可以看到格式精美的表格，如图 37-8 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_1144_0.png)

图 37-8

## 锚定到块

现在你了解了 Inline 和 Block 元素，可以通过使用 AnchoredBlock 类型的 Inline 元素将两者结合起来。AnchoredBlock 是一个抽象基类，有两个具体实现：Figure 和 Floater。

Floater 使用 HorizontalAlignment 和 Width 属性，使其内容与主内容并行显示。

从之前的示例开始，添加了一个包含 Floater 的新段落。这个 Floater 靠左对齐，宽度为 160。如图 37-9 所示，下一个段落会环绕它流动。

<Paragraph TextIndent="10" FontSize="24" KeepWithNext="True">
    <Bold>
        <Run>Mary had a little lamb</Run>
    </Bold>
</Paragraph>
<Floater HorizontalAlignment="Left" Width="160">
    <Paragraph Background="LightGray">
        <Run>Sarah Josepha Hale</Run>
    </Paragraph>
</Floater>
</Paragraph>
<Paragraph KeepTogether="True">
    <Run>
        Mary had a little lamb
        <LineBreak />
        <!-- ... -->
    </Run>
</Paragraph>

