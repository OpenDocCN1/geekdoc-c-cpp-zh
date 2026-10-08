# 14.11 Mouse-Event Handling

This section explains how to handle mouse events, such as clicks and moves, which are generated when the user interacts with a control via the mouse. Mouse events can be handled for any control that derives from System.Windows.Forms.Control. For mouse events, information about the event is passed to the event-handling method through an object of MouseEventArgs, and the delegate used to create the mouseevent handlers is EventHandler. Each mouse-handling method for these events requires an object and a MouseEventArgs as arguments.

Class MouseEventArgs contains information related to the mouse event, such as the mouse's x- and y-coordinates, the mouse button pressed (Left, Right or Middle) and the number of times the mouse was clicked. The x- and y-coordinates of the MouseEventArgs are relative to the control that generated the event—i.e., point (0,0) represents the upper-left corner of the control where the mouse event occurred. Several mouse events and event arguments are described in Fig. 14.37.

![](bbox=[0.122, 0.381, 0.877, 0.725])

+   * Mouse Events with Argument of Type MouseEventArgs
* MouseEnter: Mouse cursor enters the control's boundaries.
* MouseHover: Mouse cursor hovers within the control's boundaries.
* MouseLeave: Mouse cursor leaves the control's boundaries.
* MouseDown: Mouse button is pressed while the cursor is within a control's boundaries.
* MouseMove: Mouse cursor is moved within the control's boundaries.
* MouseUp: Mouse button is released when the cursor is over the control's boundaries.
* MouseWheel: Mouse wheel is moved while the cursor has the focus.
* Class MouseEventArgs Properties
* Button: Specifies which mouse button was pressed (Left, Right, Middle or None).
* Clicks: The number of times the mouse button was clicked.
* X: The x-coordinate within the control where the event occurred.
* Y: The y-coordinate within the control where the event occurred.

Fig. 14.37  | Mouse events and event arguments.

Figure 14.38 uses mouse events to draw on a Form. Whenever the user drags the mouse (i.e., moves the mouse while a mouse button is pressed), small circles appear at the position where each mouse event occurs during the drag operation. In line 12, the program declares property ShouldPaint, which determines whether to draw on the Form. We want the program to draw only when the mouse button is pressed (i.e., held down). Thus, when the user clicks or holds a mouse button, the system generates a MouseDown event, and the event handler (lines 21–25) sets ShouldPaint to true. When the user releases the mouse, the system generates a MouseUp event, ShouldPaint is set to false in the PainterForm_Mouse event handler (lines 28–32) and the program stops