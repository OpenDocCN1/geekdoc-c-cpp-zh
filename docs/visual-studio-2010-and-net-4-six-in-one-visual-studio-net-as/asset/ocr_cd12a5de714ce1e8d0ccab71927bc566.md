Now, in C# 4.0, you can use parameterized properties declared in COM using the indexer syntax. For example, instead of get_(), you can now write x[]. With this syntax, you can now set the cell value in the most intuitive way, just as scripts and dynamic languages do:

```
var excel = new Excel.Application();
excel.Range["A1"].Value = "Name";
```

This is just syntax. The compiler still emits calls to the get_ and set_ acceptors of the day. This syntax does not mean that you can create indexed properties in C#, because this feature still does not exist in the language. The designers encourage you to use indexers and do not plan to introduce indexed properties.

# Compiling Without PIAs

To interoperate with a certain COM interface, you must use a .NET type wrapping the functionality of that COM interface. Building these wrappers manually is very laborious, especially when you have hundreds of COM interfaces — for example, in the case of the Microsoft Office automation model.

PIAs are .NET assemblies generated from COM interfaces to facilitate strongly typed interoperability. For large objects, the related PIAs are also large. At runtime, these large assemblies can easily bloat your program. They can also cause versioning issues when they are distributed independently of your application.

For example, the Word 2007 interoperability assembly has a size about 800 KB, while the Excel binary (which you saw earlier in this chapter) takes only 18 KB. It is normal to deploy 2 MB of overhead (PIAs) for an application with a size of 18 KB.

The no-PIA feature allows you to continue using PIAs at design time without having them around runtime. Instead, the C# compiler will generate a small part of the program that acts directly to the assembly. At runtime, the PIA does not have to be loaded.

You can turn on or off this feature for each interoperability assembly. Select the assembly in Solution Explorer and set the Embed Interop Properties to True (to turn on) or False (to turn off) no-PIA. Figure 24-3 shows the property window with no-PIA turned on for the Excel interoperability assembly.

![](bbox=[0.525, 0.545, 0.875, 0.835])

FIGURE 24-3: Embed Interop Types property