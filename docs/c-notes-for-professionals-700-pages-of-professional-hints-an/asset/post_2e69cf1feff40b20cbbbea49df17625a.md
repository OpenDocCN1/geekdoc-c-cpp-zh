
### Section 142.2: Union Types in C# can also contain Struct fields

Apart from primitives, the Explicit Layout structs (Unions) in C#, can also contain other Structs. As long as a field is a Value type and not a Reference, it can be contained in a Union:

```
using System;
using System.Runtime.InteropServices;

// The struct needs to be annotated as "Explicit Layout"
[StructLayout(LayoutKind.Explicit)]
struct IPAddress
{
    // Same definition of IPAddress, from the example above
}

// Now let's see if we can fit a whole URL into a long

// Let's define a short enum to hold protocols
enum Protocol : short { Http, Https, Ftp, Sftp, Tcp }

// The Service struct will hold the Address, the Port and the Protocol
[StructLayout(LayoutKind.Explicit)]
struct Service
{
    [FieldOffset(0)] public IPAddress Address;
    [FieldOffset(4)] public ushort Port;
    [FieldOffset(6)] public Protocol AppProtocol;
    [FieldOffset(0)] public long Payload;

    public Service(IPAddress address, ushort port, Protocol protocol)
    {
        Payload = 0;
        Address = address;
        Port = port;
        AppProtocol = protocol;
    }

    public Service(long payload)
    {
        Address = new IPAddress(0);
        Port = 80;
        AppProtocol = Protocol.Http;
        Payload = payload;
    }

    public Service Copy() => new Service(Payload);

    public override string ToString() => $"{AppProtocol}//{Address}:{Port}/";
}
```

We can now verify that the whole Service Union fits into the size of a long (8 bytes).

```
var ip = new IPAddress(new Random().Next());
Console.WriteLine($"Size: {Marshal.SizeOf(ip)} bytes. Value: {ip.Address} = {ip}.");

var s1 = new Service(ip, 8080, Protocol.Https);
var s2 = new Service(s1.Payload);
s2.Address.Byte1 = 100;
s2.AppProtocol = Protocol.Ftp;
```

```
Console.WriteLine($"Size: {Marshal.SizeOf(s1)} bytes. Value: {s1.Address} = {s1}.");
Console.WriteLine($"Size: {Marshal.SizeOf(s2)} bytes. Value: {s2.Address} = {s2}.");
```

View Demo

## Chapter 143: Reactive Extensions (Rx)

### Section 143.1: Observing TextChanged event on a TextBox

An observable is created from the TextChanged event of the TextBox. Also any input is only selected if it's different from the last input and if there was no input within 0.5 seconds. The output in this example is sent to the console.

```
Observable
.FromEventPattern(textBoxInput, "TextChanged")
.Select(s => ((TextBox) s.Sender).Text)
.Throttle(TimeSpan.FromSeconds(0.5))
.DistinctUntilChanged()
.Subscribe(text => Console.WriteLine(text));
```

### Section 143.2: Streaming Data from Database with Observable

Assume having a method returning IEnumerable<T>, f.e.

```
private IEnumerable<T> GetData()
{
    try
    {
        // return results from database
    }
    catch(Exception exception)
    {
        throw;
    }
}
```

Creates an Observable and starts a method asynchronously. SelectMany flattens the collection and the subscription is fired every 200 elements through Buffer.

```
int bufferSize = 200;

Observable
.Start(() => GetData())
.SelectMany(s => s)
.Buffer(bufferSize)
.ObserveOn(SynchronizationContext.Current)
.Subscribe(items =>
{
    Console.WriteLine("Loaded {0} elements", items.Count);
    // do something on the UI like incrementing a ProgressBar
},
() => Console.WriteLine("Completed loading"));
```

## Chapter 144: AssemblyInfo.cs Examples

### Section 144.1: Global and local AssemblyInfo

Having a global allows for better DRYness, you need only put values that are different into AssemblyInfo.cs for projects that have variance. This use assumes your product has more than one visual studio project.

GlobalAssemblyInfo.cs

