# Working with Menus and Toolbars

![](bbox=[0.402, 0.092, 0.709, 0.546])

Figure 13-2

# Message Categories

There are three categories of messages that your program may be dealing with, and the category to which it belongs determines how a message is handled. The message categories are:

| Message Category | Description |
|---|---|
| Windows messages | These are standard Windows messages that begin with the WM_ prefix, with the exception of WM_COMMAND messages that we shall come to in a moment. Examples of Windows messages are WM_PAINT, which indicates that you need to redraw the client area of a window, and WM_LBUTTONUP, which signals that the left mouse button has been released. |
| Control notification messages | These are WM_COMMAND messages sent from controls (such as a list box) to the window that created the control or from a child window to a parent window. Parameters associated with a WM_COMMAND message enable messages from the controls in your application to be differentiated. |

*Table continued on following page*