
One advantage of using interfaces is the fact that a `class` can implement any number of interfaces. But you can only inherit from one class, abstract or non-abstract. An `interface` may even implement multiple interfaces itself. The syntax for defining an `interface` is as follows:

```csharp
[modifier] interface InterfaceIdentifier
{
    // Members - no access modifiers are used.
}
```

The members of an `interface` can be methods, properties, or events. No implementation details are provided by the `interface` for any of its members. The definition of the `interface` simply specifies a signature for the members that must be supplied by classes implementing it. Interfaces are usually named using an uppercase I as the first character, such as IComparable, ISearchable, or IPayable.

Interfaces are useful for forcing functionality in classes that implement them. Interfaces are especially good in multiprogrammer environments. They help to guarantee that classes conform to certain set standards and contain required methods. If a `class` implements the `interface`, it must provide the details for all of the interface’s members. Whereas `abstract` classes are used with classes that are closely related, interfaces are often best suited for providing some common functionality to unrelated classes. Because the `abstract class` is used as the base `class`, the “is a” relationship must exist. Any class derived from that base abstract class “is a” subtype of the abstract class.

## Defining an Interface

Interfaces can be defined as members of a `namespace` or `class` or by compiling to a DLL. You do this in much the same way that you created the dynamic link library components for Person and Student.

An easy approach is to put the `interface` in a separate project. In Visual Studio, use the **Class Library** template to start, and after you go into the Code Editor, replace the `class` definition with your `interface` definition.

> **NOTE** You could also define the `interface` inside the file that implements it, like the example first presented with the PresentationGUI project. However, you lose out on the advantages of component-based development. To do this, right-click the project, select **Add**, then **New Item** from the submenu from the **Solution Explorer** window and then use the **Interface** template.

Figure 11-15 shows an `interface` that is implemented by the Student `class`. It contains three `abstract` methods. Unlike an `abstract class`, it is not necessary to use the `abstract` keyword, because all methods are `abstract`. The ITraveler `interface` in Figure 11-15 includes three member methods. Notice the identifier for the `namespace` is different from the `interface` name.

![](img/36e48639a06772bcb0fa1ea2525b33a3_767_0.png)

**FIGURE 11-15**  ITraveler interface

> **NOTE**  Be sure to change the name of the `namespace` in the `interface` file also. Otherwise, you experience problems when you try to reference the file and add your `using` statement.

After you type the statements, build the interface DLL by using a **Build Solution** option from the **BUILD** menu bar. You can either select **BUILD**, **Build Solution**, or **Build** followed by the name of the project. Close the project and get ready to use the `interface`.

## Implementing the Interface

If you stored the `interface` as a separate project and created the DLL, to use the `interface` you follow the same steps as with the Person and Student DLLs. A separate Interface project was stored in the LibraryFiles folder for this chapter. From the Solution Explorer window, add a reference to the file ending in .dll. Type a `using` statement identifying the `namespace` for the `interface`.

The heading for the class definition can specify not only a base class following the colon, but one or more interfaces as follows:

```
[modifier] class ClassIdentifier : identifier [, identifier]
```

To indicate that the Student class derives from the base class Person and implements the ITraveler interface, Example 11-20 shows that you add ITraveler to the class definition line.

### EXAMPLE 11.20

```csharp
public class Student : Person, ITraveler  // Base class comes first.
{ ... }
```

If a class implements more than one interface, they all appear on the class definition line separated by commas. The base class is listed first if the class is inheriting from a base class.

Reviewing Figure 11-15, you see that ITraveler has three abstract methods as part of its definition. Because the Student class is implementing the ITraveler interface, it must define the implementation details for all three methods. Example 11-21 shows the revised Student class. It includes bodies for those methods and the GetExerciseHabits( ) method, which was defined as an abstract method in the Person class. This satisfies the implementation requirements for the methods.

### EXAMPLE 11.21

```csharp
public class Student : Person
{
    private string major;
    private string studentId;

    public Student()
    : base()
    {
    }

    // Constructor which sends 3 arguments to base class
    public Student(string id, string fname, string lname, string maj, string sId)
    : base(id, lname, fname)
    {
        major = maj;
        studentId = sId;
    }

    // Read only Property for studentID
    public string StudentId
    {
        get
        {
            return studentId;
        }
    }

    // Property for major data field
    public string Major
    {
        get
        {
            return major;
        }
        set
        {
            major = value;
        }
    }

    // Overrides GetSleepAmt()
    // method of the Person class
    public override int GetSleepAmt()
    {
        return 6;
    }

    // Using the base keyword, calls
    // the overridden GetSleepAmt()
    // method of the Person class
    public int CallOverriddenGetSleepAmt()
    {
        return base.GetSleepAmt();
    }

    // Abstract method in Person
    public override string GetExerciseHabits()
    {
        return "Exercises daily";
    }

    // Abstract method in
    // ITraveler Interface
    public string GetDestination()
    {
        return "Home";
    }

    // Abstract method in
    // ITraveler Interface
    public string GetStartLocation()
    {
        return "School";
    }

    // Abstract method in
    // ITraveler Interface
    public double DetermineMiles()
    {
        return 75.0;
    }
}
```

No other changes need to be made to the `Student` class. Of course, the body of these methods could be as sophisticated as is needed to support the business function. That is all there is to implementing an `interface`. No special changes have to occur to the `Person` or `PresentationGUI` component. They are separate, stand-alone components.

For testing purposes, the `PresentationGUI` class in the `PresentationGUIAbstractClassAndInterface` folder is modified to include calls to the three methods defined in the `interface`. Figure 11-16 shows the output generated when the new methods are called. They return the travel details.

![](img/36e48639a06772bcb0fa1ea2525b33a3_770_0.png)

**FIGURE 11-16** PresentationGUI output using interface methods

Additional Label and TextBox objects are added to the PresentationGUI class. The visibility property for each of these objects is initially set to false in PresentationGUIWithAbstractClassAndInterface. When the Show Travel Details button is clicked, the text boxes are populated with data returned from the new interface methods that were implemented in the Student class. Then, the Visible property for each of these new controls is set to true. The event-handler method for the button click event, where this code is placed, is shown in Example 11-22 along with the other event-handler methods in the PresentationGUI class. Due to space constraints the rest of the partial PresentationGUI class, stored in the PresentationGUI.Designer.cs file, is not shown.

### EXAMPLE 11.22

```csharp
public partial class PresentationGUI : Form
{
    private Student aStudent;

    public PresentationGUI()
    {
        InitializeComponent();
    }

    private void btnShow_Click(object sender, EventArgs e)
    {
        aStudent.Age = 25;
        // Calls overridden ToString() in Person
        // Returns the first name, a space, and
        // the last name
        txtBxName.Text = aStudent.ToString();
        // Calls ToString() from Object
        // Returns a number representing age
        // in string format
        txtBxAge.Text = aStudent.Age.ToString();
        txtBxID.Text = aStudent.StudentID;
        txtBxStudentSleep.Text =
            Convert.ToString(aStudent.GetSleepAmt());
        txtBxPersonSleep.Text =
            Convert.ToString(aStudent.CallOverriddenGetSleepAmt());
        // GetExerciseHabits() method defined as
        // abstract method in Person
        txtBxExercise.Text =
            aStudent.GetExerciseHabits();
        btnTravel.Visible = true;
    }

    private void PresentationGUI_Load(object sender, EventArgs e)
    {
        aStudent = new
            Student("123456789", "Maria", "Woo", "CS", "1111");
    }
}
```
