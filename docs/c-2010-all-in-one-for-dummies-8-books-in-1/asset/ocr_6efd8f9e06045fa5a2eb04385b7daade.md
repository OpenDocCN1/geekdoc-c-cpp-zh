# Dividing a Single Program into Multiple Assemblies 379

You certainly wouldn't want to rebuild all the instructions that make up a big system just because a programmer changed a single line. Visual Studio 2010 can rebuild the modified file in a multifile program and not stack all the files together.

For these reasons, the smart C# programmer divides a program into multiple .cs source files, which are compiled and built together into a single executable .exe file.

![](bbox=[0.116, 0.255, 0.193, 0.318])

A project file contains the instructions about which files should be used together and how they're compiled

You can combine project files to generate combinations of programs that depend on the user-defined classes. For example, you may want to write a program with its corresponding read program. That way, if one changes, the other is rebuilt automatically. One project would describe the write program while another describes the read program. A set of projects is known as a solution. (I could have the FileRead and FileWrite programs covered in Book III as a single combined solution, but I didn't.)

Visual C# programmers use the Visual Studio Explorer to combine multiple C# source files into projects within the Visual Studio 2008 environment. I describe Solution Explorer in Book IV.

![](bbox=[0.133, 0.545, 0.193, 0.608])

# Dividing a Single Program into Multiple Assemblies

In Studio, and in C#, Visual Basic .NET, and the other NET languages, one project equals one compiled module — otherwise known as an assembly in .NET.

The words module and assembly have somewhat different meanings, but only to advanced programmers. In this book, you can just execute the two terms.

![](bbox=[0.116, 0.646, 0.203, 0.715])

# Executable or library?

C# can produce two assembly types:

+   -Executable (. EXE): A program in its own right that contains a Main() method. You can double-click a .EXE file in Windows Explorer, for example, and cause it to run. This book is full of executables in the form of console applications. Executables often allow supporting code from libraries in other assemblies.