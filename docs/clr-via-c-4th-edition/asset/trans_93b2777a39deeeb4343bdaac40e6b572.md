
### 对象哈希码

FCL 的设计者认为，如果任意对象的任意实例都能放入哈希表集合中，那将极其有用。为此，System.Object 提供了一个虚拟的 GetHashCode 方法，以便可以为任何对象获取一个 Int32 哈希码。

如果你定义了一个类型并重写 Equals 方法，那么你也应重写 GetHashCode 方法。事实上，如果你定义的类型重写了 Equals 但没有同时重写 GetHashCode，Microsoft 的 C# 编译器会发出警告。例如，编译以下类型会产生此警告：warning CS0659: 'Program' overrides Object.Equals(object o) but does not override Object.GetHashCode()

```csharp
public sealed class Program {
  public override Boolean Equals(Object obj) { ... }
}
```

定义 Equals 的类型也必须定义 GetHashCode，原因是 System.Collections.Hashtable 类型、System.Collections.Generic.Dictionary 类型以及其他一些集合的实现要求：任何两个相等的对象必须具有相同的哈希码值。因此，如果你重写 Equals，就应重写 GetHashCode，以确保你用于计算相等性的算法与你用于计算对象哈希码的算法相对应。

基本上，当你向集合添加键/值对时，首先会获取键对象的哈希码。此哈希码指示该键/值对应存储在哪个“桶”中。当集合需要查找某个键时，它会获取指定键对象的哈希码。此哈希码标识出随后要按顺序搜索的“桶”，以查找与指定键对象相等的已存储键对象。使用这种存储和查找键的算法意味着，如果你更改了集合中的某个键对象，集合将无法再找到该对象。如果你打算更改哈希表中的某个键对象，应移除原始键/值对，修改该键对象，然后将新的键/值对重新添加到哈希表中。

定义 GetHashCode 方法可以简单直接。但根据数据类型和数据分布，要设计出能返回分布良好的一系列值的哈希算法可能并不容易。下面是一个简单示例，对于 Point 对象来说，它可能完全适用。

```csharp
internal sealed class Point {
  private readonly Int32 m_x, m_y;
  public override Int32 GetHashCode() {
    return m_x ^ m_y; // m_x XOR'd with m_y
  }
  ...
}
```

在为你的类型实例选择计算哈希码的算法时，请尽量遵循以下准则：

-   使用能提供良好随机分布的算法，以获得哈希表的最佳性能。
-   你的算法也可以调用基类型的 GetHashCode 方法，包括使用其返回值。不过，通常不应调用 Object 或 ValueType 的 GetHashCode 方法，因为这两个方法中的实现都不适合高性能哈希算法。
-   你的算法应至少使用一个实例字段。
-   理想情况下，算法中使用的字段应是不可变的；也就是说，这些字段应在构造对象时初始化，并且在对象的生存期内绝不再更改。
-   你的算法应尽可能快地执行。
-   具有相同值的对象应返回相同的代码。例如，两个文本相同的 String 对象应返回相同的哈希码值。

System.Object 的 GetHashCode 方法实现对其派生类型以及该类型中的任何字段一无所知。因此，Object 的 GetHashCode 方法返回一个保证在对象生存期内不会更改的数字。

![](img/857bdf6cef9e242b53a37f88df9a1287_168_0.png)

> **重要** 如果你由于某种原因要实现自己的哈希表集合，或者你正在实现任何会调用 GetHashCode 的代码，那么你绝不应持久化保存哈希码值。原因是哈希码值可能会变化。例如，某个类型的未来版本可能使用不同的算法来计算对象的哈希码。
>
> 有一家公司没有注意这一重要警告。在其网站上，用户可以通过选择用户名和密码来创建新账户。网站随后获取密码 String，调用 GetHashCode，并将哈希码值持久化保存到数据库中。当用户重新登录网站时，他们会输入密码。网站会再次调用 GetHashCode，并将哈希码值与数据库中存储的值进行比较。如果哈希码匹配，用户将被授予访问权限。不幸的是，当该公司升级到新版本的 CLR 时，String 的 GetHashCode 方法已经改变，现在返回不同的哈希码值。最终结果是，任何用户都无法再登录该网站！

## dynamic 基元类型

C# 是一种类型安全的编程语言。这意味着所有表达式都会解析为某个类型的实例，并且编译器只会生成尝试执行对该类型有效的操作的代码。与非类型安全的编程语言相比，类型安全的编程语言的好处是，许多程序员错误会在编译时被检测出来，从而有助于确保代码在你尝试执行之前是正确的。此外，编译时语言通常可以生成更小、更快的代码，因为它们在编译时做出更多假设，并将这些假设固化到生成的 IL 和元数据中。

然而，也有很多场合，程序必须根据直到运行时才知道的信息进行操作。尽管你可以使用类型安全的编程语言（如 C#）来与这些信息交互，但语法往往很笨拙，尤其是因为你经常需要大量处理字符串，而且性能也会受到影响。如果你编写的是纯 C# 应用程序，那么需要处理运行时确定的信息的唯一场合就是使用反射时（第 23 章讨论）。然而，许多开发人员也使用 C# 与并非用 C# 实现的组件通信。其中一些组件可能是 .NET 动态语言（如 Python 或 Ruby），也可能是支持 IDispatch 接口的 COM 对象（可能用原生 C 或 C++ 实现），还可能是 HTML 文档对象模型（DOM）对象（使用各种语言和技术实现）。在构建 Microsoft Silverlight 应用程序时，与 HTML DOM 对象通信尤其有用。

为了让使用反射或与其他组件通信的开发人员更轻松，C# 编译器提供了一种将表达式类型标记为 dynamic 的方法。你还可以将表达式的结果放入变量，并将变量类型标记为 dynamic。然后，这个动态表达式/变量可用于调用成员，例如字段、属性/索引器、方法、委托以及一元/二元/转换运算符。当你的代码通过动态表达式/变量调用成员时，编译器会生成描述所需操作的特殊 IL 代码。这种特殊代码称为有效负载。在运行时，有效负载代码会根据动态表达式/变量当前引用的对象的实际类型，确定要执行的确切操作。

以下代码演示我所讲的内容。

```csharp
internal static class DynamicDemo {
   public static void Main() {
      dynamic value;
      for (Int32 demo = 0; demo < 2; demo++) {
         value = (demo == 0) ? (dynamic) 5 : (dynamic) "A";
         value = value + value;
         M(value);
      }
   }

   private static void M(Int32 n) { Console.WriteLine("M(Int32): " + n); }
   private static void M(String s) { Console.WriteLine("M(String): " + s); }
}
```

