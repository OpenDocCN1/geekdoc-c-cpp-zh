# Figure 11-16: Menus on ProductsMain form

![](bbox=[0.085, 0.092, 0.393, 0.172])

![](bbox=[0.082, 0.189, 0.393, 0.302])

Step 2-12: Add the MenuStrip object from the Menus and Toolbars group on the Toolbox. You will see the object in the component tray. Change the name of the MenuStrip from menuStrip1 to MainMenu.

Step 2-13: Click on MainMenu in the component tray. The Menu Designer is displayed at the top of the form with the Type Here field, as shown in Figure 11-17.

# Figure 11-17: The Menu Designer

![](bbox=[0.082, 0.477, 0.308, 0.645])

Step 2-14: Type File in the Type Here field. This creates a new menu item of the type ToolStripMenuItem. Change the Text property to &File to make “F” the access key for this menu. That means you can press Alt+F to access this menu.

Step 2-15: Type Exit in the Type Here field in the dropdown menu below File. Because we add code to the Click event handler of this menu item, change its name to mnuExit to make it more meaningful. For the ShortCutKeys property, select Ctrl and x. That means pressing Ctrl+x will have the same effect as selecting this menu item.