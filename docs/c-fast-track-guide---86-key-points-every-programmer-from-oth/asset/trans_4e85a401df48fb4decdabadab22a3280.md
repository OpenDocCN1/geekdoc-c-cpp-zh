
- **减少垃圾回收开销：** 由于创建的临时对象更少，内存管理更高效。

### 性能比较

```csharp
using System;
using System.Diagnostics;
using System.Text;
class Program
{
static void Main()
{
int iterations = 10000;
// Using string
Stopwatch sw = Stopwatch.StartNew();
string result = "";
for (int i = 0; i < iterations; i++)
{
result += i.ToString(); // Creates a new string each time
}
sw.Stop();
Console.WriteLine("String time: " + sw.ElapsedMilliseconds + "ms");
// Using StringBuilder
sw.Restart();
StringBuilder sb = new StringBuilder();
for (int i = 0; i < iterations; i++)
{
sb.Append(i.ToString()); // Modifies existing buffer
}
sw.Stop();
Console.WriteLine("StringBuilder time: " + sw.ElapsedMilliseconds + "ms");
}
}
```

预期输出：String time: 150ms（因系统而异）

StringBuilder time: 2ms（快得多）

对于大量拼接，StringBuilder 要快得多。如果只是修改字符串一两次，string 就可以了。对于重复修改，StringBuilder 是最佳选择。

### 补充说明

StringBuilder 是 System.Text 的一部分。默认容量为 16 个字符，但它会自动扩展。StringBuilder.AppendFormat() 允许插入格式化文本。使用 .ToString() 获取最终字符串。与 string 不同，sb[0] = 'X'; 允许直接修改字符。

## 7. 属性控制对 C# 中字段的访问

在 C# 中，属性用于提供对类中字段的受控访问。属性可用于定义私有字段的值如何设置或获取。通过使用 getter（访问器）和 setter（修改器），属性允许你隐藏字段的实现细节，同时为外部代码提供与该字段交互的接口。

让我们看一个使用属性控制对字段访问的简单示例：

[代码示例]

```csharp
using System;
public class Person
{
private string name; // Private field
// Property to access the private field
public string Name
{
get { return name; } // Getter
set { name = value; } // Setter
}
}
public class Program
{
public static void Main()
{
Person person = new Person();
person.Name = "John Doe"; // Set the value using the setter
Console.WriteLine(person.Name); // Get the value using the getter
}
}
```

### 执行结果

John Doe

在上面的示例中，我们有一个私有字段 name，并使用属性 Name 来访问和修改其值。get 访问器检索 name 字段的值，set 访问器为其赋值。value 关键字表示传递给 setter 的值。通过使用属性，我们可以在将来需要时轻松地向 getter 或 setter 添加逻辑，而不会影响使用该属性的外部代码。

属性对于实现验证或在存储数据之前修改数据非常有用。你甚至可以使用属性来封装更复杂的逻辑，例如延迟加载或计算。

### 补充说明

在 C# 中，属性是面向对象编程的重要组成部分，因为它们允许封装。它们阻止对字段的直接访问，同时仍然提供一种与其交互的方式。通过确保字段仅以受控方式修改，使用属性可以使代码更易维护、更安全。

## 8. 自动实现属性简化代码

当 getter 或 setter 中不需要额外逻辑时，C# 中的自动实现属性是创建属性的一种简写方式。它通过自动为属性生成一个私有匿名的支持字段来简化代码，从而无需手动定义该字段以及 getter/setter 方法。

让我们看看如何使用自动实现属性简化前面的代码：

[代码示例]

```csharp
using System;
public class Person
{
    // Auto-implemented property (no need for a private field or getter/setter)
    public string Name { get; set; }
}
public class Program
{
    public static void Main()
    {
        Person person = new Person();
        person.Name = "Jane Doe"; // Set the value using the setter
        Console.WriteLine(person.Name); // Get the value using the getter
    }
}
```

### 执行结果

Jane Doe

在这个示例中，我们为 Name 使用了自动实现属性。这个版本的属性会自动为你提供支持字段，因此无需显式定义它。该属性仍然提供对字段的受控访问，但 C# 编译器会自动处理幕后实现。

当你不需要向 getter 或 setter 添加额外逻辑时，自动实现属性非常有用，可使代码更简单、更简洁。它们是减少样板代码并提高可读性的好方法，尤其适用于简单类。

### 补充说明

自动实现属性是在 C# 3.0 中引入的，它使得无需手动定义私有字段即可更轻松地创建简单属性。但是，如果你需要在 getter 或 setter 中添加验证、日志记录或其他逻辑，则需要手动定义属性（如第一个示例所示）。你还可以向自动实现属性添加访问修饰符（例如 private set），以便更好地控制谁可以修改该属性。

## 9. readonly 字段必须在构造函数中设置

在 C# 中，readonly 字段只能在声明时或类的构造函数内赋值。

以下代码展示了如何在构造函数中设置 readonly 字段，而不能在其他地方设置。

[代码示例]

```csharp
using System;
class Person
{
    // Readonly field
    public readonly string Name;

    // Constructor assigns the readonly field
    public Person(string name)
    {
        Name = name; // OK: assigning in constructor
    }

    public void ChangeName(string newName)
    {
        // Name = newName; // ERROR: Cannot assign to readonly field here
    }
}
class Program
{
    static void Main()
    {
        Person p = new Person("Alice");
        Console.WriteLine(p.Name);
    }
}
```

### 执行结果

Alice

readonly 字段是一个只能赋值一次的变量，并且只能在以下位置赋值：

- 在声明时，例如 `public readonly int x = 5;`
- 在定义该字段的类的构造函数内
- 一旦设置，就不能在其他地方更改其值，即使是在同一类的其他方法内也不行。
- 尝试在构造函数外修改它会导致编译时错误：
- "readonly 字段不能被赋值（除非在构造函数或变量初始化器中）"
- 这使得 readonly 非常适合用于在创建对象时确定、之后不应更改的值，例如配置值或标识符。
- 与 const 不同，readonly 允许使用构造函数参数在运行时设置值。

### 补充说明

如果你有一个直到运行时才能知道的值（例如用户输入），但在设置后仍不应更改，那么 readonly 是正确的选择。

readonly 字段也可以与引用类型一起使用；你可以更改对象的内容，但不能更改引用本身。示例：

```csharp
readonly List<int> numbers; → You can do numbers.Add(5);; but not
numbers = new List<int>();
```

### 执行结果

Pi: 3.14159

Created At: [当前日期和时间]

const 值在编译期间直接替换到代码中。这意味着必须使用常量表达式（如数字、字符串等）为其赋值。

示例：

```csharp
const int MaxScore = 100;
```

```csharp
const DateTime Now = DateTime.Now; (Not allowed — not a constant expression)
```

readonly 字段可以使用仅在运行时才知道的值，例如系统时间或用户输入。

这就是为什么 DateTime.Now 可用于 readonly，但不能用于 const。

const 隐式是 static 的，这意味着它在类的所有实例之间共享。readonly 则是每个实例独立的，除非显式标记为 static。

尝试为 const 字段赋予运行时值会导致编译时错误：

> “分配给 'const' 的表达式必须是常量”

### 补充说明
