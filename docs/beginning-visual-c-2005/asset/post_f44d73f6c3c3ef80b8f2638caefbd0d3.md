
## Working with Status Bars

With each view now being scaled independently, it becomes necessary to have some indication of what the current scale in a view is. A convenient way to do this would be to display the scale in the status bar that was created by default in the Sketcher application. By default the status bar appears at the bottom of the application window, below the horizontal scrollbar, although you can arrange for it to be at the top of the client area. The status bar is divided into segments called panes; the status bar in Sketcher has four panes. The one on the left contains the text Ready, and the other three are the recessed areas on the right that are used to record when CAPS lock, NUM lock and SCROLL lock are in effect.

It’s possible for you to write to the status bar that the Application wizard supplied by default, but you need to get access to the m_wndStatusBar member of the CMainFrame object for the application as this represents it. As it’s a protected member of the class, you must add a public member function to modify the status bar from outside the class. You could add the following public function member to the CMainFrame class to do this:

```
void CMainFrame::SetPaneText(int Pane, LPCTSTR Text)
{
    m_wndStatusBar.SetPaneText(Pane, Text);
}
```

The implementation goes in the .cpp file and you must add a declaration for the function to the class definition. The SetPaneText() function sets the text specified by the second parameter, Text, in the pane identified by the first parameter, Pane, in the status bar object represented by m_wndStatusBar. The status bar panes are indexed from the left, starting at 0. Now you can write to the status bar from anywhere outside the CMainFrame class using this function. For example:

```
CMainFrame* pFrame = (CMainFrame*)AfxGetApp()->m_pMainWnd;
pFrame->SetPaneText(0, "Goodbye cruel world");
```

This code fragment gets a pointer to the main window of the application and outputs the text string you see to the left-most pane in the status bar. This is fine, but the main application window is no place for a view scale. You may well have several views in Sketcher, so you really want to associate displaying the scale with each view. A better approach would be to give each child window its own status bar. The m_wndStatusBar in CMainFrame is an instance of the CStatusBar class. You can use the same class to implement your own status bars.

## Adding a Status Bar to a Frame

The CStatusBar class defines a control bar with multiple panes in which you can display information. Objects of type CStatusBar can also provide the same functionality as the Windows common status bar control through a member function GetStatusBarCtrl(). There is an MFC class that specifically encapsulates each of the Windows common controls — the one for the common status bar control is CStatusBarCtrl. However, using this directly involves quite a bit of work to integrate it with the other MFC classes, as the raw Windows control doesn’t connect to MFC. Using CStatusBar in our Sketcher program is easier and safer. The GetStatusBarCtrl() function returns a reference to a CStatusBarCtrl object that provides all the functionality of the common control, and the CStatusBar object takes care of the communications to the rest of the MFC.

The first step to utilizing it is to add a data member for the status bar to the definition of CChildFrame, which is the frame window for a view, so add the following declaration to the public section of the class:

```
CStatusBar m_StatusBar;        // Status bar object
```

> A little clarification may be required at this point. Status bars should be part of the frame, not part of the view. You don’t want to be able to scroll the status bars or draw over them. They should just remain anchored to the bottom of the window. If you added a status bar to the view, it would appear inside the scrollbars and would be scrolled whenever you scrolled the view. Any drawing over the part of the view containing the status bar would cause the bar to be redrawn, leading to an annoying flicker. Having the status bar as part of the frame avoids these problems.

You should initialize the m_StatusBar data member just before the visible view window is displayed. So, using the Properties window for the CChildFrame class, add a function to the class that is called in response to the WM_CREATE message that is sent to the application when the window is to be created. Add the following code to the OnCreate() handler:

```
int CChildFrame::OnCreate(LPCREATESTRUCT lpCreateStruct)
{
    if(CMDIChildWnd::OnCreate(lpCreateStruct) == -1)
        return -1;

    // Create the status bar
    m_StatusBar.Create(this);

    // Work out the width of the text we want to display
    CRect textRect;
    CClientDC aDC(&m_StatusBar);
    aDC.SelectObject(m_StatusBar.GetFont());
    aDC.DrawText(_T("View Scale:99"), -1, textRect, DT_SINGLELINE|DT_CALCRECT);

    // Setup a part big enough to take the text
    int width = textRect.Width();
    m_StatusBar.GetStatusBarCtrl().SetParts(1, &width);

    // Initialize the text for the status bar
    m_StatusBar.GetStatusBarCtrl().SetText(_T("View Scale:1"), 0, 0);
    return 0;
}
```

The generated code isn’t shaded. There’s a call to the base class version of the OnCreate() function, which takes care of creating the definition of the view window. It’s important not to delete this function call; otherwise, the window is not created.

## Chapter 16

The Create() function in the CStatusBar object creates the status bar. The this pointer for the current CChildFrame object is passed to the Create() function, setting up a connection between the status bar and the window that owns it. Take a look at what's happening in the code that you have added to the OnCreate() function.

### Defining the Status Bar Parts

A CStatusBar object has an associated CStatusBarCtrl object with one or more parts. Parts and panes in the context of status bars are equivalent terms—CStatusBar refers to panes and CStatusBarCtrl refers to parts. You can display a separate item of information in each part.

You can define the number of parts and their widths by a call to SetParts() member of the CStatusBarCtrl object. This function requires two arguments. The first argument is the number of parts in the status bar, and the second is an array specifying the right edge of each part in client coordinates. If you omit the call to SetParts(), the status bar has one part by default, which stretches across the whole bar; you could use this, but it looks untidy. A better approach is to size the part so that the text to be displayed fits nicely, and this is what you will do in Sketcher.

The first thing you do in the OnCreate() function is to create a temporary CRect object in which you'll store the enclosing rectangle for the text that you want to display. You then create a ClientDC object which contains a device context with the same extent as the status bar. This is possible because the status bar, like all other controls, is just a window.

Next, the font used in the status bar (set up as part of the desktop properties) is selected into the device context by calling the SelectObject() function. The GetFont() member of m_StatusBar returns a pointer to a CFont object that represents the current font. Obviously, the particular font used determines how much space the text that you want to display takes up.

You call the DrawText() member of the CClientDC object to calculate the enclosing rectangle for the text you want to display. This function has four arguments:
- The text string you need to drawn. You have passed a string containing the maximum number of characters you would ever want to display, "View Scale:99".
- The count of the number of characters in the string. You have specified this as -1, which indicates you are supplying a null-terminated string. In this case the function works out the character count.
- Your rectangle, textRect. The enclosing rectangle for the text is stored here in logical coordinates.
- One or more flags controlling the operation of the function.

You have specified a combination of two flags; DT_SINGLELINE specifies that the text is to be on a single line, and DT_CALCRECT specifies that you want the function to calculate the size of the rectangle required to display the string and store it in the rectangle pointed to by the third argument. The DrawText() function is normally used to output text, but in this instance the DT_CALCRECT flag stops the function from actually drawing the string. There are a number of other flags that you can use with this function; you can find details about them by looking up this function with Help.
