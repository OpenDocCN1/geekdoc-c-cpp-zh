
![](img/3d365b72b289213a91ade7eb366b8f35_618_0.png)

Figure 17.14

## Managing References

Adding references with Visual Studio needs some special considerations because of differences with project types. In case you’re using the full framework—that is, .NET 4.6—adding references to assemblies from the .NET Framework is still an important task to do. It doesn’t matter if you are using one of the older templates such as WPF or a newer template such as Console Application (Package). Remember: With newer templates you can still target .NET 4.5.2 (or .NET 4.6) in addition to .NET Core 1.0.

The Reference Manager, shown in Figure 17.15, enables you to add references to assemblies that are part of the .NET Framework, and also add references to assemblies that you created with library projects.

![](img/3d365b72b289213a91ade7eb366b8f35_619_0.png)

Figure 17.15

Depending on the project types you’re adding references to, the Reference Manager gives different options. Figure 17.16 shows the Reference Manager opened from a WPF application. Here you can reference shared projects and COM objects, and you can also browse for assemblies.

![](img/3d365b72b289213a91ade7eb366b8f35_619_1.png)

Figure 17.16

When you’re creating Universal Windows Platform apps, you see a new feature with the Reference Manager, as shown in Figure 17.17. Here you can reference Universal Windows Extensions, for example API extensions available with Windows IoT or Windows Mobile.

Options dialog by selecting Tools → Options. In the Options dialog select the NuGet Package Manager → Package Sources in the tree view (see Figure 17.19). By default, Microsoft’s NuGet server is configured, but you can also configure other NuGet servers or your own. With .NET Core and ASP.NET Core 1.0, Microsoft offers feeds with NuGet packages that are updated on a daily basis.

![](img/3d365b72b289213a91ade7eb366b8f35_621_0.png)

Using the NuGet Package Manager, you can not only select the package source but you can also select a filter to see all packages that are installed, or where an upgrade is available, and search for packages on the server.

> NOTE With ASP.NET Core 1.0, JavaScript libraries are no longer used from NuGet server. Instead, JavaScript package managers, such as NPM and Bower, are directly supported from within Visual Studio 2015. This is discussed in Chapter 40.

The Visual Studio code editor is where most of your development work takes place. This editor increased in size in Visual Studio after the removal of some toolbars from the default configuration, and the removal of borders from the menus, toolbars, and tab headers. The following sections take a look at some of the most useful features of this editor.

One notable feature of Visual Studio is its use of a folding editor as its default code editor. Figure 17.20 shows the code for the console application that you generated earlier. Notice the little minus signs on the left-hand side of the window. These signs mark the points where the editor assumes that a new block of code (or documentation comment) begins. You can click these icons to close up the view of the corresponding block of code just as you would close a node in a tree control (see Figure 17.21).

![](img/3d365b72b289213a91ade7eb366b8f35_622_0.png)

Figure 17.20

![](img/3d365b72b289213a91ade7eb366b8f35_622_1.png)

Figure 17.21

This means that while you are editing you can focus on just the areas of code you want to look at, hiding the bits of code you are not interested in working with at that moment. If you do not like the way the editor has chosen to block off your code, you can indicate your own blocks of collapsible code with the C# preprocessor directives, #region and #endregion. For example, to collapse the code inside the Main method, you would add the code shown in Figure 17.22.

![](img/3d365b72b289213a91ade7eb366b8f35_623_0.png)

Figure 17.22

The code editor automatically detects the #region block and places a new minus sign by the #region directive, enabling you to close the region. Enclosing this code in a region enables the editor to close it (see Figure 17.23), marking the area with the comment you specified in the #region directive. The compiler, however, ignores the directives and compiles the Main method as normal.

![](img/3d365b72b289213a91ade7eb366b8f35_623_1.png)

Figure 17.23

## Navigating Within the Editor

On the top line of the editor are three combo boxes. The right combo box enables you to navigate between members of the type you’re in. The middle combo box enables you to navigate between types. The left combo box is new with Visual Studio 2015; it enables you to navigate between different applications or frameworks. For example, if you are working on the source code of a shared project, in the left combo box of the editor you can select one of the projects where the shared project is used to see the code that is active for the selected project. The code that is not compiled for the selected project is dimmed. You can create code segments for different platforms using C# preprocessor commands.

## IntelliSense

In addition to the folding editor feature, Visual Studio’s code editor also incorporates Microsoft’s popular IntelliSense capability, which not only saves you typing but also ensures that you use the correct parameters. IntelliSense remembers your preferred choices and starts with these initially instead of at the beginning of the sometimes rather lengthy lists that IntelliSense can now provide.

The code editor also performs some syntax checking on your code, underlining these errors with a short wavy line, even before you compile the code. Hovering the mouse pointer over the underlined text brings up a small box that contains a description of the error.

## CodeLens

One great new feature in Visual Studio 2013 was the CodeLens. With Visual Studio 2015, this feature is now available in the Professional edition.

Did you ever change a method and wonder, “Did I miss a method calling this?” Now it’s really easy to find callers. The number of references is directly shown in the editor (see Figure 17.24). When you click the references link, the CodeLens opens so you can see the code of the callers and navigate to them. You can also see the reference with another new feature, the Code Map. The Code Map is discussed later in the “Architecture Tools” section.

![](img/3d365b72b289213a91ade7eb366b8f35_624_0.png)

Figure 17.24

If the source code is checked into a source control system like Visual Studio Online using Git or TFS, you can also see the authors and changes made.

## Using Code Snippets

Great productivity features from the code editor are *code snippets*. Just by writing `cw<tab><tab>` in the editor, the editor creates a `Console.WriteLine();`. Visual Studio comes with many code snippets, including the following:—

- `do`, `for`, `forr`, `foreach`, and `while` for creating loops
- `equals` for an implementation of the `Equals` method
- `attribute` and `exception` for creating `Attribute`- and `Exception`-derived types

You can see all the code snippets available with the Code Snippets Manager (see Figure 17.25) by selecting Tools ⇒ Code Snippets Manager. You can also create custom snippets.

![](img/3d365b72b289213a91ade7eb366b8f35_625_0.png)

Figure 17.25

You can also use snippets for XAML code that are available at http://xamlsnippets.codeplex.com.

## Learning and Understanding Other Windows

In addition to the code editor and Solution Explorer, Visual Studio provides a number of other windows that enable you to view and/or manage your projects from different points of view.

> **NOTE** *The rest of this section describes several other windows. If any of these windows are not visible on your monitor, you can select them from the View menu. To show the design view and code editor, right-click the filename in Solution Explorer and select View Designer or View Code from the context menu, or select the item from the toolbar at the top of Solution Explorer. The design view and code editor share the same tabbed window.*

## Using the Design View Window

If you are designing a user interface application, such as a WPF application, or a Windows control library, you can use the Design View window. This window presents a visual overview of what your form will look like. You normally use the Design View window in conjunction with a window known as the *toolbox*. The toolbox contains a large number of .NET components that you can drag onto your program. Toolbox components vary according to project type. [Figure 17.26](#) shows the items displayed within a WPF application.
