
带有额外的参数。考虑使用可选参数而非重载，这样“设置默认值”属性的默认值在 API 中是可见的。例如，构造函数签名 `Person(string firstName, string lastName, int? age = null)` 提供了文档说明：如果没有指定 `age`，它将默认为 `null`。同时请注意，构造函数也可以使用表达式体形式实现，如下所示：

```csharp
// LastName inside Id property.
#pragma warning disable CS8618
public Employee(int id) => Id = id;
```

在这种情况下，通过调用 `Id` 属性来分配 `FirstName` 和 `LastName`。遗憾的是，编译器无法检测到赋值，并且从 C# 8.0 开始，会发出警告建议将这些属性声明为可空。由于我们实际上确实设置了它们，因此禁用了该警告。

## 指南

- 如果构造函数参数仅用于设置属性，为构造函数参数（camelCase）和属性（PascalCase）使用相同的名称。
- 提供可选参数或构造函数重载以使用默认值初始化属性。

## 构造函数链：调用另一个构造函数

注意在列表 6.33 中，`Employee` 对象的初始化代码现在多处重复，因此也必须在多个地方进行维护。虽然代码量很少，但有方法可以通过构造函数初始化器从一个构造函数调用另一个构造函数来消除重复——这种做法被称为构造函数链。构造函数初始化器会在执行当前构造函数的实现体之前确定调用哪个构造函数（见列表 6.34）。从 C# 7.0 开始

### 列表 6.34：从一个构造函数调用另一个构造函数

```csharp
public class Employee
{
    public Employee(string firstName, string lastName)
    {
        FirstName = firstName;
        LastName = lastName;
    }

    public Employee(int id, string firstName, string lastName)
        : this(firstName, lastName)
    {
        Id = id;
    }

    // FirstName and LastName inside Id setter.
    #pragma warning disable CS8618
    public Employee(int id)
    {
        Id = id;

        // Look up employee name...
        // ...

        // NOTE: Member constructors cannot be called explicitly inline
        this(id, lastName);
    }
    #pragma warning restore CS8618

    public int Id { get; private set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string? Salary { get; set; } = "Not";
    // ...
}
```

要在同一个类中从一个构造函数调用另一个（针对同一个对象实例），C# 使用冒号后跟 `this` 关键字，然后是被调用构造函数声明参数列表。在这种情况下，接收所有参数的构造函数调用了接收两个参数的构造函数。通常这种调用模式是反过来的——即参数最少的构造函数调用参数最多的构造函数，并为未知的参数传递默认值。

## 主题：集中初始化

注意在列表 6.34 的 `Employee(int id)` 构造函数实现中，你无法调用 `this(firstName, lastName)`，因为该构造函数不存在这些参数。为了启用所有初始化代码都通过一个方法完成的模式，必须创建一个单独的方法，如列表 6.35 所示。

### 列表 6.35：提供初始化方法

```csharp
public class Employee {
    // FirstName and LastName inside Initialize() method.
    #pragma warning disable CS8618
    public Employee(string firstName, string lastName) {
        int id;
        // Generate an employee ID.
        // ...
        Initialize(id, firstName, lastName);
    }
    public Employee(int id, string firstName, string lastName) {
        Initialize(id, firstName, lastName);
    }
    public Employee(int id) {
        string firstName;
        string lastName;
        Id = id;
        // Look up employee data
        // ...
        Initialize(id, firstName, lastName);
    }
}
```

```csharp
#pragma warning restore CS8618
private void Initialize(
    int id, string firstName, string lastName)
{
    Id = id;
    FirstName = firstName;
    LastName = lastName;
}
// ...
```

在这种情况下，该方法命名为 `Initialize()`，它接收姓名和员工 ID。注意，你仍然可以像列表 6.34 所示，从一个构造函数调用另一个构造函数。

与通过 `Id` 属性设置 `LastName` 和 `FirstName` 未被编译器检测到一样，通过 `Initialize` 方法进行的赋值也不会被检测到，因此禁用了警告。

## 带有构造函数的不可空引用类型属性

在本章中，我们一贯地禁用了 C# 的可空警告。

> CS8618: 非可空字段/属性未初始化。考虑将其声明为可空。

当你声明引用类型 (1) 不可空字段或 (2) 不可空自动实现属性时，显而易见这些字段和属性在包含对象完全实例化之前需要初始化。如果不这样做，这些字段和属性将保持默认 `null` 值——因此它们不应被声明为非可空。

问题在于，不可空字段和属性经常被间接初始化，超出了构造函数的直接作用范围，因此超出了编译器的代码分析范围，即使它们实际上仍然被初始化了。以下是一些示例：

- 带有检查值是否为 `null` 的简单属性（见 6.20）。
- 由构造函数初始化的不可空字段或属性。
- 以 6.35 所示方式初始化的不可空字段或属性。
- 通过反射或依赖注入等外部代理初始化的不可空字段或属性。

在大多数情况下，应该避免使用读写不可空类型，特别是带有公共 `setter` 的类型，因为防止 `null` 赋值是有困难的。虽然可以通过从构造函数赋值属性来避免未初始化的非空属性编译器警告，但这是不够的。
