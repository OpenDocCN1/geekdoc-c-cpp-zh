| LinkLabel properties and an event | Description |
|---|---|
| LinkBehavior | Specifies the link's behavior, such as how the link appears when the mouse is placed over it. |
| LinkColor | Specifies the original color of the link before it's been visited. The default color (typically blue) is set by the system. |
| LinkVisited | If true, the link appears as though it has been visited (its color is changed to that specified by property VisitedLinkColor). The default value is false. |
| Text | Specifies the control's text. |
| UseMnemonic | If true, the & character in the Text property acts as a shortcut (similar to the Alt shortcut in menus). |
| VisitedLinkColor | Specifies the color of a visited link. The default color (typically purple) is set by the system. |
| Common Event (Event arguments LinkLabelLinkClickedEventArgs) | |
| LinkClicked | Generated when the link is clicked. This is the default event when the control is double clicked in Design mode. |

Fig. 15.13 | LinkLabel properties and an event. (Part 2 of 2.)

Class LinkLabelTestForm (Fig. 15.14) uses three LinkLabels to link to the C: drive, the Deitel website (www.deitel.com) and the Notepad app, respectively. The Text properties of the LinkLabels cDriveLinkLabel1, deitelLinkLabel1 and notepadLinkLabel1 describe each link's purpose.

```
```csharp
// Fig. 15.14: LinkLabelTestForm.cs
// Using LinkLabels to create hyperlinks.
using System;
using System.Windows.Forms;

namespace LinkLabelTest
{
    // Form using LinkLabels to browse the C:\ drive,
    // load a web page and run Notepad
    public partial class LinkLabelTestForm : Form
    {
        // constructor
        public LinkLabelTestForm()
        {
            InitializeComponent();
        }

        // browse C:\ drive
        private void cDriveLinkLabel_LinkClicked(object sender,
            LinkLabelLinkClickedEventArgs e)
        {
```
```

Fig. 15.14 | Using LinkLabels to create hyperlinks. (Part 1 of 3.)