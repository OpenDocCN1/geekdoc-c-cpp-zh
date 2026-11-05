one of the objects methods. This is the explicit way of creating AppDomain by .Net Applications

+   - AppDomains are created using the CreateDomain method. AppDomain instances are used to load and execute assemblies (Assembly). When an AppDomain is no longer in use, it can be unloaded.

```
```csharp
public class DemoAppDomain : MarshalByRefObject
{
    public string GetInfo()
    {
        return AppDomain.CurrentDomain.GoodName;
    }
}
public class DemoApp
{
    public static void Main()
    {
        AppDomain apd = AppDomain.CreateDomain("Technical Domain");
        DemoAppDomain apdinfo
            = (DemoAppDomain)apd.CreateInstanceAndUnwrap
            (Assembly.GetCallingAssembly().GetName().Name, "DemoAppDomain");
        Console.WriteLine("Application Name = " + apdinfo.GetInfo());
    }
}
```
```

+   - The AppDomain class implements a set of events that enable applications to respond when an assembly is loaded, when an application domain will be unloaded, or when an unhandled exception is thrown.

# ### 26.2.4 Shadow Copies and Restarts

+   - Once an assembly is loaded into an AppDomain, there is no way to remove the assembly from the AppDomain. It is possible, however, to remove an AppDomain from a process.
+   - If an updated 'dll' file is copied into an application's bin subdirectory, the ASP.NET runtime recognizes there is new code to execute. Since ASP.NET cannot swap the 'dll' file into the existing AppDomain, it starts a new AppDomain. The old application domain is "drain stopped", that is, existing requests are allowed to finish executing, and once they are all finished the AppDomain can unload. The new AppDomain starts with the new code and begins taking all new requests.
+   - Typically, when a 'dll' file loads into a process, the process locks the 'dll' file and it cannot be overwritten on the disk. However, AppDomains have a feature known as Shadow Copy that allows assemblies to remain unlocked and replaceable on disk.