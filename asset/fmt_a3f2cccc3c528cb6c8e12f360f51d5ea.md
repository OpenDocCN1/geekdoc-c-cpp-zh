
偶尔地，你可能需要访问某个类型的静态成员。在这种情况下，你可以指定 `null` 作为 `MakeMemberAccess` 方法的第一个参数，而不是指向特定对象实例的引用。下面的代码示例显示了如何创建一个 `MemberExpression` 对象来访问静态属性。

```csharp
// 假设 propertyInfo 对象是有效的 MemberInfo 对象，
// 它引用了某个类型的静态属性。
MemberExpression staticProperty = Expression.MakeMemberAccess(null, propertyInfo);
```

![](img/3ef84844c6ac82b838cfffa6448b2346_373_0.png)

## UnaryExpression 类

`UnaryExpression` 类表示基于一元操作的表达式；即只作用于单个参数的操作。一元操作的一个示例是取值的反数。要创建一个取反值的一元表达式，请使用 `Expression` 类的静态 `Negate` 方法，如代码示例所示。

```csharp
// 假设 parameter 是一个有效的 ParameterExpression 对象
Expression.UnaryExpression negation = Expression.Expression.Negate(parameter);
```

你可以使用以下方法来创建 `UnaryExpression` 对象：

- `ArrayLength`。此方法创建一个表达式，返回作为参数提供的一维数组的长度。
- `Convert`。此方法创建一个表达式，将参数指定的对象转换为由 `System.Type` 对象指定的类型。
- `ConvertChecked`。此方法创建一个表达式，将参数指定的对象转换并检查溢出。
- `Negate`。此方法创建一个对表达式值取反的表达式。
- `NegateChecked`。此方法创建一个对表达式值取反并检查溢出的表达式。
- `Not`。此方法创建一个对参数执行按位取反操作的表达式。
- `Quote`。此方法创建一个返回参数类型的常量值的表达式。
- `TypeAs`。此方法创建一个执行显式转换的表达式，如果转换失败则返回 null。
- `UnaryPlus`。此方法创建一个执行一元操作的表达式。

## 构建 Lambda 表达式

Lambda 表达式包含两个主要元素：参数列表和一个基于这些参数计算的体。例如，下面的代码示例显示了一个接受名为 x 的单个参数的 lambda 表达式。该 lambda 表达式的体是一个基于此参数的二元表达式。

```
x => x > 2
```

你使用泛型 `Expression<TDelegate>` 类型构造表示 lambda 表达式的表达式树。`TDelegate` 类型应该引用匹配 lambda 表达式的签名。在这种情况下，你可以使用 `Func<int, bool>`，表示单个参数并返回布尔值的委托。

你使用 `Expression.Parameter` 方法构建表示 lambda 表达式参数的表达式树。该方法期望参数类型和名称作为参数。然后你可以构造一个引用此参数并执行指定计算的 `BinaryExpression` 对象。最后，你可以使用泛型 `Expression.Lambda` 方法将这两个表达式树组合成 lambda 表达式，指定 lambda 表达式引用的委托类型作为参数类型。下面的代码示例显示了如何为前面示例中的 lambda 表达式构建表达式树。

```csharp
Expression<Func<int, bool>> lambda = null;
ParameterExpression param = Expression.Parameter(typeof(int), "x");
ConstantExpression two = Expression.Constant(2, typeof(int));
BinaryExpression body = Expression.GreaterThan(param, two);
lambda = Expression.Lambda<Func<int, bool>>(body, param);
Console.WriteLine(lambda.ToString());
```

下面的代码示例显示了这段代码生成了什么：

```
x => x > 2
```

问题：你会如何定义一个检查命名为 x 是否等于常量值 24 的表达式？

## 扩展阅读

