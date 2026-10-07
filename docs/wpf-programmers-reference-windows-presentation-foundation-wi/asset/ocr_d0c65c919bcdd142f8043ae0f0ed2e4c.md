# General Properties

| PROPERTY | PURPOSE |
| --- | --- |
| IsReadOnly | Determines whether the user can modify the text in a TextBox or RichTextBox. Even if IsReadOnly is True, the user can select text and press [Ctrl]+C to copy it to the clipboard, so this is a useful technique for displaying text the user might not want to. |
| IsTabStop | Determines whether the user can tab to a focusable control. Even if IsTabStop is False, the user can click on the control to give it focus. |
| IsUndoEnabled | Determines whether the user can press [Ctrl]+Z and [Ctrl]+Y to undo and redo changes in a TextBox or RichTextBox. |
| LayoutTransform | The transformation used to translate, scale, rotate, and skew the control before its container arranges its children |
| Margin | Determines how much space is left around the control within its container. This property can include one value (all margins use the same value), two values (left/right and top/bottom) or four values (left, top, right, and bottom). |
| MaxHeight | The largest height the control will give |
| MaxLines | The maximum number of lines that a TextBox will display. This is only meaningful if AcceptsReturn is True. |
| MaxWidth | The smallest width the control will give |
| MinHeight | The minimum number of lines that a TextBox will display. This is only meaningful if AcceptsReturn is True. |
| MinWidth | The smallest width the control will give |
| Name | The control's name. This is often not needed if no XAML or codebehind refers to the control. |
| Opacity | Determines how opaque the control is. The value 0 means completely transparent and 1 means completely opaque (although Expression Blend displays values between 0 and 100 in the Properties window). |
| OpacityMask | A brush that determines the opacity at parts of the control. This is a gradient brush or is defined by an image. Note that only the alpha components of the brush's colors matter and the red, green, and blue components are ignored. |

continues