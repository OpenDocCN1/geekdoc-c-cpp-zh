
## Chapter 2: Getting Started with Visual Studio 2008

Instead of exposing the caption variable as public, it is a better idea to encapsulate it as a property and use the set and get accessors to access it. To do that, right-click on the caption variable and select Refactor ⇔ Encapsulate Field (see Figure 2-54).

![](img/a977a875c7c627b45d939729705a252e_68_0.png)

Figure 2-54

Assign a name to your property (see Figure 2-55). You have the option to update all external references or all references (including the one within the class), and you can choose to preview your reference changes. When you're ready, click OK.

![](img/a977a875c7c627b45d939729705a252e_68_1.png)

Figure 2-55

After you've previewed the changes (see Figure 2-56), click Apply to effect the change.

![](img/a977a875c7c627b45d939729705a252e_68_2.png)

Figure 2-56

## Part I: C# Fundamentals

Here is the result after applying the change:

```csharp
namespace WindowsFormsApplication1
{
    public partial class Form1 : Form
    {
        private string caption;

        public string Caption
        {
            get { return caption; }
            set { caption = value; }
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            //...
        }
    }
}
```

## Extract Interface

You can use the refactoring engine to extract an interface from a class definition. Consider the following Contact class:

```csharp
namespace WindowsFormsApplication1
{
    class Contact
    {
        public string FirstName
        {
            get;
            set;
        }
        public string LastName
        {
            get;
            set;
        }
        public string Email
        {
            get;
            set;
        }
        public DateTime DOB
        {
            get;
            set;
        }
    }
}
```

## Chapter 2: Getting Started with Visual Studio 2008

Right-click the Contact class name and select Refactor ⇒ Extract Interface (see Figure 2-57).

![](img/a977a875c7c627b45d939729705a252e_70_0.png)

Figure 2-57

The Extract Interface dialog opens, and you can select the individual public members to form the interface (see Figure 2-58).

![](img/a977a875c7c627b45d939729705a252e_70_1.png)

Figure 2-58

The new interface is saved in a new .cs file. In this example, the filename is IContact.cs:

```csharp
using System;
namespace WindowsFormsApplication1
{
    interface IContact
    {
        DateTime DOB { get; set; }
        string Email { get; set; }
        string FirstName { get; set; }
        string LastName { get; set; }
    }
}
```

## Part I: C# Fundamentals

The original Contact class definition has now been changed to implement the newly created interface:

```
class Contact : WindowsFormsApplication1.IContact
{
    public string FirstName
    ...
}
```

## Promote Local Variable to Parameter

You can promote a local variable into a parameter. Here's an example:

```
private void Form1_Load(object sender, EventArgs e)
{
    LogError("File not found.");
}

private void LogError(string message)
{
    string SourceFile = "Form1.cs";
    Console.WriteLine(SourceFile + ": " + message);
}
```

You want to promote the variable SourceFile into a parameter so that callers of this function can pass in its value through an argument. To do so, select the variable SourceFile, right-click, and then select Refactor -> Promote Local Variable to Parameter (see Figure 2-59).

![](img/a977a875c7c627b45d939729705a252e_71_0.png)

Figure 2-59

Note that the local variable to be promoted must be initialized or an error will occur. The promoted variable is now in the parameter list and the call to it is updated accordingly:

```
private void Form1_Load(object sender, EventArgs e)
{
    LogError("File not found.", "Form1.cs");
}
```

```
private void LogError(string message, string SourceFile)
{
    Console.WriteLine(SourceFile + ": " + message);
}
```

## Debugging

Debugging is an important part of the development cycle. Naturally, Visual Studio 2008 contains debugging tools that enable you to observe the runtime behavior of your program. This section takes a look at those tools.

Suppose that you have the following program:

```csharp
using System;
using System.Windows.Forms;

namespace WindowsFormsApplication1
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            Console.WriteLine("Start");
            printAllOddNumbers(9);
            Console.WriteLine("End");
        }

        private void printAllOddNumbers(int num)
        {
            for (int i = 1; i <= num; i++)
            {
                if (i % 2 == 1)
                {
                    Console.WriteLine(i);
                }
            }
        }
    }
}
```

The following sections show how you can insert breakpoints into the application so that you can debug the application during runtime.

## Setting Breakpoints

To set a breakpoint in your application, in the Visual Studio 2008 Code Editor, click in the left column beside the statement at which you want to set the breakpoint (see Figure 2-60).

## Part I: C# Fundamentals

![](img/a977a875c7c627b45d939729705a252e_73_0.png)

Figure 2-60

Press F5 to debug the application. When the execution reaches the statement with the breakpoint set, Visual Studio 2008 pauses the application and shows the breakpoint (see Figure 2-61).

![](img/a977a875c7c627b45d939729705a252e_73_1.png)

Figure 2-61

## Stepping through the Code

With the application stopped at the breakpoint, you have a choice of what to do:

- **Step Into** — Press F11 (see Figure 2-62). Stepping into the code means that if the breakpoint statement is a function call, execution is transferred to the first statement in the function and you can step through the function one statement at a time.
- **Step Over** — Press F10. Stepping over the code means that if the breakpoint statement is a function call, the entire function is executed and control is transferred to the next statement after the function.
- **Step Out** — Press Shift+F11 to step out of the code (Step Out). If the statement at the breakpoint is part of a function, execution is resumed until the function exits. The control is transferred to the returning point in the calling function.

Step Into and Step Over are basically the same, except when it comes to executing functions.

![](img/a977a875c7c627b45d939729705a252e_74_0.png)

While you are at a breakpoint stepping through the code (using either F10 or F11), you can also examine the values of variables by hovering the mouse over the object you want to examine. Figure 2-63 shows value of i when the mouse is over i.

![](img/a977a875c7c627b45d939729705a252e_74_1.png)

## Watching

You can also right-click on the object you want to monitor and select Add Watch or QuickWatch (see Figure 2-64).

![](img/a977a875c7c627b45d939729705a252e_75_0.png)

Figure 2-64

When you use the Add Watch feature, the variable you are watching will be displayed in the Watch window (see Figure 2-65). As you step through your code, changes in the variable are reflected in the Watch window. In addition, you have the option to change the value of the variable directly in the Watch window.

![](img/a977a875c7c627b45d939729705a252e_75_1.png)

Figure 2-65

The QuickWatch feature also enables you to monitor the value of variables, except that the execution cannot continue until you have closed the QuickWatch window (see Figure 2-66). You can also enter an expression to evaluate and at the same time add a variable into the Add Watch window.

![](img/a977a875c7c627b45d939729705a252e_75_2.png)

Figure 2-66

## Part I: C# Fundamentals

This section demonstrates how unit testing is performed in Visual Studio 2008. Use the following Point class definition located within a Class Library project:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace UnitTesting
{
    class Point
    {
        public Point() { }
        public Point(int x, int y)
        {
            this.x = x;
            this.y = y;
        }

        public int x { get; set; }
        public int y { get; set; }

        //---calculates the length between 2 points
        public double length(Point pointOne)
        {
            return Math.Sqrt(
                Math.Pow(this.x - pointOne.x, 2) +
                Math.Pow(this.y - pointOne.y, 2));
        }
    }
}
```

## Creating the Test

For this example, create a unit test to test the length() method. To do so, right-click on the length() method and select Create Unit Tests (see Figure 2-69).

![](img/a977a875c7c627b45d939729705a252e_77_0.png)

Figure 2-69
