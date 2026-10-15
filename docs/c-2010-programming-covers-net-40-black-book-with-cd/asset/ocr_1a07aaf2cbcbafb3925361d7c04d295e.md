Now, when the user enters numbers in the text boxes and clicks the Add button, the sum of the entered numbers is displayed as a message, as shown in Figure 8.60:

![](bbox=[0.355, 0.11, 0.675, 0.315])

Figure 8.60: Displaying the Sum of Two Numbers

You can find the code to handle keyboard and mouse events in the KeyboardandMouseEvent application available on the CD.

# Specifying Mouse Cursors for Windows Forms and Controls

You can use the Cursor property to set the mouse cursor type when the mouse moves over a control. As you know, a Windows Form is also derived from the Control class; therefore, cursor types are also applied to forms. You can set the Cursor property by specifying the values given in Table 8.11:

| Table 8.11: Mouse Cursor Options |
| Constant | Description |
| AppStarting | Specifies the combination of the Arrow cursor and the Wait cursor |
| Arrow | Specifies the Arrow cursor |
| Default | Specifies the Default cursor, usually an arrow cursor |
| Hand | Specifies the Hand cursor, usually used when hovering over a Web link |
| Help | Specifies the Help cursor, a combination of an arrow and a question mark |
| HSplit | Specifies the cursor that appears when the mouse is positioned over a horizontal splitter bar |
| IBeam | Specifies the I-beam cursor, which is used to show where the text cursor appears when the mouse is clicked |
| No | Specifies the cursor that indicates a particular region is invalid for the current operation |
| NoMove2D | Specifies the cursor for mouse wheel operations when the mouse is not moving; however, the window can be scrolled in either horizontal or vertical direction. |
| NoMoveHoriz | Specifies the cursor for mouse wheel operations when the mouse is not moving; however, the window can be scrolled in a horizontal direction |
| NoMoveVert | Specifies the cursor for mouse wheel operations when the mouse is not moving; however, the window can be scrolled in a vertical direction |
| PanEast | Specifies the cursor for mouse wheel operations when the mouse is moving and the window is scrolling in horizontal right direction |
| PanNE | Specifies the cursor for mouse wheel operations when the mouse is moving and the window is scrolling in north/east direction, which means either horizontal right or vertically upward direction |
| PanNorth | Specifies the cursor for mouse wheel operations when the mouse is moving and the window is scrolling vertically in an upward direction |