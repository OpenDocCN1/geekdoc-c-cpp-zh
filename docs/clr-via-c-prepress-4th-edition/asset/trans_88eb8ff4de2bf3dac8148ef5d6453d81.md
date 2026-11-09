
```
foreach (MemberInfo mi in t.GetTypeInfo().DeclaredMembers) {
    String typeName = String.Empty;
    if (mi is Type) typeName = "(Nested) Type";
    if (mi is FieldInfo) typeName = "FieldInfo";
    if (mi is MethodInfo) typeName = "MethodInfo";
    if (mi is ConstructorInfo) typeName = "ConstructorInfo";
    if (mi is PropertyInfo) typeName = "PropertyInfo";
    if (mi is EventInfo) typeName = "EventInfo";
    Show(2, "{0}: {1}", typeName, mi);
}
}
private static void Show(Int32 indent, String format, params Object[] args) {
    Console.WriteLine(new String(' ', 3 * indent) + format, args);
}
```

编译并运行这段代码时，会产生大量输出。下面展示其中一小部分示例：

```
Assembly: mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089
Type: System.Object
    MethodInfo: System.String ToString()
    MethodInfo: Boolean Equals(System.Object)
    MethodInfo: Boolean Equals(System.Object, System.Object)
    MethodInfo: Boolean ReferenceEquals(System.Object, System.Object)
    MethodInfo: Int32 GetHashCode()
    MethodInfo: System.Type GetType()
    MethodInfo: Void Finalize()
    MethodInfo: System.Object MemberwiseClone()
    MethodInfo: Void FieldSetter(System.String, System.String, System.Object)
    MethodInfo: Void FieldGetter(System.String, System.String, System.Object ByRef)
    MethodInfo: System.Reflection.FieldInfo GetFieldInfo(System.String, System.String)
    ConstructorInfo: Void .ctor()
Type: System.Collections.Generic.IComparer`1[T]
    MethodInfo: Int32 Compare(T, T)
Type: System.Collections.IEnumerator
    MethodInfo: Boolean MoveNext()
    MethodInfo: System.Object get_Current()
    MethodInfo: Void Reset()
    PropertyInfo: System.Object Current
Type: System.IDisposable
    MethodInfo: Void Dispose()
