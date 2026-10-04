of attributes no significance. Also, in C#, each attribute can be enclosed in square brackets, or
multiple attributes can be comma-separated within a single set of square brackets. If the attribute
class's constructor takes no parameters, the parentheses are optional. As mentioned earlier, the
Attribute suffix is also optional. The following lines behave identically and demonstrate all of the
possibilities of applying multiple attributes.

```
[Serializable][Flags]
[Serializable, Flags]
[FlagsAttribute, SerializableAttribute]
[FlagsAttribute()][Serializable]
```

# Defining Your Own Attribute Class

Now that you know an attribute is an instance of a class derived from System.Attribute, and you also
now how to apply an attribute. Let's look now at how to define your own attribute classes.
Say you're the Microsoft employee responsible for adding the bit flag to enumerated types.
To accomplish, the first thing you need to do is define a FlagsAttribute class.

```
namespace System {
    public class FlagsAttribute : System.Attribute {
        public FlagsAttribute() {
    }
}
```

Notice that the FlagsAttribute class inherits from Attribute; this is what makes the Flags-
Attribute class a CLS-compliant custom attribute. In addition, the class's name has a suffix of
Attribute; this follows the standard convention but is not mandatory. Finally, all non-abstract
attributes must contain at least one public constructor. The simple FlagsAttribute constructor
takes no parameters and does absolutely nothing.

> Important You should think of an attribute as a logical state container. That is, while an at-
tribute type is a class, the class should be simple. The class should offer just one public-
structor that accepts the attribute's mandatory (or positional) state information, and the
class offer public fields/properties that accept the attribute's optional (or named) state
information. I always discourage the use of public fields, and I still discourage them for at-
tributes. It is much better to use properties because this allows more flexibility if you ever
dide to change how the attribute class is implemented.

In general, instances of the FlagsAttribute class can be applied to any target, but this attribute
should really be applied to enumerated types only. It doesn't make sense to apply the attribute to
property or a method. To tell the compiler where this attribute can legally be applied,