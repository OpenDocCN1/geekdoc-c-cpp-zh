# 85. SELF-CONTAINED VS. FRAMEWORK-DEPENDENT DEPLOYMENT IN C#

C# applications can be deployed either by including everything they need (self-contained) or relying on a pre-installed .NET runtime (framework-dependent).

Here’s how to create both types of deployment using the .NET CLI.

[Code Example]

```
# Framework-dependent deployment
dotnet publish -c Release -r win-x64—self-contained false

# Self-contained deployment
dotnet publish -c Release -r win-x64—self-contained true
```

[Execution Result]

Creates a /publish folder with either a lightweight app (framework-dependent) or a complete, standalone app (self-contained).

Self-contained deployment means all the required .NET runtime and libraries are included in the published files. The app can run on a machine without .NET installed.

The downside: the output folder is larger because it includes the runtime.

Framework-dependent deployment assumes the target machine already has the correct .NET runtime installed. The output is smaller, but portability depends on external factors.