```
~~~csharp
    // Use a property as a named parameter.
    public int Priority { get; set; }
}

[RemarkAttribute("This class uses an attribute.",
                 Supplement = "This is additional info.",
                 Priority = 10)]
class UseAttrib {
    // ...
}

class NamedParamDemo {
    static void Main() {
        Type t = typeof(UseAttrib);

        Console.Write("Attributes in " + t.Name + ": ");

        object[] attrs = t.GetCustomAttributes(false);
        foreach(object o in attrs) {
            Console.WriteLine(o);
        }

        // Retrieve the RemarkAttribute.
        Type tRemAtt = typeof(RemarkAttribute);
        RemarkAttribute ra = (RemarkAttribute)
            Attribute.GetCustomAttribute(t, tRemAtt);

        Console.Write("Remark: ");
        Console.WriteLine(ra.Remark);

        Console.Write("Supplement: ");
        Console.WriteLine(ra.Supplement);

        Console.WriteLine("Priority: " + ra.Priority);
    }
}
~~~
```

The output is shown here:

```
~~~
Attributes in UseAttrib: RemarkAttribute
Remark: This class uses an attribute.
Supplement: This is additional info.
Priority: 10
~~~
```

There is one point of interest in the program. Notice the attribute specified before **UseAttrib** that is shown here:

```
~~~csharp
[RemarkAttribute("This class uses an attribute.",
                 Supplement = "This is additional info.",
                 Priority = 10)]
~~~
```

The named attributes **Supplement** and **Priority** are *not* in any special order. These two assignments can be reversed without any change to the attribute.