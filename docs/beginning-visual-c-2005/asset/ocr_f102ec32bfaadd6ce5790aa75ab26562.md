# Creating the Document and Improving the View

Now you can add the handlers for the items in the first pop-up menu. Return to the Resource View and double-click on IDR_CURSOR_MENU. Right-click the Move menu item and then select Add Event Handler from the pop-up. You can then specify the handler in the dialog for the Event Handler wizard, as shown in Figure 15-14.

![](bbox=[0.26, 0.16, 0.85, 0.47])

Figure 15-14

It’s a COMMAND handler and is to be created in the CSketcherView class. Click the Add and Edit button to create the handler function. You can follow the same procedure to create the hander for the Delete menu item.

You don’t have to do anything for the second context menu, as you already have handlers written for them in the document class. These take care of the messages from the pop-up items automatically.

# Choosing a Context Menu

At the moment, the OnContextMenu() handler only displays the first context pop-up, no matter where the right button is clicked in the view. This isn’t really what you want it to do. The first context menu applies specifically to an element, whereas the second context menu applies in general. You want to display the first menu if there is an element under the cursor and to display the second menu if there isn’t.

You need two things to fix this up: You need a mechanism to find out which (if any) element is at the current cursor position, and you need to save the address of this element somewhere so you can use it in the OnContextMenu() handler. You can deal with saving the address of the element first because this is the easier bit.