
# 14.13 Wrap-Up

By default, a keyboard event is handled by the control that currently has the focus. Sometimes it is appropriate to have the Form handle these events. This can be accomplished by setting the Form's KeyPreview property to true, which makes the Form receive keyboard events before they're passed to another control—for example, a key press would raise the Form's KeyPress, even if a control within the Form has focus instead of the Form.

# 14.13 Wrap-Up

This chapter introduced several common GUI controls. We discussed event handling in detail, and showed how to create event handlers. We showed how delegates are used to connect event handlers to the events of specific controls. You learned how to use control's properties and Visual Studio to specify the layout of your GUI. We then demonstrated several controls, beginning with Labels, Buttons and TextBoxes. You learned how to use GroupBoxes and Panels to organize other controls. We then demonstrated CheckBoxes and RadioButtons, which are state buttons that allow users to select among several options. We displayed images in PictureBoxes, displayed helpful text on a GUI with ToolTips and specified a range of numeric input values for users with NumericUpDown. We then demonstrated how to handle mouse and keyboard events. The next chapter introduces additional GUI controls. You'll learn how to add menus to your GUIs and create Windows Forms that display multiple Forms.

# Summary

# Section 14.1 Introduction

- A graphical user interface (GUI) allows a user to interact visually with a program.
- GUIs are built from GUI controls.
- GUI controls are objects that can display information on the screen or enable users to interact with an app via the mouse, keyboard or other form of input.

# Section 14.2 Windows Forms

- Windows Forms are used to create the GUIs for programs.
- A Form is a graphical element that appears on the desktop; it can be a dialog, a window or MDI (multiple document interface) window.
- A component is an instance of a class that implements the interface, which defines the behaviors components must implement, such as how the control is loaded.
- A control is a component that has a graphical representation at runtime.
- Some components lack graphical representations (e.g., class Timer of namespace Windows.Forms). Such components are not visible at runtime.
- When there are several windows on the screen, the active window is the foremost and has a highlighted title bar. A window becomes the active window when the user clicks inside it.
- The active window is said to "have the focus."
- A Form is a container for controls and components.

# Section 14.3 Event Handling

- GUIs are event driven.
- When the user interacts with a GUI component, the interaction—known as an event—causes the program to perform a task. Common events include clicking a Button, typing in a TextBox, selecting an item from a menu, closing a window and moving the mouse.
- A method that performs a task in response to an event is called an event handler, and the overall processing of responding to events is known as event handling.

# Section 14.3.1 A Simple Event-Driven GUI

- An event handler executes only when the user performs the specific event.
- Each event handler receives two parameters when it's called. The first—an object reference typically named sender—is a reference to the object that generated the event. The second is a reference to an event objects of type EventArgs (one of its derived classes), which is typically named e. This object contains additional information about the event that occurred.
- EventArgs is the base class of classes that represent event information.

# Section 14.3.2 Auto-Generated GUI Code

- Visual Studio creates the code that initializes the GUI that you build in the GUI design window. This auto-generated code is placed in the Designer.cs file of the form.
- The auto-generated code that defines the GUI is part of the Form's class. The use of the partial modifier in the class declaration allows the class to be split among multiple files.
- The Designer.cs file contains the controls you create in Design mode.
- The Designer.cs file includes the Dispose method for releasing resources and method InitializeComponent, which sets the properties of the Form and its controls.
- Visual Studio uses the code in InitializeComponent to create the GUI you see in design view. Changing the code in this method may prevent Visual Studio from displaying the GUI properly.

# Section 14.3.3 Delegates and the Event-Handling Mechanism

- The control that generates an event is known as the event sender.
- An event-handling method—known as the event handler—responds to a particular event that a control generates.
- When an event occurs, the event sender sends its event to the handler to perform a task.
- The .NET event-handling mechanism allows you to choose your own names for event-handling methods. However, each event-handling method must declare the parameters to receive information about the event it handles.
- Event handlers are connected to a control's events via special objects called delegates.
- A delegate object holds a reference to a method with a signature specified by the delegate type's declaration.
- GUI controls have predefined delegates that correspond to every event they can generate.
- Since each event handler is declared as a delegate, the event sender can simply call the appropriate delegate when an event occurs. The delegate's job is to invoke the appropriate method.
- Event delegates represent a set of objects that all have the same signature.
- When an event occurs, each delegate calls every method referenced by a multicast delegate. Multicast delegates enable several methods to be called in a single event.
- Event delegates derive from class MulticastDelegate, which derives from class Delegate (both from namespace System).

# Section 14.3.4 Another Way to Create Event Handlers

- Double-clicking the control in the designer creates an event handler for a control's default event.
- Typically, controls can generate many different events, and each can have its own event handler.
- You can create additional event handlers through the Properties window.
- If you select a control on the Form, then click the Events icon (the lightning bolt) in the Properties window, all the events for that control are listed in the window. You can double click an event's name to display the event handler in the editor, if the event handler already exists, or to create the corresponding event handler.
- If you select an event, then use the drop-down to its right to choose an existing method that should handle that event. The methods that appear in this drop-down list are the Form class's methods that have the proper signature to be an event handler for the selected event.
- A single event can handle multiple events from multiple controls.

# Section 14.3.5 Locating Event Information

- Read the Studio documentation to learn about the different events raised by each control. To do this, select a control in the IDE and press the F1 key to display that control's online help. The web page that contains contains basic information about the control's class. Click the link to the list of events for control to display the supported events for control.

# Section 14.4 Control Properties and Layout

- Controls derive from Control (of namespace System.Windows.Forms).
- The Select method transfers the focus to a control and makes it the active control.
- The Enabled property indicates whether the user can interact with a control to generate an event.
- A programmer can hide the control from the user without disabling it by setting the Visible property to false or by calling Hide.
- Anchoring causes controls to remain at a fixed distance from the sides of the container when it is resized.
- Docking attaches a control to a container such that the control stretches across an entire side or fills the remaining space.
- The Padding property specifies the distance between the controls and the Form edges.
- The Anchor and Dock properties of a Control are set with respect to the Control's parent container, which could be a Form or other parent container (such as a Panel).
- The minimum and maximum Form (or other Control) sizes can be set via properties MinimumSize and MaximumSize, respectively.
- When dragging a control across a Form, blue lines (known as snap lines) appear to help you position the control with other controls and the Form's edges.
- Visual Studio also provides the Format menu, which contains several options for modifying your GUI's layout.

# Section 14.5 Labels, TextBoxes and Buttons

- Labels provide information (as well as images) that the user cannot directly modify.
- A TextBox (class TextBox) is an area in which text can be displayed by a program or in which the user can type text via the keyboard.
- A password TextBox is a TextBox that hides the information entered by the user. As the user types, the password TextBox masks the user input by displaying a password character (*). If you use the SystemPasswordChar property to true, the TextBox becomes a password TextBox.
