
```csharp
[DefaultMemberAttribute("Main")]
[DebuggerDisplayAttribute("Richter", Name="Jeff", Target=typeof(Program))]
public sealed class Program {
    [Conditional("Debug")]
    [Conditional("Release")]
    public void DoSomething() { }

    public Program() {
    }

    [CLSCompliant(true)]
    [STAThread]
    public static void Main() {
        // Show the set of attributes applied to this type
        ShowAttributes(typeof(Program));

        // Get the set of methods associated with the type
        MemberInfo[] members = typeof(Program).FindMembers(
            MemberTypes.Constructor | MemberTypes.Method,
            BindingFlags.DeclaredOnly | BindingFlags.Instance |
            BindingFlags.Public | BindingFlags.Static,
            Type.FilterName, "*");

        foreach (MemberInfo member in members) {
            // Show the set of attributes applied to this member
            ShowAttributes(member);
        }
    }

    private static void ShowAttributes(MemberInfo attributeTarget) {
        IList<CustomAttributeData> attributes =
            CustomAttributeData.GetCustomAttributes(attributeTarget);

        Console.WriteLine("Attributes applied to {0}: {1}",
            attributeTarget.Name, (attributes.Count == 0) ? "None" : String.Empty);

        foreach (CustomAttributeData attribute in attributes) {
            // Display the type of each applied attribute
            Type t = attribute.Constructor.DeclaringType;
            Console.WriteLine("{0}", t.ToString());
            Console.WriteLine("    Constructor called={0}", attribute.Constructor);

            IList<CustomAttributeTypedArgument> posArgs = attribute.ConstructorArguments;
            Console.WriteLine(
                "    Positional arguments passed to constructor:" +
                ((posArgs.Count == 0) ? " None" : String.Empty));
            foreach (CustomAttributeTypedArgument pa in posArgs) {
                Console.WriteLine("        Type={0}, Value={1}", pa.ArgumentType, pa.Value);
            }

            IList<CustomAttributeNamedArgument> namedArgs = attribute.NamedArguments;
            Console.WriteLine(
                "    Named arguments set after construction:" +
                ((namedArgs.Count == 0) ? " None" : String.Empty));
            foreach (CustomAttributeNamedArgument na in namedArgs) {
                Console.WriteLine("        Name={0}, Type={1}, Value={2}",
                    na.MemberInfo.Name, na.TypedValue.ArgumentType, na.TypedValue.Value);
            }
            Console.WriteLine();
        }
        Console.WriteLine();
    }
}
```

生成并运行此应用程序将产生以下输出。

```text
Attributes applied to Program:
  System.SerializableAttribute
    Constructor called=Void .ctor()
    Positional arguments passed to constructor: None
    Named arguments set after construction: None

  System.Diagnostics.DebuggerDisplayAttribute
    Constructor called=Void .ctor(System.String)
    Positional arguments passed to constructor:
      Type=System.String, Value=Richter
    Named arguments set after construction:
      Name=Name, Type=System.String, Value=Jeff
      Name=Target, Type=System.Type, Value=Program

  System.Reflection.DefaultMemberAttribute
    Constructor called=Void .ctor(System.String)
    Positional arguments passed to constructor:
      Type=System.String, Value=Main
    Named arguments set after construction: None

Attributes applied to DoSomething:
  System.Diagnostics.ConditionalAttribute
    Constructor called=Void .ctor(System.String)
    Positional arguments passed to constructor:
      Type=System.String, Value=Release
    Named arguments set after construction: None

  System.Diagnostics.ConditionalAttribute
    Constructor called=Void .ctor(System.String)
    Positional arguments passed to constructor:
      Type=System.String, Value=Debug
    Named arguments set after construction: None

Attributes applied to Main:
  System.CLSCompliantAttribute
    Constructor called=Void .ctor(Boolean)
    Positional arguments passed to constructor:
      Type=System.Boolean, Value=True
    Named arguments set after construction: None

  System.STAThreadAttribute
    Constructor called=Void .ctor()
    Positional arguments passed to constructor: None
    Named arguments set after construction: None

Attributes applied to .ctor: None
```

## 可空值类型

**本章内容：**

- C# 对可空值类型的支持 …… 443
- C# 的 null 合并运算符 …… 446
- CLR 对可空值类型的特殊支持 …… 447

如你所知，值类型的变量永远不能为 `null`；它始终包含值类型本身的值。事实上，这正是这些类型被称为*值类型*的原因。不幸的是，在某些场景下这会成为问题。例如，设计数据库时，可以将列的数据类型定义为 32 位整数，该类型会映射到框架类库（FCL）的 `Int32` 数据类型。但数据库中的列可以指示该值可为 null。也就是说，该行的列中没有值是可以的。使用 Microsoft .NET Framework 处理数据库数据可能相当困难，因为在公共语言运行时（CLR）中，无法将 `Int32` 值表示为 `null`。

![](img/857bdf6cef9e242b53a37f88df9a1287_466_0.png)

> **注意** Microsoft ADO.NET 的表适配器确实支持可空类型。但不幸的是，`System.Data.SqlTypes` 命名空间中的类型并未被可空类型取代，部分原因是这些类型之间不存在一一对应关系。例如，`SqlDecimal` 类型最多有 38 位数字，而常规 `Decimal` 类型只能达到 29 位。此外，`SqlString` 类型支持其自己的区域设置和比较选项，而普通 `String` 类型不支持这些。

再举一个例子。在 Java 中，`java.util.Date` 类是引用类型，因此这种类型的变量可以设置为 `null`。然而，在 CLR 中，`System.DateTime` 是值类型，`DateTime` 变量永远不能为 `null`。如果用 Java 编写的应用程序想要将日期/时间传递给运行 CLR 的 Web 服务，那么当 Java 应用程序发送 `null` 时就会有问题，因为 CLR 无法表示它并对其进行操作。

为了改善这种情况，Microsoft 向 CLR 添加了可空值类型的概念。要理解它们的工作原理，我们首先需要查看 FCL 中定义的 `System.Nullable<T>` 结构。

以下是 `System.Nullable<T>` 类型定义方式的逻辑表示。

```csharp
[Serializable, StructLayout(LayoutKind.Sequential)]
public struct Nullable<T> where T : struct {

   // These 2 fields represent the state
   private Boolean hasValue = false; // Assume null
   internal T value = default(T);    // Assume all bits zero

   public Nullable(T value) {
      this.value = value;
      this.hasValue = true;
   }

   public Boolean HasValue { get { return hasValue; } }

   public T Value {
      get {
         if (!hasValue) {
            throw new InvalidOperationException(
               "Nullable object must have a value.");
         }
         return value;
      }
   }

   public T GetValueOrDefault() { return value; }

   public T GetValueOrDefault(T defaultValue) {
      if (!HasValue) return defaultValue;
      return value;
   }

   public override Boolean Equals(Object other) {
      if (!HasValue) return (other == null);
      if (other == null) return false;
      return value.Equals(other);
   }

   public override int GetHashCode() {
      if (!HasValue) return 0;
      return value.GetHashCode();
   }

   public override string ToString() {
      if (!HasValue) return "";
      return value.ToString();
   }

   public static implicit operator Nullable<T>(T value) {
      return new Nullable<T>(value);
   }

   public static explicit operator T(Nullable<T> value) {
      return value.Value;
   }
}
```
