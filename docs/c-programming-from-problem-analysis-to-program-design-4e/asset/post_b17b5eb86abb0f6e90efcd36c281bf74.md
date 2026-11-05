
Looking again at Example 9-1, Line 3 begins the section of code defining the constructor for the Form1 class. Remember that a constructor has the same name as the class name—Form1. Constructors are called automatically when an object of the class is created. This constructor has one statement in its body, which is:

```csharp
Text = "Simple Windows Application";  // Line 4
```

Text is a property that can be used to set or get the caption of the title bar for the window. Observe that the string

```csharp
"Simple Windows Application"
```

appears on the title bar in Figure 9-1.

> **NOTE**
>
> You created your own property attributes using set and get when you defined your own classes. Windows forms and controls offer a wide variety of changeable properties including Text, Color, Font, Size, and Location. Much of the power of Visual Studio lies in having these properties readily available and easy to change or add through IntelliSense.

As with console-based applications, execution for Windows-based programs begins in the Main( ) method. In Example 9-1, Line 5, the first statement in the Main( ) method body instantiates or creates an object of the Form1 class. The object's identifier is winForm. The statement is listed again as follows:

```csharp
Form1 winForm = new Form1( );  // Line 5
```

The last statement in the body of Main( ), on Line 6, calls the Run( ) method. Run( ) is a class method of the Application class. The call is as follows:

```csharp
Application.Run(winForm);  // Line 6
```

The Application class is also defined as part of the System.Windows.Forms namespace. The object that is instantiated from the Form1 class is sent as the argument to its Run( ) method. It is this method call that causes the object, winForm, to be displayed as a window on your screen. This statement displays the form and places the application in a process loop so that it receives messages from the operating system when events of interest to the application are fired.

> **NOTE**
>
> Unlike instance methods, class methods, or static methods, are not called with an object. Class methods are not owned by any specific object. To call static methods, the method name is prefixed by the class name. Application is a class that has static methods (class methods) to start and stop applications. The Run( ) method starts an application; the Exit( ) method stops an application and closes all of its windows.

The amount of development time for Windows applications is greatly reduced when you use Visual Studio and C#. Because it is easy to add controls, sometimes beginning programmers get bogged down or carried away designing GUIs. Thus, before jumping into examining the different controls that can be added to the form, the next section presents some design issues that you should think about before dropping any control onto a form using Visual Studio.

## Elements of Good Design

As you start developing Windows applications, your goal should be to develop applications that are usable, that permit users to spot items in the windows quickly, and that enable users to interact with your program. Appearance matters! An attractively laid out screen with good visual organization gives users control. This is of utmost importance.

A large field of research in the field of computing is focused on **human-computer interaction (HCI)**. HCI concentrates on the design and implementation of interactive computing systems for human use. Explaining HCI fully is beyond the scope of this book, but it is a good topic for you to explore further, because it involves issues that you should consider and incorporate into your interfaces from the beginning. A few of the more important HCI considerations are presented in the following sections.

### Consistency

This is listed first because it is extremely important. Do you know how to close a Windows-based program? Sure you do. One way is to click the button labeled “X” in the upper-right corner of an active Windows application. The “X” performs the same functionality for all applications and is consistently located in that same place. Do you know which menu option to use to save your work? Again, you probably answered “Yes.” Save is almost always located on the File menu for all Windows-based applications. Consistent placement of items is important. Consistent sizing of items is important. Consistent appearance of items that are performing the same functionality is also important. These are good design features to mimic. Buttons that are providing the same functionality should be consistently located in the same general area, be sized consistently, and be designed to look consistent.

Unless you are trying to call attention to an item, keep the item the same as other items. To bring attention to an item, use contrast, make it look different, or place it in a different location; otherwise, you should be consistent with your design of graphical user interfaces.

### Alignment

Use alignment for grouping items. When you place controls on a form, place similar items together. They can be lined up to call attention to the fact that they belong together. Place similar items together and align them in the same column or same row. Use indentation to show subordination of items.

Use blank spaces to aid in grouping. Adding blank space between controls can make the difference between an attractively laid out GUI and one that is cluttered and difficult to use. Align controls with their identifying labels.

### Avoid Clutter

The Windows Form **class** is considered a container on which controls such as buttons, text, labels, text boxes, and pictures can be placed. As you are about to learn, it is easy to fill the window with controls. Pay attention to the amount of information being placed on the form. Do not crowd a form with too many controls. Buttons to be clicked should be large enough for easy use. Make sure text is readable. Use intuitive labels that are descriptive of the control they are identifying. Fonts should be large enough to be legible.

### Color

Think about your color combinations. Background colors and foreground text colors should contrast with each other. Avoid using bright colors (such as reds), especially for backgrounds; this can result in user eye fatigue. You can use color as an attention getter, but do not abuse it. Color can play a significant role in your design. A great deal of research has focused on how colors impact the GUI, and you will probably want to explore this topic further.

### Target Audience

You should begin thinking about the design of an interface in terms of who will be using it. Will the user be a child or an adult? Will they be a novice or an expert? Your target audience should be taken into consideration. Another consideration for the design of an application is where it will be displayed. C# is being used to design mobile applications for handheld devices. A GUI should be different if it is going to be displayed on a WAP (Wireless Application Protocol)-enabled device such as a tablet or a smart phone. You would want to place fewer controls and minimal graphics on such an application. The design of your interface for Windows applications that can be run on workstations equipped with large hard drives that hold graphical images should also differ from the design for Web applications that run on thin client systems over a browser. (A thin client is designed to be small because it works with a server designed to perform most of the data processing.) The amount of download overhead should be taken into consideration for a Web application. Thin client systems often do not have much computing power and can be limited in their storage capacity. You will explore Web applications in Chapter 15.

> **NOTE**
>
> In addition to templates for creating console and Windows applications, Visual Studio includes built-in design templates for creating applications for the Web and Smart devices like Windows Phones. In Chapter 15 you will develop both Web and smart device applications.

With every application that you design, you should always think about the design considerations discussed in this section. A number of useful Web sites are focused on human–computer interaction. At the time of writing this text, *www.habib.org* was one of the more exhaustive sites. It includes a number of software developer resources, such as an online bibliography, published HCI guidelines, plus links to a number of professional affiliations focusing on HCI and personal pages of designers sharing their design suggestions.

![](img/36e48639a06772bcb0fa1ea2525b33a3_540_0.png)
