![](bbox=[0.143, 0.1, 0.857, 0.494])

**Fig. 14.3** | Components and controls for Windows Forms.

# Active Window and Focus

When there are several windows on the screen, the active window is the *frontmost* and has a *highlighted title bar*. A window becomes the active window when the user clicks somewhere inside it. The active window is said to “have the focus.” For example, in Visual Studio the active window is the Toolbox when you’re selecting an item from it, or the Properties window when you’re editing a control’s properties.

# Auto-Generated Code Stored in Separate File

A Form is a container for controls and components. When you drag an item from the Toolbox onto the Form, Visual Studio generates code that creates the object and sets its basic properties. This code is updated when the control or component’s properties are modified in the IDE. Removing a control or component from the Form deletes the corresponding generated code. The IDE maintains the generated code in a separate file using *partial* classes—classes that are split among multiple files and assembled into a single class by the compiler. You could write this code yourself, but it’s much easier to allow Visual Studio to handle the details. We introduced visual programming concepts in Section 2.6. In this chapter and the next, we use visual programming to build more substantial GUIs.

# Common Form Properties, Methods and an Event

Each control or component we present in this chapter is located in namespace `System.Windows.Forms`. To create a Windows Forms app, you generally create a Windows Form, set its properties, add controls to the Form, set their properties and implement event