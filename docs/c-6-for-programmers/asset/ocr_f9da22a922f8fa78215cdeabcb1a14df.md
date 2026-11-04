+   2. Click the Form in the designer, then use the Properties window to set the Form's Text property to "Simple Event Example".
+   3. Set the Form's Font property to Segoe UI, 9pt. To do so, select the Font property in the Properties window, then click the ellipsis (...) button in the property's value field to display a font dialog.

# Adding a Button to the Form

Drag a Button from the Toolbox onto the Form. In the Properties window, set the (Name) property (which specifies the Button's variable name) to clickButton and the Text property to Click Me. By convention, a control's variable name ends with the control's type. For example, in the variable name clickButton, "Button" is the control's type.

# Adding an Event Handler for the Button's Click Event

When the user clicks the Button in this example, we want the app to respond by displaying a MessageBox. To do this, you must create an event handler for the Button's Click event, which you can do by double clicking the Button on the Form. This opens the file containing the following empty event handler in the program code:

```
private void clickButton_Click(object sender, EventArgs e)
{
}
```

By convention, the IDE names the event-handler method as objectName_eventName (e.g., clickButton_Click). The clickButton_Click event handler executes when the user clicks the clickButton control.

# Event Handler Parameters

Each event handler receives two parameters when it's called. The first—an object reference named sender by default—is a reference to the object that the user interacted with to generate the event. The second is a reference to an EventArgs object (or an object of an EventArgs derived class), which is typically named e. This object contains additional information about the event that occurred. EventArgs is the base class of all classes that represent event information.

# Displaying a MessageBox

To display a MessageBox in response to the event, insert the statement

```
MessageBox.Show("Button was clicked.");
```

in the event handler's body. The resulting event handler appears in lines 18–21 of Fig. 14.5. When you execute the app and click the Button, a MessageBox appears displaying the text "Button was clicked."

# 14.3.2 Auto-Generated GUI Code

Visual Studio places the auto-generated GUI code in the Form class's Designer.cs file—in this example, the file SimpleEventExampleForm.Designer.cs. You can open this file by expanding the Form class's node in the Solution Explorer window and double clicking the file name that ends with Designer.cs. Figs. 14.6 and 14.7 show this file's contents. The IDE collapses the code in lines 23–57 of Fig. 14.7 by default—you can click the