有关 `System.Linq.Expressions` 命名空间中表达式类型的更多信息，请参阅 [System.Linq Expressions 命名空间页面](http://go.microsoft.com/fwlink/?LinkIdId=192983)。

有关 `Expression` 类的更多信息，请参阅 [Expression 类页面](http://go.microsoft.com/fwlink/?LinkIdId=192984)。

# 在运行时获取类型信息

当你开发一个表达式树时，你无法直接使用 C# 对象的属性。

你必须使用反射来访问访问对象的类型和成员。

- 使用 `Type` 类来表示对象的类型
- 使用 `MemberInfo` 类来表示成员

```csharp
Type stringType = typeof(string);
MemberInfo stringLength = stringType.GetProperty("Length");
```

> 表示字符串类型
>
> 表示 Length 成员

## 关键点

C# 编译器会强制执行类型安全，如果你的代码不是类型安全的，它将生成编译器错误。当你使用表达式树时，类型安全性会在表达式构建后、求值之前的运行时检查。某些 `Expression` 方法（例如 `MakeMemberAccess`）期望你提供所引用成员的类型信息。其他方法（例如 `Expression.Constant` 和 `Expression.Parameter`）则期望你提供与表达式相关的常量或参数的类型信息。你可以使用反射动态获取这些类型信息。

## System.Type 类型

获取类型信息的最简单方法是使用 `typeof` 运算符。该运算符接受一个类型作为参数，并返回一个 `System.Type` 对象，该对象包含此类型的详细元数据。通用语言运行时（CLR）可以使用这些元数据来执行类型检查。

使用反射获取类型信息是一项开销较大的操作。如果你只需要引用一次类型，可以使用内联的 `typeof` 关键字；但是，如果你需要多次引用同一个类型，应该创建一个 `Type` 实例并使用该实例。

下面的代码示例显示了如何创建一个表示字符串类型的 `Type` 实例。

```csharp
Type stringType = typeof(string);
```

然后你可以像下面的代码示例所示，引用 `stringType` 对象来指定 `ParameterExpression` 对象的类型。

```csharp
ParameterExpression param = Expression.Parameter(stringType, "data");
```

## MemberInfo 类型

`Type` 类允许你引用一个类型；但是，你可能需要访问对象的成员而不是类。要引用对象的成员，可以使用 `MemberInfo` 类。`MemberInfo` 类定义在 `System.Reflection` 命名空间中。要创建 `MemberInfo` 对象，请使用 `Type` 类暴露的实例方法。有许多方法，包括 `GetField` 和 `GetProperty`，你可以通过这些方法获取有关类型公开的字段和属性的信息。这些方法中的许多都需要你以字符串指定成员名称。但请注意，如果你提供无效的成员名称，该方法将返回 `null`。

下面的代码示例显示了如何创建一个表示字符串对象 `Length` 的 `MemberInfo` 对象。你可以将 `StringLength` 对象作为 `MakeMemberAccess` 方法的 `MemberInfo` 参数，并创建一个比较字符串长度与特定值大小的表达式。

```csharp
Type stringType = typeof(string);
MemberInfo stringLength = stringType.GetProperty("Length");
string data = "Hello, World!";
MemberExpression length = Expression.MakeMemberAccess(
    Expression.Constant(data), stringLength);
ConstantExpression maxLength = Expression.Constant(25);
BinaryExpression compareLength = Expression.GreaterThan(
    length, maxLength);
Console.WriteLine(compareLength.ToString());
```

下面的代码示例显示了该代码生成的输出。

```
("Hello, World!".Length >= 25)
```

![](img/3ef84844c6ac82b838cfffa6448b2346_378_0.png)

问题：在表示字符串类型的 `Type` 类实例上调用 `GetProperty` 方法并提供字符串 "ToString"，结果是什么？

## 编译并运行动态 LINQ 查询

你可以使用 `Expression<TDelegate>` 类暴露的 `Compile` 实例方法将 lambda 编译为可执行的 lambda 表达式。

```csharp
Expression<Func<int, bool>> expressionTree =
    Expression.Lambda<Func<int, bool>>(expression, parameter);
```

```csharp
Func<int, bool> myDelegate = null;
myDelegate = expressionTree.Compile();
```

你可以将 `Compile` 方法作为扩展方法的参数参数：

```csharp
var bankAccounts = accounts.Where(expressionTree.Compile());
```

你可以使用 `Compile` 方法返回的 `TDelegate` 对象的 `DynamicInvoke` 方法来调用 lambda 表达式。

```csharp
bool response = expressionTree.Compile().DynamicInvoke(null);
```

## 关键点

表达式树仅仅是一个数据结构。要在运行时使用表达式树，必须对其进行编译。你可以通过使用 `Expression<TDelegate>` 类型的 `Compile` 方法来实现。

`Compile` 方法接收表示 lambda 表达式的树并返回一个可以调用的 `TDelegate` 对象。如果 lambda 表达式定义了 LINQ 查询的元素，你只需要遍历返回的结果来运行该表达式。

> 注意：你不局限于仅在 LINQ 查询中使用动态 lambda 表达式；在任何可以使用静态 lambda 表达式的地方，都可以使用动态构造的 lambda 表达式。要在 LINQ 查询中运行动态 lambda 表达式，可以使用 `Compile` 方法返回的 `TDelegate` 对象的 `DynamicInvoke` 方法。

# 14-46 使用 Microsoft® Visual Studio® 2010 进行 C# 编程

Alison
Antony
Charles
Chris
Louisa
Mike
Richard

**问题**：`Compile` 方法的目的是什么？

## 扩展阅读

有关关于使用表达式树构建动态查询的更多信息，请参阅 [“如何制定：使用表达式树构建动态查询 (C# 和 Visual Basic)”页面](http://go.microsoft.com/fwlink/?LinkId=1929885)。

## 实验：使用 LINQ 查询数据

- 练习 1：使用 LINQ 查询操作符
- 练习 2：构建动态 LINQ 查询

| 虚拟机 | 10266A-GEN-DEV |
| 用户名 | Student |
| 密码 | Pa$$word |

登录信息
预计耗时：60 分钟

# 目标

在完成本实验后，你将能够：

- 使用 LINQ 查询操作符从枚举集合中检索数据。
- 使用表达式树和 LINQ 扩展方法构建动态 LINQ 查询。

## 引言

在本实验中，你将使用 LINQ 查询操作符从集合中检索数据。然后你将研究如何动态构造 LINQ 查询并对其进行优化以获得更好的性能。

## 实验设置

对于本实验，你将使用提供的虚拟机环境。在开始实验之前，你必须：

- 启动 10266A-GEN-DEV 虚拟机，并使用以下凭据登录：
  - 用户名：Student
  - 密码：PaSSword

## 实验场景

![](img/3ef84844c6ac82b838cfffa6448b2346_386_0.png)

Fabrikam, Inc. 生产一系列高度敏感的测量设备，这些设备可以重复测量物体并捕获数据。

Fabrikam, Inc. 拥有大量分析数据的分析应用程序。这些数据存储在各种测量设备生成的生成文件中。然而，其中许多应用程序的逻辑非常复杂，而且应用程序本身也难以使用。你被要求构建一个更易用的应用程序来分析一组特定数据的测试结果：主梁压力测试的结果。这些数据包含以下字段：

- 测试日期。
- 记录测试时的温度。
- 施加在主梁上的压力。
- 该压力导致的主梁挠变。

此应用程序必须允许用户根据他们指定的标准来过滤他们想要查看的数据。

## 练习 1：使用 LINQ 查询操作符

在此练习中，你将编写一个程序，使用 LINQ 查询操作符来检索和显示数据。数据提供在二进制文件中。应用程序将这些数据读入 `BinaryTree` 对象中，并显示一个 WPF 窗口，允许用户指定查看数据的标准。该窗口将按日期顺序从 `BinaryTree` 对象获取并显示所有匹配的数据。

此练习的主要任务如下：

1. 打开启动解决方案。
2. 声明变量以指定压力数据文件名和 Tree 对象。
3. 添加一个方法来读取测试数据。
4. 使用 `BackgroundWorker` 对象读取测试数据。
5. 定义 LINQ 查询。
6. 执行查询。
7. 使用 `BackgroundWorker` 对象运行查询。
8. 显示结果。
9. 测试解决方案。

### 任务 1：打开启动解决方案

1. 以 Student 身份使用密码 `PassSword` 登录 10266A-GEN-DEV 虚拟机。
2. 打开 Visual Studio 2010。
3. 从 `E:\Labfiles\Lab 14\Snippets` 文件夹导入代码片段。
4. 打开 `E:\Labfiles\Lab 14\Ex1\Starter` 文件夹中的 `StressDataAnalyzer` 解决方案。
5. 检查 `StressDataAnalyzer` 应用程序的用户界面 (UI)。注意应用程序的以下功能：

- 测试数据由压力测试设备生成。数据存储在二进制数据文件中，应用程序在启动运行时会从该文件中读取数据。应用程序使用 `Tree` 对象在内存中持有数据。
- UI 包含两个主要区域。上方区域允许用户指定标准。下方区域显示结果。

测试数据标准为：

i. 测试日期。
ii. 记录测试时的温度。
iii. 施加在主梁上的压力。
iv. 该压力导致的主梁挠变。

### 任务 2：声明变量以指定压力数据文件名和 Tree 对象

1. 检查列表。
2. 在列表中找到 `TODO - Declare variables`。
3. 在列表中找到 `TODO - Define the following:`：
   a. 一个名为 `stressFileName` 的私有字符串。
   b. 一个名为 `stressData` 的 `Tree<TestResult>`。

### 任务 3：添加一个方法来读取测试数据

1. 在列表中找到 `TODO - Add a method to read the test data`。
2. 在列表中找到 `TODO - You can either type or use code manually.`。

```csharp
private void ReadTestData()
{
    // 打开持有测试数据的流。
    using (FileStream readStream = File.Open(stressFileName, FileMode.Open))
    {
        // 数据被序列化为 TestResult 实例
        BinaryFormatter formatter = new BinaryFormatter();
        TestResult initialNode = (TestResult)formatter.Deserialize(readStream);
        // 创建二叉树并将第一个项目
        // 作为根节点。
        stressData = new Tree<TestResult>(initialNode);
        // 从文件的剩余部分读取 TestResult 实例
        // 并将其加入二叉树中
        while (readStream.Position < readStream.Length)
        {
            TestResult data = (TestResult)formatter.Deserialize(readStream);
            stressData.Insert(data);
        }
    }
}
```
