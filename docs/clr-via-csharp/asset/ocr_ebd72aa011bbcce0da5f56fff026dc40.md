Compilers tend to use the **call** instruction when calling methods defined by a value type since value types are sealed. This implies that there can be no polymorphism even for their virtual methods, which causes the performance of the call to be faster. In addition, the nature of a value type instance guarantees it can never be **null**, so a **NullReferenceException** will never be thrown. Finally, if you were to call a value type's virtual method virtually, the CLR would need to have a reference to the value type's object in order to refer to the method table within it. This requires boxing the value type. Boxing puts more pressure on the heap, forcing more frequent garbage collections and hurting performance.

Regardless of whether **call** or **callvirt** is used to call an instance or virtual method, these methods always receive a hidden **this** argument as the method's first parameter. The **this** argument refers to the object being operated on.

When designing a type, you should try to minimize the number of virtual methods you define. First, calling a virtual method is slower than calling a nonvirtual method. Second, virtual methods cannot be inlined by the JIT compiler, which further hurts performance. Third, virtual methods make versioning of components more brittle, as described in the next section. Fourth, when defining a base type, it is common to offer a set of convenience overloaded methods. If you want these methods to be polymorphic, the best thing to do is to make the most complex method virtual and leave all of the convenience overloaded methods nonvirtual. By the way, following this guideline will also improve the ability to version a component without adversely affecting the derived types. Here is an example:

```
````csharp
public class Set {
    private Int32 m_length = 0;

    // This convenience overload is not virtual
    public Int32 Find(Object value) {
        return Find(value, 0, m_length);
    }

    // This convenience overload is not virtual
    public Int32 Find(Object value, Int32 startIndex) {
        return Find(value, startIndex, m_length - startIndex);
    }

    // The most feature-rich method is virtual and can be overridden
    public virtual Int32 Find(Object value, Int32 startIndex, Int32 endIndex) {
        // Actual implementation that can be overridden goes here...
    }

    // Other methods go here
}
````
```