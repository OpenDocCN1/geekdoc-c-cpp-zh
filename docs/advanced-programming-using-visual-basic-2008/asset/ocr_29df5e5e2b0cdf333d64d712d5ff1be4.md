11. Web development is done using ASP.NET.

12. The Visual Studio (VS) integrated development environment (IDE) is used to develop and debug projects. Two helpful features of the IDE are temporary projects, which don’t have to be saved, and profiles, which customize the IDE for a particular type of developer. This text uses the VB development profile.

13. The Options dialog box can be used to set the defaults for Option Explicit and Option Strict for all projects, default project file locations, and the grid in the Form Designer.

14. The My Project folder, which appears in the Solution Explorer, holds configuration files, including AssemblyInfo.vb. You can double-click on My Project to display the new Project Designer.

15. A compiled program becomes an .exe or .dll file in the bin\Debug folder of the project. The .resx file holds an XML representation of the resources for the form, including any graphics.

16. The VS IDE uses the partial classes feature to store a form class in two separate files. The programmer-written code is in a different file from the designer-written code.

17. The Project Designer can be used to set many options for the project, including the assembly information in AssemblyInfo.vb and the project resources.

18. You can deploy a Windows application by copying the .exe file to another location.

19. The My feature includes several objects that provide access to the application, resources, the user, and the user’s computer.

20. You can modify the application’s assembly information attributes in the Assembly Information dialog box or by editing the AssemblyInfo.vb file directly. To retrieve the attributes at run time, use the My.Application.Info object.

21. Toolbars and status bars improve the ease of operation for users. Menus are created with the MenuStrip and ContextMenuStrip components, a toolbar is created with a ToolStrip, and a status bar is created with a StatusStrip.

22. A form and each control have a ContextMenuStrip property, which you can set to a context menu that you create. Text controls have an automatic context menu with items for text editing.

23. An event handler can respond to events of multiple controls by adding the events to the Handles clause. Use this technique to use the same event handler for a menu item, context menu item, and toolbar button.

24. To display the date and/or time in a status bar, use the Now property of the DateTime structure. Typically, the date and time are set in the Form_Load event handler and in the Tick event handler for a Timer component, so that the time remains current.

25. When using multiple forms, the forms may be single document interface (SDI) or multiple document interface (MDI). An MDI application has parent and child forms. To create a parent, set a form’s IsMdiContainer property to true. A child form must be set in code by setting the form’s MdiParent property to the parent form.