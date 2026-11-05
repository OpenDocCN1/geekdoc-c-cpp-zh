![](bbox=[0.213, 0.12, 0.911, 0.432])

**FIGURE 10-12** Setting the ToolTip property

When you create the menu structure using the MenuStrip control, separate ToolStripMenuItem objects are created for each of the selectable menu options that you type. After you finish laying out the structure, the **Name** property for these ToolStripMenuItem objects can be set by selecting the individual menu option prior to selecting the **Name** property in the **Properties** window. This is especially important if the menu item will be wired to an event, because the name of the control becomes part of the name of the event-handler method.

> > **NOTE**
> >
> > To wire a method to an event such as a menu option means you are associating the event to a specific method. After the method is wired to the menu option, the method is executed automatically when the menu option is clicked. When the menu option is clicked, it can be said that the event triggers, happens, or is fired. This is one of the underlying concepts behind event-driven applications.

Property names such as menuExit, menuFont, menuColor, and menuHelp were set in the **Properties** window after selecting each individual ToolStripMenuItem in the **Form Designer**. Click events are registered by double-clicking on the option. Form **Designer** generates individual click event-handler methods. The click event method name for the menuExit option is menuExit_Click( ); the event handler for the menuFont option is menuFont_Click( ).