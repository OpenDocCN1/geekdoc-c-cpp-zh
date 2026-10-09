Here's an example project file (in XML), created by dotnet version 6.0.100:

```
hello-universe-0/hello-universe-0.csproj
```xml
<Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>net6.0</TargetFramework>
        <RootNamespace>hello_universe_0</RootNamespace>
        <ImplicitUsings>enable</ImplicitUsings>
        <Nullable>enable</Nullable>
    </PropertyGroup>
</Project>
```
```

We ran the dotnet new command in the directory named hello-universe-0, and it used the name as a project name by default. Running this command also created a boilerplate C# code file, named "Program.cs":

```
hello-universe-0/Program.cs
```csharp
Console.WriteLine("Hello, World!");
```
```

> This example uses C# 10.0 and .NET 6. The prior versions, for example, C# 9.0/.NET 5, used different templates, e.g., without using the top-level statements and the implicit System namespace using. We will briefly discuss this in the next few lessons.

# 1.3.1. Explanation

The C# project file is used for various purposes. As we will see later, one of the most important roles of a C# project is to help manage the (third-party) library dependencies.