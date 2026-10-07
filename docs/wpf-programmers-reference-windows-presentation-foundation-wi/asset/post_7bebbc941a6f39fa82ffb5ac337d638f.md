
# Common Properties

This appendix summarizes properties that are common to many WPF controls. See the earlier chapters and the following appendices for more information about specific kinds of controls.

## GENERAL PROPERTIES

Table A-1 summarizes general properties that apply to many controls. Note that not all properties apply to all control types.

Table A-1: General Properties

| PROPERTY | PURPOSE |
|---|---|---|
| AcceptsReturn | Determines whether a [Return] character is inserted into a TextBox or RichTextBox, or whether a [Return] character in this control is ignored. |
| AcceptsTab | Determines whether a [Tab] character is inserted into a TextBox or RichTextBox, or whether a [Tab] character moves focus to the next control. |
| Background | The control's background color |
| BorderBrush | Determines the color of the control's border. Note that you must set BorderBrush to a visible color and BorderThickness to a value >0 before you can see the border. |
| BorderThickness | Determines the thickness of the control's border. Note that you must set BorderBrush to a visible color and BorderThickness to a value >0 before you can see the border. |

## TABLE A-1 (continued)

| PROPERTY | PURPOSE |
| --- | --- |
| Content | The content that the control should contain. Some controls (such as Button and Label) can hold only a single child as content, while others (such as Grid and StackPanel) can have many children. If a control can display text (such as a Button or Label), then you can set the Content property to a string for the control to display. |
| ContextMenu | The ContextMenu that the control should display when the cursor right-clicks on it |
| Cursor | Determines the cursor displayed by the control. This can be None, No, Arrow, AppStarting, Cross, Beam, SizeAll, SizeNSES, SizeNWSE, SizeWE, ScrollNS, ScrollWE, Scroll, ScrollW, Pen, ScrollIS, ScrollIE, ScrollNW, ScrollNE, ScrollSW, ScrollSE, UpArrow, Wait, Hand, ArrowCD. |
| Foreground | The control's foreground color, usually used for text |
| Header | Some controls that display two kinds of content use a Content property for one kind and a Header for the other. For example, a GroupBox displays a caption (Header) in addition to content contained inside the GroupBox's border (Content). A few other controls such as TreeButtonItem also use a Header property to hold special kinds of content. |
| Height | Determines the control's absolute height. Often interfaces are more flexible if you let the control stretch to fill its parent rather than setting value explicitly. |
| HorizontalAlignment | Determines whether the control is aligned horizontally to the left, center, or right in its container. The special value Stretch makes the control try to fill its container. |
| HorizontalContentAlignment | Determines how content is aligned horizontally within the control. For example, you can use this property to align the text within a Label. |
| HorizontalScrollVisibility | Determines whether the horizontal scrollbar is visible. This property takes the values Auto (displayed when needed), Disabled (not displayed), Hidden (not displayed), and Visible (always displayed). |
| IsEnabled | Determines whether the control will respond to user actions. |

## General Properties

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
| MinHeight | The maximum number of lines that a TextBox will display. This is only meaningful if AcceptsReturn is True. |
| MinWidth | The smallest width the control will give |
| Name | The maximum number of lines that a TextBox will display. This is only meaningful if AcceptsReturn is True. |
| Opacity | Determines the opacity of the control. This can take values between 0 and 1. |
| Padding | Determines the extra space added inside the control's border |
| Parent | The transformation used to translate, scale, rotate, and skew the control before its container arranges its children |
| RenderTransform | The transformation used to translate, scale, rotate, and skew the control before its container arranges its children |
| Resources | The resources defined by the control. |
| SelectionStart | Gets or sets the starting position of the TextBox. |
| SelectionText | Gets or sets the text in the TextBox. |
| Style | Determines the style used by the control. |
| Tab | Determines the tab order. |
| Tag | Any arbitrary data you want to attach to the control |
| Text | Determines the text in a TextBox. |
| TextAlignment | Determines how text is arranged in a TextBox. This can be Center, Justify, Left, or Right. |
| ToolTip | The text that the control should display in a tooltip when the mouse hovers over it |

## TABLE A-1 (continued)

| PROPERTY | PURPOSE |
| --- | --- |
| Padding | The extra space added inside the control's border |
| Parent | The transformation used to translate, scale, rotate, and skew the control before its container arranges its children |
| RenderTransform | The transformation used to translate, scale, rotate, and skew the control before its container arranges its children |
| Resources | The resources defined by the control. |
| SelectionStart | Gets or sets the starting position of the TextBox. |
| SelectionText | Gets or sets the text in the TextBox. |
| Style | Determines the style used by the control. |
| Tab | Determines the tab order. |
| Tag | Any arbitrary data you want to attach to the control |
| Text | Determines the text in a TextBox. |
| TextAlignment | Determines how text is arranged in a TextBox. This can be Center, Justify, Left, or Right. |
| ToolTip | The text that the control should display in a tooltip when the mouse hovers over it |

## Font Properties

| PROPERTY | PURPOSE |
| --- | --- |
| VerticalAlignment | Determines whether the control is aligned vertically to the top, center, or bottom in its container. The special value Stretch makes the control try to fill its container. |
| VerticalContentAlignment | Determines how content is aligned vertically within the control. For example, you can use this property to align the text within a Label. |
| VerticalScrollVisibility | Determines whether the control's vertical scrollbar is visible. This can take the values Auto (displayed when needed), Disabled (not displayed), Hidden (not displayed), and Visible (always displayed). |
| Visibility | Determines whether the control is visible. This can take the values Visible (as usual), Hidden (not visible but the layout saves room for it), and Collapsed (not visible and the layout does not save room for it). |
| Width | Determines the control's absolute width. Often interfaces are more flexible if you let the control stretch to fill its parent rather than setting this value explicitly. |

# FONT PROPERTIES

Table A-2 summarizes font properties. These are useful for controls that display text as well as containers that may hold controls that display text. In particular, you can set these properties for a Window, and all of the controls in the Window use them.

Table A-2: Font Properties

| PROPERTY | PURPOSE |
| --- | --- |
| FontFamily | The name of the font such as Times New Roman or Arial. Microsoft's preferred font for Vista applications is Segoe (pronounced see-go). |
| FontSize | The size, by default in pixels. Append cm, px, or pt to specify centimeters, inches, pixels (the default), or points (1/72 inch) as "0.25in" or "12pt.\ |
| FontStyle | The font's style. This can be Normal, Italic, or Oblique (simulates italic for fonts without any italic style). |
