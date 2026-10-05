# How to set the properties that work with menu items

Each menu item you create is a separate object that has its own properties. When you use the techniques described in the last figure to create a menu or menu item, you use the Menu Designer and its shortcut menus to set the properties for each menu item. Typically, that's the easiest way to set properties for menu items. However, you can also use the Properties window to change the properties for the selected menu item.

Figure 24-5 summarizes some of the properties for menu items that you're most likely to use. To start, you can use the Form Designer to set these properties at design-time. For example, you can use the ShortcutKeys and ShowShortcutKeys to define and display a shortcut key (such as Ctrl+C) for a menu item. Then, if necessary, you can use code to change these properties at runtime. For example, you can use the Checked property to display or hide a check mark next to a menu item. Or, you can use the Enabled and Visible properties to disable or hide a menu item.

# How to write code that works with menu items

The first example in figure 24-5 shows the event handler for the Clear item of the Action menu. Since the Click event is the default event for a menu item, you can generate the declaration for the event handler by double-clicking the menu item in the Menu Designer. Then, you can use the Code Editor to enter the code that's executed by the event handler.

The second example shows the handler for the Click event of the Action menu. Since this menu item provides the same functionality as the Calculate button, the lone statement in this event handler calls the event handler for the Click event of the Calculate button. To get this to work correctly, both of the parameters for the mnuCalculate_Click method are supplied as arguments for the binCalculate_Click method.

The third example shows another way to handle the Click event for the Calculate item of the Action menu. Here, this event handler calls the PerformClick method of the Calculate button. This causes the event handler for the Click event of the Calculate button to be executed.

Of course, you can handle this situation more elegantly by wiring both events to the same event handler. For example, you can wire the Click event for the Calculate menu item and the Calculate button to an event handler named Calculate_Click. For a refresher course on wiring event handlers, see chapter 6.