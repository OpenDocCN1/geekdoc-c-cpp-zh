# USING COMMAND LINE TO CREATE DLL FILES (OPTIONAL)

To create DLL files from the Visual Studio command prompt (not the normal command prompt). With Visual Studio 2012, you get to it from **Start, All Programs, Microsoft Visual Studio 2012, Visual Studio Tools, Developer Command Prompt for VS2012**. At the command prompt, you would type the following command:

```
```text
csc /target:library /out:Person.dll Person.cs
csc /target:library /out:Student.dll Student.cs
```
```

> **NOTE**
> 
> When you type this command, you must either be in the directory that contains the .cs files or prefix the source code filename with the full path to the location of the files.

If you want to include both the Person class and the Student class in one DLL, you would type:

```
```text
csc /target:library /out:Student.dll Student.cs Person.cs
```
```

The /target:library compiler option tells the compiler to output a DLL instead of an EXE file. The /out: compiler option followed by a filename is used to specify the name for the new DLL file. You can omit the /out: option, and the DLL takes on the name of the first file listed. For this example, omitting /out:Student.dll would still create a Student.dll file because Student.cs is listed first.

# USING VISUAL STUDIO TO CREATE DLL FILES

A second option to creating a DLL file, and the one you will find more appealing, is to do everything within Visual Studio. When you first start a new solution or a new project, one of the options is to create a class library using the **Class Library** template, as shown in Figure 11-6.