
```csharp
// C# 11/.NET 7.0 之前不支持在参数上使用 nameof(text)
[return: NullIfIfNotNull(nameof(text))]
static public string TryGetDigitsAsText(string text)
{
    if (text == null) return null;

    string result = "";
    foreach (char character in text)
    {
        if (TryGetDigitAsText(character, out string digitText))
        {
            if (result != "") result += '-';
            result += digitText.ToLower();
        }
    }
    return result;
}
```

注意，从 `TryGetDigitAsText()` 调用 `digitText.ToLower()` 时即使 `text` 被声明为可空，没有使用合并运算符也不会发出警告。这是因为 `TryGetDigitAsText()` 中的 `text` 参数装饰了 `NullWhen(true)` 特性，它告知编译器：如果方法返回 true（`NullWhen` 特性指定的值），则你的意图是 `digitText` 不为空。`NullWhen` 特性是一个后置条件声明，告知调用者如果方法返回 true，则输出 `(text)` 不为空。

同样，对于 `GetDigitsAsText()`，如果为 `text` 参数指定的值不为空，则返回值将不为空。这是因为前置条件空值特性 `NullIfNotNull` 根据参数 `text` 参数的输入值是否为空来决定返回值是否可能为空。

## 进阶主题

### 使用 Null 修饰符对泛型类型参数进行装饰

在声明泛型修饰符或类型时，你偶尔可能想为类型参数装饰一个可空修饰符。问题在于，可空类型（`Nullable<T>`）与可空引用类型是不同的数据类型。因此，装饰了可空性的类型参数将需要一个约束，将类型参数限制为值类型或引用类型。如果没有这个约束，你将收到以下错误：

```
Error CS8627 类型参数必须已知为值类型或非可空引用类型。考虑添加 'class'、'struct' 或类型约束。
```

然而，如果值类型和引用类型的逻辑是相同的，那么实现两个不同的方法可能会令人沮丧——特别是由于不同的约束不会导致不同的签名，从而无法重载。考虑 6.42 中的代码。

#### 列表 6.42: 带有 MaybeNull 特性的潜在返回

```csharp
// ...
[return: MaybeNull]
static public T GetObject<T>(IEnumerable<T> sequence, Func<T, bool> match)
=>
// ...
```

假设行为是：如果满足 `match` 谓词，则返回该项。然而，如果不存在该项，意图是返回 `default(T)`，对于引用类型这是一个空。遗憾的是，编译器不允许 `T?`。为了在避免警告的同时告知调用者返回可能为空，我们使用后置条件 `MaybeNull` 特性并将返回类型保持为 `T`（无可空修饰符）。

## 解构函数

构造函数允许你获取多个参数并将它们封装到一个对象中。直到现在，我们还没有引入反向操作——将封装的项拆解为部分的构造。当然，你可以手动将每个属性赋值给变量；但如果有大量的变量，将需要许多语句。然而，通过元组，这变得简单得多。例如，你可以声明像列表 6.43 显示的 `Deconstruct()` 方法。

#### 列表 6.43: 定义和使用解构函数

```csharp
public class Employee
{
    // ...
    public void Deconstruct(
        out int id, out string firstName,
        out string lastName, out string salary)
    {
        (id, firstName, salary) =
        (Id, FirstName, Salary);
    }
    // ...
}

public class Program
{
    public static void Main()
    {
        Employee employee;
        employee = new ("Inigo", "Montoya")
        {
            // 使用初始化器语法
            Salary = "Not Enough"
        };
        // ...
        employee.Deconstruct(out _, out string firstName,
        out string lastName, out string salary);

        System.Console.WriteLine(
            "{0} {1}: {2}",
            firstName, lastName, salary);
        );
    }
}
```

这种方法可以像第 5 章预期那样通过内联参数直接调用。然而，如列表 6.44 所示，你可以通过直接将对象实例赋值给元组来隐式地调用 `Deconstruct()` 方法——解构函数。

#### 列表 6.44: 隐式调用解构函数

```csharp
public class Program
{
    public static void Main()
    {
        Employee employee;
        employee = new ("Inigo", "Montoya")
        {
            // 使用初始化器语法
            Salary = "Not Enough"
        }
        // ...
        (_, string firstName, lastName, string? salary) = employee;

        System.Console.WriteLine(
            "{0} {1}: {2}",
            firstName, lastName, salary);
        );
    }
}
```

