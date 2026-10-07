# TextBlock

The TextBlock displays read-only text as a Label does but with additional features as line wrapping, italics, and bold text (see Table B-11). The TextBlock is intended to display only a few lines of text. For more complex documents, consider using a FlowDocument. (See the "FlowDocument" section earlier in this appendix.)

You can use special inline tags or inlines to give a piece of text a special style such as bold or italic. For example, the following code text displays the text in bold in:

```
<TextBlock>A TextBlock can display <Bold>bold</Bold> text.</TextBlock>
```

# TABLE B-11: Key Properties of TextBlock

| PROPERTY | PURPOSE |
| --- | --- |
| Background | The color used to fill the control's interior |
| FontFamily | The name of the font family as Times New Roman, Arial, or Segoe |
| FontSize | The text's font size. Append cm, in, px, or pt to specify centimeters, inches, pixels (the default), or points (1/72 inch) as "25in" or "12pt". |
| FontStyle | Can be Normal, Italic, or Oblique (simulates italic for fonts without an italic style) |
| FontWeight | The text's boldness. This can be Thin, ExtraLight, Light, Normal, Medium, SemiBold, Bold, ExtraBold, Black, and ExtraBlack, although many fonts look the same for many of these values |
| Foreground | The color used to draw the text | The vertical spacing between lines. Append cm, in, px, or pt to specify centimeters, inches, pixels (the default), or points (1/72 inch) as "25in" or "12pt"
| LineSpacingStrategy | Determines how the control sizes its size. This can be maxHeight (a line is tall enough to hold all of its content) or BlockLineHeight (a line's height is determined by the control's LineHeight property). |
| Padding | The extra space added between the control's edges and the text contains |
| Text | The text displayed by the control (simple text only) |
| TextAlignment | Determines how text is aligned within the TextBlock. This can be Left, Right, Center, or Justify. |