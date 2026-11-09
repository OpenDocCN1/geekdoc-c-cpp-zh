

**members** 变量是对一个数组的引用，数组中的每个元素标识由 **MyType** 及其任何基类型（如 **System.Object**）定义的公共成员。如果你查询标识 **ToString** 方法的 **MemberInfo** 元素的 **DeclaringType** 属性，你会看到返回的是 **MyType**，因为 **MyType** 声明了一个 **ToString** 方法。另一方面，如果你查询标识 **Equals** 方法的 **MemberInfo** 元素的 **DeclaringType** 属性，你会看到返回的是 **System.Object**，因为 **Equals** 是由 **System.Object** 声明的，而不是由 **MyType** 声明的。**ReflectedType** 属性总是返回 **MyType**，因为这是在调用 **GetMembers** 执行反射时指定的类型。

调用 **GetMembers** 返回的数组中的每个元素都是层次结构中某个具体类型的一个引用（除非指定了 **BindingFlags.DeclaredOnly** 标志）。虽然 **Type.GetMembers** 方法返回类型的所有成员，但 **Type** 也提供了返回特定成员类型的方法。例如，**Type** 提供了 **GetNestedTypes**、**GetFields**、**GetConstructors**、**GetMethods**、**GetProperties** 和 **GetEvents**。这些方法都返回数组，其中每个元素分别是 **Type** 对象、**FieldInfo** 对象、**ConstructorInfo** 对象、**MethodInfo** 对象、**PropertyInfo** 对象或 **EventInfo** 对象的引用。

图 23-2 总结了应用程序用来遍历反射对象模型的类型。通过 AppDomain，你可以发现加载到其中的程序集。通过程序集，你可以发现构成它的模块。通过程序集或模块，你可以发现它定义的类型。通过类型，你可以发现其嵌套类型、字段、构造函数、方法、属性和事件。命名空间不属于此层次结构，因为它们只是类型的语法集合。如果你想列出程序集中定义的所有命名空间，你需要枚举该程序集中的所有类型并查看它们的 **Namespace** 属性。

通过类型，还可以发现它实现的接口（稍后我将展示如何做到这一点）。通过构造函数、方法、属性访问器方法或事件的添加/移除方法，你可以调用 **GetParameters** 方法获取 **ParameterInfo** 对象的数组，该数组告诉你成员参数的类型。你还可以查询只读的 **ReturnParameter** 属性来获取一个 **ParameterInfo** 对象，以获得有关成员返回值的详细信息。对于泛型类型或方法，你可以调用 **GetGenericArguments** 方法获取类型参数的集合。最后，对于这些项目中的任何一个，你都可以调用 **GetCustomAttributes** 方法获取应用于它们的自定义属性集合。

**InterfaceMethods** 和 **TargetMethods** 数组并行对应；也就是说，**InterfaceMethods[0]** 标识接口的 **MethodInfo**，而 **TargetMethods[0]** 标识由实现此接口方法的类型所定义的方法。下面是一些代码，展示如何发现类型定义的接口和接口方法：

```csharp
using System;
using System.Reflection;

// Define two interfaces for testing
internal interface IBookRetailer : IDisposable {
    void Purchase();
    void ApplyDiscount();
}

internal interface IMusicRetailer {
    void Purchase();
}

// This class implements 2 interfaces defined by this assembly
// and 1 interface defined by another assembly
internal sealed class MyRetailer : IBookRetailer, IMusicRetailer, IDisposable {
    // IBookRetailer methods
    void IBookRetailer.Purchase() { }
    public void ApplyDiscount() { }

    // IMusicRetailer method
    void IMusicRetailer.Purchase() { }

    // IDisposable method
    public void Dispose() { }

    // MyRetailer method (not an interface method)
    public void Purchase() { }
}

public static class Program {
    public static void Main() {
        // Find interfaces implemented by MyRetailer where the interface is
        // defined in our own assembly. This is accomplished using a delegate
        // to a filter method that we pass to FindInterfaces.
        Type t = typeof(MyRetailer);
        Type[] interfaces = t.FindInterfaces(TypeFilter, typeof(Program).Assembly);
        Console.WriteLine(
            "MyRetailer implements the following interfaces (defined in this assembly):");

        // Show information about each interface
        foreach (Type i in interfaces) {
            Console.WriteLine("\nInterface: " + i);

            // Get the type methods that map to the interface's methods
            InterfaceMapping map = t.GetInterfaceMap(i);
            for (Int32 m = 0; m < map.InterfaceMethods.Length; m++) {
                // Display the interface method name and which
                // type method implements the interface method.
                Console.WriteLine("  {0} is implemented by {1}",
                    map.InterfaceMethods[m], map.TargetMethods[m]);
            }
        }
    }

    // Returns true if type matches filter criteria
    private static Boolean TypeFilter(Type t, Object filterCriteria) {
        // Return true if the interface is defined in assembly identified by filterCriteria
        return t.Assembly == filterCriteria;
    }
}
```

