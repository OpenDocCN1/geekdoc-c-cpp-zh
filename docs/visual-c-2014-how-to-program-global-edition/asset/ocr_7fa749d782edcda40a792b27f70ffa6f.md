# Chapter 14 Graphical User Interfaces with Windows Forms: Part I

# Look-and-Feel Observation 14.3

You can organize a GUI by anchoring and docking controls inside a GroupBox or Panel. The GroupBox or Panel can be anchored or docked inside a Form. This divides controls into 'groups' that can be arranged easily.

To create a GroupBox, drag it from the Toolbox onto a Form. Then, drag new controls from the Toolbox into the GroupBox. These controls are added to the GroupBox's Controls property and become part of the GroupBox. The GroupBox's Text property identifies the caption to that of the GroupBox.

To create a Panel, drag it from the Toolbox onto Form. You can add controls directly to the Panel by dragging them from the Toolbox onto the Panel. To enable scrollbars, set the Panel's AutoScroll property to true. If the Panel is resized and cannot display all of its controls, scrollbars appear (Fig. 14.23). The scrollbars are used to view all the controls in the Panel—at design time and at execution time. In Fig. 14.23, we set the Panel's BorderStyle property to FixedSingle so that you can see the Panel in the Form.

![](bbox=[0.147, 0.426, 0.851, 0.646])

Fig. 14.23 | Creating a Panel with scrollbars.

The program in 14.24 uses a GroupBox and a Panel to arrange buttons. When these buttons are clicked, their event handlers change the text on a Label.

```
// Fig. 14.24: GroupBoxPanelExampleForm.cs
// Using GroupBoxes and Panels to arrange buttons.
using System;
using System.Windows.Forms;

namespace GroupBoxPanelExample
{
    // Form that displays a GroupBox and a Panel
    public partial class GroupBoxPanelExampleForm : Form
    {
```

Fig. 14.24 | Using GroupBoxes and Panels to arrange Buttons. (Part I of 2.)