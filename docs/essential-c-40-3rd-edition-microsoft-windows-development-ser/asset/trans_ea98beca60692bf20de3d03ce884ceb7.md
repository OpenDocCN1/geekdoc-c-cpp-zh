

doesn’t—and likely can’t—make certain checks. And in such cases, being able to make a dynamic call that is only runtime-verified rather than also compile-time verified is significantly more readable and succinct. Obviously, if compile-time verification is possible, statically typed programming is preferred because readable and succinct APIs could accompany it. However, in the cases where it isn’t effective, C# 4.0 enables simpler code rather than the purity of type safety.

### 实现自定义动态对象

Listing 17.31 included a method call to DynamicXml.Parse(...) that was essentially a factory method call for DynamicXml—a custom type rather than one built into the CLR Framework. However, DynamicXml doesn’t implement a FirstName or LastName property. To do so would break the dynamic support for retrieving data from the XML file at execution time, rather than compile-time-based implementation of the XML elements. In other words, DynamicXml does not use reflection for accessing its members, but rather it dynamically binds to the values based on the XML content.

The key to defining a custom dynamic type is implementation of the System.Dynamic.IDynamicMetaObjectProvider interface. Rather than implementing the interface from scratch, however, the preferred approach is to derive the custom dynamic type from System.Dynamic.DynamicObject. This provides default implementation for a host of members and allows you to override the ones that don’t fit. Listing 17.32 shows the full implementation.

### Listing 17.32: Implementing a Custom Dynamic Object

```
using System;
using System.Dynamic;
using System.Xml.Linq;

public class DynamicXml : DynamicObject
{
    private XElement Element { get; set; }

    public DynamicXml(System.Xml.Linq.XElement element)
    {
        Element = element;
    }

    public static DynamicXml Parse(string text)
    {
        return new DynamicXml(XElement.Parse(text));
    }

    public override bool TryGetMember(
        GetMemberBinder binder, out object result)
    {
        bool success = false;
        result = null;
        XElement firstDescendant =
            Element.Descendants(binder.Name).FirstOrDefault();
        if (firstDescendant != null)
        {
            if (firstDescendant.Descendants().Count() > 0)
            {
                result = new DynamicXml(firstDescendant);
            }
            else
            {
                result = firstDescendant.Value;
            }
            success = true;
        }
        return success;
    }

    public override bool TrySetMember(
        SetMemberBinder binder, object value)
    {
        bool success = false;
        XElement firstDescendant =
            Element.Descendants(binder.Name).FirstOrDefault();
        if (firstDescendant != null)
        {
            if (value.GetType() == typeof(XElement))
            {
                firstDescendant.ReplaceWith(value);
            }
            else
            {
                firstDescendant.Value = value.ToString();
            }
            success = true;
        }
        return success;
    }
}
```

The key dynamic implementation methods for this use case are TryGetMember() and the TrySetMember() (assuming you also want to assign the elements as well). Only these two method implementations are necessary to support the invocation of the dynamic getter and setter properties. Furthermore, the implementations are straightforward. First, they examine the contained XElement, looking for an element with the same name as the binder.Name—the name of the member invoked. If a corresponding XML element exists, then the value is retrieved (or set). The return value is set to true if the element exists and false if it doesn't. Automatically, a return value of false will cause the runtime to throw a Microsoft.CSharp.RuntimeBinder.RuntimeBinderException at the call site of the dynamic member invocation.

System.Dynamic.DynamicObject supports additional virtual methods if additional dynamic invocations are required. Listing 17.33 shows the list of all the overridable members.

### Listing 17.33: Overridable Members on System.Dynamic.DynamicObject

```
using System.Dynamic;

public class DynamicObject : IDynamicMetaObjectProvider
{
    protected DynamicObject();

    public virtual IEnumerable<string> GetDynamicMemberNames();
    public virtual DynamicMetaObject GetMetaObject(
        Expression parameter);
    public virtual bool TryBinaryOperation(
        BinaryOperationBinder binder, object arg,
        out object result);
    public virtual bool TryConvert(
        ConvertBinder binder, out object result);
    public virtual bool TryCreateInstance(
        CreateInstanceBinder binder, object[] args,
        out object result);
    public virtual bool TryDeleteIndex(
        DeleteIndexBinder binder, object[] indexes);
    public virtual bool TryDeleteMember(
        DeleteMemberBinder binder);
    public virtual bool TryGetIndex(
        GetIndexBinder binder, object[] indexes,
        out object result);
    public virtual bool TryGetMember(
        GetMemberBinder binder, out object result);
    public virtual bool TryInvoke(
        InvokeBinder binder, object[] args,
        out object result);
    public virtual bool TryInvokeMember(
        InvokeMemberBinder binder, object[] args,
        out object result);
    public virtual bool TrySetIndex(
        SetIndexBinder binder, object[] indexes, object value);
    public virtual bool TrySetMember(
        SetMemberBinder binder, object value);
    public virtual bool TryUnaryOperation(
        UnaryOperationBinder binder, out object result);
}
```

As Listing 17.33 shows there are member implementations for everything—from casts and various operations, through to index invocations. In addition, there is a method for retrieving all the possible member names: GetDynamicMemberNames().

### SUMMARY

This chapter discussed how to use reflection to read the metadata that is compiled into the CIL. Using reflection, you saw how to provide a late binding in which the code to call is defined at execution time rather than at compile time. Although reflection is entirely feasible for deploying a dynamic system, it is considerably slower than statically linked (compile-time), defined code. This tends to make it more prevalent and useful in development tools.

Reflection also enables the retrieval of additional metadata decorating various constructs in the form of attributes. Typically, custom attributes are sought using reflection. It is possible to define your own custom attributes that insert additional metadata of your own choosing into the CIL. At runtime, it is then possible to retrieve this metadata and use it within the programming logic.

Many view attributes as a precursor to a concept known as aspect-oriented programming, in which you add functionality through constructs such as attributes instead of manually implementing the functionality wherever it is needed. It will take some time before you see true aspects within C# (if ever); however, attributes provide a clear steppingstone in that direction, without forcing a significant risk to the stability of the language.

Finally, the chapter included a C# 4.0 introduced feature—dynamic programming using the new type dynamic. This section included a discussion of why static binding, although preferred when the API is strongly typed, has limitations when working with dynamic data.

The next chapter looks at multithreading, where attributes are used for synchronization.

## 18 Multithreading

PRIOR TO 2004, increasing computer power primarily involved increasing the power of a single processor. Limits imposed by the physics of today’s silicon microchip technology have forestalled further increases in the power of single processors. Figure 18.1 shows the plateau and even a small drop back, as the threshold of computing power versus heat dissipation stabilized to more maintainable levels.

In spite of the plateau, computer power continues to grow and Moore’s Law remains on track as multiple cores (within a single processor) and multiple processors (the microchips that plug into the motherboard) became standard on mainstream servers, workstations, and now laptops. Microsoft Windows reflects this available power by showing eight processors on the Windows Task Manager for a four-core machine with Hyper-Threading.

![](img/ef1bd88b5fdf5fb56f8510479607fe66_749_0.png)

