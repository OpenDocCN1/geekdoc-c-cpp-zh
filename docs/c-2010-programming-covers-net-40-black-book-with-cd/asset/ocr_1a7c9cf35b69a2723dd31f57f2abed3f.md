![](bbox=[0.26, 0.07, 0.71, 0.31])

Figure 10.7: Showing the TextBox Control

# The RichTextBox Control

The RichTextBox control, similar to a TextBox control, enables you to display or edit content, such as paragraphs, images, and tables. A TextBox control requires fewer resources than a RichTextBox control and is ideal when only plain text needs to be edited; whereas, the RichTextBox control is ideal when the user needs to edit formatted text, images, or tables. The RichTextBox control can perform all the functions of a TextBox control, as well as some additional functions, such as displaying fonts, colors, and links; loading text and images; and finding a specified file. You can also check the spellings of your content by enabling the SpellCheck property of the RichTextBox control. When this property is set to True, a wavy red line appears under the misspelled words. The SpellCheck property is enabled by setting its SpellCheck.IsEnabled property to True. Similar to a TextBox control, the RichTextBox control also has a context menu. It appears when a user right-clicks inside the control. The RichTextBox control includes basic editing commands similar to those in the TextBox control. However, unlike the TextBox control, the RichTextBox control includes formatting commands. The RichTextBox control implements the IInputElement interface, which includes the support for many editing commands.

Table 10.10 shows the basic editing commands supported by the RichTextBox control:

| Table 10.10: Basic Editing Commands in the RichTextBox Control |
| Editing Command | Default Key |
| AlignCenter | CTRL+E |
| AlignJustify | CTRL+J |
| AlignLeft | CTRL+L |
| AlignRight | CTRL+R |
| Backspace | BACKSPACE |
| Delete | DELETE |
| DeleteNextWord | CTRL+DELETE |
| DeletePreviousWord | CTRL+BACKSPACE |
| EnterLineBreak | SHIFT+ENTER |
| EnterParagraphBreak | ENTER |
| MoveToDocumentEnd | CTRL+END |
| MoveToDocumentStart | CTRL+HOME |