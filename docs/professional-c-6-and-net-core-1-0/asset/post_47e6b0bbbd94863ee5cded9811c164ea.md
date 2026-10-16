
![](img/3d365b72b289213a91ade7eb366b8f35_1384_0.png)

# Figure 35.2

![](img/3d365b72b289213a91ade7eb366b8f35_1384_1.png)

# Figure 35.3

# Inline

The base class for all inline flow content elements is `Inline`. You can use `Inline` elements within a paragraph of a flow document. Because within a paragraph one `Inline` element can follow another, the `Inline` class provides the `PreviousInline` and `NextInline` properties to navigate from one element to another. You can also get a collection of all peer inlines with `SiblingInlines`.

The `Run` element that was used earlier to write some text is an `Inline` element for formatted or unformatted text, but there are many more. You can have a new line after a `Run` element by using the `LineBreak` element.

The `Span` element derives from the `Inline` class and enables the grouping of `Inline` elements. Only `Inline` elements are allowed within the content of `Span`. The self-explanatory `Bold`, `Hyperlink`, `Italic`, and `Underline` classes all derive from `Span` and thus have the same functionality to enable `Inline` elements as its content, but to act on these elements differently. The following XAML code demonstrates using `Bold`, `Italic`, `Underline`, and `LineBreak`, as shown in Figure 35.4 (code file `DocumentsDemos/FlowDocumentsDemo/FlowDocument1.xaml`):

```
<Paragraph FontWeight="Normal">
    <Span>
        <Span>Normal</Span>
        <Bold>Bold</Bold>
        <Italic>Italic</Italic>
        <LineBreak />
```

```
```xml
<Underline>Underline</Underline>
</Span>
</Paragraph>
```
```

![](img/3d365b72b289213a91ade7eb366b8f35_1385_0.png)

