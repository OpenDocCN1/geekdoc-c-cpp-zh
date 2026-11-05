

## 第61章：using 指令

### 61.1节：关联别名以解决冲突

如果你使用了多个可能包含同名类的命名空间（例如 System.Random 和 UnityEngine.Random），可以使用别名来指定 Random 来自其中一个，而不必在调用中使用完整的命名空间。

例如：

```
using UnityEngine;
using System;

Random rnd = new Random();
```

这会导致编译器不确定将新变量解析为哪个 Random。相反，你可以这样做：

```
using UnityEngine;
using System;
using Random = System.Random;

Random rnd = new Random();
```

这并不妨碍你使用完全限定的命名空间来调用另一个类，如下所示：

```
using UnityEngine;
using System;
using Random = System.Random;

Random rnd = new Random();
int unityRandom = UnityEngine.Random.Range(0,100);
```

rnd 将是一个 System.Random 变量，unityRandom 将是一个 UnityEngine.Random 变量。

### 61.2节：使用别名指令

你可以使用 using 来为命名空间或类型设置别名。更多细节可以在这里找到。

语法：

```
using <identifier> = <namespace-or-type-name>;
```

示例：

```
using NewType = Dictionary<string, Dictionary<string,int>>;
NewType multiDictionary = new NewType();
//Use instances as you are using the original one
multiDictionary.Add("test", new Dictionary<string,int>());
```

### 61.3节：访问类的静态成员

版本 >= 6.0

允许你导入特定类型，并使用该类型的静态成员，而无需用类型名称限定它们。下面是一个使用静态方法的示例：

```csharp
using static System.Console;

// ...
string GetName()
{
    WriteLine("Enter your name.");
    return ReadLine();
}
```

下面是一个使用静态属性和方法的示例：

```csharp
using static System.Math;

namespace Geometry
{
    public class Circle
    {
        public double Radius { get; set; };
        public double Area => PI * Pow(Radius, 2);
    }
}
```

### 61.4节：基本用法

```csharp
using System;
using BasicStuff = System;
using Sayer = System.Console;
using static System.Console; //From C# 6

class Program
{
    public static void Main()
    {
        System.Console.WriteLine("Ignoring usings and specifying full type name");
        Console.WriteLine("Thanks to the 'using System' directive");
        BasicStuff.Console.WriteLine("Namespace aliasing");
        Sayer.WriteLine("Type aliasing");
        WriteLine("Thanks to the 'using static' directive (from C# 6)");
    }
}
```

### 61.5节：引用命名空间

```csharp
using System.Text;
//allows you to access classes within this namespace such as StringBuilder
//without prefixing them with the namespace. i.e:

//...
var sb = new StringBuilder();
//instead of
var sb = new System.Text.StringBuilder();
```

### 61.6节：将别名与命名空间关联

```csharp
using st = System.Text;
//allows you to access classes within this namespace such as StringBuilder
```

```csharp
//prefixing them with only the defined alias and not the full namespace. i.e:

//...
var sb = new st.StringBuilder();
//instead of
var sb = new System.Text.StringBuilder();
```

## 第62章：IDisposable 接口

### 62.1节：在仅包含托管资源的类中

托管资源是运行时垃圾回收器能够感知并控制的资源。BCL 中有许多可用的类，例如 SqlConnection，它是非托管资源的包装类。这些类已经实现了 IDisposable 接口——由你的代码在使用完毕后负责清理它们。

如果你的类只包含托管资源，则没有必要实现终结器。

```
public class ObjectWithManagedResourcesOnly : IDisposable
{
    private SqlConnection sqlConnection = new SqlConnection();

    public void Dispose()
    {
        sqlConnection.Dispose();
    }
}
```

### 62.2节：在包含托管和非托管资源的类中

重要的是让终结过程忽略托管资源。终结器在另一个线程上运行——当终结器运行时，托管对象可能已经不存在了。实现一个受保护的 Dispose(bool) 方法是常见做法，以确保托管资源的 Dispose 方法不会从终结器中被调用。

```
public class ManagedAndUnmanagedObject : IDisposable
{
    private SqlConnection sqlConnection = new SqlConnection();
    private UnmanagedHandle unmanagedHandle = Win32.SomeUnmanagedResource();
    private bool disposed;

    public void Dispose()
    {
        Dispose(true); // client called dispose
        GC.SuppressFinalize(this); // tell the GC to not execute the Finalizer
    }

    protected virtual void Dispose(bool disposeManaged)
    {
        if (!disposed)
        {
            if (disposeManaged)
            {
                if (sqlConnection != null)
                {
                    sqlConnection.Dispose();
                }
            }

            unmanagedHandle.Release();

            disposed = true;
        }
    }
}
```

```
{
    // do foo stuff
}
finally
{
    if (foo != null)
        ((IDisposable)foo).Dispose();
}
}
```

### 62.5节：在包含托管资源的继承类中

你可能会创建一个实现 IDisposable 的类，然后从中派生也包含托管资源的类，这种情况相当常见。建议用 virtual 关键字标记 Dispose 方法，以便客户端能够清理它们可能拥有的任何资源。

```csharp
public class Parent : IDisposable
{
    private ManagedResource parentManagedResource = new ManagedResource();

    public virtual void Dispose()
    {
        if (parentManagedResource != null)
        {
            parentManagedResource.Dispose();
        }
    }
}

public class Child : Parent
{
    private ManagedResource childManagedResource = new ManagedResource();

    public override void Dispose()
    {
        if (childManagedResource != null)
        {
            childManagedResource.Dispose();
        }
        //clean up the parent's resources
        base.Dispose();
    }
}
```

## 第63章：反射

反射是一种 C# 语言机制，用于在运行时访问动态对象属性。通常，反射用于获取有关动态对象类型和对象属性值的信息。例如，在 REST 应用程序中，反射可用于遍历序列化的响应对象。

备注：根据微软（MS）指南，性能关键的代码应避免使用反射。参见 https://msdn.microsoft.com/en-us/library/ff647790.aspx

### 63.1节：获取类型的成员

```
using System;
using System.Reflection;
using System.Linq;

public class Program
{
    public static void Main()
    {
        var members = typeof(object)
            .GetMembers(BindingFlags.Public |
                        BindingFlags.Static |
                        BindingFlags.Instance);

        foreach (var member in members)
        {
            bool inherited = member.DeclaringType.Equals(typeof(object).Name );
            Console.WriteLine($"{member.Name} is a {member.MemberType}, " +
                $"it has {(inherited ? "":"not")} been inherited.");
        }
    }
}
```

输出（关于输出顺序的说明见下文）：

GetType 是一个方法，它没有被继承。GetHashCode 是一个方法，它没有被继承。ToString 是一个方法，它没有被继承。Equals 是一个方法，它没有被继承。Equals 是一个方法，它没有被继承。ReferenceEquals 是一个方法，它没有被继承。.ctor 是一个构造函数，它没有被继承。

我们也可以在不传递任何 BindingFlags 的情况下使用 GetMembers()。这将返回该特定类型的所有公共成员。

需要注意的一点是，GetMembers 不会按任何特定顺序返回成员，因此永远不要依赖 GetMembers 返回给你的顺序。

查看演示

### 63.2节：获取方法并调用它

#### 获取实例方法并调用它

```
using System;

public class Program
{
    public static void Main()
    {

