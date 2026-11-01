You can configure the Library to display its views in different modes (see also Figure C-11):

+   - Icons
+   - Icons and Labels (which is the mode shown in Figure C-10)
+   - Icons and Descriptions

Figure C-12 shows the Library displayed in the Icons and Descriptions mode.

![](bbox=[0.15, 0.38, 0.45, 0.73])

![](bbox=[0.48, 0.35, 0.75, 0.73])

FIGURE C-11

FIGURE C-12

# OUTLETS AND ACTIONS

Outlets and actions are fundamental mechanisms in iPhone programming through which your code can connect to the views in your user interface (UI). When you use outlets, your code can programmatically reference the views on your UI, with actions serving as event handlers that handle the various events fired by the various views.

Although you can write code to connect actions and outlets, Interface Builder simplifies the process by allowing you to connect outlets and actions using the drag-and-drop technique.

# Creating Outlets and Actions

To create an action, you can click the plus sign (+) button that appears in the Class Actions section of the Identity Inspector window (see left side of Figure C-13). Remember to include the colon (:) character at the end of the action name. This character allows the action to have an input parameter of type id, like this:

```
- (IBAction) myAction:(id) sender;
```