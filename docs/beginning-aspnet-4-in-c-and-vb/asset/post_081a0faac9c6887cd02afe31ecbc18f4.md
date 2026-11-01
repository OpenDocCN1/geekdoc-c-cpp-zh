
## 26
## Interop
### WHAT'S IN THIS CHAPTER?
- COM and .NET technologies
- Using COM objects from within .NET applications
- Using .NET components from within COM clients
- Platform invoke for invoking native methods

If you have Windows programs written prior to .NET, you probably don't have the time and resources to rewrite everything for .NET. Sometimes rewriting code is useful for refactoring or rethinking the application architecture. A rewrite can also help with productivity in the long term, when adding new features is easier to do with the new technology. However, there is no reason to rewrite old code just because a new technology is available. You might have thousands of lines of existing, running code, which would require too much effort to rewrite just to move it into the managed environment.

The same applies to Microsoft. With the namespace System.DirectoryServices, Microsoft hasn't rewritten the COM objects accessing the hierarchical data store; the classes inside this namespace are wrappers accessing the ADSI COM objects instead. The same thing happens with System.Data.OleDb, where the OLE DB providers that are used by classes from this namespace do have quite complex COM interfaces.

The same issue may apply to your own solutions. If you have existing COM objects that should be used from .NET applications, or the other way around, if you want to write .NET components that should be used in old COM clients, this chapter is a starter for using COM interoperability (or interop).

If you don't have existing COM components you want to integrate with your application, or old COM clients that should use some .NET components, you can skip this chapter.

Like all other chapters, you can download the sample code for this chapter from the Wrox web site at www.wrox.com.

## .NET AND COM
COM is the predecessor technology to .NET. COM defines a component model where components can be written in different programming languages. A component written with C++ can be used from a Visual Basic client. Components can also be used locally inside a process, across processes, or across the network. Does this sound familiar? Of course, .NET has similar goals. However, the way in which these goals are achieved is different. The COM concepts became more and more complex to use and turned out not to be extensible enough. .NET fulfills goals similar to those of COM but introduces new concepts to make your job easier.

Even today, when using COM interop the prerequisite is to know COM. It doesn't matter if .NET components are used by COM clients or if COM components are used by .NET applications — you must know COM. So, this section compares COM and .NET functionality.

If you already have a good grasp of COM technologies, this section may refresh your COM knowledge. Otherwise, it introduces you to the concepts of COM — that now, using .NET, you happily don't have to deal with anymore in your daily work. However, all the problems that came with COM still apply when COM technology is integrated into .NET applications.

COM and .NET do have many similar concepts, with very different approaches to using them, including:
- Metadata
- Freeing memory
- Interfaces
- Method binding
- Data types
- Registration
- Threading
- Error handling
- Event handling

These concepts, plus the marshaling mechanism, are covered in the following sections.

### Metadata
With COM, all information about the component is stored inside the type library. The type library includes information such as names and IDs of interfaces, methods, and arguments. With .NET, all this information can be found inside the assembly itself, as you saw in Chapter 14, Reflection, and Chapter 18, Assemblies. The problem with COM is that the type library is not extensible. With C++, IDL (Interface Definition Language) files have been used to describe the interfaces and methods. Some of the IDL modifiers cannot be found inside the type library, because Visual Basic (and the Visual Basic team was responsible for the type library) couldn't use these IDL modifiers. With .NET, this problem doesn't exist because the .NET metadata is extensible using custom attributes.

As a result of this behavior, some COM components have a type library and others don't. When no type library is available, a C++ header file can be used that describes the interfaces and methods. With .NET, it is easier to use COM components that do have a type library, but it is also possible to use COM components without a type library. In that case, it is necessary to redefine the COM interface by using C# code.

### Freeing Memory
With .NET, memory is released by the garbage collector. This is completely different with COM. COM relies on reference counts.

The interface IUnknown, which is the interface that is required to be implemented by every COM object, offers three methods. Two of these methods are related to reference counts. The method AddRef() must be called by the client if another interface pointer is needed; this method increments the reference count. The method Release() decrements the reference count, and if the resulting reference count is 0, the object destroys itself to free the memory.

