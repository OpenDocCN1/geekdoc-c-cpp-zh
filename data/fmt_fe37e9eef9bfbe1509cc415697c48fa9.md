
# 类和默认构造函数的约束

在练习的这部分中，你将通过添加约束和 `new()` 来进一步实现 `Repository<T>` 类中的泛型类型 `T`。类约束强制 `Repository<T>` 只处理引用类型（类），而 `new()` 约束则检查由泛型生成的实例是否实现了默认构造函数。

1. 转到 `Repository<T>` 类并将其约束更改为：
   `class Repository<T> where T : class, IRegisterable, new()`
2. 转到 `Motorcycle` 类并实现一个接受三个参数的构造函数，用于类中可赋值的属性（`RegNo`、`Model` 和 `IsRegistered`）
3. 这会导致编译错误，使得无法构建解决方案
   `Repository<Motorcycle> morcycle = new Repository<Motorcycle>();`

```csharp
// 02_Constraints.Motorcycle 必须具有无参数构造函数的非抽象类型，才能
// 作为泛型类型或方法 '02_Constraints.Chapter2.Repository<T>' 中的参数 'T' 使用
```

出现此异常的原因是，当你实现构造函数时，编译器会自动忽略默认构造函数。

# C# 入门

4. 为了解决这个问题，你必须在 `Motorcycle` 类中实现一个默认构造函数。你通过添加一个无参数的构造函数来实现。
5. 错误应该消失。
6. 运行应用程序并点击按钮。所有的汽车应该显示在列表框中。尽管你更改了 `Repository<T>` 的约束，类仍然显示，是因为 `Car` 类是一个具有默认构造函数并实现了 `IRegisterable` 接口的类。

目前 `Motorcycle` 类的代码如下：

```csharp
class Motorcycle : IRegisterable
{
    public string RegNo { get; set; }
    public string Model { get; set; }
    public bool IsRegistered { get; set; }

    public string DisplayValue
    {
        get
        {
            return String.Format("{0} {1}: {2}", RegNo, Model, IsRegistered.ToString());
        }
    }

    public Motorcycle(string regNo, string model, bool isRegistered)
    {
        RegNo = regNo;
        Model = model;
        IsRegistered = isRegistered;
    }

    // 默认构造函数
    public Motorcycle()
    {
    }
}
```

# 扩展方法

在扩展类时经常使用继承，但在某些情况下（例如处理无法继承的密封类（`sealed class`）时），扩展方法可能是解决方案。一种场景可能是你想提取某些功能并创建一个可以用于许多不同类型的泛型版本。

扩展方法不会更改底层类型。它们必须被声明为 `public static`，并且第一个参数必须指定要扩展的类型；你通过在第一个参数前加上 `this` 关键字来实现。注意，在调用该方法时，你不需要为 `this` 参数传递值，因为它代表了使用该扩展方法的类型。包含扩展方法的类必须声明为带有 `static` 关键字。

扩展方法经常用于 MVC 应用以输出 HTML。

**重要：** 你必须在打算使用的 `.cs` 文件中放置对包含扩展方法的类的 `using` 语句。

# 示例：扩展方法

此示例代码显示了如何为密封的 `System.String` 类型创建一个扩展方法，检查字符串是否包含数字。

```csharp
public static class StringExtensions
{
    public static bool ContainsNumbers(this string value)
    {
        return Regex.IsMatch(value, @"\d+");
    }
}
```

此示例代码显示了如何调用扩展方法。

```csharp
public class UseExtensions
{
    void UseExtensionMethod(string str)
    {
        // 在类型变量上调用扩展方法
        bool hasNumbers = str.ContainsNumbers();
    }
}
```

# 链式扩展方法

如果扩展方法返回的值与它初始化时的类型相同，那么处理该类型的其他扩展方法就可以通过点 (`.`) 符号链式调用原始扩展方法。假设该扩展方法将接收一个集合并反转其项的顺序，然后返回修改后的集合。如果你想从集合中检索前 10 个项，你可以链式调用 LINQ 的 `Take` 扩展方法。

## 示例：链式扩展方法

在此示例中，`Person` 对象存储在一个集合中，使用一个带有字符串参数名称的 `Add` 扩展方法，并返回传入的 `List<Person>` 集合的修改版本。该扩展方法还应该通过调用另一个扩展方法 `Count`（该方法具有一个名为 `name` 的字符串参数）来返回名称在集合中出现的次数。

实现后，包含扩展方法的静态类应该拥有两个名为 `Add` 和 `Count` 的方法。

```csharp
public class Person
{
    public string Name { get; set; }
}
```

```csharp
public static class ChainingExtensions
{
    public static List<Person> Add(this List<Person> persons, string name)
    {
        persons.Add(new Person { Name = name });
        return persons;
    }

    public static int Count(this List<Person> persons, string name)
    {
        var count = persons.Count(p => p.Name.Equals(name));
        return count;
    }
}
```

在之前的示例中，如果添加了多个个人，`Add` 方法可以多次链式调用，因为它返回了传递的集合。一旦 `Count` 方法被调用，`List<Person>` 集合上就无法再链式调用，因为 `Count` 方法返回一个 `int`。

