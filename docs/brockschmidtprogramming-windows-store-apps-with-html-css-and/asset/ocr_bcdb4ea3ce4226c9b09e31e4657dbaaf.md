![](bbox=[0.13, 0.08, 0.35, 0.26])

Another example of a header flyout menu can be found in the Adaptive layout with CSS sample we saw in Chapter 8, "Layout and Views." It's implemented the same way we see above, with the added detail that it actually changes the page contents in response to a selection.

# Context Menus

Besides the flyout menu that we've seen so far, there are also context menus as described in Guidelines and checklist for context menus. These are specifically used for commands that are directly relevant to a selection of some kind, like clipboard commands for text, and are invoked with a right mouse click on that selection, a tap-and-hold gesture, or the context menu key on the keyboard. Text and hyperlink controls already provide such menus by default. Context menus are also good for providing commands on objects that cannot be selected (like parts of an instant messaging conversation), because app bar commands can't be contextually sensitive to such items. They're also recommended for actions that cannot be accomplished with a direct interaction of some kind. However, don't use them on page backgrounds—that's what the app bar is for because the app bar will automatically appear with a right-click gesture.

**Hint** If you process the right mouse button click event for an element, be aware that the default behavior to show the app/nav bar will be suppressed over that element. Therefore, use the right-click event judiciously, because users will become accustomed to right-clicking around the app to bring up the app/nav bar. Note also that you can programmatically invoke the app bar yourself using its `show` method.

The Context menu sample gives us some context here—I know, it's a bad pun! In all cases, you need only listen to the HTML contextmenu event on the appropriate element; you don't need to worry about mouse, touch, and keyboard separately. Scenario 1 of the sample, for instance, has a nonselectable attachment element on which it listens for the event (html/scenario1.html):

```
document.getElementById("attachment").addEventListener("contextmenu",
attachmentHandler, false);
```

In the event handler, you then create a Windows.UI.Popups.PopupMenu object (which comes from WinRT, not WinJS!), populate it with Windows.UI.Popups.UICommand objects (that contain an item label and click handler) or UICommandSeparator objects, and then call the menu's showAsync method (js/scenario1.js):

```
function attachmentHandler(e) {
var menu = new Windows.UI.Popups.PopupMenu();
menu.commands.append(new Windows.UI.Popups.UICommand("Open with", onOpenWith()));
menu.commands.append(new Windows.UI.Popups.UICommand("Save attachment",
```