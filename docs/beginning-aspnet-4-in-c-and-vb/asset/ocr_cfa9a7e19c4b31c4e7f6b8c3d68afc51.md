AppDomain. With a process viewer, you will not see the process AssemblyA.exe executing because there's no new process created. AssemblyA is loaded into the process DomainTest.exe.

```
DomainTest.exe
Main in domain New AppDomain called
```

Instead of calling the Main() method in the newly loaded assembly, you can also create a new instance. In the following example, replace the ExecuteAssembly() method with a CreateInstance(). The first argument is the name of the assembly, AssemblyA. The second argument defines the type that should be instantiated: Wrox.ProcSharp.Assemblies.AppDomains.Demo. The third argument, true, means that case is ignored. System.Reflection.BindingFlags.CreateInstance is a binding flag enumeration value to specify that the constructor should be called:

```
AppDomain secondDomain = AppDomain.CreateDomain("New AppDomain");
// secondDomain.ExecuteAssembly("AssemblyA.exe");
secondDomain.CreateInstance("AssemblyA", "Wrox.ProcSharp.Assemblies.Demo",
true, BindingFlags.CreateInstance, null, new object[] { 7, 3 },
null, null);

code snippet DomainTest/Program.cs
```

The results of a successful run of the application are as follows:

```
DomainTest.exe
Constructor with the values 7, 3 in domain New AppDomain called
```

Now you have seen how to create and call application domains. In runtime hosts, application domains are created automatically. ASP.NET creates an application domain for each web application that runs on a web server. Internet Explorer creates application domains in which managed controls will run. For applications, it can be useful to create application domains if you want to unload an assembly. You can unload assemblies only by terminating an application domain.

> Application domains are an extremely useful construct if assemblies are loaded dynamically, and the requirement exists to unload assemblies after use. Within the primary application domain, it is not possible to get rid of loaded assemblies. However, it is possible to end application domains where all assemblies loaded just within the application domain are cleaned from the memory.

With this knowledge about application domains, it is now possible to change the WPF program created earlier. The new class CodeDriverInAppDomain creates a new application domain using AppDomain .CreateDomain. Inside this new application domain, the class CodeDriver is instantiated using CreateInstanceAndUnwrap(). Using the CodeDriver instance, the CompileAndRun() method is invoked before the new app-domain is unloaded again.

```
using System;
using System.Runtime.Remoting;

namespace Wrox.ProcSharp.Assemblies
{
    public class CodeDriverInAppDomain
    {
        public string CompileAndRun(string code, out bool hasError)
        {
            AppDomain codeDomain = AppDomain.CreateDomain("CodeDriver");
            CodeDriver codeDriver = (CodeDriver)
```