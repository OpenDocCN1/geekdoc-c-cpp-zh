+   - A set of text boxes to hold a name, address, and phone number, with the combined information formatted and validated in a particular way
+   - A set of option buttons with a single property exposed as the chosen option

As with inherited controls, composite controls are only appropriate for situations that require the same functionality in multiple places. If the functionality is only needed once, then simply placing the relevant controls on the form and including appropriate logic right in the form is usually better.

Composite controls in Windows Forms are most often created using the UserControl class as a base class. Composite controls can be created using other classes as a base, however, and a later section entitled Embedding Controls in Other Controls shows an example.

# Writing a Control from Scratch

If a control needs special functionality not available in any existing control, then it can be written from scratch to draw its own visual interface and implement its own logic. This option requires more work, but it enables you to do just about anything within .NET and Windows Forms, including very sophisticated user interfaces.

To write a control from scratch, it is necessary to inherit from the Control class, which provides basic functionality such as properties for colors and size. With this basic functionality already built in, your required development tasks include adding any specific properties and methods needed for the control, writing rendering logic that will paint the control to the screen, and handling mouse and keyboard input to the control.

# INHERITING FROM AN EXISTING CONTROL

With this background on the options for creating custom controls, the next step is to look in depth at the procedures used for their development. First up is creating a custom control by inheriting from an existing control and extending it with new functionality. This is the simplest method for the creation of new controls, and the best way to introduce generic techniques that apply to all custom controls.

After you look at the general steps needed to create a custom control via inheritance, an example illustrates the details. It is important to understand that many of the techniques described for working with a control created through inheritance also apply to the other ways that a control can be created. Whether inheriting from the Control class, the UserControl class, or from an existing control, a control is a .NET class. Creating properties, methods, and events, and coordinating these members with the Visual Studio designers, is done in a similar fashion, regardless of the starting point.

# Process Overview

Here are the general stages involved in creating a custom control via inheritance from an existing control. This is not a step-by-step recipe, just an overview. A subsequent example provides more detail on the specific steps, but those steps follow these basic stages:

+   1. Create or open a Windows Control Library project and add a new custom control to the project. The class that is created will inherit from the `System.Windows.Forms.Control` base class. The line that specifies the inherited class must be changed to inherit from the control that is being used as the starting point.
+   2. The class file gets new logic added as necessary to add new functionality. Then the project is compiled with a Build operation in order to create a DLL containing the new control’s code.
+   3. The control is now ready to be used. It can be placed in the Windows Forms Toolbox with the Choose Items option in Visual Studio 2010. From that point forward, it can be dragged onto forms like any other control.