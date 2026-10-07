# INCONSISTENT INTERVALS

The RepeatButton's Interval property determines the amount of time the control tries to pause between Click events, but the actual time may vary, particularly if Interval is small. It takes a certain amount of time for the control to raise a Click event and for your program to catch and handle it.

Use the Delay and Interval properties to let the user fire Click events at a reason-speed, but don't rely on the exact timing.

![](bbox=[0.176, 0.153, 0.198, 0.273])

# RICHTEXTBOX

The RichTextBox control lets the user enter richly formatted text with such features as multiple fonts, colors, paragraphs, hanging indentation, bulleted lists, and so forth. The RichTextBox control can hold other content such as user interface elements (buttons, shapes, etc.), although there's no good way for the user to enter items at runtime.

Unfortunately, using XAML code to place content in a RichTextBox is complicated. The RichTextBox Document property contains the control's contents. The Document property should be a FlowDocument that holds other objects as Paragraphs and Tables.

The following XAML code shows how a program might create a RichTextBox and its content. Note that the word "enabled" in the control's contents is intentionally misspelled so you can see the control's built-in spell-checking feature described.

```
<RichTextBox>
<FlowDocument>
<Paragraph>
If spell checking is enabled and you left-click a misspelled word, then the menu also includes a list of possible correct spellings and an Ignore All command.</Run>
</Paragraph>
</FlowDocument>
</RichTextBox>
```

![](bbox=[0.176, 0.574, 0.198, 0.606])

Available for download on Wrox.com

UseRichTextBox

Chapter 21 has to say more about documents.

The RichTextBox is a very complex control and contains dozens of properties and methods that let you control its behavior and the format of its content. The following sections describe the RichTextBox control's most useful features. For a complete description of the control, see msdn.microsoft.com/aa90779.aspx.

# Editing Commands

The RichTextBox control automatically provides features that let the user format text. For example, if the user selects some text in the control and presses [Ctrl]+B, the RichTextBox makes the selected text bold.