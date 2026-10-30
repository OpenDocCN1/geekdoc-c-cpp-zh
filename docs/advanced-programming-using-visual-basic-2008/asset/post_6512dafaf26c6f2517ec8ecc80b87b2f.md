
## AboutBox

If you use the AboutBox template, you don’t have to write any code at all.

## SplashScreen

If you use the Splash Screen template, add one event handler to hold the form on the screen for a few seconds.

```vb
Private Sub SplashScreen1_FormClosing(ByVal sender As Object, _
    ByVal e As System.Windows.Forms.FormClosingEventArgs) _
    Handles Me.FormClosing
        ' Hold the form on the screen for about 5 seconds before closing.

        System.Threading.Thread.Sleep(5000)
End Sub
```

## Summary

- 1. The .NET Framework contains the class libraries, the common language runtime, and ASP.NET.
- 2. Managed code is compiled to run in the common language runtime (CLR).
- 3. A portable executable (PE) file contains intermediate language (managed code) and metadata.
- 4. Metadata store information about the methods, classes, and types for the runtime.
- 5. The .NET Framework is composed of a set of classes stored in the class library. The classes are organized into a hierarchy of namespaces.
- 6. The CLR treats value types and reference types differently. Each value type variable has the value stored in the variable’s memory location and is always initialized. A reference type variable holds a pointer to an actual object and may be equal to Nothing if not assigned.
- 7. The compiler produces MSIL (Microsoft intermediate language), a platform-independent set of instructions.
- 8. An assembly is the smallest deployable unit of code, which contains one or more .exe or .dll files and a manifest that describes the assembly.
- 9. The AssemblyInfo.vb file holds attributes, which are tags that contain information about the assembly.
- 10. A Reference object connects Visual Basic to external components, either assemblies or COM objects.
- 11. Web development is done using ASP.NET.
- 12. The Visual Studio (VS) integrated development environment (IDE) is used to develop and debug projects. Two helpful features of the IDE are temporary projects, which don’t have to be saved, and profiles, which customize the IDE for a particular type of developer. This text uses the VB development profile.
- 13. The Options dialog box can be used to set the defaults for Option Explicit and Option Strict for all projects, default project file locations, and the grid in the Form Designer.
- 14. The My Project folder, which appears in the Solution Explorer, holds configuration files, including AssemblyInfo.vb. You can double-click on My Project to display the new Project Designer.
- 15. A compiled program becomes an .exe or .dll file in the bin\Debug folder of the project. The .resx file holds an XML representation of the resources for the form, including any graphics.
- 16. The VS IDE uses the partial classes feature to store a form class in two separate files. The programmer-written code is in a different file from the designer-written code.
- 17. The Project Designer can be used to set many options for the project, including the assembly information in AssemblyInfo.vb and the project resources.
- 18. You can deploy a Windows application by copying the .exe file to another location.
- 19. The My feature includes several objects that provide access to the application, resources, the user, and the user’s computer.
- 20. You can modify the application’s assembly information attributes in the Assembly Information dialog box or by editing the AssemblyInfo.vb file directly. To retrieve the attributes at run time, use the My.Application.Info object.
- 21. Toolbars and status bars improve the ease of operation for users. Menus are created with the MenuStrip and ContextMenuStrip components, a toolbar is created with a ToolStrip, and a status bar is created with a StatusStrip.
- 22. A form and each control have a ContextMenuStrip property, which you can set to a context menu that you create. Text controls have an automatic context menu with items for text editing.
- 23. An event handler can respond to events of multiple controls by adding the events to the Handles clause. Use this technique to use the same event handler for a menu item, context menu item, and toolbar button.
- 24. To display the date and/or time in a status bar, use the Now property of the DateTime structure. Typically, the date and time are set in the Form_Load event handler and in the Tick event handler for a Timer component, so that the time remains current.
- 25. When using multiple forms, the forms may be single document interface (SDI) or multiple document interface (MDI). An MDI application has parent and child forms. To create a parent, set a form’s IsMdiContainer property to true. A child form must be set in code by setting the form’s MdiParent property to the parent form.
- 26. An MDI application generally has a Window menu that displays the open child windows and options for arranging the child windows. Designate the Window menu by setting the MDIWindowListItem property of the MenuStrip on the parent form.
- 27. A singleton design pattern is used to ensure that only one instance of a class can be created.
- 28. A splash screen displays as an application loads. You can create a splash screen by setting properties of a standard Windows Form or by using the Splash Screen template. Set the splash screen in the Project Designer.
- 29. Use the Sleep method of a Thread object in the splash screen's FormClosing event handler to hold the form on the screen long enough for the user to read it.
- 30. The VS IDE can automatically generate class diagrams, which show a visual representation of the classes in an application. You have many options for expanding, collapsing, rearranging, showing, and hiding elements in the class diagram.

## Key Terms

- Active Server Pages (ASP) 6
- assembly 5
- assembly information 14
- assembly manifest 5
- attributes 5
- child form 25
- class diagram 31
- common language runtime (CLR) 2
- Common Language Specification (CLS) 3
- ContextMenuStrip component 18
- DateTime structure 24
- design pattern 28
- IsMdiContainer property 26
- LayoutMdi method 27
- managed code 2
- managed data 2
- MdiParent property 26
- MenuStrip component 18
- metadata 2
- Microsoft intermediate language (MSIL) 4
- multiple document interface (MDI) 25
- My 13
- .NET Framework 2
- .NET Framework class library 2
- Now property 24
- parent form 25
- partial class 11
- partial type 11
- Project Designer 12
- reference object 5
- reference type 3
- single document interface (SDI) 25
- singleton pattern 28
- splash screen 29
- StatusStrip component 18
- thread 31
- Timer component 24
- ToolStrip component 18
- value type 3

## Review Questions

- 1. Differentiate between the .NET Framework and Visual Studio.
- 2. Explain the following
  - a. CLR
  - b. CLS
  - c. PE
  - d. MSIL
  - e. ASP.NET
- 3. Explain the relationship between the common language runtime and managed code.
- 4. What is the purpose of compiling to an intermediate language?
- 5. What is the difference between a value type and a reference type?
- 6. What is an assembly? What does an assembly contain?
- 7. What are attributes? Give three examples.
- 8. What is ASP.NET and what is its purpose?
- 9. Where can you find a project's compiled version? What else might you find in that same location?
- 10. What is the Project Designer? How is it displayed? How is it used?
- 11. How can you deploy Windows applications?
- 12. What is the VB My feature? Name at least one use for My.
- 13. Explain how to display the attributes in AssemblyInfo.vb on a form at run time.
- 14. What components does VS provide for creating menus, context menus, toolbars, and status bars?
- 15. Describe the steps necessary to make the current time appear in a status bar.
- 16. What is an MDI application? How many parent forms can be in a single MDI application?
- 17. What is a design pattern?
- 18. How is the singleton pattern implemented?
- 19. Explain how to create a splash screen, how to display it as the application loads, and how to hold it on the screen for several seconds.
- 20. What is a class diagram? How can you create and customize a class diagram using the VS IDE?

## Programming Exercises

> Note: If you prefer to write Windows Presentation Foundation (WPF) applications, rather than Windows applications, see "Windows Presentation Foundation (WPF)" in Chapter 13.

- 1.1 Create a Windows application that displays the company, title, and copyright information from the assembly information attributes. Make sure to modify the assembly information.
