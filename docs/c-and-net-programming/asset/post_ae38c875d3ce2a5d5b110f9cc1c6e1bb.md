
```
`<ProgressBar></ProgressBar>`
```

The Width and Height properties represent the width and the height of a ProgressBar. The Name property represents the name of the control, which is a unique identifier of a control. The Margin property tells the location of a ProgressBar on the parent control. The HorizontalAlignment and VerticalAlignment properties are used to set horizontal and vertical alignments.

### 20. WPF TreeView
A TreeView represents data in a hierarchical view in a parent-child relationship where a parent node can be expanded or collapsed. The left side bar of Windows Explorer is an example of a TreeView.

### 19.4 Various WPF Tools
While working in WPF below tools can be used,
- Microsoft Visual Studio
- Microsoft Visual Studio Express 2008
- Microsoft Expression Blend
- Microsoft Expression Design
- XAMLPad

### 19.5 Various WPF Assemblies and Namespaces
Below is the list of various WPF assemblies and namespaces,
- Primary Assemblies
  - PresentationCore
  - PresentationFramework
  - WindowsBase
- Namespaces
  - Windows

### 19.6 WPF Other Facilities
Apart from enhanced UI and data binding services WPF also provides below facilities,
- Provides the capability to setup generic host communication with two parties.
- Allows setting up service properties.
- Allows to make the settings in order to have a service in C# as well as a Java client.
- Allows creating standard HTTP SOAP web service with the help of WPF.
- Provides easy options to process business transactions.
- Supplies current data to various other services

### 19.7 WPF and XAML
- XAML is a new descriptive programming language developed by Microsoft to write user interfaces for next-generation managed applications. XAML is used to build user interfaces for Windows and Mobile applications that use Windows Presentation Foundation (WPF), UWP, and Xamarin Forms.
- The purpose of XAML is simple, to create user interfaces using a markup language that looks like XML. Most of the time, a designer is used to create the XAML but XAML can be manipulated manually as well.
- XAML uses the XML format for elements and attributes. Each element in XAML represents an object which is an instance of a type. The scope of a type (class, enumeration etc.) is defined by a namespace that physically resides in an assembly (DLL) of the .NET Framework library.
- Similar to XML, a XAML element syntax always starts with an open angle bracket (<) and ends with a close angle bracket (>). Each element tag also has a start tag and an end tag. For example, a Button object is represented by the <Button> object element. The following code snippet creates a Button object element.

```xml
<Button></Button>
```

Alternatively, a self-closing format can be used to close the tag.

```xml
<Button />
```

### 19.8 WPF and C#
- While XAML is used to build user interfaces in WPF, C# is used as the code-behind language in WPF. While Windows and their controls are created in XAML at design-time, they can also be created at runtime using C# language. C# is also used to write all events programming and business logic. All actions, events and rendering are done in the code behind C# code.

