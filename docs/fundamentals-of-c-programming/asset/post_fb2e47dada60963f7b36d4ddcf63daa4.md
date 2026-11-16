
## Appendices

## Appendix A

### Using Visual Studio 2015 to Develop C++ Programs

This appendix describes the task of C++ software development under Visual Studio:

- To begin creating a C++ program, you must first launch Visual Studio 2015 from the Windows start screen or other relevant shortcut. Figure A.1 shows the appropriate application tile to activate.

You soon should see a splash screen similar to the one shown in Figure A.2.

If you have never before used the Visual Studio application, you must wait a few moments while it configures the development environment for you. At this point you will indicate that Visual C++ is your preferred development language. You also may select a color scheme. The figures shown here reflect the _blue_ color scheme.

Figure A.3 shows what Visual Studio looks like when it is fully loaded and ready to use.

- After Visual Studio has started, you begin the process of developing a C++ program by creating a new project. As Figure A.4 shows, you can create a new project by following the menu sequence: _File_→_New_→_Project_

- In the dialog that results, shown on the right of Figure A.4, you should choose the project type to be _Visual C++_ in the left pane, and use _Win32 Console Application_ option in the center pane. In the name field near the bottom of the dialog, enter a name for the project; we will use the name _simple_. You may change the location to a different folder if you like, or even a different drive (such as a USB pen drive). In this example, we chose to not change the default location provided by Visual Studio.

- When you select _OK_ on the project creation dialog, a _Win32 Application Wizard_ as shown on the left of Figure A.5 appears. At this point, the instructions in the dialog say "Click **Finish** from any window to accept the current settings." **Do not select Finish**; instead, select _Next_ to continue. We have one more key step to complete so our project is set up correctly.

Figure A.1 Visual Studio application tile

![](img/e84ad11adb18201d71595b31ce6c9eff_770_0.png)

Figure A.2 Visual Studio Splashscreen

![](img/e84ad11adb18201d71595b31ce6c9eff_771_0.png)

Figure A.3 Visual Studio Ready for Use

![](img/e84ad11adb18201d71595b31ce6c9eff_771_1.png)

Figure A.4 Creating a New Project

![](img/e84ad11adb18201d71595b31ce6c9eff_772_0.png)

Figure A.5 Configuring the New Project

![](img/e84ad11adb18201d71595b31ce6c9eff_772_1.png)

- In the subsequent Applications Settings dialog (see the right image in Figure A.5), select the Empty project checkbox. The dialog should look like the right image in Figure A.5 before you proceed. Choose Finish when you are ready to continue.

- At this point, the Solution Explorer panel shows the structure of the newly created, albeit empty, project. The left image in Figure A.6 shows the newly populated Solution Explorer pane.

- Right click on the simple element in the Solution Explorer. As shown on the right in Figure A.6, select Add and New Item from the resulting pop-up menu.

- In the Add New Item dialog box, shown on the left in Figure A.7, select C++ File (.cpp) and enter a name for the C++ file in the text field at the bottom. You need not add .cpp to the end of the name, as Visual Studio will do that for you. The file here will be named simple.cpp. Press Add when done.

- As shown on the right in Figure A.7, the Solution Explorer pane now shows the file simple.cpp, and the large editor pane is ready for you to type in the source code for the program. The new source file is initially empty.

- In the editor pane with the simple.cpp tab at the top, type in the source code for our simple C++ program. Figure A.8 shows the completed code.

- You may save the source file at this point by selecting Save from the File menu or by pressing at the same time the Ctrl S keys. If you do not save your program, Visual Studio will prompt you to do so before it builds and runs your program.

- To run the program, select Debug->Start Without Debugging, as shown on the left of Figure A.9. (You also may use the Ctrl F5 key sequence to build and run the program.) Visual Studio will attempt to build the executable program. It will prompt you to save your file if you have not saved it or have made changes since the last time you saved it. The progress of the build process is displayed in the Output panel in the bottom window. One of the lines has

```
1>Compiling . . .
```

and another later has

```
1>Linking . . .
```

The last few lines are very important:

```
1>Build succeeded.
1>
1>Time Elapsed 00:00:02.98
========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ============
```

