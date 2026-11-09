Chapter 9, “Parameters,” to have the compiler infer the type from the expression on the right of the assignment operator (=).

Now, let's focus on what the compiler is actually doing. When you write a line of code like this:

```
`var o = new { property1 = expression1, ... propertyN = expressionN };`
```

the compiler infers the type of each expression, creates private fields of these inferred types, creates public read-only properties for each of the fields, and creates a constructor that accepts all these expressions. The constructor’s code initializes the private read-only fields from the expression results passed in to it. In addition, the compiler overrides Object’s **Equals**, **GetHashCode**, and **ToString** methods and generates code inside all these methods. In effect, the class that the compiler generates looks like this:

```
```csharp
[CompilerGenerated]
internal sealed class <>f__AnonymousType0<...> : Object {
    private readonly t1 f1;
    public t1 p1 { get { return f1; } }

    ...

    private readonly tn fn;
    public tn pn { get { return fn; } }

    public <>f__AnonymousType0<...>(t1 a1, ..., tn an) {
        f1 = a1; ...; fn = an; // Set all fields
    }

    public override Boolean Equals(Object value) {
        // Return false if any fields don't match; else true
    }

    public override Int32 GetHashCode() {
        // Returns a hash code generated from each fields' hash code
    }

    public override String ToString() {
        // Return comma-separated set of property name = value pairs
    }
}
```
```

The compiler generates **Equals** and **GetHashCode** methods so that instances of the anonymous type can be placed in a hash table collection. The properties are readonly as opposed to read/write to help prevent the object’s hashcode from changing. Changing the hashcode for an object used as a key in a hashtable can prevent the object from being found. The compiler generates the **ToString** method to help with debugging. In the Visual Studio debugger, you can place the mouse cursor over a variable that refers to an instance of an anonymous type, and Visual Studio will invoke the **ToString** method and show the resulting string in a datatip window. By the way, Visual Studio’s **IntelliSense** will suggest the property names as you write code in the editor—a very nice feature.