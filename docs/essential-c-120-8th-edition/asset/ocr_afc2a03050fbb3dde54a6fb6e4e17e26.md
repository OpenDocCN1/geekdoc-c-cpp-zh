Note that it isn't only console programs that can reference libraries and packages. In fact, any assembly can reference any other assembly. Frequently, one library will reference another library, creating a chain of dependencies.

# Referencing a Project or Library with Dotnet CLI

In Chapter 1, we discussed creating a console program. Doing so created a program that included a Main method—the entry point at which the program will begin executing. To add a reference to the newly created assembly, we continue where we left off with an additional command for adding a reference:

```
dotnet add .HelloWorld\HelloWorld.csproj package
\GeoCoordinates\Debug\netcoreapp2\GeoCoordinates.dll
```

Following the add argument is a file path for the compiled assembly referenced by the project.
Rather referencing the assembly, you can reference the project file. As already mentioned, this chains the projects together so that building the program will trigger the class library to compile if it hasn't compiled already. The advantage is as the program compiles, it will automatically locate the compiled class library assembly—whether it is in the debug or release directory, for example. The command for referencing a project file is as follows:

```
dotnet add .HelloWorld\HelloWorld.csproj reference
\GeoCoordinates\GeoCoordinates.csproj
```

If you have the source code for a class library and that source code changes frequently, consider referencing the class library using the class project file rather than the compiled assembly.
Upon completion of either the project or the compiled assembly reference, your project can compile with the Program class source code found in List 10.3.

# Referencing a Project or Library with Visual Studio 2022

In Chapter 1, we also discussed creating a console program with Visual Studio. This created a program that included a Main method. To add a reference to the GeoCoordinates assembly, click the Project->Add Reference... menu item.