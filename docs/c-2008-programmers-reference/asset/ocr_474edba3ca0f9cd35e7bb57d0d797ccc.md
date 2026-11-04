```
//---specify the element name to be MemberName---
[XmlElement("MemberName*")]
public MemberName Name;
...
```

Specifies that the element name MemberName be used in place of the current variable name (as defined in the class as Name).

```
//---specify the sub-element(s) of Addresses to be Address---
[XmlArrayItem("Address")]
public MemberAddress[] Addresses;
...
```

Specifies that the following variable is repeating (an array) and that each repeating element be named as Address.

```
//---empty element if city is not specified---
[XmlElement(IsNullable = true)]
public string City;
...
```

Indicates that the document must include the City element even if it is empty.

```
//---specify country and postal as attribute---
[XmlAttributeAttribute()]
public string Country;

[XmlAttributeAttribute()]
public string Postal;
...
```

Indicates that the Country and Postal property be represented as an attribute.

# XML Serialization Needs a Default Constructor

There is one more thing that you need to note when doing XML serialization. If your class has a constructor (as in the following example), you also need a default constructor:

```
[XmlRoot("MemberInformation",
Namespace = "http://www.learn2develop.net",
IsNullable = true)]
public class Member
{
    private int age;
```