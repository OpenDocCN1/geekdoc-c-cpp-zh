color-coding keywords. It also performs some syntax checks as you type, and it underlines code that causes compilation errors, also known as design-time debugging. In addition, it features IntelliSense, which automatically displays the names of classes, fields, or methods as you begin to type them. As you start typing parameters to methods, it will show you the parameter lists for the available overloads. Figure 16-1 shows the IntelliSense feature in action with one of the .NET base classes, ListBox.

![](bbox=[0.1, 0.26, 0.8, 0.68])

FIGURE 16-1

> By pressing Ctrl+Space, you can bring back the IntelliSense list box if you need it or if for any reason it is not visible.

+   - Design view editor — This editor enables you to place user-interface and data-access controls in your project; Visual Studio automatically adds the necessary C# code to your source files to instantiate these controls in your project. (This is possible because all .NET controls are instances of particular base classes.)
+   - Supporting windows — These windows allow you to view and modify aspects of your project, such as the classes in your source code, as well as the available properties (and their startup values) for Windows Forms and Web Forms classes. You can also use these windows to specify compilation options, such as which assemblies your code needs to reference.
+   - The ability to compile from within the environment — Instead of needing to run the C# compiler from the command line, you can simply select a menu option to compile the project, and Visual Studio will call the compiler for you and pass all the relevant command-line parameters to the compiler, detailing such things as which assemblies to reference and what type of assembly you want to be emitted (executable or library .dll, for example). If you want, it can also run the compiled executable