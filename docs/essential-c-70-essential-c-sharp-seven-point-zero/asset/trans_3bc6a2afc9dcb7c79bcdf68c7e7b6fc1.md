
## 静态方法

与静态字段一样，你直接通过类名来访问静态方法——例如，作为 Console.ReadLine()。此外，无需拥有实例即可访问该方法。

代码清单 6.38 提供了另一个声明和调用静态方法的示例。

### 代码清单 6.38：在 DirectoryInfo 上定义静态方法

```csharp
public static class DirectoryInfoExtension
{
    public static void CopyTo(
        DirectoryInfo sourceDirectory, string target,
        SearchOption option, string searchPattern)
    {
        if (target[target.Length - 1] !=
            Path.DirectorySeparatorChar)
        {
            target += Path.DirectorySeparatorChar;
        }
        if (!Directory.Exists(target))
        {
            Directory.CreateDirectory(target);
        }

        for (int i = 0; i < searchPattern.Length; i++)
        {
            foreach (string file in
                Directory.GetFiles(
                    sourceDirectory.FullName, searchPattern))
            {
                File.Copy(file,
                    target + Path.GetFileName(file), true);
            }
        }

        // Copy subdirectories (recursively)
        if (option == SearchOption.AllDirectories)
        {
            foreach (string element in
                Directory.GetDirectories(
                    sourceDirectory.FullName))
            {
                Copy(element,
                    target + Path.GetFileName(element),
                    searchPattern);
            }
        }
    }
}
```

```csharp
// ...
DirectoryInfo directory = new DirectoryInfo("\\Source");
directory.MoveTo(".\\Root");
DirectoryInfoExtension.CopyTo(
    directory, ".\\Target", 
    SearchOption.AllDirectories, "*");
// ...
```

在代码清单 6.38 中，`DirectoryInfoExtension.CopyTo()` 方法接受一个 `DirectoryInfo` 对象，并将底层的目录结构复制到新位置。

由于静态方法不通过特定实例引用，因此 `this` 关键字在静态方法内部无效。此外，在没有指向字段或方法所属的特定实例的引用的情况下，不可能直接从静态方法内部访问实例字段或实例方法。（请注意，`Main()` 也是静态方法的另一个示例。）

人们可能期望此方法位于 `System.IO.Directory` 类中，或者作为 `System.IO.DirectoryInfo` 上的实例方法。由于两者都不存在，代码清单 6.38 在一个全新的类上定义了这样一个方法。在本章后面“扩展方法”部分中，我们将展示如何使其表现为 `DirectoryInfo` 上的实例方法。

## 静态构造函数

除了静态字段和方法之外，C# 还支持静态构造函数。静态构造函数提供作为初始化类本身而非类实例的手段。此类构造函数不会显式调用；相反，运行时会在首次访问该类时自动调用静态构造函数，无论是通过调用常规构造函数还是通过访问类上的静态方法或字段。由于静态构造函数不能显式调用，因此静态构造函数不允许有参数。

你使用静态构造函数将类内的静态数据初始化为特定值，主要是在初始值涉及比声明时的简单赋值更复杂的逻辑时。请参见代码清单 6.39。

### 代码清单 6.39：声明静态构造函数

```csharp
class Employee
{
    static Employee()
    {
        Random randomGenerator = new Random();
        NextId = randomGenerator.Next(101, 999);
    }

    // ...
    public static int NextId = 42;
    // ...
}
```

代码清单 6.39 将 NextId 的初始值分配为 100 到 1,000 之间的一个随机整数。由于初始值涉及方法调用，因此 NextId 的初始化代码出现在静态构造函数中，而不是声明的一部分。

如果在静态构造函数和声明中都发生 NextId 的赋值，当初始化完成时其值是什么并不明显。C# 编译器生成的 CIL 会将声明赋值移动为静态构造函数内的第一条语句。因此，NextId 将包含由 randomGenerator.Next(101, 999) 返回的值，而不是在 NextId 声明期间分配的值。因此，静态构造函数内的赋值将优先于作为字段声明一部分发生的赋值，这与实例字段的情况相同。请注意，不支持定义静态终结器。

小心不要从静态构造函数中抛出异常，因为这将在应用程序剩余的生命周期内使该类型不可用。⁷

### 高级主题

#### **优先在声明期间进行静态初始化**

静态构造函数在访问类的任何成员之前执行，无论它是静态字段、其他静态成员还是实例构造函数。为了支持这一实践，编译器在所有类型静态成员和构造函数中注入检查，以确保静态构造函数首先运行。

如果没有静态构造函数，编译器将所有静态成员初始化为其默认值，并避免添加静态构造函数检查。结果是，静态赋值初始化在任何静态字段被访问之前被调用，但未必在所有静态方法或任何实例构造函数被调用之前。如果静态成员的初始化成本高昂且不需要在访问静态字段之前执行，这可能提供性能改进。因此，你应该考虑内联初始化静态字段，而不是使用静态构造函数或在声明时初始化。

#### **准则**

- 考虑内联初始化静态字段，而不是显式使用静态构造函数或声明赋值。
- 始于 2.0

## 静态属性

你还将属性声明为静态。例如，代码清单 6.40 将下一个 ID 的数据封装到一个属性中。

```
代码清单 6.40：声明静态属性
```

```csharp
class Employee
{
    // ...

    public static int NextId
    {
        get
        {
            return _NextId;
        }
        private set
        {
            _NextId = value;
        }
    }

    public static int _NextId = 42;
    // ...
}
```

几乎总是最好使用静态属性而不是公共静态字段，因为公共静态字段可以从任何地方调用，而静态属性至少提供了一定程度的封装。

- 始于 6.0

在 C# 6.0 中，包括不可访问的后备字段在内的整个 NextId 实现可以简化为带初始化的自动实现属性：

- 结束于 6.0

```csharp
public static int NextId { get; private set; } = 42;
```

## 静态类

某些类不包含任何实例字段。例如，考虑一个 Math 类，它包含对应于数学操作 Max() 和 Min() 的函数，如代码清单 6.41 所示。

### **代码清单 6.41：声明静态类**

```csharp
// Static class introduced in C# 2.0
public static class SimpleMath
{
    // params allows the number of parameters to vary
    public static int Max(params int[] numbers)
    {
        // Check that there is at least one item in numbers
        if(numbers.Length == 0)
        {
            throw new ArgumentException(
                "numbers cannot be empty", "numbers");
        }

        int result;
        result = numbers[0];
        foreach (int number in numbers)
        {
            if(number > result)
            {
                result = number;
            }
        }

        return result;
    }

    // params allows the number of parameters to vary
    public static int Min(params int[] numbers)
    {
        // Check that there is at least one item in numbers
        if(numbers.Length == 0)
        {
            throw new ArgumentException(
                "numbers cannot be empty", "numbers");
        }

        int result;
        result = numbers[0];
        foreach (int number in numbers)
        {
            if(number < result)
            {
                result = number;
            }
        }
        return result; 
    }
}
```

[脚注 7 说明]
7. 严格来说，是应用程序域的生命周期——公共语言运行时中操作系统的虚拟等价进程。

