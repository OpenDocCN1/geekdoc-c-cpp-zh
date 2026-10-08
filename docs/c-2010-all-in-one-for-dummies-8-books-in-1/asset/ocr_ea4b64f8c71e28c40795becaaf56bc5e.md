# Putting Your Classes into Class Libraries 383

After you have a class library project, you can add a driver project (or a unit test project or both) using the approach described in the next section.

![](bbox=[0.235, 0.196, 0.473, 0.276])

Figure 10-1:
A new library in Solution Explorer.

# # Adding a second project to an existing solution

If you have an existing solution — whether it’s an ongoing project or a class library project such as the one described in the previous section you can easily add a second project to your solution: either a class library project or an executable project, as a driver. Follow these steps:

+   1. After your existing solution is open in Visual Studio, right-click the solution node (the top node) in Solution Explorer.
2. From the pop-up menu, choose Add::New Project.
3. In the New Project dialog box, select the type of project you want to add.

Select a class library, a console application, a Windows Forms application, or another available type on the right side of the dialog box.

+   4. Use the Location box to navigate to the folder where you want the project.
The location you navigate depends on how you want to organize your solution. You can put the new project's folder in one of places:
* All-in-one-folder: Navigate into the main project folder, making the added project subfolder. (See Figure 10-2.)
* Side-by-side: Navigate to the folder that contains the main project folder so the two projects are at the same level. (See Figure 10-3.)

+   5. Name your project and click OK.
If the new project is a library project, choose its name carefully — it will become the name of the library’s .DLL file and the name of the namespace containing the project’s classes.