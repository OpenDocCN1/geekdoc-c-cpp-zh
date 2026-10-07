# Chapter 10: Well-Formed Types

command-line parser class. Classes and sets of classes like these can be written once and reused from many different programs. As such, they need to be grouped together into an assembly a library or class library and written for the purposes of reuse rather than only within a single program.

To create a library rather than a console project, follow the same directions provided in Chapter 1, with one exception: For .NET CLI, use Class Library or classlib for the project.

Similarly, with Visual Studio 2022, from the File->New Project... menu item (Ctrl+Shift+N), use the Search box to find All Class Library templates, and then select Class Library—the Visual C# version, or use GeoCoordinates for the project name.

Next, place the source code from Listing class from Listing 10.4 into separate files for each struct and name the file after the struct name and build the project. Building the project will compile the C# code into an assembly—a GeoCoordinates.dll file—and place it into a subdirectory of .\bin\.

# Referencing a Library

Given the library, we need to reference it from a program. For example, for a new console program using the Program class from Listing 10.3, we need to add a reference to the GeoCoordinates.dll assembly, identifying where the library is located and embedding metadata that uniquely identifies the library into the program. There are several ways to do this. First, you can reference the library project file (*.csproj), identifying which project contains library source code and forming a dependency between the two projects. You can't compile the program referencing the library until the library is compiled. This dependency causes the library to compile (if it isn't compiled already) when the program compiles. In other words, reference the compiled library (*.dll) rather than the project. This makes sense when the library is compiled separately from the program, as by by team within your organization.

Third, you can reference a NuGet package, as described in the next section.