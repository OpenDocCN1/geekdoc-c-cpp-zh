don’t have a direct dependency. Instead, the hosting application and the add-in just reference the contract assembly.

From a Composition standpoint, an interface contract is not required at all. The contract can be a simple string. To avoid conflicts with other contracts, the name of the string should contain a namespace name—for example, Wrox.ProCSharp.Composition.SampleContract, as shown in the following code snippet. Here, the class Foo is exported by using the Export attribute, and a string passed to the attribute instead of the interface:

```
[Export("Wrox.ProCSharp.Composition.SampleContract")]
public class Foo
{
    public string Bar()
    {
        return"Foo.Bar";
    }
}
```

The problem with using a contract as a string is that the methods, properties, and events provided by the type are not strongly defined. Either the caller needs a reference to the type Foo to use it, or .NET reflection can be used to access its members. The C# 4 dynamic keyword makes reflection easier to use and can be very helpful in such scenarios.

The hosting application can use the dynamic type to import a contract with the name Wrox.ProCSharp.Composition.SampleContract:

```
[Import("Wrox.ProCSharp.MEF.SampleContract")]
public dynamic Foo { get; set; }
```

With the dynamic keyword, the Foo property can now be used to access the Bar method directly. The call to this method is resolved during runtime:

```
string s = Foo.Bar();
```

Contract names and interfaces can also be used in conjunction to define that the contract is used only if both the interface and the contract name are the same. This way, you can use the same interface for different contracts.

> NOTE The dynamic type is explained in Chapter 16.

# Exporting Parts

The previous example showed the part SimpleCalculator, which exports the type Calculator with all its methods and properties. The following example contains the SimpleCalculator as well, with the same implementation that was shown previously; and two more parts, TemperatureConversion and FuelEconomy, are exported. These parts offer a UI for the hosting application.