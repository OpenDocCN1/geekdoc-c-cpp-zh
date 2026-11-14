```
int i = 25;
object o = i; // box
Console.WriteLine(o.ToString());
```

Inside WriteLine, the following code executes:

```
private static void SampleThree()
{
    object firstParm = 5;

    object o = firstParm;
    int i = (int)o; // unbox
    string output = i.ToString();
}
```

You would never write this code yourself. However, by letting the compiler automatically convert from a specific value type to System.Object, you did let it happen. The compiler was just trying to help you. It wants you to succeed. It happily generates the boxing and unboxing statements necessary to convert any value type into an instance of System.Object. To avoid this particular penalty, you should convert your types to string instances yourself before you send them to WriteLine:

```
Console.WriteLine("A few numbers:{0}, {1}, {2}",
    25.ToString(), 32.ToString(), 50.ToString());
```

This code uses the known type of integer, and value types (integers) are never implicitly converted to System.Object. This common example illustrates the first rule to avoid boxing: Watch for implicit conversions to System.Object. Value types should not be substituted for System.Object if you can avoid it.

Another common case in which you might inadvertently substitute a value type for System.Object is when you place value types in .NET 1.x collections. You should use the generic collections added in the 2.0 version of the .NET Base Class Library (BCL) over the 1.x object based collections. However, some components in the .NET BCL still use the 1.x style collections. You should understand the issues and how to avoid them.

The first incarnation of the .NET Framework collections store references to System.Object instances. Anytime you add a value type to a collection, it goes in a box. Anytime you remove an object from a collection, it gets copied from the box. Taking an object out of the box always makes a copy.