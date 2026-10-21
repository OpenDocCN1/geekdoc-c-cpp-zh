
## Figure 16-3

![](img/2359b0c604600c58fba3539c738a356e_862_0.png)

Figure 16-3 shows the grid that you can use to position controls. If the grid is not displayed, you can select the appropriate Toolbar button to display it; the Toolbar button toggles the grid on and off. Alternatively, you can display rules along the side and top of the dialog that you can use to create guide lines as shown in Figure 16-4.

## Figure 16-4

![](img/2359b0c604600c58fba3539c738a356e_862_1.png)

You create a horizontal guide by clicking the appropriate rule. You can position a guide line by dragging the arrow for it along the rule and then using one or more guides when positioning a control.

The dialog has six radio buttons that provide the pen width options. These are enclosed within a group box with the caption Pen Widths. The group box serves to enclose the radio buttons and make them operate as a group, where only one member of the group can be checked at any given time. Each radio button has an appropriate label to identify the pen width that is set when selected. There are also the default OK and Cancel buttons that close the dialog. Each of the controls in the dialog has its own set of properties that you can access and modify in the same way as for the dialog box itself.

The next step is to add the group box. As I said, the group box serves to associate the radio buttons in a group from an operational standpoint, and to provide a caption and a boundary for the group of buttons. Where you need more than one set of radio buttons, a means of grouping them is essential if they are to work properly. You can select the button corresponding to the group box from the common controls palette by clicking it; then click the approximate position in the dialog box where you want the center of the group box. This places a group box of default size on to the dialog. You can then drag the borders of the group box to enlarge it to accommodate the six radio buttons that you add. To set the caption for the group box, type the caption you want (in this, case type Pen Widths).

The last step is to add the radio buttons. Select the radio button control by clicking it and then clicking on the position in the dialog where you want to position a radio button within the group box. Do the same for all six radio buttons. For each button you can select it by clicking it; then type in the caption to change it. You can also drag the border of the button to set its size, if necessary. To display the properties window for a control, select it by clicking it; then select Properties from the pop-up. You can change the ID for each radio button in the properties window for the control to correspond better with its purpose: IDC_PENWIDTH0 for the 1 pixel pen width, IDC_PENWIDTH1 for the 0.01 inch width pen, IDC_PENWIDTH2 for the 0.02 inch pen, and so on.

You can position individual controls by dragging them around with the mouse. You can also select a group of controls by selecting successive controls with the Shift key pressed, or by dragging the cursor with the left button pressed to create a rectangle enclosing them. To align a group of controls, select the appropriate button from the Dialog Editor toolbar shown in Figure 16-5.

![](img/2359b0c604600c58fba3539c738a356e_863_0.png)

Figure 16-5

The toolbar is shown in its undocked state — that is, dragged away from the toolbar area at the top of the window. If the toolbar is not visible, you can show it by right-clicking in the toolbar area and selecting it in the list of toolbars that is displayed. You also can align controls in the dialog by selecting from the Format menu.

## Testing the Dialog

The dialog resource is now complete. You can test it by selecting the Toolbar button that appears at the left end of the toolbar in Figure 16-5 or by pressing Ctrl+T. This displays the dialog window with the basic operations of the controls available, so you can try clicking on the radio buttons. When you have a group of radio buttons, only one can be selected. As you select one, any other that was previously selected is reset. Click either of the OK or Cancel buttons or even the Close icon in the title bar for dialog to end the test. After you have saved the dialog resource, you’re ready to add some code to support it.

## Programming for a Dialog

There are two aspects to programming for a dialog: getting it displayed, and handling the effects of its controls. Before you can display the dialog corresponding to the resource you’ve just created, you must first define a dialog class for it. The Class wizard helps with this.

## Adding a Dialog Class

