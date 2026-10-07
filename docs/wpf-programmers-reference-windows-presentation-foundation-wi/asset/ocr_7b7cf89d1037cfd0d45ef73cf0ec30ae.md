# 374 | CHAPTER 21 DOCUMENTS

The ShowFlowDocument example program uses the following code to display the list shown in
Figure 21-4

```
<List MarkerStyle="Decimal">
<ListItem><Paragraph>Item one</Paragraph></ListItem>
<ListItem><Paragraph>Item two</Paragraph></ListItem>
<ListItem>
<Paragraph>
Item three. The sub-list has MarkerStyle = LowerLatin.
</Paragraph>
<List MarkerStyle="LowerLatin">
<ListItem><Paragraph>Sub-item 3a</Paragraph></ListItem>
<ListItem><Paragraph>Sub-item 3a</Paragraph></ListItem>
</List>
</Paragraph>
</ListItem>
</List>
```

![](bbox=[0.95, 0.383, 0.495, 0.597])

# Paragraph

A Paragraph groups its contents into a paragraph. A Paragraph adds some vertical space between
itself and the previous element.

A Paragraph typically contains inline elements including:

+   - Text — Plain old text

+   - Bold — Makes its text bold

+   - Figure — Embeds an area inside the ParagraphUIContainer where you can place block elements
as as a Paragraph or BlockContainer. Anchor and offset properties let you determine
where in the paragraph the Figure appears.

+   - Floater — Similar to a Figure except you cannot control exact positioning. Instead, the
FlowDocument moves the Floater to a position where it fits reasonably.