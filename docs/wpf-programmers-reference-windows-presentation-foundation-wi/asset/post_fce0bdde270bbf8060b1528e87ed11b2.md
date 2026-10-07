
# EXAMPLE Using RadioButton

The following code creates GroupBoxes that let the user select a T-shirt's color, size, and design. Each GroupBox contains a RadioButton group.

```xml
<GroupBox Header="Color">
  <StackPanel>
  <RadioButton Content="Bisque"/>
  <RadioButton Content="BlanchedAlmond"/>
  <RadioButton Content="Teal"/>
  <RadioButton Content="Thistle"/>
  </StackPanel>
</GroupBox>
<GroupBox Header="Size">
  <StackPanel>
  <RadioButton Content="Small"/>
  <RadioButton Content="Medium"/>
  <RadioButton Content="Large"/>
  </StackPanel>
</GroupBox>
<GroupBox Header="Design">
  <StackPanel>
  <RadioButton Content="Smiley"/>
  <RadioButton Content="Heart"/>
  <RadioButton Content="VB"/>
  <RadioButton Content="C#"/>
  </StackPanel>
</GroupBox>
```

# REPEATBUTTON

The RepeatButton acts like a normal Button except it repeatedly fires its Click event as long as the user holds the down (see Tables D-24 and D-25).

TABLE D-24: Key Properties of RepeatButton

| PROPERTY | PURPOSE |
| --- | --- |
| Delay | Determines the time in milliseconds after the button is pressed that it starts repeating events. |
| Interval | Determines the time in milliseconds between repeated Click events. |

TABLE D-25: Key Events for RepeatButton

| EVENT | PURPOSE |
| --- | --- |
| Click | Occurs when the control is first pressed and when repeat clicks occur. |

# EXAMPLE Using RepeatButton

The following code creates a Rectangle and two RepeatButtons. The btnWider Click and btnThinner Click event handlers the Buttons' Click events.

```xml
<Rectangle Name="rect" Fill="Red" Width="100" Height="100"/>
<RepeatButton Content="Wider" Delay="250" Interval="50"
Clicks="btnWider_Click" />
<RepeatButton Content="Thinner" Delay="250" Interval="50"
Clicks="btnThinner_Click" />
```

The following C# code shows the event handlers:

```csharp
// Make the Rectangle wider
private void btnWider_Click(object sender, RoutedEventArgs e)
{
    rectColor.Width += 10;
}

// Make the Rectangle thinner.
private void btnThinner_Click(object sender, RoutedEventArgs e)
{
    if (rectColor.Width > 10) rectColor.Width -= 10;
}
```

When you press the Wider button, the event immediately makes the rectangle 10 pixels wider. A quarter-second (250 milliseconds) later, the first click occurs, and the event handler widens the rectangle again. Every 50 milliseconds after you release the mouse, the Click event fires again, and the event handler wisely the control.

The Thinner button works similarly.

# RICHTEXTBOX

The RichTextBox lets the user enter formatted text (see Table D-26). Place a FlowDocument with formatting inside the RichTextBox. For more information on FlowDocuments, see the section “FlowDocument” in Appendix B.

TABLE D-26: Key Properties of RichTextBox

| PROPERTY | PURPOSE |
|---|---|
| AcceptsReturn | Determines whether the control accepts the [Return] key and creates a new line. |
| AcceptsTab | Determines whether the control accepts the [Tab] key or whether that key moves focus to another control. |
| AutoWordSelection | Determines whether the control automatically selects entire words if the user drags the mouse across them. |

# RichTextBox | 477

| PROPERTY | PURPOSE |
| --- | --- |
| CanRedo | Returns True if the control has an undone action that it can redo. |
| CanUndo | Returns True if the control has an action that it can undo. |
| CaretPosition | Gets or sets the current insertion position. |
| Document | Gets or sets the FlowDocument displayed by the control. |
| IsReadOnly | Determines whether the control can interact with the user. |
| Selection | Returns a Selection object that represents the current selection. That Object's property returns the plaintext. |
| SpellCheck | Returns a SpellCheck object that manages spell-checking for the control. Its IsEnabled property determines whether the control highlights misspelled words. |
| SpellCheck.IsEnabled | Enables or disables spell-checking. |
| UndoLimit | Determines the number of actions stored in the Undo queue. |

The TextBox has many important methods that you may need to use (see Tables D-27 and D-28).

| METHOD | PURPOSE |
| --- | --- |
| AppendText | Adds text to the end of the control's contents. |
| BeginChange | Starts adding changes into a change block created by DeclareChangeBlock. |
| Copy | Copies the control's current selection to the clipboard. |
| Cut | Cuts the control's current selection to the clipboard. |
| DeclareChangeBlock | Creates a change block to group subsequent changes as a single group for undo and redo. |
| EndChange | Stops adding changes into a change block created by DeclareChangeBlock. |
| GetNextSpellingError | Returns a TextPointer that represents the position of the next spelling error. |
| GetSpellingError | Returns a SpellingError object for any spelling error at a given point. |
| GetSpellingErrorRange | Returns a TextRange object for any spelling error at a given point. |

# TABLE D-27 (continued)

| METHOD | PURPOSE |
| --- | --- |
| LineDown | Scrolls the control's contents down one line. |
| LineLeft | Scrolls the control's contents left one line. |
| LineRight | Scrolls the control's contents right one line. |
| LineUp | Scrolls the control's contents up one line. |
| PageDown | Scrolls the control's contents down one page. |
| PageLeft | Scrolls the control's contents left one page. |
| PageRight | Scrolls the control's contents right one page. |
| PageUp | Scrolls the control's contents up one page. |
| Paste | Pastes the clipboard's contents over the control's current selection. |
| Redo | Redoes the most recently undone action. |
| ScrollToEnd | Scrolls to the end of the content. |
| ScrollToHome | Scrolls to the beginning of the control's content. |
| SelectAll | Selects all of the control's contents. |
| Undo | Undoes the most recently performed action. |

# TABLE D-28:

| EVENT | PURPOSE |
| --- | --- |
| Changed | Occurs when the control's contents change. |

# EXAMPLE Using RichTextBox

The following code shows how the RichTextBox responds when the user selects a font. For example, if the user selects a font, the code makes font name display Arial.

```csharp
// Display the selection's properties.
private void rchNotes.SelectionChanged(object sender, RoutedEventArgs e)
{
  if (rchNotes == null) return;

  // Font family.
  FontFamily font_family = rchNotes.Selection.GetPropertyValue(TextElement.FontFamily) as FontFamily;
  if (font_family == null)
  {
    cbo.Text = "";
  } else
    cbo.Text = font_family.Source;
  }

  // Size.
  cbo.Text = rchNotes.Selection.GetPropertyValue(TextElement.FontSize).ToString();

  // Color.
  SolidColorBrush br = rchNotes.Selection.GetPropertyValue(TextElement.ForegroundProperty) as SolidColorBrush;
  if (br == null)
  {
    cboColor.Text = "";
  } else
    switch (br.Color.ToString())
    {
        case "Black":
            // ...
            break;
        case "Red":
            // ...
            break;
        case "Green":
            // ...
            break;
    }
}
```

The code again checks that the user has made a selection and converts the newly selected item into a string. It uses a switch statement to fix the correct color. The code for the other ComboBoxes is similar to these two examples. The following code executes when the RichTextBox's selection changes. For example, if the user moves the insertion cursor or clicks-drags to select a new piece of text, the selection changes and this code updates the ComboBoxes to display the values that actually apply to the new selection.

![FIGURE-1](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_517_0.png)
