Class MouseEventArgs contains information related to the mouse event, such as the mouse pointer's x- and y-coordinates, the mouse button pressed (Right, Left or Middle) and the number of times the mouse was clicked. The x- and y-coordinates of the MouseEventArgs object are relative to the control that generated the event—i.e., point (0,0) represents the upper-left corner of the control where the mouse event occurred. Several common mouse events and event arguments are described in Fig. 14.37.

Mouse events and event arguments

Mouse Events with Event Argument of Type EventArgs
MouseEnter | Mouse cursor enters the control's boundaries.
MouseHover | Mouse cursor hovers within the control's boundaries.
MouseLeave | Mouse cursor leaves the control's boundaries.

Mouse Events with Event Argument of Type MouseEventArgs
MouseDown | Mouse button is pressed while the mouse cursor is within a control's boundaries.
MouseMove | Mouse cursor is moved while in the control's boundaries.
MouseUp | Mouse button is released when the cursor is over the control's boundaries.
MouseWheel | Mouse wheel is moved while the control has the focus.

Class MouseEventArgs Properties
Button | Specifies which mouse button was pressed (Left, Right, Middle or None).
Clicks | The number of times that the mouse button was clicked.
X | The x-coordinate within the control where the event occurred.
Y | The y-coordinate within the control where the event occurred.

Fig. 14.37 | Mouse events and event arguments.

Figure 14.38 uses mouse events to draw on a Form. Whenever the user drags the mouse (i.e., moves the mouse while a mouse button is pressed), small circles appear on the Form at the position where each mouse event occurs during the drag operation.

```
```csharp
// Fig. 14.38: PainterForm.cs
// Using the mouse to draw on a Form.
using System;
using System.Drawing;
using System.Windows.Forms;

namespace Painter
{
    // creates a Form that's a drawing surface
    public partial class PainterForm : Form
    {
        bool ShouldPaint { get; set; } = false; // whether to paint
```
```

Fig. 14.38 | Using the mouse to draw on a Form. (Part 1 of 2.)