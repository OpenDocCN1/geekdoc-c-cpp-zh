However, this code won't compile. The problem is variables passed by reference to a method must be of the same type as declared in the method signature. In other words, Swap expects two Object references, not two String references. To swap the two String references, you must do the following.

```
public static void SomeMethod() {
String s1 = "Jeffrey";
String s2 = "Richter";

// Variables that are passed by reference
// must match the method expects.
Object o1 = s1, o2 = s2;
Swap(ref o1, ref o2);

// Now cast the objects back to strings.
s1 = (String)o1;
s2 = (String)o2;

Console.WriteLine(s1); // Displays "Richter"
Console.WriteLine(s2); // Displays "Jeffrey"
}
```

This version of SomeMethod does compile and execute as expected. The reason why the parameters passed must match the parameters expected by the method is to ensure that type safety is preserved. The following code, thankfully won't compile, how sure type safety is compromised.

```
internal sealed class SomeType {
public Int32 m_val;
}
```

```
public sealed class Program {
public static void Main() {
SomeType st;
}
```

```
// The following line generates error CS1503: Argument '1':
// cannot convert from 'ref SomeType' to 'ref object'
GetObject(out st);
```

```
Console.WriteLine(st.m_val);
```

```
public static void GetAnObject(out Object o) {
o = new String('X', 100);
}
```

In this code, Main expects GetAnObject to return a SomeType object. However, GetAnObject's signature expects a reference to Object, GetAnObject is free to initialize o to an object of any type. In this example, when GetAnObject returned Main, st would refer to a String, which is clearly not a SomeType object, and the call to Console.WriteLine would certainly fail. Fortunately, the C# compiler won't compile the preceding code because st is a reference to SomeType, but GetAnObject requires a reference to an Object.