[Figure 35.4](#)

AnchoredBlock is an abstract class that derives from Inline and is used to anchor Block elements to flow content. Figure and Floater are concrete classes that derive from AnchoredBlock. Because these two inline elements become interesting in relation to blocks, these elements are discussed later in this chapter.

> **NOTE** *The flow documents added to the solution need to be set to* `Build Action` **="Content"** *and* `Copy to Output Directory` **="Copy if newer"** *with the Visual Studio Properties Window for having them available in the same directory as the executables.*

Another Inline element that maps UI elements that have been used in previous chapters is InlineUIContainer. InlineUIContainer enables adding all UIElement objects (for example, a Button) to the document. The following code segment adds an InlineUIContainer with ComboBox, RadioButton, and TextBox elements to the document (the result is shown in [Figure 35.5](#)) (code file DocumentsDemos/FlowDocumentsDemo/FlowDocument2.xaml):

```
```xml
<Paragraph TextAlignment="Center">
    <Span FontSize="36">
        <Italic>c|elements</Italic>
    </Span>
    <LineBreak />
    <LineBreak />
    <InlineUIContainer>
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition />
                <RowDefinition />
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition />
                <ColumnDefinition />
            </Grid.ColumnDefinitions>
            <ComboBox Width="40" Margin="3" Grid.Row="0">
                <ComboBoxItem Content="Filet Mignon" />
                <ComboBoxItem Content="Rib Eye" />
                <ComboBoxItem Content="Sirloin" />
            </ComboBox>
            <StackPanel Grid.Row="0" Grid.RowSpan="2" Grid.Column="1">
```

```
<RadioButton Content="Raw" />
<RadioButton Content="Medium" />
<RadioButton Content="Well done" />
</StackPanel>
<TextBox Grid.Row="1" Grid.Column="0" Width="140" />
</Grid>
</InlineUIContainer>
</Paragraph>
```

![](img/3d365b72b289213a91ade7eb366b8f35_1386_0.png)

Figure 35.5

# Block

Block is an abstract base class for block-level elements. Blocks enable grouping elements contained to specific views. Common to all blocks are the properties PreviousBlock, NextBlock, and SiblingBlocks that enable you to navigate from block to block. Setting BreakPageBefore and BreakColumnBefore page and column breaks are done before the block starts. A Block also defines a border with the BorderBrush and BorderThickness properties.

Classes that derive from Block are Paragraph, Section, List, Table, and BlockUIContainer. BlockUIContainer is similar to InlineUIContainer in that you can add elements that derive from UIElement.

Paragraph and Section are simple blocks; Paragraph contains inline elements, and Section is used to group other Block elements. With the Paragraph block you can determine whether a page or column break is allowed within the paragraph or between paragraphs. You can use KeepTogether to disallow breaking within the paragraph; KeepWithNext tries to keep one paragraph and the next together. If a paragraph is broken by a page or column break, MinWidowLines defines the minimum number of lines that are placed after the break; MinOrphanLines defines the minimum number of lines before the break.

The Paragraph block also enables decorating the text within the paragraph with TextDecoration elements. Predefined text decorations are defined by TextDecorations: Baseline, Overline, Strikethrough,

and Underline.

The following XAML code shows multiple Paragraph elements. One Paragraph element with a title follows another with the content belonging to this title. These two paragraphs are connected with the attribute KeepWithNext. It’s also assured that the paragraph with the content is not broken by setting KeepTogether to True (code file DocumentsDemos/FlowDocumentsDemo/ParagraphDemo.xaml):

```
<FlowDocument
    ColumnWidth="300" FontSize="16" FontFamily="Segoe UI"
    ColumnRuleWidth="3"
    ColumnRuleBrush="Violet">
    <Paragraph FontSize="36">
        <Run>Lyrics</Run>
    </Paragraph>
    <Paragraph TextIndent="10" FontSize="24" KeepWithNext="True">
        <Bold>
            <Run>Mary had a little lamb</Run>
        </Bold>
    </Paragraph>
    <Paragraph KeepTogether="True">
        <Run>Mary had a little lamb,</Run>
        <LineBreak />
        <Run>little lamb, little lamb,</Run>
        <LineBreak />
        <Run>Mary had a little lamb,</Run>
        <LineBreak />
        <Run>whose fleece was white as snow.</Run>
        <LineBreak />
        <Run>And everywhere that Mary went,</Run>
        <LineBreak />
        <Run>Mary went, Mary went,</Run>
        <LineBreak />
        <Run>and everywhere that Mary went,</Run>
        <LineBreak />
        <Run>the lamb was sure to go.</Run>
    </Paragraph>
    <Paragraph TextIndent="10" FontSize="24" KeepWithNext="True">
        <Bold>
            <Run>Humpty Dumpty</Run>
        </Bold>
    </Paragraph>
    <Paragraph KeepTogether="True">
        <Run>Humpty dumpty sat on a wall</Run>
        <LineBreak />
        <Run>Humpty dumpty had a great fall</Run>
        <LineBreak />
        <Run>All the King's horses</Run>
        <LineBreak />
        <Run>And all the King's men</Run>
        <LineBreak />
        <Run>Couldn't put Humpty together again</Run>
    </Paragraph>
</FlowDocument>
```

The result is shown in Figure 35.6.

+   - [ ] Monday
+   - [ ] Tuesday
+   - [ ] Wednesday

# Figure 35.7

# Tables

The Table class is very similar to the Grid class that defines rows and columns (see Chapter 34, “Windows Desktop Applications with WPF”). The following example demonstrates creating a FlowDocument with a Table. The table is now created programmatically, and the XAML file contains the FlowDocumentReader (code file DocumentsDemos/TableDemo/MainWindow.xaml):

```
<Window x:Class="TableDemo.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="Table Demo" Height="350" Width="525">
<FlowDocumentReader x:Name="reader" />
</Window>
```

The data that is shown in the table is returned from the property F1Results (code file DocumentsDemos/TableDemo/MainWindow.xaml.cs):

```
private string[][] F1Results =>
new string[][]
{
new string[] { "1.", "Lewis Hamilton", "384" },
new string[] { "2.", "Nico Rosberg", "317" },
new string[] { "3.", "David Ricciardo", "238" },
new string[] { "4.", "Valtteri Botas", "186" },
new string[] { "5.", "Sebastian Vettel", "167"}
};
```

To create tables, you can add TableColumn objects to the Columns property. With TableColumn you can specify the width and background. The Table also contains TableRowGroup objects. The TableRowGroup has a Rows property whereby TableRow objects can be added. The TableRow class defines a Cells property that enables adding TableCell objects. TableCell objects can contain any Block element. Here, a Paragraph is used that contains the Inline element Run:

```
var doc = new FlowDocument();
var t1 = new Table();
t1.Columns.Add(new TableColumn
```
