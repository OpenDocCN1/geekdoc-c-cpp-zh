
# 590 Chapter 14 Graphical User Interfaces with Windows Forms: Part I

```csharp
20 MessageBox.Show("Button was clicked.");
21 {
22 }
23 }
```

![](img/57baed2319be0bb1b5f98674846f2711_590_0.png)

**Fig. 14.5** | Simple event-handling example. (Part 2 of 2.)

## Renaming the Form1.cs File
Using the techniques in Section 2.6, create a Form containing a Button. First, create a new Windows Forms app SimpleEventExample. Then:

- 1. Rename the Form1.cs file to SimpleEventExampleForm.cs in the Solution Explorer.
- 2. Click the Form in the designer, use the Properties window to set the Form's Text property to "Simple Event Example".
- 3. Set the Form's property to Segoe UI, 9pt. To do so, select the font property in the Properties window, then the ellipsis (...) button in the property's value field to display a font dialog.

### Adding a Button to the Form
Drag Button from the Toolbox onto the Form. In the Properties window, set the (Name) property (which specifies the Button's variable name) to clickButton and the Text property to Click. By convention, a control's variable name ends with the control's type. For example, in the variable name clickButton, "Button" is the control's type.

### Adding an Event Handler for the Button's Click Event
When the user clicks the Button, we want the app to respond by displaying a MessageBox. To do this, you must create an event handler for the Button's Click event, which you can do by double clicking the Button on the Form. This opens the file containing following empty void handler in the program code:

```csharp
private void clickButton_Click(object sender, EventArgs e)
{
}
```

By convention, the IDE names the event-handler method as objectName_Event (e.g., clickButton_Click). The clickButton_Click event handler executes when the user clicks the clickButton control.

### Event Handler Parameters
Each handler receives two parameters when it's called. The first—an object reference sender by default—is a reference to the object that the user interacted with to generate the event. The second is a reference to an EventArgs object (or an object of EventArgs derived class), which is typically named e. This object contains additional information about the event that occurred. EventArgs is the base class of all classes that represent event information.

#### Displaying a MessageBox
To display a MessageBox in response to the event, insert the statement

```csharp
MessageBox.Show("Button was clicked.");
```

in the event handler's body. The resulting event handler appears in lines 18–21 of Fig. 14.5. When you execute the app and click the Button, a MessageBox appears the text "Button was clicked.".

## 14.3.2 Auto-Generated GUI Code
Visual Studio places the auto-generated GUI code in the class's Designer.cs file—in this example, the file SimpleEventExample.Designer.cs. You can open this file by expanding the Form class in the Solution Explorer and double clicking the file name that ends with Designer.cs. Figs. 14.6 and 14.7 show this file's contents. The IDE collapses the code in lines 23–57 of Fig. 14.4 by default—you can click the next to line 23 to expand the code, then click the icon next to that line to collapse it.

![](img/57baed2319be0bb1b5f98674846f2711_591_0.png)

Fig. 14.6 First half of the Visual Studio generated code file.

Fig. 14.7 Second half of the Visual Studio generated code file.

Now that you have studied classes and objects in detail, this code will be easier to understand. Since this code is created and maintained by Visual Studio, you generally do not need to look at it. In fact, you do not need to understand most of the code here to build GUI apps. However now we take a closer look to help you understand how GUI works.

The auto-generated code that defines the GUI is actually part of the form’s class—in the partial SimpleEventExampleForm. Line 3 of 14.6 (and line 9 of 14.5) uses the partial member, which allows this code to be split among multiple files, including the files that contain auto-generated code and those where you write your own code. Line 59 of 14.7 declares the clickButton that we created in Design mode. It is declared as an instance variable of class SimpleEventForm. By default, all declarations for controls created through C#'s design window have a private access modifier. The code also includes the Dispose method for releasing resources (Fig. 14.6, lines 14–21) and method InitializeComponent (Fig. 14.7, lines 29–55), which contains the code that creates the Button, sets some of the Button's and the Form's properties. The property values correspond to the Properties window for each control. Visual Studio adds comments to the code it generates, as in lines 33–35. Line 42 was generated when we created the event handler for the Button's Click event.

Method InitializeComponent is called when the Form is created, and establishes properties such as the Form title, the Form size, controls and text. Visual Studio also uses this code in method to create the GUI you see in design view. Changing the code in InitializeComponent may prevent Visual Studio from displaying the GUI.

#### Error-Prevention Tip 14.1
Code in the Designer.cs file that is generated by building a GUI in Design mode is not meant to be modified directly, which is why this code is placed in a separate file. Modifying this code can prevent the GUI from being displayed correctly in Design mode and might cause an app to function incorrectly. In Design mode, it's recommended that you modify properties only in the Properties window, not in the Designer.cs file.

## 14.3 Delegates and the Event-Handling Mechanism
The control that generates an event is known as the event sender. An event-handling method—known as the event handler—responds to a particular event that controls. When the event occurs, the event sender calls its handler to perform a task (i.e., to “handle the event").

The .NET event-handling mechanism allows you to choose your own names for event-handling methods. However, each event-handling method must declare the parameters to receive the event that it handles. Since you can choose your own method names, an event sender such as a Button cannot know in advance which method will respond to its events. So, we need a mechanism to identify which method is the event handler for an event.

### Delegates
Event handlers are connected to a control's events via special objects called delegates. A delegate type specifies the return type and signature of a method—in event handling, the delegate specifies the return type and arguments for an event handler. UI controls have predefined delegates that correspond to every event they can generate. For example, the delegate for a Button's Click event is EventHandler (namespace System). The only help documentation declares this type as follows:

```csharp
public delegate void EventHandler(object sender, EventArgs args);
```

This uses the delegate keyword to declare a type EventHandler, which can hold references to methods that return void and receive two parameters—one of object (the sender) and one of EventArgs. If you compare the delegate declaration with ClickButton's first line (Fig. 14.5), the resulting event handler appears in lines 18–21 of Fig. 14.5. When you execute the app and click the Button, a MessageBox appears the text "Button was clicked.".

#### Indicating the Method that Delegate Would Call
Since the event occurs, the event sender calls its handler to perform a task (i.e., to “handle the event"). The .NET event-handling mechanism allows you to choose your own names for event-handling methods. However, each event-handling method must declare the parameters to receive the event that it handles. Since you can choose your own method names, an event sender such as a Button cannot know in advance which method will respond to its events. So, we need a mechanism to identify which method is the event handler for an event.

Each handler receives two parameters when it's called. The first—an object reference sender by default—is a reference to the object that the user interacted with to generate the event. The second is a reference to an EventArgs object (or an object of EventArgs derived class), which is typically named e. This object contains additional information about the event that occurred. EventArgs is the base class of all classes that represent event information.

#### (Optional) Multiple Delegates
Event handlers are connected to a control's events via special objects called delegates. A delegate type specifies the return type and signature of a method—in event handling, the delegate specifies the return type and arguments for an event handler. UI controls have predefined delegates that correspond to every event they can generate. For example, the delegate for a Button's Click event is EventHandler (namespace System). The only help documentation declares this type as follows:

```csharp
public delegate void EventHandler(object sender, EventArgs args);
```

This uses the delegate keyword to declare a type EventHandler, which can hold references to methods that return void and receive two parameters—one of object (the sender) and one of EventArgs. If you compare the delegate declaration with ClickButton's first line (Fig. 14.5), the resulting event handler appears in lines 18–21 of Fig. 14.5. When you execute the app and click the Button, a MessageBox appears the text "Button was clicked.".

![](img/57baed2319be0bb1b5f98674846f2711_593_0.png)

#### 14.3.4 Another Way to Create Event Handlers
For the GUI app in14.5, you double clicked the Button control on the Form to create its event handler. This technique creates an event handler for a control's default event—the event that's most frequently used with that control. Controls can generate many different events, and each one can have its own event handler. For instance, your app can also provide an event handler for a Button MouseHover event, which occurs when the mouse pointer remains over the Button for a short period of time.

#### Using the Properties Window to Create Event Handlers
You can create event handlers through the Properties window. If you select a control on the Form, then click the Events (the light bolt icon in Fig 14.8) in the Properties window, that's events are listed in the window. You can double click an event's name to display in the editor an existing event handler for that event, or to create the event handler if it doesn't exist yet in code. You can also select an event, then use the drop-down list to choose an existing method that should be used as the event handler for that event. The methods that appear in this drop-down list are the Form classes that have the proper signature to be an event handler for the selected event. You can return to viewing the properties of a control by selecting the Properties icon (Fig. 14.8).

A single method handles events from multiple controls. For example, consider an app that displays CheckBoxes represent bold and italic fonts. The user could select bold, italic or both. In this case, the font's style depends on both CheckBoxes, so their
