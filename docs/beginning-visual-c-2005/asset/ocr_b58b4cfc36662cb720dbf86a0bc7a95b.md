Properties are simply parameters that determine how the menu item will appear and behave. Figure 13-4 displays the properties for the menu item grouped by category. If you would rather have them displayed in alphabetical sequence, just click the second button from the left. Note that the Popup property is set as True by default; this is because the new menu item is at the top level on the menu bar so it would normally present a pop-up menu when it is selected. Clicking any property in the left column enables you to modify it in the right column. In this case you want to leave everything as it is so you can just close the Properties window. No ID is necessary for a pop-up menu item because selecting it just displays the menu beneath and there’s no event for your code to handle. Note that you get a new blank menu box for the first item in the pop-up menu as well as one on the main menu bar.

It would be better if the Element menu appeared between the View and Window menus, so place the cursor on the Element menu item and keeping the left mouse button pressed, drag it to a position between the View and Window menu items, and release the left mouse button. After positioning the new Element menu item, the next step is to add items on the pop-up menu that corresponds to it.

# Adding Items to the Element Menu

Select the first item (currently labeled “Type Here”) in the Element pop-up menu by clicking it; then type &Line as the caption and press the Enter key. You can see the properties for this menu item by double-clicking it; the properties for this first item in the pop-up menu are shown in Figure 13-5.

![](bbox=[0.338, 0.431, 0.604, 0.889])

Figure 13-5