Right-click the dialog box that you just created in the Resource Editor pane and then select Add Class from the pop-up tool display the Class Wizard dialog. You’ll define a new dialog class derived from the MFC class CDialog, so select that class name from the Base Class: drop-down list box. You can enter the class name as CPenDialog in the Class name: edit box. The Class Wizard dialog should look as shown in Figure 16-6.

![](img/2359b0c604600c58fba3539c738a356e_864_0.png)

Figure 16-6

Click the Finish button to create the new class.

The CDialog class is a window class (derived from the MFC class CWnd) that’s specifically for displaying and managing dialogs. The dialog resource that you have created automatically associates with an object of type CPenDialog because the IDD class member is initialized with the ID of the dialog resource:

```
class CPenDialog : public CDialog
{
    DECLARE_DYNAMIC(CPenDialog)

public:
    CPenDialog(CWnd* pParent = NULL);   // standard constructor
    virtual ~CPenDialog();

    // Dialog Data
    enum { IDD = IDD_PENWIDTH_DLG };
protected:
    virtual void DoDataExchange(CDataExchange* pDX);   // DDX/DDV support

    DECLARE_MESSAGE_MAP()
};
```

## Chapter 16

The highlighted statement defines IDD as a symbolic name for the dialog ID in the enumeration. Incidentally, using an enumeration is the only way you can get an initialized data member into a class definition. If you try putting an initial value for any regular data member declaration, it won’t compile. You will get an error message about illegal use of pure syntax. It works here because an enum defines a symbolic name for a value of type int. Unfortunately, you can only define values of type int in this way. It’s not strictly necessary here because the initialization for IDD could be done in the constructor, but this is how Class wizard chooses to do it. This technique is more commonly used to define a symbol for the dimension of an array (a member of a class), in which case using an enumeration is your only option.

Having your own dialog class derived from CDialog means that you get all the functionality that that class provides. You can also customize the dialog class by adding data members and functions to suit your particular needs. You’ll often want to handle messages from controls within the dialog class, although you can also choose to handle them in a view or a document class if this is more convenient.

## Modal and Modeless Dialogs

There two different types of dialog, termed modal and modeless dialogs, and they work in completely different ways. Although a modal dialog remains in effect, all operations in the other windows in the application are suspended until the dialog box is closed, usually by clicking an OK or Cancel button. With a modeless dialog, you can move the focus back and forth between the dialog box and other windows in your application just by clicking them, and you can continue to use the dialog box at any time until you close it. Class wizard is an example of a modal dialog; the Properties window is modeless.

A modeless dialog box is created by calling the Create() function defined in the CDialog class, but because you’ll only be using modal dialogs in the Sketcher example, you’ll call the DoModal() function for the dialog object, as you’ll see shortly.

## Displaying a Dialog

Where you put the code to display a dialog in your program depends on the application. In the Sketcher program, it is convenient to add a menu item that, when selected, results in the pen width dialog being displayed. You’ll put this in the IDR_SketcherTYPE menu bar. As both the width and the color are associated with a pen, you can rename the Color menu as Pen. You do this just by double-clicking the Color menu item in the Resource Editor pane to open its Properties window and changing the value of the Caption property to &Pen. Closing the window puts the change into effect.

When you add the Width menu item to the Pen menu, you should separate it from the colors in the menu. You can add a separator after the last color menu item by right-clicking the empty menu item and selecting the Insert Separator menu item from the pop-up. You can then enter the new Width item as the next menu item after the separator. The menu item ends with an ellipsis (three periods) to indicate that it displays a dialog; this is a standard Windows convention. Double-click the menu to display the menu properties for modification, as shown in Figure 16-7.

Enter ID_PENWIDTH as the ID for the menu item as shown in Figure 16-7. You can also add a status bar prompt for it and because you’ll also add a toolbar button, you can include text for the tool tip as well. Remember, you just put the tooltip text following the status bar prompt text, separated from it by "\n". Here the value for the Prompt property is "Change pen width\nShow pen width options". The menu will look as shown in Figure 16-8.
