# 4.5.2  Using Visual Studio (Windows)

As mentioned previously, Visual Studio supports both GUI and CUI modes of operation. Key in your program using the built-in editor of Visual Studio or Windows Notepad, and save the file as **first_prog.c**. The sequence of steps for each of these modes is explained next.

**GUI Mode**  The *Build* menu in the Menu bar has all the necessary options for compilation and execution. In this mode, you need to invoke the compile and link phases separately:

+   - *Preprocess and Compile*  Use *Build > Compile first_prog.c* and observe the window pane at the bottom. If you see compilation errors, note their line numbers, edit the source file and repeat the compilation. You may ignore the warnings for the time being. On successful compilation, you should see the message `first_prog.obj - 0 error(s)`, signifying that the object file, **first_proj.obj**, has been created. This file contains machine code but is not ready to run because it contains unresolved references (3.15).
+   - *Link*  Linking is done with *Build > Build first_prog.exe*, when you should see the message `first_prog.exe - 0 error(s)`. The executable, **first_prog.exe** has been created.

![](bbox=[0.084, 0.43, 0.911, 0.907])

**FIGURE 4.2**  Visual Studio: Compiling and Executing a Program