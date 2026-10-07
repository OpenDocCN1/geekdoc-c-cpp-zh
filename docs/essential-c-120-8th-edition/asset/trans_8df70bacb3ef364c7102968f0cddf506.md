

## 472 第 8 章：接口

# 表 8.1：默认接口重构特性（续）

| C# 8.0 引入的接口构造体 | 示例代码 |
|---|---|
| **protected 访问修饰符**<br>仅可从与定义该类<br>不同的类中的成员进行访问。 | `public interface IPerson<br>{<br>// ...&lt;<br>protected void Initialize() =><br>/* ... */ };` |
| **private 访问修饰符**<br>私有访问修饰符<br>限制成员仅在其声明的<br>接口中可被调用。它被<br>设计用于支持默认接口<br>重构。所有<br>私有成员必须包含<br>实现。 | `public interface IPerson<br>{<br>string FirstName { get; set; };<br>string LastName { get; set; };<br>string Name => GetName();<br>private string GetName() =><br>`${FirstName} {LastName}`;` |
| **internal 访问修饰符**<br>internal 成员仅在<br>其所在的相同<br>程序集内部可见。 | `public interface IPerson<br>{<br>string FirstName { get; set; };<br>string LastName { get; set; };<br>string Name => GetName();<br>internal string GetName() =><br>`${FirstName} {LastName}`;` |
| **protected internal 访问修饰符**<br>private 和 protected 的<br>超集；private<br>成员在相同<br>程序集内部可见，<br>也可以从派自于同一<br>接口的其他接口可见。像保护<br>成员一样，程序集<br>外部类无法看到<br>protected internal 成员。 | `public interface IPerson<br>{<br>string FirstName { get; set; };<br>string LastName { get; set; };<br>string Name => GetName();<br>protected internal string GetName() =><br>`${FirstName} {LastName}`;` |
| private protected 访问修饰符 | 仅可以在包含它的接口或派自于实现接口的接口中访问保护的成员。即使是实现接口的类也无法访问保护成员，如 Person 类中的 PersonTitle 属性所示。 | ```csharp
class Program{
    static void Main()
{
        IPerson person = null;
        // 非派生类无法访问
        // private protected 成员。
        Console.WriteLine(person?.GetName());
    }

    public interface IPerson
    {
        string FirstName { get; }
        string LastName { get; }
        string Name => GetName();
        private protected string GetName() => $"{FirstName} {LastName}";
    }

    public interface IEmployee
    {
        int EmployeeId => Employee.GetHashCode();
    }

    public class Person : IPerson
    {
        public Person(string firstName, string lastName)
        {
            FirstName = firstName ?? throw new ArgumentNullException(nameof(firstName));
            LastName = lastName ?? throw new ArgumentNullException(nameof(lastName));
        }

        public string FirstName { get; }
        public string LastName { get; }
        // private protected 接口成员
        // 在派生类中不可访问。
        public int PersonTitle => GetName().ToUpper();
    }
``` |
| virtual 修饰符 | 默认情况下，实现的接口成员是 virtual（虚的），这意味着当调用接口成员时，具有相同签名的派生实现将被调用。然而，与 public 访问修饰符一样，你可以显式将成员标记为 virtual 以提高清晰度。对于未实现的接口成员，不允许使用 virtual。同样，virtual 与 private、static 和 sealed 修饰符不兼容。 | public interface IPerson {
  // 未实现的成员上
  // 不允许使用 virtual
  virtual string LastName { get; set; }
  virtual string Name => GetName();
  private string GetName() {
    return "${LastName}";
  } |
| sealed 修饰符 | 为了防止派生类重写方法，可以将其标记为 sealed，从而确保该方法的实现不会被派生类修改。相关信息请参见列表 8.13。 | public interface IWorkflowActivity {
  // 私有的，因此不是 virtual
  private void Start() => Console.WriteLine("IWorkflowActivity.Start()...");
  // 使用 sealed 防止重写
  sealed void Run() {
    try {
      Start();
      InternalRun();
    } finally {
      Stop();
    }
  }
  protected void InternalRun();
  // 私有的，因此不是 virtual
  private void Stop() => Console.WriteLine("IWorkflowActivity.Stop()...");
} |

## 第 8 章：接口

表 8.1：默认接口重构特性

| C# 8.0 引入的构造体 | 示例代码 |
| --- | --- |
| abstract 修饰符 | abstract 修饰符仅允许用于没有实现的成员，由于此类成员默认如此，该关键字没有效果。所有 abstract 成员自动为 virtual，显式将 abstract 声明为 virtual 会触发编译错误。 | ```csharp
public interface IPerson {
    // 未实现的成员上
    // 不允许使用 virtual
    // virtual / abstract string FirstName
    set { get; set; }
    string LastName { get; set; }
    // 带有实现的成员上
    // 不允许使用 abstract
    // virtual / abstract string Name => GetName();
    private string GetName() => $"{FirstName} {LastName}";
}
``` |
| 部分接口和部分方法 | 现在可以为方法提供部分实现。部分方法始终是私有的——它们不支持访问修饰符。对于没有输出数据的可选的完全实现方法。 | ```csharp
public interface IThing {
    string Value { get; protected set; }
    void SetValue(string value);
    AssertValueValid(value);
    Value = value;
}
public interface IThing {
    void AssertValueValid(string value);
    // 如果值无效则抛出异常
    switch(value) {
        case null:
            throw new ArgumentNullException(nameof(value));
        case "":
            throw new ArgumentException("空字符串无效", nameof(value));
        case string _:
            if (string.IsNullOrWhiteSpace(value)) {
                throw new ArgumentException("不能为空格", nameof(value));
            }
            break;
    }
}
``` |

表8.1 有两个值得注意的点。首先，重要的是不支持自动实现的属性，因为不支持（自动实现属性的）实例字段。这与支持实例字段和自动实现属性的抽象类有显著区别。

其次，注意接口上的静态成员默认也是 public 的。虽然静态成员始终具有实现，在这一点上与静态成员密切对应，相比之下，接口实例目的目的是支持多态，因此它们默认为 public。

## 使用保护接口成员进行额外的封装和多态

在创建类时，程序员在选择允许重写方法时应非常小心，因为他们无法控制派生实现。virtual 方法不应包含关键代码，因为如果派生类重写了它们，这些方法可能永远不会被调用。

> 列表 8.13：粗率依赖虚方法的实现

```
public class WorkflowActivity {
    private static void Start()
    {
        // 关键代码
    }
    public virtual void Run()
{
        Start();
        // 执行某些操作...
        Stop();
    }
    private static void Stop()
    {
        // 关键代码
    }
}
```

在重写 Run() 时，开发者可能会调用关键的 Start() 和 Stop() 方法。

