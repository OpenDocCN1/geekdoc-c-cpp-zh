them for use at runtime. However, when multiple versions of a component existed, they typically overwrote the binary/registrations, causing other programs to start using the new version. If the new version is not completely backward compatible, chances are high something breaks in other installed applications.

Early on in the design of .NET, it was determined that this problem had to be resolved. This called for a new naming and versioning story on the new units of deployment (that is, the assemblies). The first important change to the deployment story is the support for xcopy deployment, allowing (library) assemblies to sit alongside application assemblies, with no registration needed whatsoever. At the center of this feature lies the self-describing nature of assemblies, carrying all required metadata for type discovery with them.

To illustrate xcopy deployment in practice, let's create an application with an assembly on which it depends. You'll see how to declare such dependencies in a Visual Studio solution later, but for now we'll go with plain command-line compilation. First, we create the library consisting of the following C# code file:

```
```csharp
// Calc.cs
public static class Calc
{
    public static int Add(int a, int b)
    {
        return a + b;
    }
}
```
```

To compile the library into a .dll assembly, invoke the following command:

```
```bash
csc /t:library calc.cs
```
```

Given the new calc.dll file, we now create an application that depends on it. To do so, enter the following code in a new file:

```
```csharp
// Program.cs
class Program
{
    static void Main()
    {
        System.Console.WriteLine(Calc.Add(3, 4));
    }
}
```
```

To establish the dependency between both assemblies, the compiler needs an additional flag, as shown here. Notice that the default target type is exe, so we don't need a /t flag:

```
```bash
csc /r:calc.dll program.cs
```
```