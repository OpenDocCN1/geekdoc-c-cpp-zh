Designing user interfaces (UIs) for applications is one of the most important and crucial tasks. User interacts and uses the functionality of an application through its UI. A UI contains visually appealing interface with controls that can be customized as per user requirements. Apart from Console applications that run directly from Command Prompt, other applications, such as Windows Forms applications and Windows Presentation Foundation (WFP) applications designed on .NET Framework are built using forms. A form is a building block of an application and represents visual surface on which different Windows controls, such as Buttons and Labels are displayed to the user. You can build a Windows Forms application by adding controls to forms and customizing their behavior by using any .NET compliant language, such as C# and Visual Basic .NET (VB .NET). In other words, a form acts as a container for .NET controls. In addition, it offers various features, such as tabbed navigation (the feature by which a user can navigate to all the controls in a cycle), ordering of tabs, and listening to mouse events.

You can customize a form by specifying its characteristics, such as size, location, appearance, and fore color by using the **Form** class properties, such as **Size**, **Location**, **BackColor**, and **ForeColor**. Different customizations can be applied to forms so that they represent different visual effects for different users. Methods such as **SetDesktopLocation()** can be used to define the position of a form on the desktop. You can also define events, such as **Activated** to perform some modifications to a control, while the control is in active state.

In this chapter, you learn about the common operations that can be performed on a form, such as changing the title of a form and adding controls to a form. In addition, you learn to handle mouse and keyboard events for Windows Forms application. Finally, you learn to add different controls to a form and use them.

Now, let's first learn about the common operations that can be performed on a form in the following section.

# ## Performing Common Operations on Form

As stated earlier, a form constitutes a part of Microsoft .NET Framework and has a Graphical User Interface (GUI) for building Windows Forms applications. You can add different types of controls, such as **Button**, **Label**, and **RichTextBox** to a form to create Windows Forms applications. A control can be added to a form from Toolbox by either dragging and dropping it or double-clicking it.

# ### Note

> A Toolbox consists of icons of all the controls that can be added on a form. You can drag and then drop the controls on a form or simply double-click a control to add it to a form. To open Toolbox, select **View -> Toolbox**.

Let's discuss the following basic operations that can be performed on a form:

+   - Changing the title of a form
+   - Showing and hiding the Maximize, Minimize, and Close buttons
+   - Specifying the initial state and position of a form
+   - Creating a multiform Windows Forms application
+   - Setting the startup form in a multiform Windows Forms application
+   - Using the MessageBox.Show() Method
+   - Adding a control to a form
+   - Anchoring and docking a control
+   - Enabling and disabling controls
+   - Specifying the tab order of controls

Let's first learn to change the title of a form.