Type: System.Collections.Generic.IEnumerator`1[T]
    MethodInfo: T get_Current()
    PropertyInfo: T Current
Type: System.ArraySegment`1[T]
    MethodInfo: T[] get_Array()
    MethodInfo: Int32 get_Offset()
    MethodInfo: Int32 get_Count()
    MethodInfo: Int32 GetHashCode()
    MethodInfo: Boolean Equals(System.Object)
    MethodInfo: Boolean Equals(System.ArraySegment`1[T])
    MethodInfo: Boolean op_Equality(System.ArraySegment`1[T], System.ArraySegment`1[T])
    MethodInfo: Boolean op_Inequality(System.ArraySegment`1[T], System.ArraySegment`1[T])
    ConstructorInfo: Void .ctor(T[])
    ConstructorInfo: Void .ctor(T[], Int32, Int32)
    PropertyInfo: T[] Array
    PropertyInfo: Int32 Offset
    PropertyInfo: Int32 Count
    FieldInfo: T[] _array
    FieldInfo: Int32 _offset
```

由于 MemberInfo 是成员层次结构的根，因此我们有必要再稍微讨论一下它。表 23-1 列出了 MemberInfo 类提供的几个只读属性和方法。这些属性和方法对于类型的所有成员都是通用的。别忘了 System.TypeInfo 派生自 MemberInfo，因此 TypeInfo 也提供表 23-1 中所示的所有属性。

**表 23-1** 所有 MemberInfo 派生类型共有的属性和方法

| 成员名称 | 成员类型 | 描述 |
| --- | --- | --- |
| Name | String 属性 | 返回成员的名称。 |
| DeclaringType | Type 属性 | 返回声明该成员的 `Type`。 |
| Module | Module 属性 | 返回声明该成员的 `Module`。 |
| CustomAttributes | 返回 IEnumerable<CustomAttributeData> 的属性 | 返回一个集合，其中每个元素标识一个应用于该成员的自定义属性实例。自定义属性可应用于任何成员。尽管 `Assembly` 并不派生自 `MemberInfo`，但它提供了可用于程序集的相同属性。 |

查询 DeclaredMembers 所返回集合的每个元素都是对层次结构中某个具体类型的引用。尽管 TypeInfo 的 DeclaredMembers 属性返回该类型的所有成员，但 TypeInfo 也提供了一些方法，用于返回指定字符串名称所对应的特定成员类型。例如，TypeInfo 提供 GetDeclaredNestedType、GetDeclaredField、GetDeclaredMethod、GetDeclaredProperty 和 GetDeclaredEvent。这些方法分别返回对 TypeInfo 对象、FieldInfo 对象、MethodInfo 对象、PropertyInfo 对象或 EventInfo 对象的引用。此外还有 GetDeclaredMethods 方法，它返回一组 MethodInfo 对象，描述与指定字符串名称匹配的方法。

图 23-2 总结了应用程序用来遍历反射对象模型所使用的类型。从 AppDomain 可以找到加载到其中的程序集。从程序集可以找到构成它的模块。从程序集或模块可以找到它定义的类型。从类型可以找到它的嵌套类型、字段、构造函数、方法、属性和事件。命名空间不属于此层次结构，因为它们只是类型在语法上的集合。如果要列出程序集中定义的所有命名空间，需要枚举该程序集中的所有类型，并查看它们的 Namespace 属性。

从类型还可以找到它实现的接口。并且，从构造函数、方法、属性访问器方法或事件添加/移除方法中，可以调用 GetParameters 方法获取 ParameterInfo 对象数组，该数组会告诉你成员参数的类型。还可以查询只读的 ReturnParameter 属性，以获取一个 ParameterInfo 对象，从而了解成员返回类型的详细信息。对于泛型类型或方法，可以调用 GetGenericArguments 方法获取类型参数集合。最后，对于上述任何项，都可以查询 CustomAttributes 属性，以获取应用于它们的自定义属性集合。

![](img/3f2c86949cdef7e2f9e27c37c607b28e_598_0.png)

**图 23-2** 应用程序用来遍历反射对象模型的类型。

## 调用类型的成员

现在你已知道如何发现类型定义的成员，可能还想调用其中一个成员。调用的含义取决于被调用成员的种类。表 23-4 列出了要调用每种成员时应调用的方法。

**表 23-4** 如何调用成员

| 成员类型 | 调用成员的方法 |
| --- | --- |
| FieldInfo | 调用 `GetValue` 获取字段的值。<br>调用 `SetValue` 设置字段的值。 |
| ConstructorInfo | 调用 `Invoke` 构造该类型的实例并调用构造函数。 |
| MethodInfo | 调用 `Invoke` 调用该类型的方法。 |
| PropertyInfo | 调用 `GetValue` 调用属性的 get 访问器方法。<br>调用 `SetValue` 调用属性的 set 访问器方法。 |
| EventInfo | 调用 `AddEventHandler` 调用事件的 add 访问器方法。<br>调用 `RemoveEventHandler` 调用事件的 remove 访问器方法。 |

PropertyInfo 类型表示属性的元数据信息（如第 10 章“属性”所述）；也就是说，PropertyInfo 提供 CanRead、CanWrite 和 PropertyType 只读属性。这些属性指示属性是否可读或可写，以及属性是什么数据类型。PropertyInfo 还具有只读的 GetMethod 和 SetMethod 属性，它们返回表示获取和设置属性值的方法的 MethodInfo 对象。PropertyInfo 的 GetValue 和 SetValue 方法是为了方便而存在的；在内部，它们会调用相应的 MethodInfo 对象。为了支持带参数的属性（C# 索引器），GetValue 和 SetValue 方法提供了一个 Object[] 类型的索引参数。

EventInfo 类型表示事件的元数据信息（如第 11 章“事件”所述）。EventInfo 类型提供只读的 EventHandlerType 属性，返回事件基础委托的 Type。EventInfo 类型还具有只读的 AddMethod 和 RemoveMethod 属性，它们返回与向事件添加委托或从事件移除委托的方法相对应的 MethodInfo 对象。要添加或移除委托，可以调用这些 MethodInfo 对象，也可以调用 EventInfo 更方便的 AddEventHandler 和 RemoveEventHandler 方法。

下面的示例应用程序演示了使用反射访问类型成员的各种方式。SomeType 类表示一个具有各种成员的类型：一个私有字段（m_someField）、一个公共构造函数（SomeType），它接受通过引用传递的 Int32 参数、一个公共方法（ToString）、一个公共属性（SomeProp）和一个公共事件（SomeEvent）。定义了 SomeType 类型后，我提供了三个不同的方法，它们使用反射访问 SomeType 的成员。每个方法都以不同方式使用反射来完成同一件事：

- `BindToMemberThenInvokeTheMember` 方法演示如何绑定到成员并在稍后调用它。
- `BindToMemberCreateDelegateToMemberThenInvokeTheMember` 方法演示如何绑定到对象或成员，然后创建一个引用该对象或成员的委托。通过委托进行调用非常快，而且这种技术能带来更快的
