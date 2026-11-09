
called, which returns a DynamicMetaObject-derived type. This type can process all of the member, method, and operator bindings for the object. Both the IDynamicMetaObjectProvider interface and the DynamicMetaObject base class are defined in the System.Dynamic namespace, and both are in the System.Core.dll assembly.

Dynamic languages, such as Python and Ruby, endow their types with DynamicMetaObject-derived types so that they can be accessed in a way appropriate for them when manipulated from other programming languages (like C#). Similarly, when accessing a COM component, the C# runtime binder will use a DynamicMetaObject-derived type that knows how to communicate with a COM component. The COM DynamicMetaObject-derived type is defined in the System.Dynamic.dll assembly.

If the type of the object being used in the dynamic expression does not implement the IDynamicMetaObjectProvider interface, then the C# compiler treats the object like an instance of an ordinary C#-defined type and performs operations on the object using reflection.

One of the limitations of dynamic is that you can only use it to access an object's instance members because the dynamic variable must refer to an object. But, there are occasions when it would be useful to dynamically invoke static members of a type where the type is determined at run time. To accomplish this, I have created a StaticMemberDynamicWrapper class that derives from System.Dynamic.DynamicObject, which implements the IDynamicMetaObjectProvider interface. The class internally uses quite a bit of reflection (covered in Chapter 23, "Assembly Loading and Reflection"). Here is the code for my StaticMemberDynamicWrapper class.

```csharp
internal sealed class StaticMemberDynamicWrapper : DynamicObject {
    private readonly TypeInfo m_type;
    public StaticMemberDynamicWrapper(Type type) { m_type = type.GetTypeInfo(); }

    public override IEnumerable<String> GetDynamicMemberNames() {
        return m_type.DeclaredMembers.Select(mi => mi.Name);
    }

    public override Boolean TryGetMember(GetMemberBinder binder, out object result) {
        result = null;
        var field = FindField(binder.Name);
        if (field != null) { result = field.GetValue(null); return true; }

        var prop = FindProperty(binder.Name, true);
        if (prop != null) { result = prop.GetValue(null, null); return true; }
        return false;
    }

    public override Boolean TrySetMember(SetMemberBinder binder, object value) {
        var field = FindField(binder.Name);
        if (field != null) { field.SetValue(null, value); return true; }

        var prop = FindProperty(binder.Name, false);
        if (prop != null) { prop.SetValue(null, value, null); return true; }
        return false;
    }

    public override Boolean TryInvokeMember(InvokeMemberBinder binder, Object[] args,
        out Object result) {
        MethodInfo method = FindMethod(binder.Name);
        if (method == null) { result = null; return false; }
        result = method.Invoke(null, args);
        return true;
    }

    private MethodInfo FindMethod(String name, Type[] paramTypes) {
        return m_type.DeclaredMethods.FirstOrDefault(mi => mi.IsPublic && mi.IsStatic
            && mi.Name == name
            && ParametersMatch(mi.GetParameters(), paramTypes));
    }

    private Boolean ParametersMatch(ParameterInfo[] parameters, Type[] paramTypes) {
        if (parameters.Length != paramTypes.Length) return false;
        for (Int32 i = 0; i < parameters.Length; i++) {
            if (parameters[i].ParameterType != paramTypes[i]) return false;
        }
        return true;
    }

    private FieldInfo FindField(String name) {
        return m_type.DeclaredFields.FirstOrDefault(fi => fi.IsPublic && fi.IsStatic
            && fi.Name == name);
    }

    private PropertyInfo FindProperty(String name, Boolean get) {
        if (get) {
            return m_type.DeclaredProperties.FirstOrDefault(
                pi => pi.Name == name && pi.GetMethod != null &&
                pi.GetMethod.IsPublic && pi.GetMethod.IsStatic);
        }
        return m_type.DeclaredProperties.FirstOrDefault(
            pi => pi.Name == name && pi.SetMethod != null &&
            pi.SetMethod.IsPublic && pi.SetMethod.IsStatic);
    }
}
```

To invoke a static member dynamically, construct an instance of this class by passing in the Type you want it to operate on and put the reference in a dynamic variable. Then, invoke the desired static member by using instance member syntax. Here is an example of how to invoke String's static Concat(String, String) method.

```csharp
dynamic stringType = new StaticMemberDynamicWrapper(typeof(String));
var r = stringType.Concat("A", "B");    // dynamically invoke String's static Concat method
Console.WriteLine(r);                   // Displays "AB"
```

## Type and Member Basics

In this chapter:

- The Different Kinds of Type Members ...... 151
- Type Visibility ...... 154
- Member Accessibility ...... 156
- Static Classes ...... 158
- Partial Classes, Structures, and Interfaces ...... 159
- Components, Polymorphism, and Versioning ...... 160

In Chapters 4 and 5, I focused on types and what operations are guaranteed to exist on all instances of any type. I also explained how all types fall into one of two categories: reference types and value types. In this and the subsequent chapters in this part, I'll show how to design types by using the different kinds of members that can be defined within a type. In Chapters 7 through 11, I'll discuss the various members in detail.

### The Different Kinds of Type Members

A type can define zero or more of the following kinds of members:

- **Constants** A constant is a symbol that identifies a never-changing data value. These symbols are typically used to make code more readable and maintainable. Constants are always associated with a type, not an instance of a type. Logically, constants are always static members. Discussed in Chapter 7, "Constants and Fields."
- **Fields** A field represents a read-only or read/write data value. A field can be static, in which case the field is considered part of the type's state. A field can also be instance (nonstatic), in which case it's considered part of an object's state. I strongly encourage you to make fields private so that the state of the type or object can't be corrupted by code outside of the defining type. Discussed in Chapter 7.
- **Instance constructors** An instance constructor is a special method used to initialize a new object's instance fields to a good initial state. Discussed in Chapter 8.
- **Type constructors** A type constructor is a special method used to initialize a type's static fields to a good initial state. Discussed in Chapter 8.
- **Methods** A method is a function that performs operations that change or query the state of a type (static method) or an object (instance method). Methods typically read and write to the fields of the type or object. Discussed in Chapter 8.
- **Operator overloads** An operator overload is a method that defines how an object should be manipulated when certain operators are applied to the object. Because not all programming languages support operator overloading, operator overload methods are not part of the Common Language Specification (CLS). Discussed in Chapter 8.
- **Conversion operators** A conversion operator is a method that defines how to implicitly or explicitly cast or convert an object from one type to another type. As with operator overload methods, not all programming languages support conversion operators, so they're not part of the CLS. Discussed in Chapter 8.
- **Properties** A property is a mechanism that allows a simple, field-like syntax for setting or querying part of the logical state of a type (static property) or object (instance property) while ensuring that the state doesn't become corrupt. Properties can be parameterless (very common) or parameterful (fairly uncommon but used frequently with collection classes). Discussed in Chapter 10, "Properties."
- **Events** A static event is a mechanism that allows a type to send a notification to one or more static or instance methods. An instance (nonstatic) event is a mechanism that allows an object to send a notification to one or more static or instance methods. Events are usually raised in response to a state change occurring in the type or object offering the event. An event consists of two methods that allow static or instance methods to register and unregister interest in the event. In addition to the two methods, events typically use a delegate field to maintain the set of registered methods. Discussed in Chapter 11, "Events."
- **Types** A type can define other types nested within it. This approach is typically used to break a large, complex type down into smaller building blocks to simplify the implementation.

Again, the purpose of this chapter isn't to describe these various members in detail but to set the stage and explain what these various members all have in common.

Regardless of the programming language you're using, the corresponding compiler must process your source code and produce metadata and Intermediate Language (IL) code for each kind of member in the preceding list. The format of the metadata is identical regardless of the source programming language you use, and this feature is what makes the CLR a *common language run time*. The metadata is the common information that all languages produce and consume, enabling code in one programming language to seamlessly access code written in a completely different programming language.

This common metadata format is also used by the CLR, which determines how constants, fields, constructors, methods, properties, and events all behave at run time. Simply stated, metadata is the key to the whole Microsoft .NET Framework development platform; it enables the seamless integration of languages, types, and objects.
