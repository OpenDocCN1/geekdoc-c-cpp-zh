# 83. IMPROVE CODE QUALITY WITH ROSLYN ANALYZERS

C# developers can use code analyzers powered by Roslyn to automatically detect issues, enforce best practices, and maintain clean code.

The following example shows how to use a Roslyn analyzer to detect an unused variable, and how it appears in a development environment like Visual Studio.

[Code Example]

```
```csharp
// Example C# code that would trigger a Roslyn analyzer warning
using System;
class Program
{
static void Main()
{
int unusedVariable = 42; // This line will trigger a warning from analyzers
Console.WriteLine("Hello, world!");
}
}
```
```

[Execution Result]

A squiggly line appears under 'unusedVariable', and a warning like:
IDE0059: Unnecessary assignment of a value to 'unusedVariable'

Roslyn is the .NET Compiler Platform, which not only compiles code but also exposes powerful APIs to analyze and refactor code. Visual Studio uses Roslyn analyzers internally to give developers real-time feedback on coding issues.