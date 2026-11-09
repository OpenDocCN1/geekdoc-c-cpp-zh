of attributes has no significance. Also, in C#, each attribute can be enclosed in square brackets, or multiple attributes can be comma-separated within a single set of square brackets. If the attribute class's constructor takes no parameters, the parentheses are optional. Finally, as mentioned earlier, the Attribute suffix is also optional. The following lines behave identically and demonstrate all of the possible ways of applying multiple attributes.

```
```
[Serializable][Flags]
[Serializable, Flags]
[FlagsAttribute, SerializableAttribute]
[FlagsAttribute()][Serializable()]
```
```

# ## Defining Your Own Attribute Class

You know that an attribute is an instance of a class derived from System.Attribute, and you also know how to apply an attribute. Let's now look at how to define your own custom attribute classes. Say you're the Microsoft employee responsible for adding the bit flag support to enumerated types. To accomplish this, the first thing you have to do is define a FlagsAttribute class.

```
```
namespace System {
    public class FlagsAttribute : System.Attribute {
        public FlagsAttribute() {
        }
    }
}
```
```

Notice that the FlagsAttribute class inherits from Attribute; this is what makes the FlagsAttribute class a CLS-compliant custom attribute. In addition, the class's name has a suffix of Attribute; this follows the standard convention but is not mandatory. Finally, all non-abstract attributes must contain at least one public constructor. The simple FlagsAttribute constructor takes no parameters and does absolutely nothing.

> > **Important** You should think of an attribute as a logical state container. That is, while an attribute type is a class, the class should be simple. The class should offer just one public constructor that accepts the attribute's mandatory (or positional) state information, and the class can offer public fields/properties that accept the attribute's optional (or named) state information. The class should not offer any public methods, events, or other members.
> >
> > In general, I always discourage the use of public fields, and I still discourage them for attributes. It is much better to use properties because this allows more flexibility if you ever decide to change how the attribute class is implemented.

So far, instances of the FlagsAttribute class can be applied to any target, but this attribute should really be applied to enumerated types only. It doesn't make sense to apply the attribute to a property or a method. To tell the compiler where this attribute can legally be applied, you apply