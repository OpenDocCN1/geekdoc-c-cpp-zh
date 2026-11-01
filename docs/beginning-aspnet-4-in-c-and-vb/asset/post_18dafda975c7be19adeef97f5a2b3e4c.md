
The image is sized and positioned in the control. The SizeMode property can be AutoSize, CenterImage, Normal, and StretchImage.

You can change the size of the display of the PictureBox by setting the ClientSize property. You load the PictureBox by first creating an Image-based object. For example, to load a JPEG file into a PictureBox, you would do the following:

```
Bitmap myJpeg = Bitmap.FromFile("whatever.png") as Bitmap;
pictureBox1.Image = myJpeg;
```

## ProgressBar
The ProgressBar control is a visual clue to the status of a lengthy operation. It indicates to users that there is something going on and that they should wait. The ProgressBar control works by setting the Minimum and Maximum properties, which correspond to the progress indicator being all the way to the left (Minimum) or all the way to the right (Maximum). You set the Step property to determine the number that the value is incremented each time the PerformStep method is called. You can also use the Increment method and increment the value by the value passed in the method call. The Value property returns the current value of the ProgressBar.

## TextBox, RichTextBox, and MaskedTextBox
The TextBox control is one of the most used controls in the toolbox. The TextBox, RichTextBox, and MaskedTextBox controls are all derived from TextBoxBase. TextBoxBase provides properties such as MultiLine and Lines. MultiLine is a Boolean value that allows the TextBox control to display text in more than one line. Each line in a text box is a part of an array of strings. This array is exposed through the Lines property. The Text property returns the entire text box contents as a single string. TextLength is the total length of the string that text will return. The MaxLength property will limit the length of the text to the specified amount.

SelectedText, SelectionLength, and SelectionStart all deal with the currently selected text in the text box. The selected text is highlighted when the control has focus.

The TextBox control adds a couple of interesting properties. AcceptsReturn is a Boolean value that will allow the TextBox to capture the Enter key. If the value is set to false, the Enter key clicks the default button on the form. When AcceptsReturn is set to true, pressing the Enter key creates a new line in the TextBox. CharacterCasing determines the casing of the text in the text box. The CharacterCasing enumeration contains three values, Lower, Normal, and Upper. Lower lowercases all text regardless of how it is entered, Upper renders all text in uppercase letters, and Normal displays the text as it is entered. The PasswordChar property takes a char that represents what is displayed to the users when they type text in the text box. This is typically used for entering passwords and PINs. The Text property will return the actual text that was entered; only the display is affected by this property.

The RichTextBox is a text-editing control that can handle special formatting features. As the name implies, the RichTextBox control uses Rich Text Format (RTF) to handle the special formatting. You can make formatting changes by using the Selection properties: SelectionFont, SelectionColor, and SelectionBullet, and paragraph formatting with SelectionIndent, SelectionRightIndent, and SelectionHangingIndent. All of the Selection properties work in the same way. If a section of text is highlighted, a change to a Selection property affects the selected text. If no text is selected, the change takes effect with any text that is inserted to the right of the current insertion point.

The text of the control can be retrieved by using the Text property or the Rtf property. The Text property returns just the text of the control, whereas the Rtf property returns the formatted text.

The LoadFile method can load text from a file in a couple of different ways. It can use a string that represents the path and filename or it can use a stream object. You can also specify the RichTextBoxStreamType. The following table lists the values of RichTextBoxStreamType.

| VALUE | DESCRIPTION |
|---|---|
| PlainText | No formatting information. In places that contained OLE objects, spaces are used. |
| RichTextNoOleObjs | Rich Text formatting, but spaces where the OLE objects would have been. |
| RichText | Formatted RTF with OLE objects in place. |
| PlainTextOleObjs | Plain text with text replacing the OLE objects. |
| UnicodePlainText | Same as PlainText but Unicode encoded. |

The SaveFile method works with the same parameters, saving the data from the control to a specified file. If a file by that name already exists, it will be overwritten. In the example, an RTF file is included as a resource in the application, and this text is loaded into the control when the form is loaded.

The MaskedTextBox has the ability to limit what the user may input into the control. It also allows for automatic formatting of the data entered. Several properties are used in order to validate or format the user's input. Mask is the property that contains the mask string, which is similar to a format string. The number of characters allowed, the data type of allowed characters, and the format of the data are all set using the Mask string. A MaskedTextProvider-based class can also provide the formatting and validation information needed. The MaskedTextProvider can only be set by passing it in on one of the constructors.

Three different properties will return the text of the MaskedTextBox. The Text property returns the text of the control at the current moment. This could be different, depending on whether or not the control has focus, which depends on the value of the HidePromptOnLeave property. The prompt is a string that users see to guide them on what should be entered. The InputText property always returns just the text that the user entered. The OutputText property returns the text formatted according to the IncludeLiterals and IncludePrompt properties. If, for example, the mask is for a phone number, the Mask string might include parentheses and a couple of dashes. These would be the literal characters and would be included in the OutputText property if the IncludeLiterals property were set to true.

A couple of extra events also exist for the MaskedTextBox control. OutputTextChanged and InputTextChanged are raised when InputText or OutputText changes.

## Panel
A Panel is simply a control that contains other controls. Grouping controls together and placing them in a panel makes it a little easier to manage them. For example, you can disable all of the controls in the panel by disabling the panel. Because the Panel control is derived from ScrollableControl, you can also get the advantage of the AutoScroll property. If you have too many controls to display in the available area, place them in a Panel and set AutoScroll to true — now you can scroll through all of the controls.

Panels do not show a border by default, but by setting the BorderStyle property to something other than none, you can use the Panel to visually group related controls using borders. This makes the user interface more user-friendly.

Panel is the base class for the FlowLayoutPanel, TableLayoutPanel, TabPage, and SplitterPanel. Using these controls, you can create a very sophisticated and professional-looking form or window. The FlowLayoutPanel and TableLayoutPanel are especially useful for creating forms that resize properly.

## FlowLayoutPanel and TableLayoutPanel
FlowLayoutPanel and TableLayoutPanel are recent additions to the .NET Framework. As the names suggest, the panels offer the capability to lay out a form using the same paradigm as a Web Form. FlowLayoutPanel is a container that allows the contained controls to flow in either the horizontal or vertical direction. Instead of wrapping, it allows for the clipping of the controls. Flow direction is set using the FlowDirection property and the FlowDirection enumeration. The WrapContents property determines if controls flow to the next row or column when the form is resized or if the control is clipped.
