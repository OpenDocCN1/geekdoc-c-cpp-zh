
the program asks the computer to do something it is unable to do, like accessing a file with an invalid path or dividing a number by zero.

The process of identifying errors (bugs) is called **debugging**. Testing programs to identify and eliminate errors is an extremely important part of developing software.

## Review Questions

- 1.1 Consider Google as a software system. What would be the input, process and output for Google?
- 1.2 Consider a software system that enrolls students into classes. Identify some key inputs that the system needs every time a student enrolls in a class, and the subtasks (process) that need to be performed. What are some outputs the system should produce for students and instructors?
- 1.3 List the major steps in developing a program.
- 1.4 Incorrect punctuation in a program is an example of what type of error?
- 1.5 A payroll program uses the wrong formula to compute overtime pay. What type of error is it?
- 1.6 True or false: A program that doesn’t have any syntax errors should produce the correct results.

## 1.2 Introduction to Visual Studio

In this section, you will learn how to use Visual Studio (VS) to create the user interface and write C# programs. Visual Studio is an integrated development environment (IDE) for developing applications in a variety of languages, including C#, Visual Basic, C++, Python and HTML/JavaScript. VS supports development of desktop and web applications for Windows, Android and iOS. A major strength of Visual Studio is that it provides a user-friendly environment for developing applications.

### Installing Visual Studio

You may download Visual Studio Community 2015 from the following website:

https://www.visualstudio.com/downloads/download-visual-studio-vs

To install Visual Studio, *open* the downloaded **vs_community.exe** file. The installation software will guide you through the process. The first time you start Visual Studio, you will be asked to choose the *Development Settings* and a *Color Theme*. Choose *Visual C#* for settings. You may change these settings later, as described in Tutorial 1.

### Components of Visual Studio

Though you have the choice to write programs in a variety of languages, the CPU can understand only **Machine Language**, which is extremely difficult for humans to understand. Machine Language requires detailed instructions that consist of patterns of bits (0 and 1), like 10001010, and are dependent on the machine (the specific type of computer). Because of the need to write detailed machine-dependent instructions, Machine Language is called a **low-level language**.

Running a program, as described earlier, consists of (1) the compiler translating the source code (the project) into Microsoft Intermediate Language Assembly and (2) the Common Language Runtime translating the assemblies from Intermediate Language to Machine Language and executing the program to produce the output.

Next, we will look at how to work with Visual Studio to develop C# programs.

## Review Questions

- 1.7 What is the only programming language that the CPU can understand?
- 1.8 What is a compiler?
- 1.9 What is an interpreter?
- 1.10 What is Microsoft Intermediate Language Assembly?
- 1.11 What is the function of Common Language Runtime in Visual Studio?

## Creating an Application in Visual Studio

To become familiar with the Visual Studio environment, let’s create an application for an ice cream parlor, consisting of a simple Windows form to compute and display the cost for an order of ice cream. We will follow the five steps identified earlier to develop it:

### 1. Define the purpose

Purpose: Compute and display the total cost for an order of ice cream
Input: Unit price, number of scoops
Process: Compute total cost
Total cost: unit price * number of scoops
Output: Total cost

### 2. Design and develop the Graphical User Interface (GUI)

Figure 1-4 presents the design of the form that shows the user interface to let the user enter the number of scoops and unit price to display the cost. You will create the form in Tutorial 1.

Figure 1-4: Windows form to compute ice cream cost

![](img/143bad48262566137acc9c41f668a88f_22_0.png)

## 1.3 Visual Studio Environment

This section introduces the various windows and the environment within Visual Studio.

Figure 1-7 shows the default form named Form1 in the Designer window, the Toolbox on the left, and the Solution Explorer window and the Properties window on the right.

The appearance of the form will vary with the version of Visual Studio and Windows you use. For example, the title of the form is centered in Windows 8 and 10, whereas it is left justified in Windows 7.

The Designer window allows you to create the user interface by adding controls to a form.

The Toolbox contains the components to build the user interface. The items within the Toolbox (e.g., ComboBox, TextBox and Label) are called controls.

The Solution Explorer window shows the name of the Solution, which is a container of projects; the name of the project (or projects, if there are multiple projects); and the names of the files within each project. If the name of the Solution is not displayed, select

Tools, Options, Projects and Solutions, General and check Always Show Solution

The Properties window displays and lets you set the properties of the currently selected object in the Designer window. For example, the Name field in the Properties window shows that the current name of the form is Form1.

Select Visual C# from Templates, Other Languages. For the type of application, select Windows Forms Application, as shown in Figure 1-6.

For Name, enter Ch1_IntroProgramming.

Select the Location, if different from the default folder.

Leave the CheckBox for Create directory for solution unchecked so that both the Project and the Solution will be created in the same folder. (If there are multiple Projects within a Solution, it would be better to have separate directories for the Solution and Projects.) Note that the default name for the Solution is the same as that of the Project.) Click OK.

The Visual Studio development environment appears, as shown in Figure 1-7.

## Figure 1-7: Visual Studio environment

![](img/143bad48262566137acc9c41f668a88f_26_0.png)

A brief description of each property is displayed at the bottom of the properties window when you click on the property, as shown in Figure 1-8. Make sure you expand the description area to make the description visible. If the description is not displayed, right click the property and check Description.

## Figure 1-8: Description of properties

![](img/143bad48262566137acc9c41f668a88f_26_1.png)

### Displaying a closed window

If any window is not displayed, select View from the menu, and select the corresponding window.

## Figure 1-11: Solution Explorer with autohide on

![](img/143bad48262566137acc9c41f668a88f_28_0.png)

To turn autohide off, click on the tab and click the pushpin.

### Menu and toolbar items

The menu and toolbar, shown in Figure 1-12, provide access to an extensive set of functions.

## Figure 1-12: Menu and toolbar

![](img/143bad48262566137acc9c41f668a88f_28_1.png)

The function of each toolbar item is displayed in a ToolTip box when you hover the mouse pointer over the item. For a general understanding of the functions, you may view the descriptions of the Toolbar items by displaying the Tooltips. You will become more familiar with them through the projects in this book.

### Adding and deleting forms

You may add a form to the project as follows:

- Select: Project, Add Windows Form. You will see the Add New Item window.
- Make sure Visual C# Items and Windows Forms are selected.
- Type in a name for the form. Click Add.

To delete a form,

- Right click the name of the file (.cs) in the Solutions window, and select Delete.

Deleting a file deletes the form and all files associated with the form permanently.

### Excluding a form from the project

You may exclude a form from the Solution Explorer but still keep the files associated with the form, in the project folder, as follows:

- Right click the file name (.cs) in the Solution Explorer, and select Exclude from Project.