### 19.9 WPF Advantages
- 1. It's more compatible with current standards.
- 2. It is flexible, many things could be achieved without having to write or purchase new controls.
- 3. In WPF, UI elements are designed in XAML while behaviors can be implemented in procedural languages such as C# and VB.Net. So it is very easy to separate behavior from the designer code.
- 4. XAML (Extensible Application Markup Language) makes it easy to create and edit GUI, and allows the work to be split between a designer part (XAML) and a programming part (C#, VB.NET etc.). Graphical design tools can work on simple XML documents instead of parsing code.
- 5. WPF supports databinding, which allows to get a more clean separation of data and layout.
- 6. WPF makes use of hardware acceleration for drawing the GUI, for better performance.
- 7. WPF supports user interfaces framework for both windows applications and web applications (Silverlight/XBAP).
- 8. With XAML, the programmers can work in parallel with the designers. The separation between a GUI and its behavior can allow us to easily change the look of a control by using styles and templates.
- 9. Rich composition of controls - Controls in WPF are highly composable. Almost any type of controls can be defined as content of another. Put an image into a button to create an image button, or put a list of videos into a list box to choose a video file.

## Two Marks Questions with Answers

Q.1 What are the capabilities of WPF ?
Ans. :
- It has all the equivalent common user controls like buttons, checkboxes, sliders etc.
- It has all the capabilities of HTML and Flash.
- It supports fixed and flow format document.
- It provides the facility of data binding, animation and multimedia.

Q.2 What are resources in WPF ?
Ans. : In WPF, resources are used to provide a simple way to reuse commonly defined objects and values. They also facilitate you to set the properties of multiple controls at a time. For example, you can set the background property on several elements in a WPF application using a single resource.

Q.3 What is XAML ? What is the use of XAML ?
Ans. :
- XAML is a declarative XML based language. It facilitates you to define objects and properties in XML. Its documents are loaded by XAML parser.

XAML is used to describe the objects, properties and their relation in between them. It makes you able to create any type of objects i.e. graphical and non-graphical.

### Q.4 What are the different types of layout controls in WPF ?
Ans. : Following are the different types of layout controls :
- Grid
- DockPanel
- WrapPanel
- Canvas
- UniformGrid
- StackPanel

### Q.5 What is the difference between Dynamic Resource and Static Resource ?
Ans. :

| Sr. No. | Static Resource | Dynamic Resource |
|---|---|---|
| 1. | Static Resources evaluate the resource one time only. | Dynamic Resource evaluates the resources every time they are required. |
| 2. | Static Resource is light. | Dynamic Resource is heavy due to frequently evaluated. |

## Long Answered Questions
- Q.1 Explain WPF architecture. (Refer section 19.2)
- Q.2 Discuss various features of WPF. (Refer section 19.3)
- Q.3 What are namespaces provided in WPF ? (Refer section 19.5)
- Q.4 What are benefits of WPF ? (Refer section 19.9)
- Q.5 What are WPF assemblies ? (Refer section 19.5)

## Notes

## Unit - IV

## CHAPTER - 20

## WINDOW BASED APPLICATIONS

Syllabus : Window Based Applications.

| Section No. | Topic Name | Page No. |
|---|---|---|
| 20.1 | .NET Environment | 20 - 2 |
| 20.2 | C# Language Editor and Integrated Environment | 20 - 3 |
| 20.3 | Understanding the Design and Code Views | 20 - 12 |
| 20.4 | User Interface Elements and Control Class Hierarchy in C# | 20 - 16 |
| 20.5 | Programming with the Windows Controls | 20 - 21 |
| 20.6 | C# MDI Form | 20 - 59 |
| 20.7 | Dialog Box | 20 - 66 |
| 20.8 | Event Handling Basics | 20 - 68 |
|  | Two Marks Questions with Answers | 20 - 78 |
|  | Long Answered Questions | 20 - 81 |

## 20.1 .NET Environment

### Concept
- 1. Visual Studio is the Integrated Development Environment in which developers can work while creating programs in one of many languages, including C#, for the .NET Framework.
- 2. IDE can be used to create console as well as Graphical User Interface (GUI) applications along with Windows Forms or WPF (Windows Presentation Foundation) applications, web applications, and web services in both native code together with managed code for all platforms supported by Microsoft Windows, Windows Mobile, Windows CE, .NET Framework, .NET Compact Framework and Microsoft Silverlight.

### Explanation
- 3. IDE offers a set of tools that help to write and modify the code, and detect and correct errors in the programs.
- 4. Visual Studio supports various programming languages by means of language services, which allow the code editor and debugger to support most of the modern day programming languages, provided a language-specific service exists.
- 5. IDE includes a code editor that supports syntax highlighting and code completion using IntelliSense for variables, functions and methods, language constructs like loops and queries.
- 6. Microsoft Visual Studio IDE supports application development throughout the entire application lifecycle, from design to deployment. IDE has tools for writing code, designing interfaces, and also for getting a general overview of files or classes in the application.
- 7. Microsoft Visual Studio provides tools for development of various types of applications. These tool set includes Windows Forms Designer, WPF (Windows Presentation Foundation) Designer, Web development, Class designer, Data designer and Mapping designer.
- 8. **Microsoft Visual Studio is available in the following editions**
  - 1. **Visual Studio Express -** Visual Studio Express is a free edition with this edition one can build the app for Windows 8, Windows Phone, and the web. The languages available as part of the Express editions are :
    - Visual Basic Express
    - Visual C++ Express
