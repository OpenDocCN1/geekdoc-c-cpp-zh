Here's a C# project file for this project:

```
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net6.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <Nullable>enable</Nullable>
  </PropertyGroup>
</Project>
```

This is essentially the same as the one scaffolded by the *dotnet* tool.

We can run the program as follows:

```
dotnet run
```

The output is the same as before:

```
Hello World!!!
```

# ### 1.4.2. Grammar

If you are new to the "modern C#", then the program may look a bit strange.

This example uses a (new-ish) syntax called the "expression-bodied method". When a method body includes one statement (or, more precisely, one expression or a "return" statement), we can do away with the method body block and just use an expression in lieu of the method body block.

It uses a syntax similar to a "Lambda expression", as we will see later in the book, using the "fat arrow" symbol (⇒). This sample code is equivalent to the following: