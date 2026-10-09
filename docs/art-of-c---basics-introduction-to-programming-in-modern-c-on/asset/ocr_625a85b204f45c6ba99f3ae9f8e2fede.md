# 1.3. Code Reading - A New C# Project

Another use of the projects is to set the global settings across the different C# source code files and the build outputs, etc. For example, for this "hello-universe-0" project, the output is set to "Exe", indicating that the project is to produce an executable program, or an "application".

```
<OutputType>Exe</OutputType>
```

Its target is set to "net6.0" (because we used the version 6 of *dotnet*). That is, we are targeting the .NET 6 runtime.

```
<TargetFramework>net6.0</TargetFramework>
```

*net6.0* is a cross-platform target that provides, and uses, the common denominator of all the APIs. For any previous version of the .NET, for example for 5.0, you can set the target framework to the appropriate version, e.g., `net5.0`. If we set the target to, for instance, `net6.0-windows`, then we could additionally use certain Windows APIs (like for GUI programming), but our program may not run on other platforms like Linux or Mac.

As mentioned, the "implicit global using" setting is an *opt-in* feature. This is most likely due to the backward compatibility concerns. You can enable it in the project files as follows.

```
<ImplicitUsings>enable</ImplicitUsings>
```

This is enabled by default if you scaffold your app using the *dotnet* CLI or the Visual Studio project wizard. If you are starting a new project, then there is no reason not to use this feature. Virtually every programming language has some similar support except, maybe, C and C++. It reduces a lot of redundant boilerplate code.

If you set the `ImplicitUsings` flag to `enable`, then the following system namespaces are automatically, and "globally", imported.