
使用了命名实参（§11.6.2.1）。例如，给定 *M* 的定义分部方法声明：

```csharp
partial class P
{
    static partial void M(int x);
}
```

然后，在另一个文件中的实现分部方法声明和调用：

```csharp
partial class P
{
    static void Caller() => M(y: 0);
    static partial void M(int y) {}
}
```

这是**无效的**，因为该调用使用的是实现分部方法声明中的实参名称，而不是定义分部方法声明中的实参名称。

*注释结束*

如果分部类型声明的任何部分都不包含给定分部方法的实现声明，则调用该方法的任何表达式语句都会直接从合并类型声明中移除。因此，该调用表达式（包括任何子表达式）在运行时没有效果。该分部方法本身也会被移除，并且不会成为合并类型声明的成员。

如果给定分部方法存在实现声明，则保留对该分部方法的调用。该分部方法会生成一个与实现分部方法声明类似的方法声明，但有以下不同：

- 不包含 `partial` 修饰符。
- 生成的方法声明中的特性是定义分部方法声明和实现分部方法声明中的特性按未指定顺序组合而成的。重复项不会移除。
- 生成的方法声明中参数上的特性是定义分部方法声明和实现分部方法声明中对应参数的特性按未指定顺序组合而成的。重复项不会移除。

如果为分部方法 *M* 提供了定义声明但没有提供实现声明，则以下限制适用：

- 从 *M* 创建委托是编译时错误（§11.7.15.6）。
- 在转换为表达式树类型的匿名函数内部引用 *M* 是编译时错误（§8.6）。
- 作为 *M* 调用的一部分出现的表达式不会影响明确赋值状态（§9.4），这可能会导致编译时错误。
- *M* 不能作为应用程序的入口点（§7.1）。

分部方法有助于允许类型声明的一部分自定义另一部分的行为，例如，由工具生成的部分。考虑以下分部类声明：

```csharp
partial class Customer
{
    string name;

    public string Name
    {
        get => name;
        set
        {
            OnNameChanging(value);
            name = value;
            OnNameChanged();
        }
    }

    partial void OnNameChanging(string newName);
    partial void OnNameChanged();
}
```

如果此类在没有任何其他部分的情况下编译，则定义分部方法声明及其调用将被移除，并且生成的合并类声明将等效于以下内容：

```
class Customer
{
    string name;

    public string Name
    {
        get => name;
        set => name = value;
    }
}
```

但是，假设提供了另一部分，它提供了这些分部方法的实现声明：

```
partial class Customer
{
    partial void OnNameChanging(string newName) =>
        Console.WriteLine($"Changing {name} to {newName}");

    partial void OnNameChanged() =>
        Console.WriteLine($"Changed to {name}");
}
```

那么生成的合并类声明将等效于以下内容：

```
class Customer
{
    string name;

    public string Name
    {
        get => name;
        set
        {
            OnNameChanging(value);
            name = value;
            OnNameChanged();
        }
    }

    void OnNameChanging(string newName) =>
        Console.WriteLine($"Changing {name} to {newName}");

    void OnNameChanged() =>
        Console.WriteLine($"Changed to {name}");
}
```

## 14.6.10 扩展方法

当方法的第一个参数包含 this 修饰符时，该方法称为扩展方法。扩展方法只能声明在非泛型、非嵌套的静态类中。扩展方法的第一个参数除 this 外不能有任何修饰符，并且参数类型不能是指针类型。

*示例：* 以下是一个声明了两个扩展方法的静态类的示例：

```
public static class Extensions
{
    public static int ToInt32(this string s) => Int32.Parse(s);

    public static T[] Slice<T>(this T[] source, int index, int count)
    {
        if (index < 0 || count < 0 || source.Length - index < count)
        {
            throw new ArgumentException();
        }
        T[] result = new T[count];
        Array.Copy(source, index, result, 0, count);
        return result;
    }
}
```

示例结束

扩展方法是常规静态方法。此外，当包含它的静态类在作用域内时，可以使用实例方法调用语法（§11.7.8.3）调用扩展方法，并将接收者表达式作为第一个参数。

*示例：* 以下程序使用上面声明的扩展方法：

```
static class Program
{
    static void Main()
    {
        string[] strings = { "1", "22", "333", "4444" };
        foreach (string s in strings.Slice(1, 2))
        {
            Console.WriteLine(s.ToInt32());
        }
    }
}
```

Slice 方法可在 string[] 上使用，ToInt32 方法可在 string 上使用，因为它们已声明为扩展方法。该程序的含义与以下使用普通静态方法调用的程序相同：

```
static class Program
{
    static void Main()
    {
        string[] strings = { "1", "22", "333", "4444" };
        foreach (string s in Extensions.Slice(strings, 1, 2))
        {
            Console.WriteLine(Extensions.ToInt32(s));
        }
    }
}
```

*示例结束*

## 14.6.11 方法体

方法声明的 *方法体* 由块体、表达式体或分号组成。

抽象方法和外部方法声明不提供方法实现，因此它们的方法体仅由分号组成。对于任何其他方法，方法体是一个块（§12.3），其中包含调用该方法时要执行的语句。

方法的 *有效返回类型* 在返回类型为 void 时，或者方法为 async 且返回类型为 System.Threading.Tasks.Task 时，为 void。否则，非 async 方法的有效返回类型是其返回类型，而返回类型为 System.Threading.Tasks.Task<T> 的 async 方法的有效返回类型为 T。

当方法的有效返回类型为 void 且该方法具有块体时，块中的 return 语句（§12.10.5）不得指定表达式。如果 void 方法的块正常完成（即控制流离开方法体末尾），该方法只是返回到其调用方。

当方法的有效返回类型为 void 且该方法具有表达式体时，表达式 E 应为语句表达式（statement_expression），并且该体完全等效于形式为 { E; } 的语句体。

当方法的有效返回类型不是 void 且该方法具有块体时，该方法体中的每个 return 语句都应指定一个可隐式转换为有效返回类型的表达式。值返回方法的方法体终结点不应可达。换言之，在具有块体的值返回方法中，控制流不允许离开方法体末尾。

当方法的有效返回类型不是 void 且该方法具有表达式体 E 时，该表达式应可隐式转换为有效返回类型，并且该体完全等效于形式为 { return E; } 的块体。

*示例：* 在以下代码中

```
class A
{
    public int F() {} // Error, return value required

    public int G()
    {
        return 1;
    }
}
```
