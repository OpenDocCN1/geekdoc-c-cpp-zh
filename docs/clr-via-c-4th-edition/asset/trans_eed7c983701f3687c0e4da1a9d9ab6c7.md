
被调用，并返回一个派生自 DynamicMetaObject 的类型。该类型可以处理对象的所有成员、方法和运算符绑定。IDynamicMetaObjectProvider 接口和 DynamicMetaObject 基类都定义在 System.Dynamic 命名空间中，并且都位于 System.Core.dll 程序集中。

动态语言（如 Python 和 Ruby）为其类型赋予派生自 DynamicMetaObject 的类型，以便当从其他编程语言（如 C#）操作这些类型时，能够以适合它们的方式访问。类似地，当访问 COM 组件时，C# 运行时绑定器将使用一个知道如何与 COM 组件通信的、派生自 DynamicMetaObject 的类型。用于 COM 的、派生自 DynamicMetaObject 的类型定义在 System.Dynamic.dll 程序集中。

如果 dynamic 表达式中使用的对象类型没有实现 IDynamicMetaObjectProvider 接口，那么 C# 编译器会将该对象视为普通 C# 定义类型的实例，并使用反射对该对象执行操作。

dynamic 的局限性之一是，你只能使用它来访问对象的实例成员，因为 dynamic 变量必须引用对象。但是，有时动态调用某个类型的静态成员会很有用，而该类型是在运行时确定的。为实现这一点，我创建了一个 StaticMemberDynamicWrapper 类，它派生自 System.Dynamic.DynamicObject，而后者实现了 IDynamicMetaObjectProvider 接口。该类在内部使用了相当多的反射（第23章“程序集加载和反射”中已介绍）。以下是我的 StaticMemberDynamicWrapper 类的代码。

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

要动态调用静态成员，请通过传入希望其操作的 Type 来构造此类的实例，并将该引用放入 dynamic 变量中。然后，使用实例成员语法调用所需的静态成员。以下示例演示如何调用 String 的静态 Concat(String, String) 方法。

```csharp
dynamic stringType = new StaticMemberDynamicWrapper(typeof(String));
var r = stringType.Concat("A", "B");    // dynamically invoke String's static Concat method
Console.WriteLine(r);                   // Displays "AB"
```

## 类型与成员基础

本章内容：

- 不同类型的类型成员 ...... 151
- 类型可见性 ...... 154
- 成员可访问性 ...... 156
- 静态类 ...... 158
- 分部类、结构和接口 ...... 159
- 组件、多态和版本控制 ...... 160

在第4章和第5章中，我重点介绍了类型，以及对于任何类型的实例都保证存在哪些操作。我还解释了所有类型如何归入两类之一：引用类型和值类型。在本部分本章及后续章节中，我将展示如何通过使用可在类型内定义的不同种类的成员来设计类型。在第7章至第11章中，我将详细讨论各种成员。

### 不同类型的类型成员

一个类型可以定义以下种类成员中的零个或多个：

- **常量** 常量是标识永不改变的数据值的符号。这些符号通常用于使代码更易读、更易维护。常量始终与类型关联，而不是与类型的实例关联。从逻辑上说，常量始终是静态成员。详见第7章“常量和字段”。
- **字段** 字段表示只读或可读写的数据值。字段可以是静态的，此时该字段被视为类型状态的一部分。字段也可以是实例（非静态）的，此时它被视为对象状态的一部分。我强烈建议将字段设为私有，这样类型或对象的状态就不会被定义类型之外的代码破坏。详见第7章。
- **实例构造函数** 实例构造函数是一种特殊方法，用于将新对象的实例字段初始化为合适的初始状态。详见第8章。
- **类型构造函数** 类型构造函数是一种特殊方法，用于将类型的静态字段初始化为合适的初始状态。详见第8章。
- **方法** 方法是执行操作的函数，这些操作会更改或查询类型（静态方法）或对象（实例方法）的状态。方法通常读取和写入类型或对象的字段。详见第8章。
- **运算符重载** 运算符重载是一种方法，它定义当某些运算符应用于对象时，应如何操作该对象。由于并非所有编程语言都支持运算符重载，因此运算符重载方法不属于公共语言规范（CLS）的一部分。详见第8章。
- **转换运算符** 转换运算符是一种方法，它定义如何隐式或显式地将对象从一种类型强制转换或转换为另一种类型。与运算符重载方法一样，并非所有编程语言都支持转换运算符，因此它们不属于 CLS 的一部分。详见第8章。
- **属性** 属性是一种机制，它允许使用简单的、类似字段的语法来设置或查询类型（静态属性）或对象（实例属性）的逻辑状态的一部分，同时确保该状态不会被破坏。属性可以无参数（非常常见），也可以带参数（相当少见，但经常与集合类一起使用）。详见第10章“属性”。
- **事件** 静态事件是一种机制，它允许类型向一个或多个静态或实例方法发送通知。实例（非静态）事件是一种机制，它允许对象向一个或多个静态或实例方法发送通知。事件通常是在提供事件类型或对象中发生状态变化时引发的。事件由两个方法组成，这两个方法允许静态或实例方法注册和注销对该事件的关注。除了这两个方法之外，事件通常还使用一个委托字段来维护已注册方法的集合。详见第11章“事件”。
- **类型** 类型可以在其内部定义其他类型（嵌套类型）。这种方法通常用于将大型、复杂的类型分解为更小的构建块，以简化实现。

同样，本章的目的不是详细描述这些各种成员，而是铺陈背景并解释这些各种成员的共同点。

无论你使用哪种编程语言，相应的编译器都必须处理你的源代码，并为前面列表中的每种成员生成元数据和中间语言（IL）代码。无论你使用哪种源编程语言，元数据的格式都是相同的，而这一特性正是使 CLR 成为 *公共语言运行时* 的原因。元数据是所有语言都会生成和使用的一种公共信息，它使一种编程语言中的代码能够无缝访问用另一种完全不同的编程语言编写的代码。

CLR 也使用这种通用元数据格式，它决定常量、字段、构造函数、方法、属性和事件在运行时的行为方式。简而言之，元数据是整个 Microsoft .NET Framework 开发平台的关键；它实现了语言、类型和对象的无缝集成。
