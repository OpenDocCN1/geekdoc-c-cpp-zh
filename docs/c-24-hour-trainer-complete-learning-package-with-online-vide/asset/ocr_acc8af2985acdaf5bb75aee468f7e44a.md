# CREATING CONTEXT MENUS

A context menu appears when you right-click a particular control. In a Windows Forms application, using a context menu is almost as easy as using a main menu. Figure 5-5 shows an application displaying a context menu.

Start by dropping a ContextMenuStrip on the form. Like a MenuStrip, a ContextMenuStrip appears below the form in the Component Tray so you can just double-click the Toolbox's ContextMenuStrip tool and not worry about positioning it.

![](bbox=[0.52, 0.19, 0.82, 0.42])

FIGURE 5-5

Unlike a MenuStrip, a ContextMenuStrip does not appear at the top of the form. In the Form Designer, you can click a MenuStrip either on the form or in the Component Tray to select it. To select a ContextMenuStrip, you must click it in the Component Tray.

After you select the ContextMenuStrip, you can edit it much as you can a MenuStrip. The big difference is that a ContextMenuStrip does not have top-level menus, just submenu items.

Figure 5-6 shows the Form Designer with a ContextMenuStrip selected. By now the menu editor should look familiar.

![](bbox=[0.13, 0.6, 0.45, 0.83])

FIGURE 5-6

After you create a ContextMenuStrip, you need to associate it with the control that should display it. To do that, simply set the control's ContextMenuStrip property to the ContextMenuStrip. To do that, select the control's ContextMenuStrip property in the Properties window, click the dropdown