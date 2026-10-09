
使用 nameof 运算符的优势在于，如果标识符名称发生变化，重构工具会自动更改 nameof 的参数。如果未使用重构工具，代码将不再编译，从而强制开发人员手动更改该参数。

对于属性验证器的情况，参数始终是 value 且无法更改，因此可以说利用 nameof 运算符带来的好处已经消失。尽管如此，为了与以下准则保持一致，仍应考虑在所有 paramName 参数的情况下继续使用 nameof 运算符：对于接受此参数的异常（如 ArgumentNullException 和 ArgumentException），始终对传入的 paramName 参数使用 nameof。

## 只读和只写属性

通过移除属性的 getter 或 setter 部分，你可以改变属性的可访问性。仅带有 setter 的属性是只写属性，这是一种相对罕见的情况。同样，仅提供 getter 会使属性成为只读属性；任何尝试赋值的行为都会导致编译错误。例如，要使 Id 变为只读，你可以按照清单 6.21 中所示的方式编写代码。

### 清单 6.21：在 C# 6.0 之前定义只读属性

```csharp
class Program
{
    static void Main()
    {
        Employee employee1 = new Employee();
        employee1.Initialize(42);
        // 错误：属性或索引器 'Employee.Id'
        // 不能被赋值；它是只读的
        // employee1.Id = "498";
    }
}

class Employee
{
    public void Initialize(int id)
    {
        // 因为 Id 属性没有 setter，所以使用字段
        // 它是只读的
        _Id = id.ToString();
    }
}
```

```csharp
// ...
// Id 属性声明
public string Id
{
    get => _Id;
    // 未提供 setter
}
private string _Id;
}
```

清单 6.21 在 Employee 的 Initialize() 方法内部而不是通过属性来分配字段值（_Id = id）。通过属性进行赋值会导致编译错误，就像在 Program.Main() 中那样。

从 C# 6.0 开始，还支持**自动实现的只读属性**，如下所示：

```csharp
public bool[,] Cells { get; } = new bool[2, 3, 3];
```

这显然是对 C# 6.0 之前方法的重大改进，特别是考虑到只读属性在诸如项目数组或清单 6.21 中的 Id 等场景中非常常见。

关于自动实现的只读属性，有一个重要的注意事项是，与只读字段类似，编译器要求必须通过初始化器（或在构造函数中）进行初始化。在前面的代码片段中，我们使用了初始化器，但如我们稍后将看到的，在构造函数内部对 Cells 进行赋值也是允许的。

鉴于准则规定不应从外部访问字段，在 C# 6.0 环境中编程的人会发现，几乎没有必要使用 C# 6.0 之前的语法；相反，程序员始终可以使用自动实现的只读属性。唯一的例外可能是当只读修改字段的 dataType 与属性的 dataType 不匹配时——例如，如果字段类型为 int，而只读属性类型为 double。

## 准则

-   如果属性值不应被更改，则应创建只读属性。
-   在 C# 6.0（或更高版本）中，如果属性值不应被更改，应创建自动实现的只读属性，而不是带有后台字段的只读属性。

## 作为虚字段的属性

如前所述，属性表现得像虚字段。在某些情况下，你甚至不需要后台字段。相反，属性 getter 返回计算出的值，而 setter 解析该值并将其持久化到其他成员字段（如果存在的话）。例如，考虑清单 6.22 中显示的 Name 属性实现。输出 6.7 显示了结果。

### 清单 6.22：定义属性

