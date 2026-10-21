# # Chapter 16

The Create() function in the CStatusBar object creates the status bar. The this pointer for the current CChildFrame object is passed to the Create() function, setting up a connection between the status bar and the window that owns it. Take a look at what's happening in the code that you have added to the onCreate() function.

# ## Defining the Status Bar Parts

A CStatusBar object has an associated CStatusBarCtrl object with one or more parts. Parts and panes in the context of status bars are equivalent terms—CStatusBar refers to panes and CStatusBarCtrl refers to parts. You can display a separate item of information in each part.

You can define the number of parts and their widths by a call to SetParts() member of the CStatusBarCtrl object. This function requires two arguments. The first argument is the number of parts in the status bar, and the second is an array specifying the right edge of each part in client coordinates. If you omit the call to SetParts(), the status bar has one part by default, which stretches across the whole bar; you could use this, but it looks untidy. A better approach is to size the part so that the text to be displayed fits nicely, and this is what you will do in Sketcher.

The first thing you do in the onCreate() function is to create a temporary CRect object in which you'll store the enclosing rectangle for the text that you want to display. You then create a ClientDC object which contains a device context with the same extent as the status bar. This is possible because the status bar, like all other controls, is just a window.

Next, the font used in the status bar (set up as part of the desktop properties) is selected into the device context by calling the SelectObject() function. The GetFont() member of m_StatusBar returns a pointer to a CFont object that represents the current font. Obviously, the particular font used determines how much space the text that you want to display takes up.

You call the DrawText() member of the CClientDC object to calculate the enclosing rectangle for the text you want to display. This function has four arguments:

+   - The text string you need to drawn. You have passed a string containing the maximum number of characters you would ever want to display, "View Scale:99".
+   - The count of the number of characters in the string. You have specified this as -1, which indicates you are supplying a null-terminated string. In this case the function works out the character count.
+   - Your rectangle, textRect. The enclosing rectangle for the text is stored here in logical coordinates.
+   - One or more flags controlling the operation of the function.

You have specified a combination of two flags; DT_SINGLELINE specifies that the text is to be on a single line, and DT_CALCRECT specifies that you want the function to calculate the size of the rectangle required to display the string and store it in the rectangle pointed to by the third argument. The DrawText() function is normally used to output text, but in this instance the DT_CALCRECT flag stops the function from actually drawing the string. There are a number of other flags that you can use with this function; you can find details about them by looking up this function with Help.