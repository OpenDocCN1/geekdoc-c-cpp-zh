
You might design a window that includes several locations on your screen where a user could input different values. You might have many different buttons on that same screen, with one labeled Compute. With Windows applications, you register events about which you want your program to receive notification. For example, you might want your program to be notified when the user clicks the Compute button. For this situation, you would write in your program a method called an event handler, indicating what should be done when that Compute button is clicked. If this is the only event-handler method you include, your program, once launched, would be in a process loop—or wait state—until that Compute button was clicked.

The body of the event-handler method for the Compute button might include statements to perform a calculation and then display the formatted results on the Windows form. When the user clicks the Compute button, an event is fired. The operating system sends a message to your program indicating that the event you registered has occurred. The associated method to handle the event is then executed automatically.

Think about your own experience using any Windows-based program. Take, for example, your word-processing program. After being launched, the program appears to be sitting idle allowing you to type forever. However, it is in a process loop after it is launched. When you select an option from one of the menus, an event is fired. Select an option such as Find or Search and a dialog box prompts you to enter the word for the search. Another event is fired when you press the Enter key indicating you have finished typing the search word. This event-handler method performs the search in your document. Until you clicked on the menu bar, the program was just waiting for a notification from the operating system that an event of interest had occurred.

Unlike console-based applications that exit after all statements have been sequentially executed, Windows-based applications, after they are launched, sit idly waiting for notification of a registered event. The program remains in the operating system environment in a process loop. This means your program could be minimized, resized, or closed like other Windows applications. Someone could surf the Web for hours while your program was still running, or write an English paper using another application. Your program’s code would be ready and still waiting for an event to be fired when the user made the program’s window active again.

Another important difference is sequential order. Unlike the sequential nature you expect with console-based applications, in which one statement executes followed by the next, no sequential order exists with methods that handle events for Windows applications. If you have many options on your screen, or many buttons, you do not know which one the user will click first or whether any of them will be clicked. Again, think about your experiences using a Windows-based word processor. Each time you use the program, you select different options or use different menu selections.

With Windows applications, many different types of events can be fired. As a developer, you select actions your program should respond to and write event handlers for those events. If you have five buttons on the screen, button1 might not be the one clicked first every time. These event-handler methods can be executed in a different order every time your application runs.

![](img/36e48639a06772bcb0fa1ea2525b33a3_534_0.png)

Windows applications not only function differently, they also look different. Windows applications tend to have a consistent user interface—one that is considered more user-friendly than what you find with console-based applications. In many cases, the user interface of a Windows application is considered as important as the application’s power behind the scenes.

## Graphical User Interfaces

Have you ever tried to use a computer program and said to yourself “Okay, what do I do next?” or been unable to exit a program or perform some function that you knew the program was supposed to be able to do? The culprit was probably the interface. **The interface** is the front end of a program. It is the visual image you see when you run a program. The interface is what allows users to interact with your program. Although a program may be powerful and offer rich functionality, those functions may remain unused unless they present the user with easy methods of interaction. Often users of programs actually identify the interface as the program itself, when in reality, the interface is just one facet of the program.

The interfaces you designed thus far have not been graphical. Your program interaction was primarily limited to accepting input through the `ReadLine()` method and displaying output in the form of a single font at the DOS console window. In this chapter, the interface changes. Instead of interacting with the black console screen, you will design Windows-based, graphical user interface (GUI) applications. These types of applications are displayed on a Windows form, as shown in Figure 9-1.

![](img/36e48639a06772bcb0fa1ea2525b33a3_535_0.png)

**FIGURE 9-1** — Windows-based form

A **graphical user interface (GUI)** can include menus, buttons, pictures, and text in many different colors and sizes. Think of the form in Figure 9-1 as a container waiting to hold additional controls, such as buttons or labels. **Controls** are objects that can display and respond to user interaction. In Figure 9-1, the form has a title bar, complete with an icon on the left, a textual caption in the title bar, and the typical Windows Minimize, Maximize, and Close buttons. The C# code used to create this blank form is shown in Example 9-1.

### EXAMPLE 9.1

```csharp
// Windows0.cs                  Author: Doyle
// Demonstrates creating a blank container form
using System.Windows.Forms;                         // Line 1
namespace Windows0
{
    public class Form1 : Form                      // Line 2
    {
        public Form1()                              // Line 3
        {
            Text = "Simple Windows Application";   // Line 4
        }
        public static void Main()
        {
            Form1 winForm = new Form1();            // Line 5
            Application.Run(winForm);               // Line 6
        }
    }
}
```

The code in Example 9-1 could be written using an editor such as Notepad and executed from the command line. This is not recommended for developing Windows-based applications. The Visual Studio integrated development environment (IDE) automatically generates all the code needed for a blank Windows form for you. If you do not use the IDE, you lose out on the built-in, drag-and-drop construction capabilities and the ease of modifying controls during design. The program listing in Example 9-1 is much smaller than what is generated from Visual Studio. Later in the chapter, you will have a chance to compare Example 9-1 with the code Visual Studio actually generates. Before doing that and before exploring the rich Visual Studio environment, it is useful to evaluate what is actually required to create a Windows application in C#.

Examine the statements in Example 9-1. Notice that the using directive labeled Line 1 imports types or classes from the System.Windows.Forms namespace. This is where most of the classes for developing Windows-based applications are organized. By including this directive, you avoid having to fully qualify references to classes organized under the System.Windows.Forms namespace.

> **NOTE**
>
> The Windows applications you will be creating will always refer to the System.Windows.Forms namespace. Visual Studio automatically adds this reference when you select the C# **Windows Forms Application** template, and it makes available for you the data types or classes needed to create a Windows Application Project.

The class heading definition labeled Line 2 looks a little different from what you have seen previously. It includes not only the class name, but a colon followed by another class name. The second class is called the **base class**; the first is called the **derived class**. Look closely at this statement again.

```csharp
public class Form1 : Form                         // Line 2
```

The colon is used in the definition to indicate that the new class being defined, Form1, is derived from a base class named System.Windows.Forms.Form. The default name given for a Windows application class in Visual Studio is Form1. You do not have to change the class name, but you might want to so that the name better represents the application.

> **NOTE**
>
> Because the namespace System.Windows.Forms was included in the using directive, the fully qualified name of System.Windows.Forms.Form can be written as Form. You will find, however, that Visual Studio often inserts the fully qualified name when you look at the code generated by the IDE.

When a class is derived from another class, the new class inherits the functionality of the base class. Form is a predefined .NET class that includes a number of methods and properties used to create a basic Windows screen. Form1 inherits the characteristics of the Form class. You will learn more about inheritance in Chapter 11 when you study advanced object-oriented concepts. For now, think about inheritance as it relates to your family tree. Just as you can inherit traits from your father, such as hair color or height, Form1 inherits methods and properties from the predefined System.Windows.Forms.Form class. As you reexamine the form created for Figure 9-1 using Example 9-1, notice that it includes fully functional Close, Minimize, and Maximize buttons in the upper-right corner of the form. No new code had to be written to add these features. Form1 inherited this functionality from the Form class. Remember that one of the beauties of object-oriented programming is not having to reinvent the wheel. Inheriting characteristics from base classes adds functionality to your program without the burden of your having to do additional coding.

> **NOTE**
>
> Unlike your family tree, in which you inherit traits from two distinctively different individuals, your mother and your father, in C# and all .NET languages you are limited to single inheritance. Thus, you can not just add a second or third colon (e.g., on Line 2 in Example 9-1) and follow that with additional class names. You are limited to deriving from one base class. You will learn more about this in Chapter 11.
