```
private readonly tn fn;
public tn get { return fn; }
```

```
public <?>f_AnonymousType<...>(tl a1, ..., tn an) {
fl1 = a1; ... fn = an; // Set all fields
}
```

```
public override Boolean Equals(Object value) {
// Return false if any fields don't match;
}
```

```
public override Int32 GetHashCode() {
// Returns a hash code generated from each fields'\n}
```

```
public override String ToString() {
// Return comma-separated set of property name = value pairs
}
```

The compiler generates Equals and GetHashCode methods so that instances of the anonymous type can be placed in a hash table. The properties are readonly as opposed to read/write to prevent the object's hashcode from changing. Changing the hashcode for an object used in a hashtable can prevent the object from being found. The compiler generates the ToString method to help with debugging. In the Visual Studio debugger, you can place the mouse cursor over a variable that refers to an instance of an anonymous type, and Visual Studio will invoke the ToString method and show the resulting string in a datatip window. By way, Visual Studio's IntelliSense will suggest the properties as you write code in the editor—a very nice feature.

The compiler supports two anonymous syntaxes for declaring a property inside an anonymous type where it can infer the property names and types from variables.

```
String Name = "Grant";
DateTime dt = DateTime.Now;
```

```
// Anonymous type with two properties
// 1. Name property set to Grant
// 2. Int32 Year property set to the Year inside the dt
var o2 = new { Name, Year = dt.Year };
```

In this example, the compiler determines that the first property should be called Name. Because Name is the name of a local variable, the compiler sets the type of the property to be the same type as the local variable: String. For the second property, the compiler uses the type of the field/property: Year is an Int32 property of the DateTime class, and therefore the Year property in the anonymous type will also be an Int32. Now, when the compiler constructs an instance of this anonymous type, it will set the instance's Name property to the same value that is in the Name local variable so Name property will return to the same "Grant" string. The compiler will set the instance's Year property to the same value that is returned from dt's Year property.