You can see in Figure 26-3, a dual interface is derived from IDispatch but provides the additional methods of the interface directly in the vtable. Scripting clients can use the IDispatch interface to invoke the Add and Sub methods, whereas clients aware of the vtable can call the Add and Sub methods directly.

![](img/d7d2ffa0a76feaab821930e95daace93_759_0.png)

FIGURE 26-3

### Casting and QueryInterface
If a .NET class implements multiple interfaces, casts can be done to get one interface or another. With COM, the interface IUnknown offers a similar mechanism with the method QueryInterface(). As discussed in the previous section, the interface IUnknown is the base interface of every interface, so QueryInterface() is available anyway.

### Method Binding
How a client maps to a method is defined with the terms early and late binding. Late binding means that the method to invoke is looked for during runtime. .NET uses the System.Reflection namespace to make this possible (see Chapter 14).

COM uses the IDispatch interface discussed earlier for late binding. Late binding is possible with dispatch and dual interfaces.

With COM, early binding has two different options. One way of early binding, also known as vtable binding, is to use the vtable directly — this is possible with custom and dual interfaces. The second option for early binding is also known as ID binding. Here the dispatch ID is stored inside the client code, so during runtime only a call to Invoke() is necessary. GetIDsOfNames() is called during design time. With such clients, it is important to remember that the dispatch ID must not be changed.

### Data Types
For dual and dispatch interfaces, the data types that can be used with COM are restricted to a list of automation-compatible data types. The Invoke() method of the IDispatch interface accepts an array of VARIANT data types. The VARIANT is a union of many different data types, such as BYTE, SHORT, LONG, FLOAT, DOUBLE, BSTR, IUnknown, IDispatch, and so on. VARIANTS have been easy to use from Visual Basic, but it was complex to use them from C++. .NET has the object class instead of VARIANTS.

With custom interfaces, all data types available with C++ can be used with COM. However, this also restricts the clients that can use this component to certain programming languages.

### Registration
.NET distinguishes between private and shared assemblies, as discussed in Chapter 18. With COM, all components are globally available through a registry configuration.

All COM objects have a unique identifier that consists of a 128-bit number and is also known as class ID (CLSID). The COM API call to create COM objects, `CoCreateInstance()`, just looks into the registry to find the CLSID and the path to the DLL or EXE to load the DLL or launch the EXE and instantiate the component.

Because such a 128-bit number cannot be easily remembered, many COM objects also have a ProgID. The ProgID is an easy-to-remember name, such as `Excel.Application`, that just maps to the CLSID.

In addition to the CLSID, COM objects also have a unique identifier for each interface (IID) and for the type library (typelib ID).

Information in the registry is discussed in more detail later in the chapter.

### Threading
COM uses apartment models to relieve the programmer of having to deal with threading issues. However, this also adds some more complexity. Different apartment types have been added with different releases of the operating system. This section discusses the single-threaded apartment and the multithreaded apartment.

![](img/d7d2ffa0a76feaab821930e95daace93_760_0.png)

### Single-Threaded Apartment
The *single-threaded apartment (STA)* was introduced with Windows NT 3.51. With an STA, only one thread (the thread that created the instance) is allowed to access the component. However, it is legal to have multiple STAs inside one process, as shown in Figure 26-4.

In this figure, the inner rectangles with the lollipop represent COM components. Components and threads (curved arrows) are surrounded by apartments. The outer rectangle represents a process.

With STAs, there's no need to protect instance variables from multiple-thread access, because this protection is provided by a COM facility, and only one thread accesses the component.

A COM object that is not programmed with thread safety marks the requirements for an STA in the registry with the registry key `ThreadingModel` set to `Apartment`.

![](img/d7d2ffa0a76feaab821930e95daace93_760_1.png)

### Multithreaded Apartment
Windows NT 4.0 introduced the concept of a *multithreaded apartment (MTA)*. With an MTA, multiple threads can access the component simultaneously. Figure 26-5 shows a process with one MTA and two STAs.