These lines indicate the build was successful.

- A console window appears with the output of your program. The right image in Figure A.9 shows this text window. You can press any key on the keyboard to close the window. If the console window does not appear, you have typographical errors in your program; return to the editor, fix the errors, and try to run the program again.

Figure A.6 Adding a C++ Source File

![](img/e84ad11adb18201d71595b31ce6c9eff_773_0.png)

Figure A.7 Ready to Edit the C++ Source File

![](img/e84ad11adb18201d71595b31ce6c9eff_773_1.png)

Figure A.8 Editor Pane

![](img/e84ad11adb18201d71595b31ce6c9eff_774_0.png)

Figure A.9 Building and Running the Program

![](img/e84ad11adb18201d71595b31ce6c9eff_774_1.png)

- When you finished with Visual Studio, select the File->Exit menu items as shown in Figure A.10.

These are the steps for writing a basic C++ program in Visual Studio 2015. While the steps initially may seem complex and tedious, they will become natural after you have written a few C++ programs.

When the program was run, the Visual Studio environment created a console window in which to run the program.

```
This is a simple C++ program:
Press any key to continue . . .
```

The first line of the output was printed by the program. The second line prompting the user to press any key to continue is added by the Visual C++ run-time environment so the console window stays visible long enough for the user to see the output. If you run the program from the standard Windows command shell (CMD.EXE, usually found in the Start menu under Accessories and named Command Prompt), only the program's output will appear and the "Press any key to continue . . ." message will not appear.

The following summarizes the steps you should follow when writing a C++ program using the Visual Studio IDE:

- In the main menu:
  - File->New->Project (or Ctrl Shift N)

- Select "Win32 Console Project" and click "Next" to set the "Empty Project" option

Figure A.10 Exiting Visual Studio

![](img/e84ad11adb18201d71595b31ce6c9eff_775_0.png)

- In the Solution Explorer pane right click on “Source Files” and select Add->New Item.

- Select C++ File (.cpp) and enter the name of your file

- Type in the source code for your program in the editor panel

- Save your file: File->Save filename (or Ctrl S)

- In the main menu: Debug->Start Without Debugging (or Ctrl F5)

It is possible to develop C++ programs without using Visual Studio’s integrated development environment. Visual Studio comes with some additional tools for command-line development. Appendix B describes how you can edit the C++ source code with a standalone text editor and compile and run the program from the Windows command prompt (CMD.EXE). Command-line development under Linux and macOS is covered in B. Some programmers prefer the freedom of using their favorite editor, a standalone compiler, and scripts to automate the build process.

## Appendix B

### Command Line Development

An integrated development environment (IDE) like Visual Studio combines all the tools a developer needs into one comprehensive application. While this approach works well for most programmers, some developers prefer a less centralized approach, using instead command line tools to manage the development process. Command line tools are focused and fast, and each tool itself is fairly simple compared to a full-featured IDE. A developer may prefer a different editor to one provided by the IDE. Developers can build scripts around command line tools to automate the building and testing process.

There are a few commands that are essential for working within the command-line environment. These center around manipulating and using files and folders. Our discussion assumes the Windows CMD.EXE shell, and we will note differences with macOS and Linux as needed. Linux and macOS are both Unix-like operating systems.

When you run CMD.EXE in Windows, the Terminal application on a Mac, or a bash terminal in Linux, the operating system presents a text-based console window. You type commands into this window and receive text feedback. Most of the commands are programs that you launch by typing their name. The following lists common commands useful for using the command-line.

- dir

When the command line interface starts it locates you in a particular folder, or directory, in the file system managed by the operating system. Your location is known as the current working directory. The command dir prints a list of the files in your current working directory. On Unix-like machine the ls -l command performs similar work. The command dir /w displays a wide listing of the files with fewer details; the ls command is the equivalent on Unix-like systems.

- mkdir name

Creates a new subdirectory (subfolder) named name in the current directory. Subdirectories allow you to better organize your files.

- cd name

Changes your current directory to be that specified by name. Some examples of its use include

- cd Code

Changes the current working directory to be the subdirectory named Code. Here the name is relative to the current directory. It is an error to provide a name that does not correspond to a subdirectory of the current directory.
