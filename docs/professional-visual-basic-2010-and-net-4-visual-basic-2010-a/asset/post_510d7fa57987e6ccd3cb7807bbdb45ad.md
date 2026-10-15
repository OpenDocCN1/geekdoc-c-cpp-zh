
When any type of control is added to the form, a new variable is added to the form class. Controls are represented by variables; and, just as form properties are set in code, form controls are added in code. The Button class in the System.Windows.Forms namespace implements the Button control on the Toolbox. Each control added to a form has a class that implements the functionality of the control. For the standard controls, these classes are usually found in the System.Windows.Forms namespace. The WithEvents keyword has been used in the declaration of the new variable so that it can respond to events raised by the button.

The bulk of the code changes are in the InitializeComponent procedure. Nine lines of code have been added to help set up and display the Button control. The first addition to the procedure is a line that creates a new instance of the Button class and assigns it to the button variable:

```
Me.ButtonTest = New System.Windows.Forms.Button()
```

Before a button is added to the form, the form’s layout engine must be paused. This is done using the next line of code:

```
Me.SuspendLayout()
```

The next four lines of code set the properties of the button. The Location property of the Button class sets the location of the top-left corner of the button within the form:

```
Me.ButtonTest.Location = New System.Drawing.Point(13, 13)
```

The location of a control is expressed in terms of a Point structure. Next, the Name property of the button is set:

```
Me.ButtonTest.Name = "ButtonTest"
```

The Name property acts exactly as it did for the form, setting the textual name of the button. The Name property has no effect on how the button is displayed on the form; it is used to recognize the button’s context within the source code. The next four lines of code assign values to the Size, TabIndex, Text, and UseVisualStyleBackColor properties of the button:

```
Me.ButtonTest.Size = New System.Drawing.Size(104, 23)
Me.ButtonTest.TabIndex = 0
Me.ButtonTest.Text = "Run Code"
Me.ButtonTest.UseVisualStyleBackColor = True
```

Code snippet from Form1.Designer

The Size property defines the height and width of the control; it is being set because the default button size didn’t display the full label, and so the button’s size was increased. The TabIndex property of the button is used to set the order in which the control is selected when a user cycles through the controls on the form using the Tab key. The higher the number, the later the control gains focus. Each control should have a unique number for its TabIndex property. The Text property of a button sets the text that appears on the button. Finally, the UseVisualStyleBackColor property indicates that when this button is drawn, it uses the current visual style. This is a Boolean value and typically you can accept this default, but you can customize the background so that a given button doesn’t default to the current visual style.

Once the properties of the button have been set, it needs to be added to the form. This is accomplished with the next line of code:

```
Me.Controls.Add(Me.ButtonTest)
```

The System.Windows.Forms.Form class (from which your Form1 class is derived) has a property called Controls that keeps track of all of the child controls of the form. Whenever you add a control to a form in the designer, a line similar to the preceding one is added automatically to the form’s initialization process.

Finally, near the bottom of the initialization logic is the final code change. The form is given permission to resume the layout logic:

```
Me.ResumeLayout(False)
```

In addition to the code that has been generated in the Form1.Designer.vb source file, you have created code that lives in the Form1.vb source file:

```
```vb
Public Class Form1

    Private m_count As Integer
    Public Property Count() As Integer
        Get
            Return m_count
        End Get
        Set(ByVal value As Integer)
            m_count = value
        End Set
    End Property

    ''' <summary>
    '''
    ''' </summary>
    ''' <param name="sender"></param>
    ''' <param name="e"></param>
    ''' <remarks></remarks>
    Private Sub ButtonTest_Click(ByVal sender As System.Object,
                                 ByVal e As System.EventArgs) Handles ButtonTest.Click

        Count += 1
        MessageBox.Show("Hello World shown " + Count.ToString() + " times.",
                        "Hello World Message Box",
                        MessageBoxButtons.OK,
                        MessageBoxIcon.Information)

    End Sub
End Class
```
```

> *Code snippet from Form1*

This code reflects the event handler added for the button. The code contained in the handler was already covered, with the exception of the naming convention for event handlers. Event handlers have a naming convention similar to that in previous versions of Visual Basic: The control name is followed by an underscore and then the event name. The event itself may also have a standard set of parameters. At this point, you can test the application, but to do so let’s first look at your build options.

## Building Applications

For this example, it is best to build your sample application using the Debug build configuration. The first step is to ensure that Debug is selected as the active configuration. As noted earlier in this chapter around Figure 1-7 you’ll find the setting available on your project properties. It’s also available from the main Visual Studio display in the Solution Configurations drop-down list box that’s part of the Standard Toolbar. Visual Studio provides an entire Build menu with the various options available for building an application. There are essentially two options for building applications:

- **Build** — This option uses the currently active build configuration to build the project or solution, depending upon what is available.
- **Publish** — For Visual Basic developers, this option starts the process of creating a release build, but note that it also ties in with the deployment of your application, in that you are asked to provide an URL where the application will be published.

The Build menu supports building for either the current project or the entire solution. Thus, you can choose to build only a single project in your solution or all of the projects that have been defined as part of the current configuration. Of course, anytime you choose to test-run your application, the compiler will automatically perform a compilation check to ensure that you run the most recent version of your code.

You can either select Build from the menu or use the Ctrl+Shift+B keyboard combination to initiate a build. When you build your application, the Output window along the bottom edge of the development
environment will open. As shown in Figure 1-25, it displays status messages associated with the build process. This window should indicate your success in building the application.

If problems are encountered while building your application, Visual Studio provides a separate window to help track them. If an error occurs, the Task List window will open as a tabbed window in the same region occupied by the Output window (refer to Figure 1-25). Each error triggers a separate item in the Task List; if you double-click an error, Visual Studio automatically repositions you on the line with the error. Once your application has been built successfully, you can run it.

Once your application has been built successfully, you will find the executable file located in the targeted directory. By default, for .NET applications this is the \bin subdirectory of your project directory.

![](img/d99870e80390742f93963da7be0b2e61_66_0.png)

FIGURE 1-25

## Running an Application in the Debugger

As discussed earlier, there are several ways to start your application. Starting the application launches a series of events. First, Visual Studio looks for any modified files and saves those files automatically. It then verifies the build status of your solution and rebuilds any project that does not have an updated binary, including dependencies. Finally, it initiates a separate process space and starts your application with the Visual Studio debugger attached to that process.

When your application is running, the look and feel of Visual Studio’s IDE changes, with different windows and button bars becoming visible (see Figure 1-26). While your code remains visible, the IDE displays additional windows — by default, the Immediate Window appears in the same location as the Output Window as a new tabbed window. Others, such as the Call Stack, Locals, and Watch windows, may also be displayed over time as you work with the debugger. (Not all of these windows are available to users of Visual Studio Express Edition.) These windows are used by the debugger for reviewing the current value of variables within your code.

![](img/d99870e80390742f93963da7be0b2e61_66_1.png)

FIGURE 1-26