```csharp
using System.Reflection;
using System.Runtime.InteropServices;
//using Stackoverflow domain as a made up example

// It is common, and mostly good, to use one GlobalAssemblyInfo.cs that is added
// as a link to many projects of the same product, details below
// Change these attribute values in local assembly info to modify the information.
[assembly: AssemblyProduct("Stackoverflow Q&A")]
[assembly: AssemblyCompany("Stackoverflow")]
[assembly: AssemblyCopyright("Copyright © Stackoverflow 2016")]

// The following GUID is for the ID of the typelib if this project is exposed to COM
[assembly: Guid("4e4f2d33-aaab-48ea-a63d-1f0a8e3c935f")]
[assembly: ComVisible(false)] //not going to expose ;)

// Version information for an assembly consists of the following four values:
// roughly translated from I reckon it is for SO, note that they most likely
// dynamically generate this file
//      Major Version  - Year 6 being 2016
//      Minor Version  - The month
//      Day Number     - Day of month
//      Revision       - Build number
// You can specify all the values or you can default the Build and Revision Numbers
// by using the '*' as shown below: [assembly: AssemblyVersion("year.month.day.*")]
[assembly: AssemblyVersion("2016.7.00.00")]
[assembly: AssemblyFileVersion("2016.7.27.3839")]
```

AssemblyInfo.cs - one for each project

```csharp
//then the following might be put into a separate Assembly file per project, e.g.
[assembly: AssemblyTitle("Stackoverflow.Redis")]
```

You can add the GlobalAssemblyInfo.cs to the local project using the following procedure:

- 1. Select Add/Existing Item... in the context menu of the project
- 2. Select GlobalAssemblyInfo.cs
- 3. Expand the Add-Button by clicking on that little down-arrow on the right hand
- 4. Select "Add As Link" in the buttons drop down list

### Section 144.2: [AssemblyVersion]

This attribute applies a version to the assembly.

```csharp
[assembly: AssemblyVersion("1.0.*")]
```

The * character is used to auto-increment a portion of the version automatically every time you compile (often used for the "build" number)

### Section 144.3: Automated versioning

Your code in source control has version numbers either by default (SVN ids or Git SHA1 hashes) or explicitly (Git tags). Rather than manually updating versions in AssemblyInfo.cs you can use a build time process to write the version from your source control system into your AssemblyInfo.cs files and thus onto your assemblies.

The GitVersionTask or SemVer.Git.Fody NuGet packages are examples of the above. To use GitVersionTask, for instance, after installing the package in your project remove the Assembly*Version attributes from your AssemblyInfo.cs files. This puts GitVersionTask in charge of versioning your assemblies.

Note that Semantic Versioning is increasingly the de facto standard so these methods recommend using source control tags that follow SemVer.

### Section 144.4: Common fields

It's good practice to complete your AssemblyInfo's default fields. The information may be picked up by installers and will then appear when using Programs and Features (Windows 10) to uninstall or change a program.

The minimum should be:

- AssemblyTitle - usually the namespace, i.e. MyCompany.MySolution.MyProject
- AssemblyCompany - the legal entities full name
- AssemblyProduct - marketing may have a view here
- AssemblyCopyright - keep it up to date as it looks scruffy otherwise

'AssemblyTitle' becomes the 'File description' when examining the DLL's Properties Details tab.

### Section 144.5: [AssemblyTitle]

This attribute is used to give a name to this particular assembly.

```csharp
[assembly: AssemblyTitle("MyProduct")]
```

### Section 144.6: [AssemblyProduct]

This attribute is used to describe the product that this particular assembly is for. Multiple assemblies can be components of the same product, in which case they can all share the same value for this attribute.

```csharp
[assembly: AssemblyProduct("MyProduct")]
```

### Section 144.7: [InternalsVisibleTo]

If you want to make internal classes or functions of an assembly accessable from another assembly you declare this by InternalsVisibleTo and the assembly name that is allowed to access.

In this example code in the assembly MyAssembly.UnitTests is allowed to call internal elements from MyAssembly.

```csharp
[assembly: InternalsVisibleTo("MyAssembly.UnitTests")]
```

This is especially useful for unit testing to prevent unnecessary public declarations.
