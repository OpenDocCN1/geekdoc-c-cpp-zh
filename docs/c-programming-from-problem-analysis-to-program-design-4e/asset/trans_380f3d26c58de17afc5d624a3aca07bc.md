
使用接口的一个优点是，一个 `class` 可以实现任意数量的接口。但你只能从一个类继承，无论它是抽象类还是非抽象类。一个 `interface` 甚至可以自身实现多个接口。定义 `interface` 的语法如下：

```csharp
[modifier] interface InterfaceIdentifier
{
    // Members - no access modifiers are used.
}
```

`interface` 的成员可以是方法、属性或事件。`interface` 不为其任何成员提供实现细节。`interface` 的定义仅指定实现它的类必须提供的成员签名。接口通常使用大写 I 作为第一个字符来命名，例如 IComparable、ISearchable 或 IPayable。

接口有助于强制实现它的类具备相应功能。接口在多程序员环境中尤其有用。它们有助于确保类符合某些既定标准并包含必需的方法。如果 `class` 实现 `interface`，则必须为接口的所有成员提供实现细节。`abstract` 类用于密切相关的类，而接口通常最适合为不相关的类提供一些公共功能。由于 `abstract class` 用作基 `class`，因此必须存在“是一个”关系。任何从该基抽象类派生的类都是该抽象类的“是一个”子类型。

## 定义接口

接口可以定义为 `namespace` 或 `class` 的成员，也可以通过编译为 DLL 来定义。执行此操作的方式与为 Person 和 Student 创建动态链接库组件的方式大致相同。

一种简单的方法是将 `interface` 放在单独的项目中。在 Visual Studio 中，使用 **类库** 模板开始，然后进入代码编辑器后，用你的 `interface` 定义替换 `class` 定义。

> **注意** 你也可以在实现该 `interface` 的文件中定义它，就像最初在 PresentationGUI 项目中给出的示例那样。但是，你会失去基于组件的开发优势。要这样做，请右键单击该项目，从 **解决方案资源管理器** 窗口的子菜单中选择 **添加**，然后选择 **新建项**，接着使用 **接口** 模板。

图 11-15 展示了一个由 Student `class` 实现的 `interface`。它包含三个 `abstract` 方法。与 `abstract class` 不同，不必使用 `abstract` 关键字，因为所有方法都是 `abstract`。图 11-15 中的 ITraveler `interface` 包含三个成员方法。注意 `namespace` 的标识符与 `interface` 名称不同。

![](img/36e48639a06772bcb0fa1ea2525b33a3_767_0.png)

**图 11-15** ITraveler 接口

> **注意** 请务必同时更改 `interface` 文件中 `namespace` 的名称。否则，当你尝试引用该文件并添加 `using` 语句时，会遇到问题。

键入这些语句后，使用 **生成** 菜单栏中的 **生成解决方案** 选项生成接口 DLL。你可以选择 **生成** > **生成解决方案**，或选择 **生成** 后跟项目名称。关闭项目，准备使用该 `interface`。

## 实现接口

如果你将 `interface` 存储为单独项目并创建了 DLL，那么使用该 `interface` 的步骤与使用 Person 和 Student DLL 相同。本章的 LibraryFiles 文件夹中存储了一个单独的 Interface 项目。从解决方案资源管理器窗口中，添加对以 .dll 结尾的文件的引用。键入一条 `using` 语句，标识该 `interface` 的 `namespace`。

类定义的开头不仅可以指定冒号后的基类，还可以指定一个或多个接口，如下所示：

```
[modifier] class ClassIdentifier : identifier [, identifier]
```

为了表明 Student 类派生自基类 Person 并实现 ITraveler 接口，示例 11-20 展示了将 ITraveler 添加到类定义行中。

### 示例 11.20

```csharp
public class Student : Person, ITraveler  // Base class comes first.
{ ... }
```

如果一个类实现多个接口，它们都会出现在类定义行中，并用逗号分隔。如果该类继承自基类，则首先列出基类。

回顾图 11-15，可以看到 ITraveler 的定义中包含三个抽象方法。由于 Student 类实现 ITraveler 接口，因此它必须为所有三个方法定义实现细节。示例 11-21 展示了修改后的 Student 类。它包括这些方法的方法体，以及 GetExerciseHabits( ) 方法，该方法在 Person 类中定义为抽象方法。这满足了这些方法的实现要求。

### 示例 11.21

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

无需对 `Student` 类做其他更改。当然，这些方法的方法体可以根据支持业务功能的需要而复杂化。实现 `interface` 的全部内容就是这些。`Person` 或 `PresentationGUI` 组件无需进行特殊更改。它们是各自独立的组件。

为了测试，修改了 `PresentationGUIAbstractClassAndInterface` 文件夹中的 `PresentationGUI` 类，使其包含对 `interface` 中定义的三个方法的调用。图 11-16 展示了调用这些新方法时生成的输出。它们返回旅行详细信息。

![](img/36e48639a06772bcb0fa1ea2525b33a3_770_0.png)

**图 11-16** 使用接口方法的 PresentationGUI 输出

向 PresentationGUI 类添加了额外的 Label 和 TextBox 对象。在 PresentationGUIWithAbstractClassAndInterface 中，这些对象的可见性属性最初都设置为 false。单击“显示旅行详细信息”按钮时，文本框中会填充从 Student 类中实现的新接口方法返回的数据。然后，将这些新控件的 Visible 属性设置为 true。放置此代码的按钮单击事件的事件处理程序方法如示例 11-22 所示，同时还包括 PresentationGUI 类中的其他事件处理程序方法。由于篇幅限制，存储在 PresentationGUI.Designer.cs 文件中的 PresentationGUI 分部类的其余部分未显示。

### 示例 11.22

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
