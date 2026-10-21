# Exercising the Toolbar Buttons

Build the application once again and execute it. You should see the application window shown in Figure 13-15.

![](bbox=[0.315, 0.172, 0.797, 0.443])

Figure 13-15

There are some amazing things happening here. The toolbar buttons that you added already reflect the default settings that you defined for the new menu items. If you let the cursor linger over one of the new buttons, the prompt for the button appears in the status bar. The new buttons work as a complete substitute for the menu items and any new selection made, using either the menu or the toolbar, is reflected by showing the toolbar button depressed, as well as the check against the menu item.

If you close the document view window, Sketcher1, you’ll see that our toolbar buttons are automatically grayed and disabled. If you open a new document window, they are automatically enabled once again. You can also try dragging the toolbar with the cursor. You can move it to either side of the application window, or have it free-floating. You can also enable or disable it through the View > Toolbar menu option. You got all this without writing a single additional line of code!

# Adding Tooltips

There’s one further tweak that you can add to your toolbar buttons that is remarkably easy: adding tooltips. A tooltip is a small box that appears adjacent to the toolbar button when you let the cursor linger on the button. The tooltip contains a text string that is an additional clue as to the purpose of the toolbar button.

To add tooltips, select the Resource View tab and, after expanding the resource list, click the String Table folder and double-click the resource. This contains the IDs and prompt strings associated with menu items and toolbar buttons. You should see the IDs for the menus that you added earlier together with the prompt text for each under the caption heading. To add a tooltip, you just need to add \n (the newline character), followed by the tooltip text to the end of the caption text. For the prompt text you have already entered you can double-click text to enable editing of it and then add \n to the end of the prompt text in the caption