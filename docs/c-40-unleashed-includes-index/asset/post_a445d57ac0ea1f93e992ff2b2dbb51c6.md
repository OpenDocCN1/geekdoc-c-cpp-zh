
```csharp
Console.WriteLine();

if (selectedOperation == 0)
    break;

ICalculation operation = operations[selectedOperation - 1];
int a = ReadInt("a: ");
int b = ReadInt("b: ");
Console.WriteLine("Result = " + operation.Calculate(a, b));
Console.WriteLine();
Console.WriteLine();
}
}
```

Notice we’re printing all operations to the screen based on the type name of the class implementing the operation. There are various ways by which we could provide more customization of operation names (for example, by adding a get-only Name string property to our interface). Later on, we’ll see another way to associate this kind of descriptive metadata to an object, using custom attributes that are discovered through the reflection APIs, too.

In the preceding code, we’re using a small ReadInt helper function that reads an integer value from the console, retrying as long as the user doesn’t provide a valid input:

```csharp
static int ReadInt(string prompt)
{
    int result = 0;
    bool valid = false;
    while (!valid)
    {
        Console.Write(prompt);
        valid = int.TryParse(Console.ReadLine(), out result);
    }
    return result;
}
```

If we were to stick with built-in operations online, it would suffice to provide a list of built-in operation instances from GetOperations (for example, as follows using an iterator):

```csharp
static IEnumerable<ICalculation> GetOperations()
{
    yield return new Addition();
    yield return new Subtraction();
    yield return new Multiplication();
    yield return new Division();
    // You can add other built-in operations here easily...
}
```

Given this simple implementation, we already have a useful (admittedly simple) calculator, as shown in Figure 21.6.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1093_0.png)

FIGURE 21.6 Our extensible calculator without any extensions loaded.

## Discovery and Loading of Extensions

Besides the built-in extensions, we also want to be able to load all the extensions provided by third-party vendors. There are two contractual aspects to this: first, the requirement to implement our ICalculation interface, and second, the need to put extension assemblies in a place where the host application can find them (referred to as the “repository” in Figure 21.4). We’ll assume extensions live in an Extensions folder alongside the application executable.

Using reflection, we can now discover extension types in assemblies. There are two sides to this: We first need to find all the assemblies and load them. After we’ve done this, we then need to scan the assemblies for types implementing ICalculation and create an instance of those. We’ll assume a default constructor is required for extensions.

### DISCOVERY, SAFER AND SIMPLIFIED

This discovery process is of interest to us in the scope of this example because of its use of reflection for various operations. However, a few limitations and drawbacks apply when it’s implemented in the way shown here. For one thing, looking for assemblies simply by searching .dll files and trying to load them through the reflection APIs is a gross simplification of things. We might want to discover types not only based on a directory containing assemblies, but look elsewhere, too.

Second, loading those assemblies can fail for a variety of reasons. Maybe the .dll file is not an assembly but a native DLL or another kind of file that got disguised with a .dll extensions for some reason.

Finally, assemblies cannot be unloaded unless the containing application domain gets unloaded as a whole. Misbehaving assemblies or assemblies without any useful extension types will be loaded into the program’s memory.

Frameworks like System.Addins and the MEF help to avoid such issues.

```csharp
static IEnumerable<ICalculation> GetExtensions()
{
    if (Directory.Exists("Extensions"))
    {
        var icalc = typeof(ICalculation);

        foreach (var file in Directory.EnumerateFiles("Extensions", "*.dll"))
        {
            // For isolation, one will like to use AppDomains...
            var asm = Assembly.LoadFrom(file);

            // "LINQ to Reflection" to the rescue.
            var extTypes = from t in asm.GetTypes()
                           where t.GetInterfaces().Contains(icalc)
                           select t;

            foreach (var ext in extTypes)
                yield return (ICalculation)Activator.CreateInstance(ext);
        }
    }
}
```

In this piece of code, we find all .dll files in an Extension subfolder (relative to the working directory; that is, the place where the application's executable lives). After loading the files through Assembly.LoadFrom (also in the System.Reflection namespace), we use LINQ to filter the assembly's types by those that implement the ICalculation interface. To do so, we rely on the GetInterfaces method on System.Type.

Finally, after we've found all types that implement the ICalculation interface, we can instantiate each of them, using the Activator.CreateInstance method we've seen before. This assumes a default constructor is present.

Given the preceding method, we can now tweak the GetExtensions method to include both the discovered and the built-in operations (again using a LINQ operator):

```csharp
static IEnumerable<ICalculation> GetOperations()
{
    return GetBuiltinOperations().Concat(GetExtensions());
}

static IEnumerable<ICalculation> GetBuiltinOperations()
{
    // And seen earlier...
}
```

```csharp
static IEnumerable<ICalculation> GetExtensions()
{
    // As seen above...
}
```

## THOUGHTS ON CONSTRUCTORS AND STATE

The fact we're reusing the same instance of an operation type for all calculations that use it implies those types should be careful with state. If state from one use of the calculation object sticks around and can influence subsequent operations, you may be in trouble.

Alternatively, we could create new instances of the calculation objects each time we're going to reuse them. In such a configuration, you'll still want to discover the types only once but defer the instance creation calls until the point of every use.

This brings us to a further discussion about the implicit contract of requiring a specific constructor (which cannot be captured in an interface) on extensions. Because we're taking all discovery tasks on ourselves, to the point of finding types that adhere to a certain interface contract, we're responsible for creating the instances.

Alternatively, you could think of using an interface with a single member GetExtensions that every extension assembly needs to have for discovery purposes. But all we've done then is put more burden on the extension provider, and we still need to discover this hypothetical IExtensionProvider implementation, again with the need to invoke some constructor.

### Writing and Deploying an Extension

Development of an extension happens in a separate project, resulting in the creation of a separate assembly, and is usually created by a third party. The definition of such an extension should be self-explanatory, given our simple interface. For example:

```csharp
using Extensibility;
namespace Geometry
{
    public class Pythagoras : ICalculation
    {
        public int Calculate(int a, int b)
        {
            return (int)Math.Sqrt(a * a + b * b);
        }
    }
}
```

Now we need to put the resulting file, Geometry.dll, in the Extensions subfolder where the host application is looking to discover extensions. In a real-world scenario, some installer will be used to facilitate this task when deploying extensions to end-user machines, but

for demonstration (and development) purposes, we can simply copy it. The following folder structure is required:

ExtensiCalc
- ExtensiCalc.exe
- Extensions
- Geometry.dll

To simplify debugging of our own extensions, to be loaded by the host application, we can configure the build process in Visual Studio with a post-build step on the Geometry project. Figure 21.7 illustrates a configuration that will copy the built file to the appropriate location using some relative paths. Because we're building to the bin\Debug folder underneath the Geometry folder, we need to go three levels up so that we can take a right turn into the ExtensiCalc (host application) build folder. From here, we construct the path to the Extensions subfolder alongside the ExtensiCalc executable, again under bin\Debug (assuming you're building in Debug configuration). The $(TargetPath) variable is provided by MSBuild and contains the full path to the built assembly file. Such variables can be discovered by using the Edit Post-build button.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1096_0.png)

FIGURE 21.7 Configuration of a Post-build event to copy a built assembly file.

Finally, when we run the application now, we should see a Pythagoras entry appear in the operations menu, as shown in Figure 21.8.

## Managed Extensibility Framework

One of the frameworks that helps with creating extensible applications on the .NET platform is MEF. Although a thorough discussion about MEF is beyond the scope of this chapter, a short introduction is warranted, especially because .NET 4 is the first version of the framework to ship this new technology out of the box.