当你编译并运行上述代码时，你会得到以下输出：

```
MyRetailer implements the following interfaces (defined in this assembly):

Interface: IBookRetailer
    Void Purchase() is implemented by Void IBookRetailer.Purchase()
    Void ApplyDiscount() is implemented by Void ApplyDiscount()

Interface: IMusicRetailer
    Void Purchase() is implemented by Void IMusicRetailer.Purchase()
```

请注意，`IDisposable` 接口没有出现在输出中，因为这个接口不是在 EXE 文件的程序集中声明的。

### 调用类型的成员

既然你已经知道如何发现类型定义的成员，你可能想要调用其中一个成员。*调用*（invoke）的含义取决于被调用的成员类型。调用 `FieldInfo` 可以让你获取或设置字段的值，调用 `ConstructorInfo` 可以让你创建类型的实例并向构造函数传递参数，调用 `MethodInfo` 可以让你调用方法、传递参数并获取其返回值，调用 `PropertyInfo` 可以让你调用属性的 get 或 set 访问器方法，调用 `EventInfo` 可以让你添加或移除事件处理程序。

让我们先讨论如何调用方法，因为这是你可以调用的最复杂的成员。然后我们将讨论如何调用其他成员。`Type` 类提供了一个 `InvokeMember` 方法，可以让你调用成员。`InvokeMember` 有多个重载版本。我将讨论其中一个较常见的重载；其他重载的工作方式类似。

```csharp
public abstract class Type : MemberInfo, ... {
    public Object InvokeMember(
        String name,             // Name of member
        BindingFlags invokeAttr, // How to look up members
        Binder binder,           // How to match members and arguments
        Object target,           // Object to invoke member on
        Object[] args,           // Arguments to pass to method
        CultureInfo culture);    // Culture used by some binders
}
```

当你调用 **InvokeMember** 时，它会在类型的成员中搜索匹配项。如果没有找到匹配项，会抛出 **System.MissingMethodException**、**System.MissingFieldException** 或 **System.MissingMemberException** 异常。如果找到匹配项，**InvokeMember** 会调用该成员。如果成员有返回值，**InvokeMember** 会将其返回给你。如果成员没有返回值，**InvokeMember** 会返回 null。如果你调用的成员抛出了异常，**InvokeMember** 会捕获该异常并抛出一个新的 **System.Reflection.TargetInvocationException**。**TargetInvocationException** 对象的 **InnerException** 属性将包含被调用方法实际抛出的异常。就我个人而言，我不喜欢这种行为。我更希望 **InvokeMember** 不包装异常，而是让它直接传递出来。

在内部，**InvokeMember** 执行两个操作。首先，它必须选择要调用的适当成员——这称为*绑定*（binding）。其次，它必须实际调用成员——这称为*调用*（invoking）。当你调用 **InvokeMember** 时，你传递一个字符串作为 *name* 参数，指示你想要 **InvokeMember** 绑定的成员名称。但是，类型可能提供多个同名成员。毕竟，一个方法可能有多个重载版本，或者一个方法和一个字段可能同名。当然，**InvokeMember** 必须先绑定到单个成员，然后才能调用它。传递给 **InvokeMember** 的所有参数（*target* 参数除外）都用于帮助 **InvokeMember** 决定绑定到哪个成员。让我们仔细看看这些参数。

**binder** 参数标识一个对象，其类型派生自抽象 **System.Reflection.Binder** 类型。派生自 **Binder** 的类型封装了 **InvokeMember** 应如何选择单个成员的规则。**Binder** 基类型定义了抽象虚方法，如 **BindToField**、**BindToMethod**、**ChangeType**、**ReorderArgumentArray**、**SelectMethod** 和 **SelectProperty**。在内部，**InvokeMember** 通过 **InvokeMember** 的 **binder** 参数传入的 **Binder** 对象调用这些方法。

Microsoft 定义了一个内部的（未记录的）具体类型，称为 **System.DefaultBinder**，它派生自 **Binder**。这个 **DefaultBinder** 类型随 FCL 一起发布，Microsoft 期望几乎所有人都使用这个绑定器。一些编译器供应商会定义自己的 **Binder** 派生类型，并将其发布在由其编译器生成的代码所使用的运行时库中。^1 当你向 **InvokeMember** 的 **binder** 参数传递 **null** 时，它将使用一个

^1 本书附带的代码包含一个 **SimpleBinder** 类的源代码，演示如何定义自己的 **Binder** 派生类型。

