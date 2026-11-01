In this section, a COM object is defined with .NET code that is used by a COM client with the help of a COM callable wrapper (CCW). By using the object from a COM client, you will see how to create a type library from the .NET assembly, use different .NET attributes to specify COM interop behaviors, and register the .NET assembly as a COM component. Then, a COM client with C++ is created to use the CCW. Finally, the .NET component is expanded to offer COM connection points.

# COM Callable Wrapper

If you want to access a COM component with a .NET client, you have to work with an RCW. To access a .NET component from a COM client application, you must use a CCW. Figure 26-11 shows the CCW that wraps a .NET class, and offers COM interfaces that a COM client expects to use. The CCW offers interfaces such as IUnknown, IDispatch, and others. It also offers interfaces such as IConnectionPointContainer and IConnectionPoint for events. Of course, the CCW also offers the custom interfaces that are defined by the .NET class such as IWelcome and IMath. A COM client gets what it expects from a COM object — although a .NET component operates behind the scenes. The wrapper deals with methods such as AddRef(), Release(), and QueryInterface() from the IUnknown interface, whereas in the .NET object you can count on the garbage collector without the need to deal with reference counts.

![](bbox=[0.12, 0.6, 0.85, 0.78])

FIGURE 26-11

# Creating a .NET Component

In the following example, you build the same functionality into a .NET class that you have previously built into a COM component. Start by creating a C# class library, and name it DotNetServer. Then add the interfaces IWelcome and IMath, and the class DotNetComponent that implements these interfaces. The attribute ComVisible(true) makes the class and interfaces available for COM:

```
using System;
using System.Runtime.InteropServices;

namespace Wrox.ProCSharp.Interop.Server
{
    [ComVisible(true)]
    public interface IWelcome
    {
        string Greeting(string name);
    }

    [ComVisible(true)]
    public interface IMath
    {
        int Add(int val1, int val2);
        int Sub(int val1, int val2);
```