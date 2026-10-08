
## 14.12 Keyboard-Event Handling

![](img/57baed2319be0bb1b5f98674846f2711_623_0.png)

Whenever the mouse moves over a control, the MouseMove event for control occurs. Inside the PainterForm_MouseMove event handler (lines 35–46), the program draws only if ShouldPaint is true (i.e., a mouse button is pressed). In the using state, line 40 calls inherited from method CreateGraphics to create a Graphics object that allows the program to draw on the Form. Class Graphics provides methods to draw various shapes. For examples, lines 42–43 use method FillEllipse to draw a circle. The first parameter to method FillEllipse is an instance of class SolidBrush, as argument which specifies the solid color that will fill the shape. The color is specified by predefined color constants—we selected Color.Blueviolet. FillEllipse draws an oval in a bounding rectangle that is specified by the x- and y-coordinates of its upper-left corner, its width and height—the four arguments to the method. The x- and y-coordinates represent the location of the mouse event and can be taken from the mouse-event arguments (e.X and e.Y). To draw, we set the width and height of the bounding rectangle so that they're equal—in which there are 40 pixels. Graphics, SolidBrush and Color are all of namespace System.Drawing. Recall from Chapter 13 that the using automatically calls Dispose on the object that was created in the parentheses keyword using. This is important because Graphics objects are a limited resource. Calling Dispose on a Graphics object ensures that its resources are returned for the system.

Key events occur when keyboard keys are pressed and released. Such events can be handled for any control that inherits from System.Windows.Control. There are three key—KeyPress, KeyUp and KeyDown. The KeyPress event occur when the user presses a character or the space bar key. The specific key or KeyChar of the event handler is KeyEventArgs.

The KeyEvent does not indicate whether modifier keys (e.g., Shift, Alt and Ctrl) were pressed when a key event occurred. If this information is important, the KeyError or KeyDown can be used. The KeyEventArgs argument for each of these events contains information about modifier keys. 14.39 lists important key event information. Several properties return values from the Keys enumeration, which provides constants that specify the various keys on a keyboard. Like the FontStyle enumeration (Section 14.7), the Keys enumeration is represented with a set of bits, so the enumeration's constants can be combined with the bitwise operators to indicate multiple key pressed at the same time.

### Keyboard events and event arguments

| Key Events with Event Arguments of Type KeyEventEventArgs |
| :--- | :--- |
| KeyDown | Generated when a key is initially pressed. |
| KeyUp | Generated when a key is released. |
| Key Event with Event Argument of Type KeyPressEventArgs |
| KeyPress | Generated when a key is pressed. Raised after KeyDown and before KeyUp. |
| KeyPressEventArgsProperties |
| KeyChar | Returns the ASCII character for the key. |
| KeyEventEventArgsProperties |
| Alt | Indicates the Alt key was pressed. |
| Control | Indicates the Control key was pressed. |
| Shift | Indicates the Shift key was pressed. |
| KeyCode | Returns the code for the key as a value from the Keys enumeration. This does not include modifier-key information. It's used to test for a specific key. |
| KeyData | Returns the code for the key combined with modifier information as Keys. This property contains all information about the pressed key. |
| KeyValue | Returns the key as an int, rather than a value from the Keys enumeration. The int value is known as Windows virtual key. |
| Modifiers | Returns a value indicating any pressed keys (Alt, Ctrl and Shift). This property is used to determine modifier-key information only. |

Fig. 14.39 | Keyboard events and event arguments. Figure 14.40 demonstrates the use of key handlers to display a key pressed by user. The program is a Form with two Labels that displays the pressed key on one and modifier key information on the other.

```csharp
// Fig 14.40: KeyDemo.cs
// Displaying information about the key pressed.
using System;
using System.Windows.Forms;

namespace KeyDemo
{
    // Form to display key information when key is pressed
    public partial class KeyDemo : Form
    {
        // default constructor
        public KeyDemo()
        {
            InitializeComponent();
        }

        // display the character pressed using KeyChar
        private void KeyDemo_KeyPress(object sender, EventArgs e)
        {
            charLabel.Text = $"Key pressed: {e.KeyChar}";
        }

        // display modifiers, code, data and key value
        private void KeyDemo_KeyDown(object sender, EventArgs e)
        {
            keyInfoLabel.Text = (e.Alt ? "Yes" : "No") + "\n" +
                                $"Shift: {e.Shift ? "Yes" : "No"}\n" +
                                $"Ctrl: {e.Control ? "Yes" : "No"}\n" +
                                $"KeyCode: {e.KeyCode}\n" +
                                $"KeyData: {e.KeyData}\n";
        }

        // clear labels when key released
        private void KeyDemo_KeyUp(object sender, EventArgs e)
        {
            charLabel.Text = "";
            keyInfoLabel.Text = "";
        }
    }
}
```

![](/57baed2319be0bb1b5f98674846f2711_625_0.png)

Fig. 14.40 | Displaying information about the key pressed. (Part 2 of 3).

### Chapter 14 Graphical User Interfaces with Windows Forms: Part I

| c) A pressed | d) Tab pressed |
| :--- | :--- |
| KeyDemo A | KeyDemo Tab |
| Key pressed: A | Key pressed: Tab |
| Alt: No | Alt: No |
| Shift: Yes | Shift: No |
| Ctrl: No | Ctrl: No |
| KeyCode: A | KeyCode: Tab |
| KeyData: A, Shift | KeyData: Tab |
| KeyValue: 65 | KeyValue: 9 |

Fig. 14.40 | Displaying information about the key pressed. (Part 3 of 3.)

ControlLabel displays the character value of the key pressed, whereas keyInfoLabel displays information relating to the pressed key. because the KeyDown and KeyPress events carry different information, the Form (KeyDemo) handles both.

The KeyPress event handler (lines 18–21) accesses the KeyChar property of the KeyEventArgs object. This returns the key as a char, which we then display in charLabel (line 1). If the key is not an ASCII character, then the KeyPress event will not occur, and charLabel will not display any text. ASCII is a common encoding for letters, numbers, punctuation marks and other characters. It does not support keys such as the function keys (F1) or modifier keys (Alt, Ctrl and Shift).

The KeyDown event handler (lines 24–33) displays information from its KeyEventArgs object. The handler tests for all Alt, Shift and Control keys that the corresponding key is pressed and false if otherwise. The handler then returns the KeyCode, KeyData and KeyValue properties.

The KeyCode property returns an enumeration value (line 30). The KeyCode property returns the key, but does not provide any information about modifier keys. Thus, both a capital and a lowercase “a” are represented as A.

The KeyData property (line 31) also returns an enumeration value, but includes modifier-key data. Thus, if “A” is input, the KeyData shows both A and Shift were pressed. KeyValue(line 32) returns an integer representing the key. int is the code. The code is useful when testing for non-ASCII keys like F12.

The KeyUp event handler (lines 36–40) clears Label1 when the key is released. As we see from the output, non-ASCII keys are not displayed in charLabel, because the KeyPress event is not generated. For example, charLabel does not display any text when you press the F7 key, as shown in Fig. 14.40(b). However, the KeyDown event still is generated, and KeyInfo displays information about the key’s pressed. The Keys enumeration can be used to test for specific keys by comparing the KeyCode of the pressed key values to the Keys enumeration.
