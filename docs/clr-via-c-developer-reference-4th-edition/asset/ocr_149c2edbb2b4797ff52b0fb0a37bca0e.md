For example, if you define the following class.

```
public class SomeType {
}
```

it is as though you wrote the code as follows.

```
public class SomeType {
    public SomeType() : base() { }
}
```

If the class is abstract, the compiler-produced default constructor has protected accessibility; otherwise, the constructor is given public accessibility. If the base class doesn't have a parameterless constructor, the derived class must explicitly call a base constructor or the compiler will issue an error. If the class is static (sealed and abstract), the compiler will not emit a default constructor at all into the class definition.

A class can define several instance constructors. Each constructor must have a different signature, and each can have different accessibility. For verifiable code, a class's constructor must call its base class's constructor before accessing any of the inherited fields of the base class. The C# compiler will generate a call to the base class's constructor automatically if the derived class does not explicitly invoke one of the base class's constructors. Ultimately, System.Object's public, parameterless constructor gets called. This constructor does nothing—it simply returns. This is because System.Object defines no instance fields, and therefore its constructor has nothing to do.

In a few situations, an instance of a type can be created without an instance constructor being called. In particular, calling Object'MemberwiseClone method allocates memory, initializes the object's fields, and then copies the source object's bytes to the new object. Also, a constructor is usually not called when deserializing an object with the runtime serializer. The deserialization code allocates memory for the object without calling a constructor by using the System.Runtime.Serialization.Formatter's type GetUninitializedObject or GetSafeUninitializedObject (see Chapter 24, "Serialization").

> Important You should not call any virtual methods within a constructor that can affect the object being constructed. The reason is if the virtual method is overridden in the type being instantiated, the derived type's implementation of the overridden method will execute, but all of the fields in the hierarchy have not been fully initialized. Calling a virtual method would therefore result in unpredictable behavior.

```
internal sealed class SomeType {
    private Int32 m_x = ;
}
```