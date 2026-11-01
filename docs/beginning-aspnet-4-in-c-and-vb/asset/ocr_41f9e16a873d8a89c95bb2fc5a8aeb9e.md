```
```
</StackPanel>
<TextBox Grid.Row="1" Grid.Column="0" Width="140"></TextBox>
</Grid>
</InlineUIContainer>
</Paragraph>
```
```

code snippet FlowDocumentsDemo/FlowDocument2.xaml

# Block

Block is an abstract base class for block-level elements. Blocks allow grouping elements contained to specific views. Common with all blocks are the properties PreviousBlock, NextBlock, and SiblingBlocks that allow you to navigate from block to block. Setting BreakPageBefore and BreakColumnBefore page and column breaks are done before the block starts. A Block also defines a border with the BorderBrush and BorderThickness properties.

Classes that derive from Block are Paragraph, Section, List, Table, and BlockUIContainer. BlockUIContainer is similar to InlineUIContainer in that you can add elements that derive from UIElement.

Paragraph and Section are simple blocks where Paragraph contains inline elements; Section is used to group other Block elements. With the Paragraph block you can determine whether a page or column break is allowed within the paragraph or between paragraphs. KeepTogether can be used to disallow breaking within the paragraph; KeepWithNext tries to keep one paragraph and the next together. If a paragraph is broken by a page or column break, MinWidowLines defines the minimum number of lines that are placed after the break and MinOrphanLines defines the minimum number of lines before the break.

The Paragraph block also allows decorating the text within the paragraph with TextDecoration elements. Predefined text decorations are defined by TextDecorations: Baseline, Overline, Strikethrough, and Underline.

The following XAML code shows multiple Paragraph elements. One Paragraph element with a title follows another with the content belonging to this title. These two paragraphs are connected with the attribute KeepWithNext. It's also assured that the paragraph with the content is not broken by setting KeepTogether to True. The result is shown in Figure 37-6.

```
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
    </Paragraph>
```
```