```csharp
class Program
{
    static void Main()
    {
        Employee employee1 = new Employee();

        employee1.Name = "Inigo Montoya";
        System.Console.WriteLine(employee1.Name);

        // ...
    }
}

class Employee
{
    // ...

    // FirstName 属性
    public string FirstName
    {
        get
        {
            return _FirstName;
        }
        set
        {
            _FirstName = value;
        }
    }
    private string _FirstName;

    // LastName 属性
    public string LastName
    {
        get => _LastName;
        set => _LastName = value;
    }
    private string _LastName;
    // ...

    // Name 属性
    public string Name
    {
        get
        {
            return $"{ FirstName } { LastName }";
        }
        set
        {
            // 将赋值的字符串拆分为
            // 名和姓
            string[] names;
            names = value.Split(new char[]{' '});
            if(names.Length == 2)
            {
                FirstName = names[0];
                LastName = names[1];
            }
            else
            {
                // 如果未分配全名，
                // 则抛出异常
                throw new System. ArgumentException (
                    $"分配的值 '{ value }' 无效", "value");
            }
        }
    }
    public string Initials => $"{ FirstName[0] } { LastName[0] }";
    // ...
}
```

### 输出 6.7

Inigo Montoya

Name 属性的 getter 将 FirstName 和 LastName 属性返回的值连接起来。事实上，分配的名称值实际上并没有被存储。当对 Name 属性进行赋值时，右侧的值会被解析为名和姓的部分。

## Getter 和 Setter 上的访问修饰符

如前所述，不从属性外部访问字段是一种良好的实践，因为这样做会绕过可能插入的任何验证或额外逻辑。不幸的是，C# 1.0 不允许在属性的 getter 和 setter 部分之间具有不同的封装级别。因此，无法创建公共的 getter 和私有的 setter，使得外部类对属性具有只读访问权限，而类内部的代码可以写入该属性。

在 C# 2.0 中，支持在属性实现的 get 或 set 部分（而不是两者都指定）上放置访问修饰符，从而覆盖在属性声明上指定的访问修饰符。清单 6.23 演示了如何做到这一点。

### 清单 6.23：在 Setter 上放置访问修饰符

```csharp
class Program
{
    static void Main()
    {
        Employee employee1 = new Employee();
        employee1.Initialize(42);
        // 错误：属性或索引器 'Employee.Id'
        // 在此上下文中不能使用，因为 set
        // 访问器不可访问
        employee1.Id = "490";
    }
}

class Employee
{
    public void Initialize(int id)
    {
        // 设置 Id 属性
        Id = id.ToString();
    }
    // ...
    // Id 属性声明
    public string Id
    {
        get => _Id;
        // 提供访问修饰符仅在 C# 2.0 及
        // 更高版本中是可能的
        private set => _Id = value;
    }
    private string _Id;
}
```

通过在 setter 中使用 private，该属性对于 Employee 以外的类表现为只读。在 Employee 内部，该属性表现为可读/可写，因此你可以在类本身内部分配该属性。在 getter 或 setter 上指定访问修饰符时，请确保该访问修饰符比整个属性的访问修饰符更具限制性。例如，将属性声明为 *private* 而将 setter 声明为 *public* 会导致编译错误。

## 准则

-   应在所有属性的 getter 和 setter 实现上应用适当的可访问性修饰符。
-   不要仅提供 setter 的属性，或不要提供 setter 具有比 getter 更宽泛的可访问性的属性。

## 不允许将属性和方法调用作为 *ref* 或 *out* 参数值

C# 允许属性像字段一样使用，但作为 *ref* 或 *out* 参数值传递时除外。*ref* 和 *out* 参数值在内部是通过将内存地址传递给目标方法来实现的。然而，由于属性可以是没有后台字段的 *virtual* 字段，或者是 *read-only* 或 *write-only*，因此无法传递底层存储的地址。因此，你无法将属性作为 *ref* 或 *out* 参数值传递。方法调用也是如此。相反，当代码需要将属性或方法调用作为 *ref* 或 *out* 参数值传递时，代码必须先将值复制到变量中，然后传递该变量。一旦方法调用完成，代码必须将该变量重新赋值给属性。

## 高级主题

## 属性内部结构

清单 6.24 表明，getter 和 setter 在公共中间语言（CIL）中分别显示为 `get_FirstName()` 和 `set_FirstName()`。

### 清单 6.24：由属性生成的 CIL 代码

```cil
// ...
.field private string _FirstName
.method public hidebysig specialname instance string
    get_FirstName() cil managed
```
