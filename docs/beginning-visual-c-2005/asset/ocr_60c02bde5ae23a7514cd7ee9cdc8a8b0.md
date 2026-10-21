are to work properly. You can select the button corresponding to the group box from the common controls palette by clicking it; then click the approximate position in the dialog box where you want the center of the group box. This places a group box of default size on to the dialog. You can then drag the borders of the group box to enlarge it to accommodate the six radio buttons that you add. To set the caption for the group box, type the caption you want (in this, case type Pen Widths).

The last step is to add the radio buttons. Select the radio button control by clicking it and then clicking on the position in the dialog where you want to position a radio button within the group box. Do the same for all six radio buttons. For each button you can select it by clicking it; then type in the caption to change it. You can also drag the border of the button to set its size, if necessary. To display the properties window for a control, select it by clicking it; then select Properties from the pop-up. You can change the ID for each radio button in the properties window for the control to correspond better with its purpose: IDC_PENWIDTH0 for the 1 pixel pen width, IDC_PENWIDTH1 for the 0.01 inch width pen, IDC_PENWIDTH2 for the 0.02 inch pen, and so on.

You can position individual controls by dragging them around with the mouse. You can also select a group of controls by selecting successive controls with the Shift key pressed, or by dragging the cursor with the left button pressed to create a rectangle enclosing them. To align a group of controls, select the appropriate button from the Dialog Editor toolbar shown in Figure 16-5.

![](bbox=[0.32, 0.47, 0.65, 0.5])

Figure 16-5

The toolbar is shown in its undocked state — that is, dragged away from the toolbar area at the top of the window. If the toolbar is not visible, you can show it by right-clicking in the toolbar area and selecting it in the list of toolbars that is displayed. You also can align controls in the dialog by selecting from the Format menu.

# Testing the Dialog

The dialog resource is now complete. You can test it by selecting the Toolbar button that appears at the left end of the toolbar in Figure 16-5 or by pressing Ctrl+T. This displays the dialog window with the basic operations of the controls available, so you can try clicking on the radio buttons. When you have a group of radio buttons, only one can be selected. As you select one, any other that was previously selected is reset. Click either of the OK or Cancel buttons or even the Close icon in the title bar for dialog to end the test. After you have saved the dialog resource, you’re ready to add some code to support it.

# Programming for a Dialog

There are two aspects to programming for a dialog: getting it displayed, and handling the effects of its controls. Before you can display the dialog corresponding to the resource you’ve just created, you must first define a dialog class for it. The Class wizard helps with this.