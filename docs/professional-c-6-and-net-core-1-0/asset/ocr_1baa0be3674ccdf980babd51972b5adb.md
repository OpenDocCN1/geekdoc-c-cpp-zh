Thus, it is quite useful to be able to edit them all as one single unit in Visual Studio. Visual Studio enables this by regarding all the projects as forming one solution, and treating the solution as the unit that it reads in and allows you to work on.

Up until now, this chapter has been loosely talking about creating a console project. In fact, in the example you are working on, Visual Studio has actually created a solution for you—although this particular solution contains just one project. You can see this scenario reflected in the Solution Explorer (see Figure 17.9), which contains a tree structure that defines your solution.

![](bbox=[0.177, 0.259, 0.824, 0.707])

# Figure 17.9

In this case, the project contains your source file, Program.cs, as well as a project configuration file, project.json, which enables you to define project descriptions, versions, and dependencies. The Solution Explorer also indicates the NuGet packages and assemblies that your project references. You can see this by expanding the References folder in the Solution Explorer.

If you have not changed any of the default settings in Visual Studio, you will probably find the Solution Explorer in the top-right corner of your screen. If you cannot see it, just go to the View menu and select Solution Explorer.