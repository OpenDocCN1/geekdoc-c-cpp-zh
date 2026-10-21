# # Working with Menus and Toolbars

# ## Adding Message Handlers to Update the User Interface

To set the check mark correctly for the new menus, you need to add the second kind of message handler, UPDATE_COMMAND_UI (signifying update command user interface), for each of the new menu items. This sort of message handler is specifically aimed at updating the menu item properties before the item is displayed.

Go back to viewing the Sketcher.rc file in the Editor window. Right-click the Black item in the Color menu and select Add Event Handler from the pop-up menu. You can then select UPDATE_COMMAND_UI as the message type and CSketcherDoc as the class as shown in Figure 13-10.

![](bbox=[0.15, 0.5, 0.85, 0.75])

The name for an update function has been generated OnUpdateColorBlack(). Because this seems a reasonable name for the function you want, click the Add and Edit button and have the Event Handler wizard generate it. As well as generating the skeleton function definition in SketcherDoc.cpp, its declaration is added to the class definition. An entry for it is also made in the message map that looks like this:

```
ON_UPDATE_COMMAND_UI (ID_COLOR_BLACK, OnUpdateColorBlack)
```

This uses the ON_UPDATE_COMMAND_UI () macro that identifies the function you have just generated as the handler to deal with update messages corresponding to the ID shown. You could now enter the code for the new handler but I'll let you add command update handlers for each of the menu items for both the Color and Element menus first.

# ## Coding a Command Update Handler

You can access the code for the OnUpdateColorBlack() handler in the CSketcherDoc class by selecting the function in Class View. This is the skeleton code for the function: