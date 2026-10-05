# How to open or close an existing project

To open a project, you can use the File→Open→Project/Solution command to display the dialog box shown in 1-7. From this dialog box, you can locate and open your C# projects. You can also open a recently used project using the File→Recent Projects command.

In case you're not familiar with this notation, File→Open→Project/Solution means to pull down the File menu from the menu bar, select the Open submenu, and select the Project/Solution command. Usually, you only need to pull down one menu and select a command. Sometimes, you need to go from a menu to one or more submenu and then to the command.

The Open Project dialog box in this figure shows both the solution file and the project file for a project. As this figure explains, a project can contain multiple files, including the for source code. A solution, on the other hand, is a container that holds one or more projects.

For the applications in this book, a solution contains just a simple project. In that case, there's not much distinction between a solution and a project. However, a solution can contain more than one project. This is often the case for large applications that are developed by teams of programmers.

With a multi-solution project, programmers can work independently on the projects that make up the solution. In fact, the projects don't even have to be written in the same language. For example, a solution can contain two projects, one in C#, the other in Visual Basic.

At this point, you might wonder whether you should open a project or a solution. In this figure, for example, FinancialCalculations.sln is a solution and FinancialCalculations.csproj is a C# project. In most cases, it doesn't matter whether you open the solution or the project. Either way, both the solution and the project files will be opened. When you use the File→Close Solution command, both the solution and the project files will be closed.

# Some possible menu variations

Curiously, some of the menus vary slightly based on the import and export settings that are the first time you run Visual Studio 2010. Don't be surprised if you find that you use the File→Open Project command to open a project on your system instead of the File→Open→Project/Solution command. In this book, we show the menu that you get when you use the Visual C# Development Settings, and we'll show you how to change your settings in the next chapter. Since these menu variations are trivial, though, you shouldn't have any trouble using menus even unless the ones on your system are slightly different than the ones we specify.