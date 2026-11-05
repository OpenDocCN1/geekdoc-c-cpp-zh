
- 14. The **Control** class has a number of methods, including `Focus()`, `Hide()`, `Select()`, and `Show()`.
- 15. Controls that you add to a form are objects or instances of one of the predefined classes such as `Label`, `TextBox`, and `Button`. They inherit the properties, methods, and events from the **Control** class.
- 16. `Label` objects are normally used to provide descriptive text for another control. In addition to the inherited members, they have their own unique properties, methods, and events.
- 17. `TextBox` objects are probably the most commonly used controls, because they can be used for both input and output. In addition to the inherited members, they have their own unique properties, methods, and events.
- 18. `Button` objects are added to your form to add functionality. Users can click `Button` objects to perform a specific task. In addition to the inherited members, they have their own unique properties, methods, and events.

## EXERCISES

- 1. One of the differences between a console application and a Windows application is:
  - a. Classes can only be used with console applications.
  - b. One font size is used with console applications.
  - c. Variables must be declared with console applications.
  - d. Windows applications require that program statements be placed in a `class`.
  - e. Execution always begins in the `Main()` method for console applications.

- 2. Which `namespace` includes most of the `Control` classes for developing Windows applications?
  - a. `System`
  - b. `System.Windows.Controls`
  - c. `System.Windows.Components.Forms`
  - d. `System.Windows.Forms`
  - e. `System.Windows.Drawing`

- 3. Which of the following inherits members from the `Control` class?
  - a. `Label`
  - b. `Form`
  - c. `TextBox`
  - d. a and c
  - e. all of the above

- 4. The ____________ is the front end of a program that represents the presentation layer or the visual image of the program.
  - a. interface
  - b. control
  - c. Visual Studio
  - d. IDE
  - e. framework

- 5. A(n) ____________ is a notification from the operating system that an action has occurred, such as the user clicking the mouse or pressing a key.
  - a. method call
  - b. statement
  - c. event
  - d. GUI
  - e. handler

- 6. Which of the Control objects is viewed as a container that can hold other objects when you design a Windows application?
  - a. Control
  - b. Button
  - c. Window
  - d. Frame
  - e. Form

- 7. Which property is used to set the caption for the Windows title bar?
  - a. Caption
  - b. Text
  - c. Title
  - d. TitleBar
  - e. WindowTitle

- 8. The class heading `public class AForm : Form` indicates that:
  - a. Form is a derived class of the AForm class.
  - b. AForm is the base class for the Form class.
  - c. The class being defined is identified as Form.
  - d. AForm inherits the members of the Form class.
  - e. none of the above

- 9. If the name of the `class` is `graphicalForm`, the following:
  `public graphicalForm()` is an example of a(n):
  - a. accessor method
  - b. property
  - c. constructor
  - d. mutator method
  - e. data member

- 10. You would use an IDE such as Visual Studio to construct Windows applications because it has the following capability:
  - a. drag-and-drop construction
  - b. IntelliSense features
  - c. access to the Properties window listing properties and events
  - d. access to the Toolbox for dropping controls
  - e. all of the above

- 11. `Click` is an example of a(n):
  - a. event
  - b. property
  - c. method
  - d. control
  - e. handler

- 12. Visual Studio has a number of windows that can be viewed during design. The window used to hold controls that are dragged and dropped during construction is called the:
  - a. Property
  - b. Code Editor
  - c. Form Designer
  - d. Solution Explorer
  - e. Class View

- 13. If the `System.Windows.Forms` `namespace` is imported, the following statement:
  `this.textbox1 = new System.Windows.Forms.TextBox();`
  can be written as:
  - a. `this.textbox1 = new TextBox();`
  - b. `textbox1 = new TextBox();`
  - c. `textbox1 = new System.Windows.Forms.TextBox();`
  - d. all of the above
  - e. none of the above

- 14. The statement that actually constructs or instantiates a `Button` object is:
  - a. `this.button1 = new System.Windows.Forms.Button();`
  - b. `private System.Windows.Forms.Button button1;`
  - c. `this.Controls.AddRange(this.button1);`
  - d. `button1.Name = "A button";`
  - e. `button1.Click += new System.EventHandler(this.button1_Click);`

- 15. The statement that registers a Button object click event with the operating system is:
  - a. `this.button1ClickEvent = new System.Windows.Forms.Button();`
  - b. `private System.Windows.Forms.Button button1ClickEvent;`
  - c. `this.Controls.AddRange(this.button1ClickEvent);`
  - d. `button1.Click = "Register Me";`
  - e. `button1.Click += new System.EventHandler(this.button1_Click);`

- 16. The property of the TextBox control that is used to set all characters to uppercase as they are typed is:
  - a. CharacterCasing
  - b. Text
  - c. ToUpper
  - d. UpperCase
  - e. ConvertToUpper

- 17. Which of the following might be the heading for an event-handler method?
  - a. `private void btn1_Click(object sender, System.EventArgs e)`
  - b. `Application.Run(new TempAgencyForm());`
  - c. `btnCalculate.Click += new System.EventHandler(this.btnCalculate_Click);`
  - d. `this.btnCalculate = new System.Windows.Forms.Button();`
  - e. none of the above

- 18. Which of the following design considerations leads to more user-friendly presentation layers for GUIs?
  - a. Avoid clutter.
  - b. Be consistent with font, color, and placement.
  - c. Design for the target audience.
  - d. Use contrast to call attention to something.
  - e. all of the above

- 19. The `#region ... #endregion` is an example of a C# ____________.
  - a. Windows **class** declaration statement
  - b. required statement for creating Windows applications
  - c. reference to a **namespace** called region
  - d. preprocessor directive
  - e. collapsible segment of code that must be used for Windows applications

- 20. During design, how can you separate the business logic from the presentation layer?
  - a. Create two forms, one for input and the other for output.
  - b. Create two objects using an object-oriented approach.
  - c. Create at least two methods.
  - d. Create separate classes for each.
  - e. all of the above

- 21. Describe at least three ways Windows applications differ from console applications.

- 22. Identify which property could be set so that a Form **object** would perform the following function:
  - a. Change the background color for the form.
  - b. Set the default font to Courier for all controls that are added.
  - c. Change the size of the window to 400 by 400.
  - d. Associate a name of designForm with the Form **object**.
  - e. Position the window near the center of the screen.

- 23. Describe what might be done to respond to a button click event.

- 24. List at least five issues to consider when you plan the design of graphical user interfaces.

- 25. Describe the process that must occur to get a TextBox **object** added to a Form **object**. In your description, consider not only how the process is performed with Visual Studio, but also what steps would be necessary to do it manually.

## PROGRAMMING EXERCISES

- 1. Create a Windows application that contains a button labeled OK and a textbox labeled Name. Change the properties of the Form to have a different background color of your choosing. Change the Font property to a font of your choice. Initially clear the text from the textbox. Align the controls so they are aesthetically pleasing.

- 2. To the project developed in the preceding exercise, add an event handler for the button so that when the user clicks the OK button, the value entered is cleared, the form changes color, and a message is displayed on a label prompting the user to enter their name.
