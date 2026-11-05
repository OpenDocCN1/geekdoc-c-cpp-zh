# 88. RAPID DEV CYCLES WITH DOTNET WATCH

The dotnet watch command automatically re-runs your project when you make changes to source files.

Use dotnet watch to continuously monitor your code and rerun your app instantly upon edits. Great for fast feedback loops.

[Code Example]

```
# Open a terminal in your project directory and run:
dotnet watch run
// Example: Program.cs
Console.WriteLine("This is the initial version.");
// After saving changes while dotnet watch is running:
Console.WriteLine("Code updated! dotnet watch reloaded the app.");
```

[Execution Result]

```
Terminal output:
dotnet watch □ started
watch : Started
This is the initial version.
watch : File changed: Program.cs
watch : Restarting
Code updated! dotnet watch reloaded the app.
```

dotnet watch is part of the .NET CLI toolset and works like a live observer of your project.