该语法生成的 CIL 代码与列表 6.43 中高亮的代码相同——只是语法更简单（且不那么明显调用了 `Deconstruct()` 方法）。注意，该语法允许使用元组语法匹配 `out` 参数赋值。它不允许赋值元组类型：

```csharp
(int, string, string, string) tuple = employee;
```

或者使用带命名的项：

```csharp
(int id, string firstName, string lastName, string salary) tuple = employee
```

要声明解构函数，方法名必须是 `Deconstruct`，签名返回 `void` 并仅接受两个或多个 `out` 参数。给定这样的签名，可以将对象实例直接赋值给元组而无需显式调用。注意，在 C# 10 之前，所有赋值值都需要声明。在 C# 10 中，这一限制被消。

## 静态成员

第 1 章中的 HelloWorld 示例简单提到了静态。本节更完整地定义了 `static` 关键字。首先，让我们考虑一个示例。假设每个员工的 `Id` 需要是唯一的。实现这一点的方法是存储一个计数器来跟踪每个员工。然而，如果将值存储为实例字段，则每次实例化对象都会创建一个新的 `NextId` 字段，导致每个 `Employee` 实例都消耗该字段的内存。最大的问题是，每实例化一次 `Employee`，之前实例化对象的 `NextId` 值都需要更新为下一个 ID。在这种情况下，你需要一个所有 `Employee` 实例共享的字段。

### 语言对比：C++——全局变量和函数

与其之前的语言不同，C# 没有全局变量或全局函数。C# 中的所有字段和方法都出现在类的上下文中。在 C# 领域，全局字段或函数的等效物是静态字段或函数。全局变量/函数与 C# 静态字段/方法之间没有功能上的区别，静态字段/方法可以包含 `private` 等访问修饰符，从而限制访问并提供更好的封装。

### 静态字段

要定义跨实例可用的数据，你使用 `static` 关键字，如列表 6.45 所示。

#### 列表 6.45: 声明静态字段

```csharp
public class Employee
{
    public Employee(string firstName, string lastName)
    {
        FirstName = firstName;
        LastName = lastName;
        Id = NextId;
        NextId++;
    }
    // ...

    public static int NextId;
    public int Id { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string? Salary { get; set; } = "Not Enough";

    // ...
}
```

12. 在 C# 7.0 中引入。

在增加 `Id` 之前，立即将新 `Employee` 对象的 `Id` 值赋值为 `NextId`。当创建 `Employee` 类的另一个实例时，`NextId` 会增加，新 `Employee` 对象的 `Id` 字段将持有不同的值。

就像实例字段（非静态字段）可以在声明时初始化一样，静态字段也是如此，如列表 6.46 所示。

#### 列表 6.46：在声明时为静态字段

```sharp
public class Employee
{
  //...
  public static int NextId = 42;
  //...
}
```

与实例字段不同，如果未为静态字段提供初始化，则静态字段将自动分配其默认值（0、null、false 等）——这等同于 `default(T)`，其中 `T` 是类型的名称。因此，即使在 C# 代码中从未显式地为该静态字段赋值，也可能访问它。

非静态字段（或实例字段）为每个所属的对象提供了新的存储位置。相比之下，静态字段不属于实例，而是属于类本身。因此，你通过类名从类外部访问静态字段。考虑列表 6.47 所示的新的 `Program` 类（使用列表 6.45 中的 `Employee` 类以及输出 6.8）。

#### 列表 6.47：访问静态字段

```csharp
using System;

public class Program
{
  public static void Main()
  {
    Employee.NextId = 1000000;

    Employee employee1 = new(
      "Inigo", "Montoya");
    Employee employee2 = new(
      "Princess", "Buttercup");

    Console.WriteLine(
      "{0} {1} ({2})",
      employee1.FirstName,employee1.LastName,employee1.Id);
    Console.WriteLine(
      "{0} {1} ({2})",
      employee2.FirstName,employee2.LastName,employee2.Id);
    Console.WriteLine(
      "$NextId = {Employee.NextId}");
  }
}
// ...
```

#### 输出 6.8

Inigo Montoya (1000000)

Princess Buttercup (1000001)

NextId = 1000002