```csharp
List<Person> persons = new List<Person>();

public int ChainingExtensionMethods(string searchName)
{
    return persons.Add("Jonas").Add("Lisa").Add("Jonas").Count(searchName);
}
```

# 泛型方法

当方法需要使用未确定的类型时，泛型非常有用。当类型确定时，泛型方法可以处理任何类型并返回一个封闭泛型方法。

## 示例：泛型方法

```csharp
public interface ICounter
{
    string CompareValue { get; }
}

public class Animal : ICounter
{
    public string Race { get; set; }
    public string Type { get; set; }
    public string CompareValue { get { return Race; } }
}
```

在创建集合中存储的对象时使用的 `Animal` 类实现了 `ICounter` 接口，使得可以使用 `CountItems` 扩展方法。

```csharp
public class UseExtensions
{
    List<Animal> items = new List<Animal>();

    public int GenericExtensionMethods(string filter)
    {
        items.Add(new Animal { Race = "Cat", Type = "Egyptian Mau" });
        items.Add(new Animal { Race = "Dog", Type = "Boxer" });
        items.Add(new Animal { Race = "Cat", Type = "Siberian" });
        return CountItems(filter);
    }
}
```

从 `btnGenericExtensionMethods` 按钮的 `Click` 事件创建 `UseExtensions` 类的实例，并调用 `GenericExtensionMethods` 方法来使用扩展方法。

```csharp
private void btnGenericExtensionMethods_Click(object sender, EventArgs e)
{
    var extensions = new UseExtensions();
    var count = extensions.GenericExtensionMethods("Cat");
    lblResult.Text = count.ToString();
}
```

## 练习：泛型扩展方法

在此练习中，你将创建一个名为 `Search` 的扩展方法，它将对车辆的任何字符串属性进行过滤，并将结果显示在列表框中。

### 创建 Search 扩展方法

创建一个名为 `Search` 的扩展方法，它将搜索 `Repository` 类中所在项的所有可用的字符串属性。`Search` 方法将返回一个 `IEnumerable<T>`，其中包含所有至少有一个字符串属性包含方法参数提供的搜索字符串的项目。

你必须假装你没有访问 `Repository` 类的权限，就像它是第三方类库的一部分一样。你将在循环中使用反射（reflection）来逐个查找项的属性，并在第二个（内部）循环中，你将遍历泛型 `T` 的可读属性，以查找属性名称是否存在于泛型类型中。使用属性名称检查当前项中的对应属性是否包含传入的字符串搜索参数的值。

1. 创建一个名为 `Extensions` 的新类并将其更改为 `static`。
2. 创建一个名为 `Search` 的 `public static` 方法，并使用泛型 `T` 声明。
3. 为该方法添加两个参数：
   a. 第一个是方法要作用的对象，此参数应该用 `this` 关键字修饰。将参数命名为 `rep` 并将其声明为 `Repository<T>`。由于你无法直接访问 `Repository<T>` 类中的集合，你可以通过 `Repository` 的 `Get` 方法获取其项权限。
   b. 第二个是名为 `search` 的字符串参数，包含要搜索的字符串。

由于 `Repository<T>` 类具有约束，此方法也具有这些约束。

```csharp
public static class Extensions
{
    public static IEnumerable<T> Search<T>(this Repository<T> rep, string search) where T : class, IRegisterable, new()
    {
        ...
    }
}
```

4. 找到在传递类型 `T` 中定义的所有字符串属性。为此，你需要：
   a. 使用 `typeof` 调用类型 `T` 的 `GetProperties` 方法以获取 `T` 的实际类型。
   b. 使用 LINQ 方法找到声明为 `string` 且可读的属性：
      i. 要检查属性是否为特定类型，可以在 `Where` 方法的 Lambda 变量中使用当前项的 `PropertyType`，并与你追求的类型进行比较。
      ii. 要检查属性是否可读，可以检查 `Where` 方法 Lambda 变量中当前项的 `CanRead` 属性。
   c. 将结果属性保存在名为 `readProps` 的变量中。

```csharp
var readProps = typeof(T).GetProperties().Where(p => p.PropertyType == typeof(string) && p.CanRead);
```

5. 创建一个名为 `result` 的 `List<T>`，用于存放与传入字符串搜索值匹配的项目。
6. 添加一个 `foreach` 循环，遍历 `Repository<T>` 类集合中的所有项；你可以通过调用传递 `Search` 方法的 `rep` 参数的 `Get` 方法来访问项。
7. 在循环内部添加 `if` 语句，检查当前项是否已在 `result` 集合中。如果存在，则使用 `continue` 关键字立即跳转到下一个项。

```csharp
var result = new List<T>();
foreach (var item in rep.Get())
{
    if (result.Contains(item)) continue;
    // ... 后续逻辑
}
```

8. 在 `if` 语句之后，遍历你在第 4 步中获取的所有字符串类型属性。在检查当前循环项中的这些值时，你需要使用这些属性的名称。
9. 要检查当前循环项的属性值，你需要：
   i. 在项上调用 `GetType` 方法。
   ii. 在 `GetType` 方法上调用 `GetProperty` 方法，并将从内部循环遍历的属性集合中获取的属性名称传入。
