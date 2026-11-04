arrow on the right, and select the ContextMenuStrip. The rest is automatic. When the user right-clicks the control, it automatically displays the ContextMenuStrip.

# WPF MENUS

To create a menu in a WPF application, add a Menu control to the window and use your preferred method to make it attach itself to the top. For example, if the window contains a Grid, you can make the Menu fill the Grid's top row. Alternatively, if the window contains a DockPanel, you can dock the Menu to the top.

After you create the Menu, you can add items to it in two ways. First, you can use the Properties window's menu editor. Select the Menu, find the Menu's Items property in the Properties window, and click the ellipsis to the right to open the editor shown in Figure 5-7.

![](bbox=[0.1, 0.46, 0.65, 0.62])

FIGURE 5-7

Use the editor to add and modify the items in the menu. Set a menu item's Header property to the text that you want it to display. Place an underscore in front of the character that you want the item to use as an accelerator key. For example, the menu item in Figure 5-5 has Header set to _Edit so when you press Alt at run time, it will appear as Edit.

To make a submenu, click the ellipsis to the right of the Items property in the menu item editor (in the bottom right in Figure 5-5).

> > NOTE You can put practically anything inside a WPF menu. A menu could hold CheckBoxes, RadioButtons, ComboBoxes, Sliders, even a Grid containing a whole slew of other controls.
> >
> > However, that's not what users expect to see in a menu, so adding too many unusual items can make a menu confusing. Normally menus should contain only MenuItems and Separators.

The second way you can create a menu hierarchy is to edit the XAML code manually. That may seem intimidating, but it's actually not too hard, particularly if you make a few menu items and then copy and paste their code.