要设置并检索 `NextId` 静态字段的初始值，你应该使用类名 `Employee`，而不是类型实例的引用。唯一可以省略类名的地方是类内部（或派生类内部）。换句话说，在其他 `Employee.NextId` 中，`Employee(..)` 构造函数没有使用 `Employee.NextId`，因为该代码出现在 `Employee` 类本身的语境中，因此该语境是隐含的。变量的作用域是该变量可以通过其未限定名称被引用的程序语境；静态字段的作用域是类（以及任何派生类）的语境。

尽管你引用静态字段的方式与引用实例字段略有不同，但在同一个类中无法定义一个具有相同名的静态字段和实例字段。由于误引用错误字段的可能性很高，因此 C# 设计者决定防止此类代码出现。因此，名称的重叠会在声明空间内引入冲突。

### 数据可以同时与类和对象关联

类和对象都可以都可以拥有关联的数据，就像它们创建的模具和组件一样。

例如，一个模具可能拥有对应于所创建组件数量的数据、下一个组件的序列号、注入模具的塑料的当前颜色，以及它每小时生产的组件数量。同样，一个组件有自己的序列号、颜色，可能还有创建组件的日期和时间。虽然组件的颜色对应于组件创建时模具内塑料的颜色，但它显然不包含对应于当前模具中塑料颜色的数据，或即将产生的下一个组件的序列号。

在设计对象时，程序员应该注意恰当地声明字段、属性和方法，确定是静态的还是实例的。通常情况下，你应该将不访问任何数据的方法声明为静态方法。同样，静态字段存储与类对应的数据，例如新实例的默认值或已创建的实例数量。实例字段存储与对象关联的数据。

### 静态方法

与静态字段一样，你直接通过类名访问静态方法——例如 `Console.ReadLine()`。此外，不需要实例即可访问该方法。

列表 6.48 提供了另一个关于声明和调用静态方法的示例。

#### 列表 6.48：在 DirectoryInfoExtension 上定义静态方法

```csharp
public static class DirectoryInfoExtension
{
    public static void CopyTo(
        DirectoryInfo sourceDirectory, string target,
        SearchOption option, string searchPattern)
    {
        if (target[target.Length - 1] != Path.DirectorySeparatorChar)
        {
            target += Path.DirectorySeparatorChar;
        }
        Directory.CreateDirectory(target);

        for (int i = 0; i < searchPattern.Length; i++)
        {
            foreach (string file in
                Directory.EnumeratedFiles(
                    sourceDirectory.FullName, searchPattern))
            {
                File.Copy(file,
                    target + Path.GetFileName(file), true);
            }
        }

        // 拷贝子目录（递归地）
        if (option == SearchOption.AllDirectories)
        {
            // ...
        }
    }
}
```

*(注：此处提供的原文代码块似乎存在逻辑重复或混乱，翻译时已按原文结构进行对齐)*

*(由于原文文本在列表 6.48 之后存在大量的逻辑重复和代码片段混合，以下将严格基于原文呈现的文本进行翻译)*

#### 输出 6.8

Inigo Montoya (1000000)

Princess Buttercup (1000001)

NextId = 1000002

要设置并检索 `NextId` 静态字段的初始值，你应该使用类名 `Employee`，而不是类型实例的引用。唯一可以省略类名的地方是类内部（或派生类内部）。换句话说，在其他 `Employee.NextId` 中，`Employee(..)` 构造函数没有使用 `Employee.NextId`，因为该代码出现在 `Employee` 类本身的语境中，因此该语境是隐含的。变量的作用域是该变量可以通过其未限定名称被引用的程序语境；静态字段的作用域是类（以及任何派生类）的语境。

尽管你引用静态字段的方式与引用实例字段略有不同，但在同一个类中无法定义一个具有相同名的静态字段和实例字段。由于误引用错误字段的可能性很高，因此 C# 设计者决定防止此类代码出现。因此，名称的重叠会在声明空间内引入冲突。

### 数据可以同时与类和对象关联

类和对象都可以拥有关联的数据，就像它们创建的模具和组件一样。

例如，一个模具可能拥有对应于所创建组件数量的数据、下一个组件的序列号、注入模具的塑料的当前颜色，以及它每小时生产的组件数量。同样，一个组件有自己的序列号、颜色，可能还有创建组件的日期和时间。虽然组件的颜色对应于组件创建时模具内塑料的颜色，但它显然不包含对应于当前模具中塑料颜色的数据，或即将产生的下一个组件的序列号。
