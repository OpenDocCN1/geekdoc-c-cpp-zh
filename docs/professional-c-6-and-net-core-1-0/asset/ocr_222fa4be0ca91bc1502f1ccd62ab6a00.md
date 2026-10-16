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