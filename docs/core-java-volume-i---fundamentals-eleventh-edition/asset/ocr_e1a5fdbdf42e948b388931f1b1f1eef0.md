```
    public void menuSelected(MenuEvent event)
    {
        saveAction.setEnabled(!readonlyItem.isSelected());
        saveAsAction.setEnabled(!readonlyItem.isSelected());
    }
```

> > **CAUTION:** Disabling menu items just before displaying the menu is a clever idea, but it does not work for menu items that also have accelerator keys. Since the menu is never opened when the accelerator key is pressed, the action is never disabled, and is still triggered by the accelerator key.

| java.swing.JMenuItem 1.2 |
|---|
| • void setEnabled(boolean b)<br>enables or disables the menu item. |

| java.swing.event.MenuListener 1.2 |
|---|
| • void menuSelected(MenuEvent e)<br>is called when the menu has been selected, before it is opened. |
| • void menuDeselected(MenuEvent e)<br>is called when the menu has been deselected, after it has been closed. |
| • void menuCanceled(MenuEvent e)<br>is called when the menu has been canceled, for example, by a user clicking outside the menu. |

Listing 11.6 is a sample program that generates a set of menus. It shows all the features that you saw in this section: nested menus, disabled menu items, checkbox and radio button menu items, a pop-up menu, and keyboard mnemonics and accelerators.

**Listing 11.6** menu/MenuFrame.java

```
    1 package menu;
    2
    3 import java.awt.event.*;
    4 import javax.swing.*;
    5
```