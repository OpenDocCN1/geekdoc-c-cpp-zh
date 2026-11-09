However, AppDomain's **Load** method returns a reference to an assembly. Because the **System.Assembly** class isn't derived from **System.MarshalByRefObject**, the assembly object must be marshaled by value back to the calling AppDomain. But the CLR will now use the calling AppDomain's settings to locate the assembly and load it. If the assembly can't be found using the calling AppDomain's policy and search locations, a **FileNotFoundException** is thrown. This behavior is usually undesirable and is the reason that you should avoid AppDomain's **Load** method.

In most dynamically extensible applications, **Assembly's Load** method is the preferred way of loading an assembly into an AppDomain. However, it does require that you have all of the pieces that make up an assembly's identity. Frequently, developers write tools or utilities (such as ILDasm.exe, PEVerify.exe, CorFlags.exe, GACUtil.exe, SGen.exe, SN.exe, XSD.exe) that perform some kind of processing on an assembly. All of these tools take a command-line argument that refers to the path name of an assembly file (including file extension). To load an assembly specifying a path name, you call **Assembly's LoadFrom** method:

```
```csharp
public class Assembly {
    public static Assembly LoadFrom(String path);
    // Less commonly used overloads of LoadFrom are not shown
}
```
```

Internally, **LoadFrom** first calls **System.Reflection.AssemblyName**'s static **GetAssemblyName** method, which opens the specified file, finds the AssemblyDef metadata table's entry, and extracts the assembly identity information and returns it in a **System.Reflection.AssemblyName** object (the file is also closed). Then, **LoadFrom** internally calls **Assembly's Load** method, passing it the **AssemblyName** object. At this point, the CLR applies version-binding redirection policy and searches the various locations looking for a matching assembly. If **Load** finds the assembly, it will load it, and an **Assembly** object that represents the loaded assembly will be returned; **LoadFrom** returns this value. If **Load** fails to find an assembly, **LoadFrom** loads the assembly at the path name specified in **LoadFrom**'s argument. Of course, if an assembly with the same identity is already loaded, **LoadFrom** simply returns an **Assembly** object that represents the already loaded assembly.

By the way, the **LoadFrom** method allows you to pass a URL as the argument. Here is an example:

```
```csharp
Assembly a = Assembly.LoadFrom(@"http://Wintellect.com/SomeAssembly.dll");
```
```

When you pass an Internet location, the CLR downloads the file, installs it into the user's download cache, and loads the file from there. Note that you must be online or an exception will be thrown. However, if the file has been downloaded previously, and if Windows Internet Explorer has been set to work offline (see Internet Explorer's Work Offline menu item in its File menu), the previously downloaded file will be used, and no exception will be thrown. You can also call **UnsafeLoadFrom**, which can load a Web-downloaded assembly, bypassing some security checks.