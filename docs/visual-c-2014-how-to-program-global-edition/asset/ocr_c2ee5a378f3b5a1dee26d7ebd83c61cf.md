# 116 Chapter 3 Introduction to C# App Programming

to display one with WithLine, so you know exactly which version of WriteLine you want to use, you can close the Parameter Info window by pressing the Esc key, or simply keep typing and ignore it. After you type your code, select File > Save All to save the project.

![](bbox=[0.142, 0.203, 0.857, 0.43])

Fig. 3.7 | Parameter Info window.

# 3.3.4 Compiling and Running the App

You're now ready compile and execute your app. Depending on the project's type, the compiler may compile the code into files with a .exe (executable) extension, .dll (dynamically linked library) extension or one of several others—you can find these files in project's subfolders on disk. These files are called assemblies and are the packaging units used for C# code. These assemblies contain the Microsoft Intermediate Language (MSIL: Section 1.9.2) code for the app.

To compile the app, select Build > Build Solution. If the app contains compile-time errors, this will compile your code and build it into an executable (named Welcome1.exe, in one of project's subdirectories). To execute it, press Ctrl + F5, which invokes the Main method (Fig. 3.1). If you attempt to run the app before building it, the IDE will build your app first, then run it only if there are no compilation errors. The statement in line 10 of Main displays Welcome to C# Programming!. Figure 3.8 shows the results of executing this app, displayed in a console (Command Prompt) window. Leave the app project open in Visual Studio: we will go back to it later in this section. [Note: The console window normally has a black background and white text. We reconfigured it to have a white background and black text for readability. If you would like to do this, right click anywhere in the Command Prompt tab of the dialog that appears.]

![](bbox=[0.142, 0.858, 0.857, 0.915])

Fig. 3.8 | Executing the app shown in Fig. 3.1.