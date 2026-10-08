# Auto-Generated Code Stored in Separate File

A Form is a container for controls and components. When you drag an item from the Toolbox, Visual Studio generates code that creates the object and sets its basic properties. This code is updated when the control or component's properties are modified in the IDE. Removing a control or component from the Form deletes the corresponding generated code. The IDE maintains the generated code in a separate file using partial classes—classes that are split among multiple files and assembled into a single class by the compiler. You could write this yourself, but it is much easier to use Visual Studio to handle the details. We introduced visual programming concepts in Section 2.6. In this chapter and the next, we will use visual programming to build more substantial GUIs.

# Common Form Properties, Methods, and an Event

Each control or component presented in this chapter is located in namespace System.Forms. To create a Windows Forms app, you generate a Windows Form, set its properties and implement event handlers (methods) that respond to events generated when a user interacts with the controls. Figure 14.4 lists common properties, common methods, and a common event.

| Form methods and an event | Description |
| --- | --- |
| **Common Properties** | |
| AcceptButton | Default Button that is clicked when you press Enter.
| AutoScroll | bool value (false by default) that allows scrollbars when needed.
| CancelButton | Button that is clicked when the Escape key is pressed.
| FormBorderStyle | Border style for the Form (Sizable by default).
| Font | Font of text displayed on the Form, and the default font for controls to the Form.
| Text | Text in the Form's title bar |
| **Common Methods** | |
| Close | Closes a Form and releases all resources, as the memory used for the Form's contents. A closed Form cannot be reopened.
| Hide | Hides a Form, but does not destroy the Form or release its resources.
| Show | Displays a hidden Form.
| **Common Event** | |
| Load | Occurs before a Form is displayed to the user. You'll learn about events and event-handling in the next section |

**Fig. 14.4** | Common Form properties, methods and an event.

# 14.3 Event Handling

Normally, a user interacts with an app's GUI to indicate the tasks that the app should perform. For example, when you write an e-mail in an e-mail app, clicking the Send button