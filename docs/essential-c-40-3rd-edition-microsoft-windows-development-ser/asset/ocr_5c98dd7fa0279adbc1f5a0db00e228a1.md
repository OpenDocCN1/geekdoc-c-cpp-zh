doesn’t—and likely can’t—make certain checks. And in such cases, being able to make a dynamic call that is only runtime-verified rather than also compile-time verified is significantly more readable and succinct. Obviously, if compile-time verification is possible, statically typed programming is preferred because readable and succinct APIs could accompany it. However, in the cases where it isn’t effective, C# 4.0 enables simpler code rather than the purity of type safety.

# Implementing a Custom Dynamic Object

Listing 17.31 included a method call to DynamicXml.Parse(...) that was essentially a factory method call for DynamicXml—a custom type rather than one built into the CLR Framework. However, DynamicXml doesn’t implement a FirstName or LastName property. To do so would break the dynamic support for retrieving data from the XML file at execution time, rather than compile-time-based implementation of the XML elements. In other words, DynamicXml does not use reflection for accessing its members, but rather it dynamically binds to the values based on the XML content.

The key to defining a custom dynamic type is implementation of the System.Dynamic.IDynamicMetaObjectProvider interface. Rather than implementing the interface from scratch, however, the preferred approach is to derive the custom dynamic type from System.Dynamic.DynamicObject. This provides default implementation for a host of members and allows you to override the ones that don’t fit. Listing 17.32 shows the full implementation.

# LISTING 17.32: Implementing a Custom Dynamic Object

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
```