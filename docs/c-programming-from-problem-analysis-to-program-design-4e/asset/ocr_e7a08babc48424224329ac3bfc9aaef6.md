> **NOTE**
> 
> The illustration shown in Figure 9-10 show controls available in Visual Studio. You might see a slightly different listing if you are using a different version or if the **Toolbox** has been previously customized.

If your **Toolbox** window is not visible, one way to activate it is to select **Toolbox** from the **VIEW** menu. The **All Windows Forms Controls** in the **Toolbox** are only visible when you are using the Designer. If the **Code Editor** window is active, you must select the Designer tab to gain access to the **All Windows Forms** controls.

# Placing, Moving, Resizing, and Deleting Control Objects

Two procedures are used to place a control on your form. After the control is selected, you can either double-click the control or drag and drop the control to the correct location. If you use the double-click approach, the control is always placed in the upper-left corner of the form—even if it overlaps other controls. To move the control, position the mouse pointer over the control until you see the standard Windows crossbars. With the left mouse button pressed, you can drag the control to its new location.

In Design view, you can resize controls using the standard Windows conventions of positioning the mouse pointer over the resizing handles. When you get the double-sided arrow, hold down the left mouse button and drag the border to the desired size. Another option available to you is to use the **Properties** window and set the **Size** property.

> **NOTE**
> 
> Select multiple controls using your mouse by either drawing an outline around the controls that are to be formatted or holding down the **Ctrl** key while you click on the controls.

To delete a control, first select the control by clicking on it. The sizing handles become visible. Now pressing the Delete or Backspace key not only removes the control visually from the **Form Designer** view, but also removes all the constructor code and associated property changes relating to the selected object.

> **NOTE**
> 
> Just as you spent time designing a prototype for a console-based application, you should design a prototype for your Windows form. Randomly placing controls on your form leads to unorganized source code. It is probably best to place all labels, then all buttons, and so on. That way, like items are grouped together in your program listing.

When you copy and paste controls on the form, you normally must always move the object to the new position after it is pasted. Windows Forms **Designer** has a SnapLine