
```csharp
private int i;
private int i2;
private string s;
private string s2;
private bool b;
```

Fig.C#-1.14

As you can see in Fig.C#-1.14, typing *private* once replaces all the instances of *public* in each of the lines. Next, let's discuss the call hierarchy feature.

## Call Hierarchy of Methods

One of the most significant and helpful features added to Visual Studio 2010 is Call Hierarchy. This feature allows you to display the following:

- Calls made to and from a selected method, property, or constructor in the Code Editor window
- Implementations of an interface member
- Overrides of a virtual or abstract member

> **Note**
>
> You learn about interfaces and their implementations, abstract and virtual classes, and members in detail in Chapter 4, *Introducing Object-Oriented Programming Constructs*

You can access the Call Hierarchy window by selecting and then right-clicking a method, property, or constructor name in the Code Editor. You can then select the *View Call Hierarchy* option from the context menu that appears, as shown in Fig.C#-1.15:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_26_0.png)

Fig.C#-1.15

In our case, the Call Hierarchy window in the Code Editor displays the calls that have been made to and from the **PrintInfo()** method, as shown in Fig.C#-1.16:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_26_1.png)

Fig.C#-1.16

The Call Hierarchy feature enables you to navigate through the source code. It also helps understand the flow of code in an application.

Next, let's discuss the faster code generation feature in Visual Studio 2010.

## Facilitation of Faster Code Generation

In the Visual Studio 2010 IDE, Microsoft has introduced an interesting new feature called Faster Code Generation. You can understand this feature better through an example. Let's suppose that we have a class called Shapes in an application.

> **Note**
>
> *A class can be created in C# by using the class keyword. You can declare and then define variables, methods, and objects inside the class. You learn more about classes and how to create a class in C# in detail in Chapter 4, Introducing Object-Oriented Programming Constructs.*

Now, if you write a method or class name that you have not already defined in the application, an error is generated. In our case, we have written a class name Circle, which we have not defined. Fig.C#-1.17 shows a wavy red line that appears below the class name Circle, indicating an error:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_27_0.png)

Fig.C#-1.17 shows a squiggly line below the class name, Circle. Place the mouse pointer on the class name to display a down arrow below the name. Now, click the down arrow and select the Generate new type option from the drop-down list that appears, as shown in Fig.C#-1.18:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_27_1.png)

When you select the Generate new type option from the drop-down list, the Generate New Type dialog box appears, as shown in Fig.C#-1.19:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_28_0.png)

Fig.C#-1.19

Note that in Fig.C#-1.19, we have selected the Add to existing file radio button so that the Circle class can be created in the same application in which the Shapes class is defined. Fig.C#-1.20 shows the code that is generated for the Circle class:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_28_1.png)

Fig.C#-1.20

Next, let's learn about another new feature of Visual Studio 2010, that is, Consume-first mode of IntelliSense.

## The Consume-First Mode of IntelliSense

IntelliSense in Visual Studio 2010 provides two alternatives to complete a statement in the Code Editor window. These alternatives are the suggestion mode and the consume-first mode of IntelliSense. The suggestion mode feature of IntelliSense helps in automatically completing the text as you type in the Code Editor window. To enable the suggestion mode of IntelliSense, you can press the CTRL+ALT+Space keys in combination. The consume-first mode of IntelliSense, on the other hand, disables the suggestion mode, which stops IntelliSense from automatically completing the text as you type it. You can disable the suggestion mode of IntelliSense by pressing the CTRL+ALT+Space keys in combination. To enable the suggestion mode of IntelliSense, you can press the same keys again.

## Export or Import Breakpoints

Visual Studio 2010 allows you to export or import breakpoints. A breakpoint is a debugging tool that can be used to halt the execution of a .NET application. Breakpoints can be inserted on either a single line of code in a .NET application or on multiple lines of code. The export breakpoints feature allows you to export breakpoints to some other location, such as a different system, to debug a portion of a .NET application. After debugging, the breakpoints can be imported back to the application.

You can export or import breakpoints by using the Breakpoints window, which you can open by selecting Debug→Windows→Breakpoints from the menu bar, as shown in Fig.C#-1.21:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_29_0.png)

Fig.C#-1.21

This opens the Breakpoints window.

> **Tip**
>
> You can also open the Breakpoints window by using the CTRL+ALT+B keys in combination.

You can insert a breakpoint into a particular piece of code by right-clicking the code and selecting Breakpoint→Insert Breakpoint from the context menu. In Visual Studio 2010, once you have inserted a breakpoint in your application, you can send it to your colleagues along with a bug report. You can pass on breakpoint(s) to your colleagues by using the Export breakpoints button of the Breakpoints window. Breakpoints are exported as an XML file to a location of your choice, from where they can be later imported to a .NET application using the Import breakpoints button of the Breakpoints window, as shown in Fig.C#-1.22:

Export Breakpoints Import Breakpoints

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_29_1.png)

Fig.C#-1.22

This feature is useful when you need to send the breakpoints through electronic mail (e-mail) to another user or want to change all of the breakpoints at once with a text editor.

Now, before we show you how to install Visual Studio 2010 on your computer, let's first briefly describe the different editions of Visual Studio 2010.

## Editions of Visual Studio 2010

There are different editions of Visual Studio 2010 available in the market. Each edition has its own set of features to cater to different users. The following is a brief description of the different editions of Visual Studio 2010:

- **Visual Studio 2010 Ultimate edition:** Provides an integrated environment of tools and infrastructure for the server, which helps to simplify the entire application development process. This edition of Visual Studio 2010 helps produce meaningful business results by using productive, predictable, and customizable processes. It lets you target more platforms and technologies, such as cloud and parallel computing.
- **Visual Studio 2010 Premium edition:** Offers an environment that simplifies application development. This edition contains advanced tools to solve the most difficult problems. The advanced code analysis, testing, and debugging tools help individuals and teams to develop high-end applications in which there is a minimal chance of creating bugs.
- **Visual Studio 2010 Professional edition:** Simplifies the basic tasks of creating, debugging, and deploying applications. It enhances creativity with powerful design surfaces. This edition targets several platforms, such as Silverlight, SharePoint, and Cloud applications. The integrated support in Visual Studio for Test Driven Development (TDD) and new debugging tools ensures high quality solutions.

Now let's learn to install Visual Studio 2010 on your computer.

Let's perform the following steps to install Visual Studio 2010:

1. *Insert* the DVD-ROM of Visual Studio 2010 in the DVD-ROM drive of your computer. The **Microsoft Visual Studio 2010 Setup** wizard appears (Fig.C#-1.23).
2. *Click* the **Install Microsoft Visual Studio 2010** link, as shown in Fig.C#-1.23:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_31_0.png)

Fig.C#-1.23

A message box appears, which states that the setup is copying the resources required to install Visual Studio 2010 in a temp directory, as shown in Fig.C#-1.24:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_31_1.png)

Fig.C#-1.24
