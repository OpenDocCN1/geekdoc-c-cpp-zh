# 12 Chapter 1: Introducing C#

programs, as this one. (On Windows, an .exe file is also created.) By default, the compiled output for a .NET application is placed into a subdirectory according to the TargetFramework identified in the project file, as shown in Listing 1.2 (/bin/Debug/net7.0/). The Debug directory is used because the default configuration is debug. This configuration allows the output to be optimized for debugging rather than for performance. The compiled output does not execute on its own. Rather, it needs the CLI to host the code. For .NET applications, this requires using the dotnet (dotnet on Linux and Mac) process as a host for the application. Hence why the program is executed with the dotnet run command. That said, there is a way to generate a stand-alone executable that includes the necessary runtime files so installing the dotnet runtime is not required—see the "Advanced Topic: Publishing a Stand-Alone Executable" (On Windows, the .exe file can be used directly, if the dotnet runtime is installed, rather than using dotnet run.)

# Essential C# Source Code

Both the source code and the manuscript text are available at https://essentialcsharp.com. Alternatively, the source code for this is available for download on GitHub directly at https://github.com/IntelliTest/EssentialCsharp. Instructions for compiling and running the code are available in the README.md file at the same location.

An alternative approach is to paste the source code into the HelloWorld program created earlier in the chapter and execute the source code.

# C# Syntax Fundamentals

Once you successfully compile and run the HelloWorld program, you are ready to start dissecting the code to learn its individual parts. Of course, Listing 1.1 is the simplest of C# programs with a single statement.

# Statements and Statement Delimiters

The single statement is Console.WriteLine(), which is used to write a line of text to the console. C# generally uses a semicolon to indicate the end of a statement,