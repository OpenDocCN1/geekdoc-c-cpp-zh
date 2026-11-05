# ### 22.2.3 Positional and named parameters

Attribute classes can have *positional parameters* and *named parameters*. Each public instance constructor for an attribute class defines a valid sequence of positional parameters for that attribute class. Each non-static public read-write field and property for an attribute class defines a named parameter for the attribute class. For a property to define a named parameter, that property shall have both a public get accessor and a public set accessor.

*Example:* The following example defines an attribute class named `HelpAttribute` that has one positional parameter, `url`, and one named parameter, `Topic`. Although it is non-static and public, the property `Url` does not define a named parameter, since it is not read-write. Two uses of this attribute are also shown:

```
    [AttributeUsage(AttributeTargets.Class)]
    public class HelpAttribute : Attribute
    {
        public HelpAttribute(string url) // url is a positional parameter
        {
            ...
        }

        // Topic is a named parameter
        public string Topic
        {
            get;
            set;
        }

        public string Url { get; }
    }

    [Help("http://www.mycompany.com/xxx/Class1.htm")]
    class Class1
    {
    }

    [Help("http://www.mycompany.com/xxx/Misc.htm", Topic ="Class2")]
    class Class2
    {
    }
```

*end example*

# ### 22.2.4 Attribute parameter types

The types of positional and named parameters for an attribute class are limited to the *attribute parameter types*, which are:

+   - One of the following types: bool, byte, char, double, float, int, long, sbyte, short, string, uint, ulong, ushort.
+   - The type object.
+   - The type System.Type.
+   - Enum types.