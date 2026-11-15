# Why Dynamic Binding?

In addition to reflection, we can define custom types to invoke dynamically. Consider using dynamic invocation to retrieve the values of an XML element, for example. Rather than using the strongly typed syntax of Listing 17.30, using dynamic invocation we could call person.FirstName and person.LastName.

# LISTING 17.30: The CIL for Attributes in General

```
using System;
using System.Xml.Linq;

// ...
XElement person = XElement.Parse(
    @"<Person>
        <FirstName>Inigo</FirstName>
        <LastName>Montoya</LastName>
    </Person>");
Console.WriteLine("{0} {1}",
    person.Descendants("FirstName").FirstOrDefault().Value,
    person.Descendants("LastName").FirstOrDefault().Value);
// ...
```

Although the code in Listing 17.30 is not overly complex, compare it to Listing 17.31—an alternative approach that uses a dynamically typed object.

# LISTING 17.31: The CIL for Attributes in General

```
using System;

// ...
dynamic person = DynamicXml.Parse(
    @"<Person>
        <FirstName>Inigo</FirstName>
        <LastName>Montoya</LastName>
    </Person>");
Console.WriteLine("{0} {1}",
    person.FirstName, person.LastName);
// ...
```

The advantages are clear, but does that mean dynamic programming is preferable to static compilation?