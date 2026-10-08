
## 15.13 Visual Inheritance

same name, the fully qualified class names can be used to distinguish the classes in the app and prevent a name conflict (also called a name collision).

### Step 3: Compiling the Class Library

To allow other Forms to inherit from VisualInheritanceForm, we must pack Visual-InheritanceForm as a class library and compile it into a .dll file. Such a file is known as a dynamically linked library—away to package classes that you can refer to from others. Right click the project name in the Solution Explorer and select Properties, then the Application type drop-down list, change Windows Application to Class Library. Building the project produces the .dll. You can configure a project to be a class library when you first create it by selecting the Class Library template in the New Project dialog. [Note: A library cannot exist as a stand-alone app. The screen captures in Fig. 15.45 were taken before changing the project to a class library.]

### Step 4: Adding a Reference to the Class Library

Once the class is compiled and stored in the class library, the library can be referenced from any app by adding to Visual Studio to find the class library file. To visually inherit from VisualInheritanceBaseForm, first create a new Windows app. Right click the References in the Solution Explorer window and select Add Reference... from the pop-up menu that appears. The dialog box will contain a list of class libraries from the .NET Framework. Some libraries, like the one containing the System namespace, are those that you’re going to add to the IDE. These ones are not list.

In the Reference Manager dialog box, click the Browse... button. When you build a class library, Visual places the .dll file in the project's bin\Debug or bin\Release folder, depending on whether the Solution Configurations drop-down list in the IDE's toolbar is set to Debug or Release. In the Browse tab, you can navigate to the directory containing the class library you created in Step 3, as shown in Fig. 15.46. Select the .dll file and click Add.

![](img/57baed2319be0bb1b5f98674846f2711_693_0.png)

Fig. 15.46 | Using the Reference Manager dialog to browse for a DLL. (Part I of 2.)

![](img/57baed2319be0bb1b5f98674846f2711_694_0.png)

Fig. 15.46 | Using the Reference Manager dialog to browse for a DLL. (Part 2 of 2)

**Step 5: Using the Class—Deriving from a Base Form***

Open the file that defines the new app's GUI and modify the line that defines the class to indicate that the app's Form should inherit from class VisualInheritanceBase. The class-declaration should now appear as follows:

```
public partial class VisualInheritanceTest:
    VisualInheritanceBase.VisualInheritanceBase
```

Unless you specify namespace VisualInheritance in a using directive, you must use the fully qualified name VisualInheritanceBase.VisualInheritanceBase. In Design-view, the new app's Form should now display the controls inherited from the base Form (Fig. 15.47). We can now add more components to the Form.

![](img/57baed2319be0bb1b5f98674846f2711_694_1.png)

Fig. 15.47 | Form demonstrating visual inheritance.

## **Class VisualInheritanceTest**

Class VisualInheritanceTest (Fig. 15.48) is a derived class of VisualInheritanceBaseForm. The output illustrates the functionality of the program. The components, their layouts and the functionality of base class VisualInheritanceBaseForm (Fig. 15.45) are inherited by VisualInheritanceTest. We added an additional button with text About this Program. When you press this button, method button_Click (Fig. 15.48, lines 19–25) is invoked. This method displays another MessageBox providing different informative text (lines 21–24).

```
// Fig. 15.48: VisualInheritanceTestForm.cs
// Derived Form using visual inheritance.
using System;
using System.Windows.Forms;

namespace VisualInheritanceTest
{
    // derived Form using visual inheritance
    public partial class VisualInheritanceTestForm :
        VisualInheritanceBase.VisualInheritanceBase
    {
        // constructor
        public VisualInheritanceTestForm()
        {
            InitializeComponent();
        }

        // display MessageBox when Button is clicked
        private void aboutButton_Click(object sender, EventArgs e)
        {
            MessageBox.Show("This program was created by Deitel & Associates.",
                "About This Program", MessageBox.OK,
                MessageBoxIcon.Information);
        }
    }
}
```

![](img/57baed2319be0bb1b5f98674846f2711_695_0.png)

Fig. 15.48 | Derived Form using visual inheritance.

If a user clicks the Learn More button, the event is handled by the base-class event handler learnMoreButton_Click. Because VisualInheritanceBase uses a private access modifier to declare its controls, VisualInheritanceTestForm cannot modify the controls inherited from class VisualInheritanceBase or programmatically. The IDE displays a small icon at the top left of the visually inherited controls to indicate that they're inherited and cannot be altered.

## 15.14 User-Defined Controls

The .NET Framework allows you to create custom controls. These custom controls appear in your Toolbox and can be added to Forms, Panels or Groups in the same way you add Buttons, Labels and other predefined controls. The simplest way to create a custom control is to derive a class from an existing control, such as a Label. This is useful if you want to add functionality to an existing control, rather than replacing it with one that provides the desired functionality. For example, you can create a new type of Label that behaves like a normal Label but has a different appearance. You can accomplish this by inheriting from Label and overriding OnPaint.

### Method OnPaint

All controls have OnPaint method, which the system calls when a component must be redrawn (when the control is resized). The method receives a PaintEventArgs object, which contains graphics information—property Graphics is the object used to draw, and property ClipRectangle defines the rectangular boundary of the control. When the system raises a Paint event to draw the control on the screen, the control catches the event and calls its OnPaint method. The base class's OnPaint should be called explicitly from an overridden OnPaint implementation before executing custom paint code. In most cases, you will need to ensure that the original painting code you execute is defined within the control's class.

### Creating New Controls

To create a new control composed of existing controls, use UserControl. Controls added to a custom control are constituent controls. For a program, you could create a UserControl composed of a Button, a Label and a TextBox, each associated with some functionality (for example, the button setting the Label's text to that contained in the TextBox). The UserControl acts as a container for the controls added to it. The UserControl handles constituent controls, but it does not determine how these constituent controls are displayed. Each control can handle its own Paint event or override OnPaint. Both the Paint handler and OnPaint are passed a PaintEventArgs object, which can be used to draw graphics (lines, rectangles, and so on) on the constituents.

Using another technique, you can create a new-control by inheriting from Control. This class does not define any specific behavior; that's left to you. Instead, Control handles the items associated with all controls, such as events and sizing methods. Method OnPaint should contain a call to the base class's OnPaint method, which calls the Paint event handlers. You add code that draws custom graphics inside the overridden OnPaint method. This technique allows for the greatest flexibility but also requires the most planning. All three approaches are summarized in Fig. 15.49.
