The next statement sets up the parts for the status bar:

```
m_StatusBar.GetStatusBarCtrl().SetParts(1, &width);
```

The expression m_StatusBar.GetStatusBarCtrl() returns a reference to the CStatusBarCtrl object that belongs to m_StatusBar. The reference returned is used to call the SetParts() function for the object. The first argument to SetParts() defines the number of parts for the status bar — which is 1 in this case. The second argument is typically the address of an array of type int containing the x coordinate of the right hand edge of each part in client coordinates. The array has one element for each part in the status bar. Because you have only one part, you passes the address of the single variable, width, which contains the width of the rectangle you stored in textRect. This is in client coordinates because the device context uses MM_TEXT by default.

Finally, you set the initial text in the status bar with a call to the SetText() member of CStatusBarCtrl. The first argument is the written text string, the second is the index position of the part which contains the text string, and the third argument specifies the appearance of the part on the screen. The third argument can be any of the following:

| Style Code | Appearance |
|---|---|
| 0 | The text has a border that appears recessed into the status bar. |
| SBT_NOBORDERS | The text is drawn without borders. |
| SBT_OWNERDRAW | The text is drawn by the parent window. |
| SBT_POPOUT | The text has a border that appears to stand out from the status bar. |

In your code, you specify the text with a border so that it appears recessed into the status bar. You could try the other options to see how they look.

# Updating the Status Bar

If you build and run the code now, the status bars appears, but they show only a scale factor of 1, no matter what scale factor is actually being used — not very useful. What you need to do is to add code somewhere that changes the text each time a different scale is chosen. This means modifying the OnViewScale() handler in CSketcherView to change the status bar for the frame. Only four additional lines of code are required:

```
void CSketcherView::OnViewScale()
{
    CScaleDialog aDlg;                    // Create a dialog object
    aDlg.m_Scale = m_Scale;               // Pass the view scale to the dialog
    if(aDlg.DoModal() == IDOK)
    {
        m_Scale = aDlg.m_Scale;           // Get the new scale

        // Get the frame window for this view
        CChildFrame* viewFrame = static_cast<CChildFrame*>(GetParentFrame());

        // Build the message string
```