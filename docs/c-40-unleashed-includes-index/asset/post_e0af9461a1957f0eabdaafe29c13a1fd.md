
At the point we declare the local variable of type Destruct, the default constructor is called, causing Constructing to be printed. At the point the method exits, the code compiled for the method ensures the stack-allocated object is destructed by a call to the destructor. This is a form of deterministic cleanup.

For the heap-allocated example, the output differs slightly. Here the responsibility of deleting the object is upon the user by using the delete operator. At that very point in time, the destructor will be called:

```
Heap - begin
Constructing
Destructing
Heap - end
```

This, again, is a form of deterministic cleanup. In both cases, it's either lexical scoping or manual user intervention that causes the destructor to be called. In none of the cases does a runtime service kick in to call the destructor's code.

## Defining Finalizers in C#

Before discussing their behavior in full detail, also contrasting it to the C++ behavior shown earlier, we first show how to declare a finalizer in C#. Because they share the C++ syntax, the language specification calls them destructors, but to avoid confusion with any of your C++ programmer friends, let's call them finalizers.

Here's a finalizer defined in C#, using the class's name prefixed with a ~ character:

```
class A
{
    ~A()
    {
        Console.WriteLine("Destructing instance of A");
    }
}
```

Finalizers cannot have an access modifier, nor can they have any parameters. They cannot be called explicitly by the user (so it doesn't make sense to pass parameters), as you will see.

## How Finalizers Are Run

Now let's move on to the discussion about their behavior and best practices associated with the use of finalizers. In contrast to C++, finalizers are called by the runtime when the object instance is no longer accessible by user code. The runtime service in charge of their invocation is the garbage collector that's responsible for releasing memory held by heap-allocated objects at a point after they've become unreachable by code. Earlier we discussed the mark-and-sweep mechanism employed by the garbage collector to scan memory, mark objects that are still alive, and collect the ones that cannot be used any longer.

When an object gets garbage collected and it implements a finalizer, that method will be scheduled to be run by the garbage collector before the final reclamation of the memory held by the object. Because of how the garbage collector works, finalizers put additional stress on the runtime. Here's why.

During garbage collection, the runtime's execution of managed code is suspended because memory is being manipulated and references are temporarily inconsistent. If code were allowed to run at this time, this would pose a breach in type safety because following a managed reference could lead you into no-man's land. As a result, code in finalizers cannot be run while the collection is in progress. Instead, the object that has become eligible for finalization (determined by the implementation of a custom finalizer) is put in a queue to be processed later when the execution engine is restarted after the garbage collection that was in-flight.

Because of this behavior, use of an empty finalizer is the worst possible thing you can put an object through because you simply postpone its death for no good reason. You'll soon learn how the use of a finalizer can and should be avoided whenever possible. But first, let's show a finalizer being called:

```
static void Main()
{
    A a = new A();

    // Won't collect before the application quits.
    Console.ReadLine();
}

class A
{
    ~A()
    {
        Console.WriteLine("Destructing instance of A");
    }
}
```

Unless something totally unexpected happens, causing the garbage collector to kick in for the preceding fragment, the finalizer for the instance of A won't get called until the very last point in time when the application quits. There's simply not enough stress on the managed heap to warrant a collection in the preceding example. To truly illustrate the nondeterministic behavior of finalization, let's show a more contrived example of excessive allocation, resulting in collection:

```
while (true)
{
    A a = new A();
}
```

A new object is allocated on the heap for every iteration through the loop. This causes the heap to grow until generation 0 becomes full. At that point, the garbage collector will kick in to collect objects that are no longer reachable. In fact, all objects allocated by prior iterations are unreachable because we overwrote the local variable in which their reference was kept. To show which objects get allocated and which ones get finalized, we'll add some counting mechanism to A:

```
class A
{
    private static int s_id;
    private int _id;

    public A()
    {
        _id = s_id++;
        Console.WriteLine("Allocated instance " + _id);
    }

    ~A()
    {
        Console.WriteLine("Finalized instance " + _id);
    }
}
```

When executing this code, results will likely vary from computer to computer and from run to run because of the parameters the garbage collector takes into account (such as the system's overall memory pressure). However, you should see objects being allocated for a long while until the very first collection kicks in and removes orphaned instances:

```
Allocated instance 8338
Allocated instance 8339
Allocated instance 8340
Allocated instance 8341
Finalized instance 8331
Allocated instance 8342
Allocated instance 8343
Finalized instance 6
Finalized instance 7
```

The order in which those objects get finalized is totally nondeterministic. You could also monitor collection count to see when a gen0 collection happens:

```csharp
int gen0 = 0;
while (true)
{
    A a = new A();
    var new0 = GC.CollectionCount(0);
    if (gen0 != new0)
    {
        Console.WriteLine("Gen0 collection triggered");
        gen0 = new0;
    }
}
```

## How Finalizers Are Implemented

To justify our naming of finalizers over destructors, take a look in ILDASM at the generated code, as shown in Figure 12.6. As you can see, C# destructors get turned into methods that override the Finalize method, which is defined on System.Object. The user's custom logic and a call to the base class's finalizer live inside this method. Although we still have to learn about inheritance, the idea is simple. When a class derives from another one to specialize its behavior, it's essential for the base class's cleanup logic to run as part of finalization. The code in our finalizer will be equivalent to the following:

```csharp
~A()
{
    try {
        Console.WriteLine("Finalized instance " + _id);
    }
    finally {
        base.Finalize();  // Calls System.Object's Finalize method.
    }
}
```

Even though destructors turn into Finalize methods, C# disallows direct use of this method (for example, using the override keyword). Visual Basic, on the other hand, doesn't add destructor syntax and lets users override the Finalize method.

## NOT FOR STRUCTS

Finalizers can only be defined on classes. The bookkeeping to determine when a struct's finalizer has to run would seriously hamper their lightweight nature.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_624_0.png)

FIGURE 12.6 Destructors override the Finalize method.

## Disposal Before Collection: IDisposable

Finalizers are typically implemented to ensure resources that are beyond the garbage collector's domain of responsibility get cleaned up properly. A good example is when you must deal with unmanaged resources (for example, in Win32 interop scenarios requiring manual release of object using calls to CloseHandle). Although lots of Win32 APIs have been wrapped in the .NET Framework, you might sometimes need to P/Invoke some other APIs manually. As an example, consider the CreateJobObject Win32 function, which allows for the creation of jobs, which are groups of processes. A managed code wrapper could look like this:

```
public class Job
{
    [DllImport("kernel32.dll", CharSet = CharSet.Unicode, SetLastError = true)]
    static extern IntPtr CreateJobObject(SECURITY_ATTRIBUTES att, string name);

    [DllImport("kernel32.dll", SetLastError = true)]
    static extern bool AssignProcessToJobObject(IntPtr job, IntPtr process);

    [DllImport("kernel32.dll", SetLastError = true)]
    static extern bool TerminateJobObject(IntPtr job, uint exitCode);

    private IntPtr _handle;

    private Job(IntPtr handle)
    {
        _handle = handle;
    }

    public static Job CreateOrOpen(string name)
    {
        // Notice a "null" name is allowed by the Win32 function.
        var res = CreateJobObject(null, name);
