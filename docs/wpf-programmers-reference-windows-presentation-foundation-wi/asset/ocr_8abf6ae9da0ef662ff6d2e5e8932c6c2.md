# TABLE B-11 (continued)

| PROPERTY | PURPOSE |
|---|---|
| TextTrimming | Determines how text is trimmed if it doesn't fit. This can be None (text is truncated), CharacterEllipsis (text is trimmed to the nearest character and followed by an ellipsis), or WordEllipsis (text is trimmed to the nearest est word and followed by an ellipsis). |
| TextWrapping | Determines whether the control wraps across multiple lines. This can be Wrap, NoWrap, and WrapWithOverflow. |

TABLE B-12 summarizes the most useful inlines supported by the TextBlock.

# TABLE B-12: Key Inlines for TextBlock

| PROPERTY | PURPOSE |
|---|---|
| Bold | Makes the enclosed text. |
| Hyperlink | Creates a hyperlink. If the project is running in a web browser, Frame, or other host that provides navigation, you can use the NavigateUri property to the URL or filename that you opened when the user clicks on the Hyperlink. If the host does not provide navigation, you can handle the Hyperlink's RequestNavigate event using NavigateUri property is filled. You can also catch the Hyperlink's Click event. |
| InlineUIContainer | Contains a user interface element such as a Button or TextBox. |
| Italic | Makes the enclosed text italic. |
| LineBreak | Inserts a line break. |
| Run | Contains a run of formatted text. Use the Run's Foreground, Background, and other properties to format the enclosed text. |
| Span | Groups other inlines. Span can contain the inlines Bold, Figure, Floater, Hyperlink, InlineUIContainer, Italic, LineBreak, Run, Span, and Underline. |
| Underline | Makes the enclosed text underlined. |

# EXAMPLE TextBlock with Inlines

The following code creates a TextBlock that demonstrates various inlines:

```
<TextBlock Grid.Row="0" Grid.Column="0" Background="White" HorizontalAlignment="Stretch" TextWrapping="NoWrap" TextAlignment="Left">
```