# Xcopy Deployment

One of the early goals of the .NET Framework was to simplify the deployment model for applications. This was known as the “xcopy deployment” vision, meaning one can just copy an application’s binaries to some folder and run the application from that location as is, without requiring any registration or so on. In the world of COM, there was a much higher burden on installing and running applications because components typically required registration in the Registry for the runtime to find them.

To illustrate matters, let’s create a new Visual Studio solution with two projects in it: a console application that will result in the application’s main executable (containing the UI) and a class library containing the logic of a calculator. The former refers to the latter, using the Add Reference dialog’s Projects tab. The result should look like Figure 25.22, highlighting the cross-project reference.

![](bbox=[0.08, 0.5, 0.42, 0.75])

FIGURE 25.22 A project referring to another project.

Feel free to add some Calculator type to the Calculator class library project and use it from the CalculatorUI console application project. Because the default namespace for both projects will differ, you must add a namespace import to refer to the class library’s Calculator class.

What matters more than the application assemblies’ logic is the organization of the application in terms of the different binary files, which we can inspect after compiling the whole solution. Figure 25.23 shows the bin\Debug output folder for a debug build of the CalculatorUI project. Ignoring the vshost executable, which is used for debugging purposes when pressing F5 in Visual Studio, and debug symbol files (.PDBs), there are two assemblies here. One is the CalculatorUI.exe file itself, and the other is the class library Calculator.dll assembly it referred to.