In the entry method Main of the console application, a new instance of the Program class is created, and then the Bootstrapper method is invoked. In the Bootstrapper method, a ContainerConfiguration is created. With the ContainerConfiguration, a fluent API can be used to configure this object. The method WithPart<Calculator> finds the exports of the Calculator class to have it available from the composition host. The CompositionHost instance is created using the CreateContainer method of the ContainerConfiguration (code file AttributeBasedSample/SimpleHost/Program.cs):

```
public static void Main()
{
    var p = new Program();
    p.Bootstrapper();
    p.Run();
}

public void Bootstrapper()
{
    var configuration = new ContainerConfiguration()
        .WithPart<Calculator>();
    using (CompositionHost host = configuration.CreateContainer())
    {
        //etc.
    }
}
```

Besides using the method WithPart (which has overloads and generic versions as well as non-generic versions), you can also use WithParts to add a list of parts and use WithAssembly or WithAssemblies to add the exports of an assembly.

Using the CompositionHost, you can access exported parts with the GetExport and GetExports methods:

```
Calculator = host.GetExport<ICalculator>();
```

You can also use more “magic.” Instead of specifying all the export types you need to access, you can use the SatisfyImports method that is an extension method for the CompositionHost. The first parameter requires an object with imports. Because the Program class itself defines a property that has an Import attribute applied, the instance of the Program class can be passed to the SatisfyImports method. After invoking SatisfyImports, you will see that the Calculator property of the Program class is filled (code file AttributeBasedSample/SimpleHost/Program.cs):

```
using (CompositionHost host = configuration.CreateContainer())
{
    host.SatisfyImports(this);
}
```

With the Calculator property, you can use the methods from the interface ICalculator. GetOperations invokes the methods of the previously created add-in, which returns four operations. After asking the user what operation should be invoked and requesting the operand