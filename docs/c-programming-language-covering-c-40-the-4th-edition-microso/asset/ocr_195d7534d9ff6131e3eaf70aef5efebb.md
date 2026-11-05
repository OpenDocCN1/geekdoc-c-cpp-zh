Likewise, a value of type object or a value of an interface type can be converted back to a class type without changing the reference (but, of course, a runtime type check is required in this case).

Since structs are not reference types, these operations are implemented differently for struct types. When a value of a struct type is converted to type object or to an interface type that is implemented by the struct, a boxing operation takes place. Likewise, when a value of type object or a value of an interface type is converted back to a struct type, an unboxing operation takes place. A key difference from the same operations on class types is that boxing and unboxing copy the struct value either into or out of the boxed instance. Thus, following a boxing or unboxing operation, changes made to the unboxed struct are not reflected in the boxed struct.

> **ERIC LIPPERT** This is yet another reason why value types should be immutable: If a change is impossible, then the fact that changes made to an unboxed struct are not reflected in the boxed struct becomes irrelevant. Rather than dealing with the unexpected and confusing semantics, avoid them altogether.

When a struct type overrides a virtual method inherited from System.Object (such as Equals, GetHashCode, or ToString), invocation of the virtual method through an instance of the struct type does not cause boxing to occur. This is true even when the struct is used as a type parameter and the invocation occurs through an instance of the type parameter type. For example:

```
using System;
struct Counter
{
    int value;
    public override string ToString() {
        value++;
        return value.ToString();
    }
}
class Program
{
    static void Test<T>() where T: new() {
        T x = new T();
        Console.WriteLine(x.ToString());
        Console.WriteLine(x.ToString());
        Console.WriteLine(x.ToString());
    }
    static void Main() {
        Test<Counter>();
    }
}
```