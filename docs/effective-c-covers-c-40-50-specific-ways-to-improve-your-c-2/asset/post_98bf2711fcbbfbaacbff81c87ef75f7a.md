
Of course, you would never do that because you know better than to create public data members (see Item 1). The JIT compiler understands your need for both efficiency and elegance, so it inlines the property accessor. The JIT compiler inlines methods when the speed or size benefits (or both) make it advantageous to replace a function call with the body of the called function. The standard does not define the exact rules for inlining, and any implementation could change in the future. Moreover, it’s not your responsibility to inline functions. The C# language does not even provide you with a keyword to give a hint to the compiler that a method should be inlined. In fact, the C# compiler does not provide any hints to the JIT compiler regarding inlining. (You can request that a method not be inlined using the System.Runtime.CompilerServices.MethodImpl attribute, specifying the NoInlining option. It’s typically done to preserve method names on the callstack for debugging scenarios.)

```
[MethodImpl(MethodImplOptions.NoInlining)]
```

All you can do is ensure that your code is as clear as possible, to make it easier for the JIT compiler to make the best decision possible. The recommendation should be getting to be familiar by now: Smaller methods are better candidates for inlining. But remember that even small functions that are virtual or that contain try/catch blocks cannot be inlined.

Inlining modifies the principle that code gets JITted when it will be executed. Consider accessing the name property again:

```
string val = "Default Name";
if (Obj1 == null)
    val = Obj.Name;
```

If the JIT compiler inlines the property accessor, it must JIT that code when the containing method is called.

This recommendation to build smaller and composable methods takes on greater importance in the world of LINQ queries and functional programming. All the LINQ query methods are rather small. Also, most of the predicates, actions, and functions passed to LINQ queries will be small blocks of code. This small, more composable nature means that those methods, and your actions, predicates, and functions, are all more easily reused. In addition, the JIT compiler has a better chance of optimizing that code to create more efficient runtime execution.

It's not your responsibility to determine the best machine-level representation of your algorithms. The C# compiler and the JIT compiler together do that for you. The C# compiler generates IL for each method, and the JIT compiler translates that IL into machine code on the destination machine. You should not be too concerned about the exact rules the JIT compiler uses in all cases; those will change over time as better algorithms are developed. Instead, you should be concerned about expressing your algorithms in a manner that makes it easiest for the tools in the environment to do the best job they can. Luckily, those rules are consistent with the rules you already follow for good software-development practices. One more time: smaller and simpler functions.

Remember that translating your C# code into machine-executable code is a two-step process. The C# compiler generates IL that gets delivered in assemblies. The JIT compiler generates machine code for each method (or group of methods, when inlining is involved), as needed. Small functions make it much easier for the JIT compiler to amortize that cost. Small functions are also more likely to be candidates for inlining. It's not just smallness: Simpler control flow matters just as much. Fewer control branches inside functions make it easier for the JIT compiler to enregister variables. It's not just good practice to write clearer code; it's how you create more efficient code at runtime.

## 2 .NET Resource Management

The simple fact that .NET programs run in a managed environment has a big impact on the kinds of designs that create effective C#. Taking advantage of that environment requires changing your thinking from other environments to the .NET Common Language Runtime (CLR). It means understanding the .NET Garbage Collector. An overview of the .NET memory management environment is necessary to understand the specific recommendations in this chapter, so let's get on with the overview.

The Garbage Collector (GC) controls managed memory for you. Unlike native environments, you are not responsible for most memory leaks, dangling pointers, uninitialized pointers, or a host of other memory-management issues. But the Garbage Collector is not magic: You need to clean up after yourself, too. You are responsible for unmanaged resources such as file handles, database connections, GDI+ objects, COM objects, and other system objects. In addition you can cause objects to stay in memory longer than you'd like because you've created links between them using event handlers or delegates. Queries, which execute when results are requested, can also cause objects to remain referenced longer than you would expect. Queries capture bound variables in closures, and those bound variables are reachable until the containing results have gone out of scope.

Here's the good news: Because the GC controls memory, certain design idioms are much easier to implement. Circular references, both simple relationships and complex webs of objects, are much easier. The GC's Mark and Compact algorithm efficiently detects these relationships and removes unreachable webs of objects in their entirety. The GC determines whether an object is reachable by walking the object tree from the application's root object instead of forcing each object to keep track of references to it, as in COM. The EntitySet class provides an example of how this algorithm simplifies object ownership decisions. An Entity is a collection of objects loaded from a database. Each Entity may contain references to other Entity objects. Any of these entities may also contain links to other entities. Just like the relational database entity sets model, these links and references may be circular.

There are references all through the web of objects represented by different EntitySets. Releasing memory is the GC's responsibility. Because the .NET Framework designers did not need to free these objects, the complicated web of object references did not pose a problem. No decision needed to be made regarding the proper sequence of freeing this web of objects; it's the GC's job. The GC's design simplifies the problem of identifying this kind of web of objects as garbage. The application can stop referencing any entity when it's done. The Garbage Collector will know if the entity is still reachable from live objects in the application. Any objects that cannot be reached from the application are all garbage.

The Garbage Collector runs in its own thread to remove unused memory from your program. It also compacts the managed heap each time it runs. Compacting the heap moves each live object in the managed heap so that the free space is located in one contiguous block of memory. Figure 2.1 shows two snapshots of the heap before and after a garbage collection. All free memory is placed in one contiguous block after each GC operation.

![](img/28c59cb6ec56b677835aaafe709bff66_88_0.png)

Figure 2.1 The Garbage Collector not only removes unused memory, but it also moves other objects in memory to compact used memory and maximize free space.

As you've just learned, memory management (for the managed heap) is completely the responsibility of the Garbage Collector. Other system resources must be managed by developers: you and the users of your classes. Two mechanisms help developers control the lifetimes of unmanaged resources: finalizers and the IDisposable interface. A finalizer is a defensive mechanism that ensures your objects always have a way to release unmanaged resources. Finalizers have many drawbacks, so you also have the IDisposable interface that provides a less intrusive way to return resources to the system in a timely manner.

Finalizers are called by the Garbage Collector. They will be called at some time after an object becomes garbage. You don't know when that happens. All you know is that it happens sometime after your object cannot be reached. That is a big change from C++, and it has important ramifications for your designs. Experienced C++ programmers wrote classes that allocated a critical resource in its constructor and released it in its destructor:

```
// Good C++, bad C#:
class CriticalSection
{
    // Constructor acquires the system resource.
    public CriticalSection()
    {
        EnterCriticalSection();
    }

    // Destructor releases system resource.
    ~CriticalSection()
    {
        ExitCriticalSection();
    }

    private void ExitCriticalSection()
    {
        throw new NotImplementedException();
    }
    private void EnterCriticalSection()
    {
        throw new NotImplementedException();
    }
}
