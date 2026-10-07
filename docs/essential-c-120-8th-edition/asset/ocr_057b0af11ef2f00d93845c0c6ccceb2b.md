# 928 Chapter 18: Reflection, Attributes, and Dynamic Programming

FirstName or LastName property. To do so would break the dynamic support for retrieving data from the XML file at execution time rather than fostering compile-time-based implementation of the XML elements. In other words, DynamicXml does not use reflection for accessing its members but rather dynamically binds to the values based on the XML content.

The key to defining a custom dynamic type is implementation of the System.Dynamic.IDynamicMetaObject interface. Rather than implementing the interface from scratch, however, the preferred approach is to derive the custom dynamic type from System.Dynamic.DynamicObject. This provides default implementations for a host of members and allows you to override the ones that don't fit. Listing 18.32 shows the full implementation.

# Listing 18.32: Implementing a Custom Dynamic Object

```
using System.Dynamic;
using System.Linq;
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

    public override bool GetMember(Binder binder, out object result)
{
        bool success = false;
        result = null;
        XElement? firstDescendant = 
            Element.Descendants(binder.Name).FirstOrDefault();
        if(firstDescendant != null)
{
            if(firstDescendant.Descendants().Any())

```