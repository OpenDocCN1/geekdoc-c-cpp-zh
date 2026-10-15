not likely to be as familiar with the base classes used for the other techniques for creating controls, so it’s appropriate to discuss them now.

Two generic base classes are used as a starting point to create a control. It is helpful to understand something about the structure of these classes to know when the use of each is appropriate.

> The classes discussed in this chapter are all in the System.Windows.Forms namespace. There are similarly named classes for some of these in the System.Web.UI namespace (which is used for Web Forms), but these classes should not be confused with anything discussed in this chapter.

# The Control Class

The Control class is contained within the System.Windows.Forms namespace and contains base functionality to define a rectangle on the screen, provide a handle for it, and process routine operating system messages. This enables the class to perform such functions as handling user input through the keyboard and mouse. The Control class serves as the base class for any component that needs a visual representation on a Win32-type graphical interface. Besides built-in controls and custom controls that inherit from the Control class, the Form class also ultimately derives from the Control class.

In addition to these low-level windowing capabilities, the Control class also includes such visually related properties as Font, ForeColor, BackColor, and BackgroundImage. The Control class also has properties that are used to manage layout of the control on a form, such as docking and anchoring.

> The Control class does not contain any logic to paint to the screen except to paint a background color or show a background image. While it does offer access to the keyboard and mouse, it does not contain any actual input processing logic except for the ability to generate standard control events such as Click and KeyPress. The developer of a custom control based on the Control class must provide all of the functions for the control beyond the basic capabilities provided by the Control class.

A standard set of events is also furnished by the Control class, including events for clicking the control (Click, DoubleClick), for keystroke handling (KeyUp, KeyPress, KeyDown), for mouse handling (MouseUp, MouseHover, MouseDown, etc.), and drag-and-drop operations (DragEnter, DragOver, DragLeave, DragDrop). Also included are standard events for managing focus and validation in the control (GotFocus, Validating, Validated). See the help files on the Control class for details about these events and a comprehensive list.

# The UserControl Class

The built-in functionality of the Control class is a great starting point for controls that will be built from scratch, with their own display and keyboard handling logic. However, the Control class has limited capability for use as a container for other controls.

That means that composite controls do not typically use the Control class as a starting point. Composite controls combine two or more existing controls, so the starting point must be able to manage contained controls. The class that is most often used to meet this requirement is the UserControl class. Because it ultimately derives from the Control class, it has all of the properties, methods, and events discussed earlier for that class.

However, the UserControl class does not derive directly from the Control class. It derives from the ContainerControl class, which, in turn, derives from the ScrollableControl class.

As the name suggests, the ScrollableControl class adds support for scrolling the client area of the control’s window. Almost all the members implemented by this class relate to scrolling. They include AutoScroll, which turns scrolling on or off, and controlling properties such as AutoScrollPosition, which gets or sets the position within the scrollable area.