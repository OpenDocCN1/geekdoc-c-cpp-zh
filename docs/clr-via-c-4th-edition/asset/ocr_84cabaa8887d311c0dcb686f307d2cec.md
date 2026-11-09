Now, let's start gearing the discussion toward the CLR. Let's say that we have these two class definitions.

```
```csharp
internal class Employee {
    public      Int32   GetYearsEmployed()  { ... }
    public virtual String GetProgressReport() { ... }
    public static Employee Lookup(String name) { ... }
}

internal sealed class Manager : Employee {
    public override String GetProgressReport() { ... }
}
```
```

Our Windows process has started, the CLR is loaded into it, the managed heap is initialized, and a thread has been created (along with its 1 MB of stack space). This thread has already executed some code, and this code has decided to call the M3 method. All of this is shown in Figure 4-6. The M3 method contains code that demonstrates how the CLR works; this is not code that you would normally write, because it doesn't actually do anything useful.

![](bbox=[0.122, 0.326, 0.73, 0.607])

**FIGURE 4-6** The CLR loaded in a process, its heap initialized, and a thread's stack with the M3 method about to be called.

As the just-in-time (JIT) compiler converts M3's Intermediate Language (IL) code into native CPU instructions, it notices all of the types that are referred to inside M3: Employee, Int32, Manager, and String (because of "Joe"). At this time, the CLR ensures that the assemblies that define these types are loaded. Then, using the assembly's metadata, the CLR extracts information about these types and creates some data structures to represent the types themselves. The data structures for the Employee