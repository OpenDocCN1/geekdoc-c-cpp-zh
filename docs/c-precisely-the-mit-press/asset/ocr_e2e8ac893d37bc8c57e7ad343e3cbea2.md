# Attributes 217

Example 254 using the Serialization Attribute
The classes SC and SO have the Serializable attribute and therefore can be serialized and deserialized.
Field s of class SO has the NonSerialized attribute and therefore is not serialized and deserialized along
 the other fields of the class. This example uses namespaces System.Runtime.Serialization and ei-
System.Runtime.Serialization.Formatters.Soap or System.Runtime.Serialization.Formatters.Binary.

```
[Serializable()]\class SC {
    public int ci;
}
[Serializable()]
class SO {
    public int i;
    public SC c;
    [NonSerialized()] public String s;
    public SO(int i, SC c) { this.i = i; this.c = c; s = i.ToString(); }
}

Formatter fmtr = new SoapFormatter(); // Or; new BinaryFormatter();
// Serialize o1 and o2 to file "objects"
sc = new SC();
so1 = new SO(1, sc), o2 = new SO(2, c);
Stream stream = File.Open("Objects", FileMode.Create);
fmtr.Serialize(stream, o1);
// Deserialize o1 and o2 from file; the sharing of c is lost
stream = File.Open("Objects", FileMode.Open);
so1 = (SO)fmtr.Deserialize(stream), o2 = (SO)fmtr.Deserialize(stream));
```

Example 255 Declaring and Using a Custom Attribute
The AuthorAttribute is a custom attribute holding an author name and a month (of month type: see example 15). Its legal targets are classes and methods, and it may be used many times at each target.

```
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, AllowMultiple = true)]
class AuthorAttribute : Attribute {
    public readonly String Name;
    public readonly Month Month;
    public AuthorAttribute(String name, Month month) { }
    public override String ToString() { }
}
class TestAttributes {
    [Author("Donald", Month.May)]
    public void MyMethod1() { }

    [Author("Andrzej", Month.Jul)]
    [Author("Andreas", Month.Mar)]
    public void MyMethod2() { }
}
```

* Note