
- **Indexed properties** allow properties to be called with additional parameters, much like indexers work. Those are not a proper C# language feature and are restricted for use in COM interop scenarios. The main difficulty with indexed properties as a general language feature is the fact they don't distinguish the act of property retrieval and indexing into an object. For that reason, the .NET designers thought it better to leave them out for managed code APIs (and they're not part of the CLS either). In C# 4.0, they're allowed only for COM interop.
- **Optional ref modifier when calling COM imported methods.** Because the most common calling convention used on COM APIs methods is to pass parameters by reference, you can omit the ref modifier on such calls starting from C# 4.0. Again, this is not a general language feature in C# and is limited to COM interop scenarios. Recall that the philosophy of the ref modifier is to explicitly indicate, in the call site, the intent of passing a parameter by reference.
- **Mapping of object to dynamic when importing COM APIs.** Because COM is quite a dynamic experience from a typing point of view, lots of parameters and return types are typed as IUnknown or IDispatch. Those interfaces form the roots of the interface hierarchy in the world of COM and correspond roughly to .NET's System.Object base type. Up until .NET 4, importing COM libraries performed a mapping for such types onto System.Object. Now that we have dynamic, this mapping has changed to use the new dynamic type. This allows you to "dot into" lots of COM APIs directly.
- **Embedding of interop types ("no PIA")** is a tooling feature, just like the one elaborated on in the previous point. The use of interop assemblies has caused grief in the past because of difficulties with deployment with applications that are using them. One major problem with those PIAs is their size, which can go into the megabyte range for interop assemblies like Word's. Typically, you're using just a fraction of the types and functionality in the assembly, so this is a huge waste of space. In .NET 4, used portions of PIAs can be embedded into your own assembly at build time.

We now discuss those features in more detail by means of a walkthrough where we use the improved COM interop in .NET 4 to talk with Office libraries. Keep in mind that this capability is not restricted to Office but provides value for all COM interop scenarios that span a wide range of technologies (for example, lots of Windows APIs have exposure through COM).

## A NECESSARY EVIL?

New language features often get widely criticized upon their introduction. This is no different with C# 4.0's improved COM interop features or dynamic more generally. One key question here is whether it's good to extend a language simply for interoperability enhancements.

When .NET was introduced, some people hoped for a quick disappearance of old technologies such as COM, in favor of managed code. History turned out quite different; the use of COM is still prevalent.

Smooth interoperability with such COM-based libraries has been hampered by the lack of nice managed code wrappers. PIAs typically expose the APIs they target in a verbatim manner, doing a poor job at providing a true "managed code feeling" for the APIs they interoperate with. As a result, managed code developers often don't feel at home when dealing with interoperability. This in turn has led to people avoiding technologies as a whole, solely because of poor interoperability. The goal of making such scenarios easier is definitely a good thing because "COM ain't dead."

Although every new language feature starts with a negative score (counting against the introduction of the feature to avoid bloating the language), there have been plenty of scoring points that motivate the introduction of C# 4.0 dynamic. The growing popularity of dynamic languages and untyped APIs, as well as COM interoperability scenarios, were enough to go ahead and add dynamic to the language.

To avoid aging the language unnecessarily, some of those features are restricted in use to COM interop scenarios only, as mentioned previously. To conclude, you could say those new features are "a necessary evil."

## Case Study: COM Interop with Excel and Word

To illustrate the improvements to COM interop in .NET 4, we start in the old world of .NET 3.5 and show what the code for our scenario looked like back then. Based on this, we gradually make the code simpler while porting it to C# 4.0, while looking at the individual features that form the basis of those enhancements.

## Walkthrough in .NET 3.5

The examples shown in this section assume you have a recent version of Office installed, preferably version 2007 or later. In addition, make sure to have the PIA redistributable installed, which you can find by searching the Web for "download Office PIA." If everything is correctly installed, you'll find the Office interop assemblies in the Add Reference dialog in Visual Studio, as shown in Figure 22.27. You can safely ignore the runtime version on them because PIAs don't really contain code and simply provide a set of interoperability interfaces (which can be seen as runtime neutral). Depending on the versions of Office PIAs you have installed, you'll see different entries. Office 2007 corresponds to version 12.0.0.0 and Office 2010 (selected here) version 14.0.0.0.

To illustrate the situation in .NET 3.5, we use Visual Studio 2008. Alternatively, you can use Visual Studio 2010 with the target framework of the project set to .NET Framework 3.5.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1184_0.png)

FIGURE 22.27 Importing the Office PIAs.

## WHAT ABOUT THE COM TAB?

When no PIAs are available, there's always the COM tab to generate an interop assembly for a selected COM library. Alternatively, command-line tools can be used to achieve the same effect, in particular the tlbimp.exe one. TLB stands for type library.

When PIAs are available, it's recommended to use them for a variety of reasons. As the name implies, a PIA is the primary interop assembly for the target library provided by some vendor. When different generated interop assemblies are mixed together, problems on type identity (pre .NET 4) can occur.

Once the two interop assemblies, Microsoft.Office.Interop.Word and a similarly named one for Excel, have been referenced, we can start writing code. To avoid clashes in type names if we were to import the namespaces as is, we use an alias for abbreviation:

```
using Word = Microsoft.Office.Interop.Word;
using Excel = Microsoft.Office.Interop.Excel;
```

The running example will be the creation of a Word document containing an Excel graph showing memory utilization for processes on the current machine. This example has been shown on various occasions introducing C# 4.0 and nicely illustrates all the applicable features.

To get started with the Office automation model, we need to instantiate an application object that serves as the entry point to an Office application such as Word or Excel. In fact, this creates an out-of-process instance of the targeted application that we communicate with cross-process through the magic of COM. In essence, our code is behind the steering wheel of an entire Office application. This activation behavior isn't the same for all COM APIs: Some run in-process; others don't.

Figure 22.28 shows how to create an instance of the Excel application. Notice we’re using the new operator on an *interface* type (notice the icon next to the menu entry), which looks kind of weird. This works because the compiler detects that the interface type corresponds to a COM type. If we go to the definition of the Application interface (by using Go to Definition or by pressing F12), we see the following:

```csharp
[Guid("00020B05-0000-0000-C000-000000000046")]
[CoClass(typeof(ApplicationClass))]
public interface Application : _Application, AppEvents_Event
{
}
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1185_0.png)

**FIGURE 22.28**  Instantiating an Excel application object.

The attributes used here are all defined in System.Runtime.InteropServices. We don’t have the space to elaborate on them, but what the compiler (up until version 3.5) did with our code is turn it into a constructor call on the referred CoClass:

```csharp
var excel = new Excel.ApplicationClass();
```

In C# 4.0, the generated code varies slightly, as you see later in the section called “Walkthrough in .NET 4.” What matters more is we can now start writing code against the automation model of Excel. We start by making the application visible by setting the Visible property to true. This causes an Excel instance to show up. While we’re executing code, you’ll see changes getting reflected (live) in the automated application instance:

```csharp
var excel = new Excel.Application();
excel.Visible = true;
```

Next, we ask Excel to create a new workbook. Obviously, methods exist to load an existing workbook by specifying a filename. Here we’re simply creating a scratchpad on which to generate a graph, ready to be exported to Word, so we don’t need any fancy calls to load an existing file:

```csharp
// New empty workbook
excel.Workbooks.Add(Type.Missing);
```
