The different Flow content elements in WPF are as follows:

+   - Block-level elements
+   - Inline elements
+   - InlineCollection and BlockCollection elements

# Block-level Elements

Block-level elements are used to group elements under a common parent or to apply common attributes to a group. The practical implementation of the block-level elements is shown in the Immediate Solutions section of the chapter. The different block-level elements are listed in Table 11.20:

Table 11.20: Listing Block-level Elements

| Element | Description |
|---|---|
| Paragraph | Groups the content into a paragraph |
| Section | Contains other block-level elements, such as List and Table |
| List | Creates a bulleted or numeric list |
| ListItem | Creates a particular content item in the list of elements |
| Table | Creates a table |
| BlockUIContainer | Enables UIElement, such as a Button, to be embedded in a block-derived flow content |

# Inline Elements

Inline elements are used as direct containers for content that is rendered on a screen. Elements that inherit the Inline element are either contained within a Block element or another Inline element. You see the practical implementation of Inline elements in the Immediate Solutions section of the chapter. The different Inline elements are listed in Table 11.21:

Table 11.21: Listing Inline Elements

| Element | Description |
|---|---|
| LineBreak | Creates a line break in the flow content |
| Run | Contains unformatted text |
| Span | Groups other Inline elements together |
| Figure and Floater | Embeds the content in Flow documents with placement properties that can be customized independent of the primary content flow |
| InlineUIContainer | Enables UIElements, such as Button, to be embedded in an Inline content element |

# InlineCollection and BlockCollection Elements

The InlineCollection class represents a collection of Inline elements. The child elements of the InlineCollection class are Paragraph, Span, and TextBlock. The InlineCollection class can only be created inside an element that owns this class, such as TextBlock. It cannot be instantiated directly and has no default or overloaded constructor. You can create an instance of the InlineCollection class in XAML. The inheritance hierarchy of the InlineCollection class is as follows:

```
System.Object
  System.Windows.Documents.TextElementCollection
    System.Windows.Documents.InlineCollection
```

The properties of InlineCollection class are listed in Table 11.22: