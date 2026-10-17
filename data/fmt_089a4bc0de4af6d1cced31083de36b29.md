
```csharp
WriteLine(vecType.IsClass);         // writes true

WriteLine(vecType.IsEnum);          // writes false

WriteLine(vecType.IsPrimitive);     // writes false

WriteLine(vecType.IsValueType);    // writes false
```

最后，你还可以检索类型所定义的程序集的引用。这作为对 `System.Reflection.Assembly` 类实例的引用返回，该类将在稍后进行检查：

```csharp
Type t = typeof(Vector);

Assembly containingAssembly = t.Assembly;
```

#### Methods

`System.Type` 的大多数方法用于获取对应数据类型的成员的详细信息——构造函数、属性、方法、事件等。存在相当多的此类方法，但它们都遵循相同的模式。例如，两个方法检索数据类型的详细信息：`GetMethod` 和 `GetMethods`。`GetMethod` 返回对 `System.Reflection.MethodInfo` 对象的引用，其中包含有关方法的信息。`GetMethods` 返回此类引用的数组。顾名思义，区别在于 `GetMethods` 返回有关所有方法的信息，而 `GetMethod` 返回有关仅具有指定参数列表的一个方法的信息。两种方法都有重载，可接受一个额外的参数，即 `BindingFlags` 枚举值，指示应返回哪些成员——例如，是否返回公共成员、实例成员、静态成员等。

例如，`GetMethods` 的最简单重载不带参数，并返回数据类型的所有公共方法的详细信息：

```csharp
Type t = typeof(double);

foreach (MethodInfo nextMethod in t.GetMethods())

{

    // etc.

}
```

遵循相同模式的 `Type` 的成员方法如下表所示。请注意，复数名称返回数组。

| Type of object returned | Method(s) |
|---|---|
| `ConstructorInfo` | `GetConstructor`, `GetConstructors` |
| `EventInfo` | `GetEvent`, `GetEvents` |
| `FieldInfo` | `GetField`, `GetFields` |
| `MemberInfo` | `GetMember`, `GetMembers`, `GetDefaultMembers` |
| `MethodInfo` | `GetMethod`, `GetMethods` |
| `PropertyInfo` | `GetProperty`, `GetProperties` |

`GetMember` 和 `GetMembers` 方法返回有关数据类型任何或所有成员的详细信息，无论这些成员是构造函数、属性、方法等。

#### The `TypeView` Example

本节通过一个简短的示例 `TypeView` 演示 `Type` 类的一些功能，你可以使用它来列出数据类型的成员。该示例演示了如何将 `TypeView` 用于 `double`；然而，你只需更改示例代码中的一行，就可以用任何其他数据类型替换此类型。

运行应用程序的结果是向控制台输出以下内容：

```
Analysis of type Double

Type Name: Double

Full Name: System.Double

Namespace: System

Base Type: ValueType
```

公共成员：
- System.Double Method IsInfinity
- System.Double Method IsPositiveInfinity
- System.Double Method IsNegativeInfinity
- System.Double Method IsNaN
- System.Double Method CompareTo
- System.Double Method CompareTo
- System.Double Method Equals
- System.Double Method op_Equality
- System.Double Method op_Inequality
- System.Double Method op_LessThan
- System.Double Method op_GreaterThan
- System.Double Method op_LessThanOrEqual
- System.Double Method op_GreaterThanOrEqual
- System.Double Method Equals
- System.Double Method GetHashCode
- System.Double Method ToString
- System.Double Method ToString
- System.Double Method ToString
- System.Double Method ToString
- System.Double Method Parse
- System.Double Method Parse
- System.Double Method Parse
- System.Double Method Parse
- System.Double Method TryParse
- System.Double Method TryParse
- System.Double Method GetTypeCode
- System.Object Method GetType
- System.Double Field MinValue
- System.Double Field MaxValue
- System.Double Field Epsilon
- System.Double Field NegativeInfinity
- System.Double Field PositiveInfinity
- System.Double Field NaN

控制台显示数据类型的名称、完整名称、命名空间以及基类型的名称。接下来，它简单地遍历该数据类型的所有公共实例成员，并显示每个成员的声明类型、成员类型（方法、字段等）和成员名称。声明类型是实际声明该类型成员的类的名称（例如，如果成员是在 `System.Double` 中定义或重写的，则显示 `System.Double`；如果成员只是从基类继承的，则显示相应基类型的名称）。

`TypeView` 不显示方法的签名，因为你是通过 `MemberInfo` 对象检索所有公共实例成员的详细信息，而 `MemberInfo` 对象不提供参数信息。要检索这些信息，你需要引用 `MethodInfo` 和其他更具体的对象，这意味着你需要分别获取每种成员类型的详细信息。

`TypeView` 的示例代码使用了以下依赖项和命名空间：

#### 依赖项

```
NETStandard.Library
```

#### 命名空间

- `System`
- `System.Reflection`
- `System.Text`
- `static System.Console`

`TypeView` 确实显示了所有公共实例成员的详细信息；但对于 `double` 类型，唯一定义的详细信息是字段和方法。`TypeView` 的代码如下。首先，你需要添加一些 `using` 语句：

```
using System;

using System.Reflection;

using System.Text;

using static System.Console;
```

你需要 `System.Text`，因为你使用 `StringBuilder` 对象来构建文本。整个代码在一个类 `Program` 中，该类有几个静态方法和一个静态字段，即一个名为 `OutputText` 的 `StringBuilder` 实例，用于构建要在消息框中显示的文本。`Main` 方法和类声明如下：

```csharp
class Program

{

    private static StringBuilder OutputText = new StringBuilder();

    static void Main()

    {

        // modify this line to retrieve details of any other data type

        Type t = typeof(double);

        AnalyzeType(t);

        WriteLine($"Analysis of type {t.Name}");

        WriteLine(OutputText.ToString());

        ReadLine();

    }

}
```

`Main` 方法的实现首先声明一个 `Type` 对象来表示你选择的数据类型。然后调用 `AnalyzeType` 方法，该方法从 `Type` 对象中提取信息并用于构建输出文本。最后，将输出写入控制台。`AnalyzeType` 是完成大部分工作的地方：

```csharp
static void AnalyzeType(Type t)

{

    TypeInfo typeInfo = t.GetTypeInfo();

    AddToOutput($"Type Name: {t.Name}");

    AddToOutput($"Full Name: {t.FullName}");

    AddToOutput($"Namespace: {t.Namespace}");

    Type tBase = t.BaseType;

    if (tBase != null)

    {

        AddToOutput($"Base Type: {tBase.Name}");

    }

}
```

```csharp
}

AddToOutput("\npublic members:");

foreach (MemberInfo NextMember in t.GetMembers())

{

#if DNXCORE

AddToOutput($"{member.DeclaringType} {member.Name} ");

#else

AddToOutput($"{member.DeclaringType} {member.MemberType} {member.Name} ");

#endif

}
```

在 `AnalyzeType` 方法中，你通过访问 `Type` 对象的各种属性来获取所需的类型名称信息，然后调用 `GetMembers` 方法获取一个 `MemberInfo` 对象数组，用于显示每个成员的详细信息。请注意，你使用辅助方法 `AddToOutput` 来构建要显示的文本：

```csharp
static void AddToOutput(string Text)

{

    OutputText.Append("\n" + Text);

}
```

### `Assembly` 类

`Assembly` 类定义在 `System.Reflection` 命名空间中，提供对给定程序集元数据的访问。它还包含一些方法，使你能够加载甚至执行程序集——前提是该程序集是可执行文件。与 `Type` 类一样，`Assembly` 包含太多的方法和属性，无法在此一一介绍，因此本节仅介绍入门所需以及完成 `WhatsNewAttributes` 示例所需的方法和属性。

在对 `Assembly` 实例执行任何操作之前，你需要将相应的程序集加载到正在运行的进程中。你可以使用静态成员 `Assembly.Load` 或 `Assembly.LoadFrom` 来完成。这两个方法的区别在于，`Load` 接受程序集的名称，运行时会在多个位置搜索以尝试定位该程序集。这些位置包括本地目录和全局程序集缓存。`LoadFrom` 接受程序集的完整路径名，不会尝试在其他任何位置查找该程序集：

```csharp
Assembly assembly1 = Assembly.Load("SomeAssembly");

Assembly assembly2 = Assembly.LoadFrom

(@"C:\My Projects\Software\SomeOtherAssembly");
```

这两个方法还有多个其他重载，提供额外的安全信息。加载程序集后，你可以使用它的各种属性来获取信息，例如其完整名称：

```csharp
string name = assembly1.FullName;
```

### 获取有关程序集中定义类型的详细信息

`Assembly` 类的一个不错的功能是，它使你能够获取相应程序集中定义的所有类型的详细信息。你只需调用 `Assembly.GetTypes` 方法，该方法返回包含所有类型详细信息的 `System.Type` 引用数组。然后，你可以按照上一节所述操作这些 `Type` 引用：

```csharp
Type[] types = theAssembly.GetTypes();

foreach(Type definedType in types)

{

    DoSomethingWith(definedType);

}
```

### 获取有关自定义特性的详细信息

你用来查找程序集或类型上定义了哪些自定义特性的方法，取决于特性所附加到的对象类型。如果你想查找作为整体的程序集上附加了哪些自定义特性，需要调用 `Attribute` 类的静态方法 `GetCustomAttributes`，并传入对程序集的引用：

> 注意：这其实非常重要。你可能想知道，为什么在定义自定义特性时，要费尽周折为它们编写类，为什么 Microsoft 没有提供更简单的语法。答案就在这里。自定义特性确实以对象的形式存在，当程序集加载时，你可以读取这些特性对象，检查它们的属性，并调用它们的方法。

```csharp
Attribute[] definedAttributes = Attribute.GetCustomAttributes(assembly1);

// assembly1 is an Assembly object
```

用于获取程序集特性的 `GetCustomAttributes` 有几个重载。如果在调用时除了程序集引用之外不指定任何参数，它只会返回为该程序集定义的所有自定义特性。你也可以通过指定第二个参数来调用 `GetCustomAttributes`，该参数是一个 `Type` 对象，指示你感兴趣的特性类。在这种情况下，`GetCustomAttributes` 返回一个数组，其中包含所有指定类型的特性。

请注意，所有特性都是作为普通的 `Attribute` 引用检索的。如果你想调用为自定义特性定义的任何方法或属性，需要将这些引用显式转换为相应的自定义特性类。你可以通过调用 `Assembly.GetCustomAttributes` 的另一个重载（这次传入一个 `Type`）来获取附加到给定数据类型上的自定义特性的详细信息。

该引用描述了要检索任何附加属性的类型。然而，若要获取附加到方法、构造函数、字段等上的属性，则需要调用 `GetCustomAttributes` 方法，该方法是 `MethodInfo`、`ConstructorInfo`、`FieldInfo` 等类之一的成员。

如果你只期望给定类型的单个属性，可以改为调用 `GetCustomAttribute` 方法，该方法返回单个 `Attribute` 对象。在 `WhatsNewAttributes` 示例中，你将使用 `GetCustomAttribute` 来查明 `SupportsWhatsNew` 属性是否存在于程序集中。为此，你调用 `GetCustomAttribute`，传入对 `WhatsNewAttributes` 程序集的引用，以及 `SupportsWhatsNewAttribute` 属性的类型。如果此属性存在，你会得到一个 `Attribute` 实例。如果程序集中没有定义它的任何实例，你会得到 `null`。如果找到两个或多个实例，`GetCustomAttribute` 会抛出 `System.Reflection.AmbiguousMatchException`。该调用如下所示：

```
Attribute supportsAttribute =

    Attribute.GetCustomAttribute(assembly1,

typeof(SupportsWhatsNewAttribute));
```

### 完成 `WhatsNewAttributes` 示例

你现在已有足够的信息来完成 `WhatsNewAttributes` 示例，即为示例中的最终程序集 `LookUpWhatsNew` 编写源代码。应用程序的这一部分是控制台应用程序。不过，它需要引用 `WhatsNewAttributes` 和 `VectorClass` 的其他程序集。

`LookupWhatsNew` 项目的示例代码使用了以下依赖项和命名空间：

#### 依赖项

- `NETStandard.Library`
- `VectorClass`
- `WhatsNewAttributes`

#### 命名空间

- `System`
- `System.Collections.Generic`
- `System.Linq`
- `System.Reflection`
- `System.Text`
- `WhatsNewAttributes`
- `static System.Console`

在此文件的源代码中，你首先指明要引入的命名空间。`System.Text` 出现在这里是因为你需要再次使用 `StringBuilder` 对象。`System.Linq` 用于过滤某些属性（代码文件 `LookupWhatsNew/Program.cs`）：

```
using System;

using System.Collections.Generic;

using System.Linq;

using System.Reflection;
```
