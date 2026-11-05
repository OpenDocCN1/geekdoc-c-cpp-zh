A delegate can reference either a static method (such as Square or Math.Sin in the previous example) or an instance method (such as m.Multiply in the previous example). A delegate that references an instance method also references a particular object, and when the instance method is invoked through the delegate, that object becomes this in the invocation.

Delegates can also be created using anonymous functions, which are “in-line methods” that are created on the fly. Anonymous functions can see the local variables of the surrounding methods. Thus the multiplier example above can be written more easily without using a Multiplier class:

```
double[] doubles = Apply(a, (double x) => x * 2.0);
```

An interesting and useful property of a delegate is that it does not know or care about the class of the method it references; all that matters is that the referenced method has the same parameters and return type as the delegate.

> BILL WAGNER  This property of delegates make them an excellent tool for providing interfaces between components with the lowest possible coupling.

# 1.12 Attributes

Types, members, and other entities in a C# program support modifiers that control certain aspects of their behavior. For example, the accessibility of a method is controlled using the public, protected, internal, and private modifiers. C# generalizes this capability such that user-defined types of declarative information can be attached to program entities and retrieved at runtime. Programs specify this additional declarative information by defining and using attributes.

The following example declares a HelpAttribute attribute that can be placed on program entities to provide links to their associated documentation.

```
using System;
public class HelpAttribute: Attribute
{
    string url;
    string topic;
    public HelpAttribute(string url) {
        this.url = url;
    }
    public string Url {
        get { return url; }
    }
}
```