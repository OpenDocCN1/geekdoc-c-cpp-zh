# Chapter 21

example, whether or not a control is visible in the application window and whether or not a control is enabled to allow user interaction are determined by the property values that are set. You can set a control’s properties interactively when you assemble the GUI using the IDE. You can also set property values at runtime using functions that you add to the program or via code that you add to existing functions through the code Editor pane. The classes also define functions that you call to perform operations on the control.

When you create a project for a Windows Forms application, an application window based on the Form class is created along with all the code to display the application window. After you create a Windows Forms project, there are four distinct operations involved in developing a Windows Forms application:

+   - You create the GUI interactively in the Form Design tab that is displayed in the Editor pane by selecting controls in the Toolbox window and placing them on the form. You can also create additional form windows.
+   - You modify the properties for the controls and the forms to suit your application needs in the Properties window.
+   - You can create click event handlers for a control by double-clicking the control on the Form Design tab. You can also set an existing function as the handler for an event for a control from its Properties window.
+   - You can modify and extend the classes that are created automatically from your interaction with the Form Design tab to meet the needs of your application.

You’ll get a chance to see how it works in practice.

# Understanding Windows Forms Applications

You first need to get an idea of how the default code for a Windows Forms application works. Create a new CLR project using the Windows Forms Application template and assign the name Ex21_01 to the project. The Editor pane displays a graphical representation of the application window because with a Windows Forms application you build the GUI graphically. Even double-clicking Form1.h in the Solution Explorer pane does not display the code, but you can see it by right-clicking in the Editor window and selecting View Code from the context menu.

The code defines the Form1 class that represents the application window, and the first thing to note is that the code is defined in its own namespace:

```
namespace Ex21_01
{
    using namespace System;
    using namespace System::ComponentModel;
    using namespace System::Collections;
    using namespace System::Windows::Forms;
    using namespace System::Data;
    using namespace System::Drawing;

    // rest of the code
}
```