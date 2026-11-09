+   6. Click the OK button to close the **New Project** dialog box. The **MyStatusStrip** application is created (Fig.VB-4.22).

+   7. *Drag and drop* a **Label** control and a **TextBox** control on the form from the **Toolbox**.

+   8. *Select* the **Label** control in the form and *set* its **Text** property to **Enter text:** in the **Properties** window.

+   9. *Select* the **TextBox** control in the form, then set its **Multiline** property to **True** in the **Properties** window, and then *resize* it to accommodate multiple lines of text.

+   10. *Drag and drop* a **StatusStrip** control on the form from the **Menus & Toolbars** tab of the **Toolbox**. The **StatusStrip** control is added to both the bottom of the form and the component tray (Fig.VB-4.22).

You can notice in Fig.VB-4.22 that by default, the **StatusStrip** control does not have any items. In the subsequent steps, we add items to the **StatusStrip** control.

+   11. *Select* the **StatusStrip** control in the form, *select* the **Items** property of the **StatusStrip** control in the **Properties** window, and *click* the ellipsis button (...) in front of this property, as shown in Fig.VB-4.22.

![](bbox=[0.342, 0.335, 0.681, 0.537])

Fig.VB-4.22

The **Items Collection Editor** dialog box opens (Fig.VB-4.23).

+   12. *Select* the **StatusLabel** option from the **Select item and add to list below:** drop-down list, (Fig.VB-4.23).

+   13. *Click* the **Add** button (Fig.VB-4.23). A control corresponding to the **StatusLabel** option, **ToolStripStatusLabel1**, is added under the **StatusStrip** control, **StatusStrip1**, in the **Members** list box (Fig.VB-4.24).

+   14. *Select* the **DropDownButton** option from the **Select item and add to list below:** drop-down list (Fig.VB-4.24).

+   15. *Click* the **Add** button to add the selected option, (Fig.VB-4.24).

![](bbox=[0.241, 0.684, 0.499, 0.815])

![](bbox=[0.525, 0.684, 0.781, 0.815])

Fig.VB-4.23　　　　　　　　　　　　　　Fig.VB-4.24

A control corresponding to the **DropDownButton** option, **ToolStripDropDownButton1**, is added under the **StatusStrip1** node in the **Members** list box (Fig.VB-4.25).