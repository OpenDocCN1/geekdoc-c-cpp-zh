files, and seeing what the other team sees. It is good practice to use a source control in order to check-ins, and avoid editing the same physical file. Subversion or Team Foundation Server work great — Foundation Server is even integrated into Blend with source control.

Even if there is only one person working on a project, both Visual Studio and Blend offer to easily switch to the other tool, and continue working there. For example, right-clicking an XAML file in the Solution of Visual Studio offers to open the XAML (the entire solution) in Blend — and similarly, Blend can open the project in Visual Studio, as shown in Figure 8-46. If a project is already present in the other tool, switching between the two tools with Alt+Tab prompts for the changes.

# Blendability

Even Blend can use the same project as Visual Studio, it does not automatically mean that the project is editable in Blend. There may be a control or data object that accesses the server for some data in its constructor. Because the server may not be available in design time, property accesses and bindings are run when initializing the visual designer, this will result in an error, even if running the projects work perfectly. Blend and Visual Studio 2010 display useful error information in this case, as shown in Figure 8-47 and 8-48.

![](bbox=[0.557, 0.108, 0.86, 0.417])

FIGURE 8-46: Right-clicking on a file in Blend offers to open the solution in Visual Studio

> Exception thrown on 'BrokenUserControl': Cannot create an instance of 'BrokenUserControl'. Click here to hide detail.

An unhandled exception has occurred
Something wrong has happened

at Designer.Demo.BrokenUserControl.Initialize(c:\users\demo\documents\visual studio\2010\Projects\...)
at Designer.Demo.BrokenUserControl.Initialize(line 20)
Click here for debugging common load failures

![](bbox=[0.095, 0.768, 0.518, 0.863])

FIGURE 8-47: Design time error in Visual Studio