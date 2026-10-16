

```
Console.WriteLine("These are the constructors in our Customer class:--");
foreach (ConstructorInfo c in constructorInfo)
{
    Console.WriteLine(c);
}
```

Type 类中调用的 GetConstructors() 方法会返回 ConstructorInfo 类型的数组——基本上，是反射类型内部定义的所有公共构造函数的列表。

好的，现在我们想要显示 Customer 类的所有公共方法，并且，同样我们只有一个，所以当程序执行时你在控制台上看到的只有这一个名称。要做到这一点，代码看起来像这样：

```
static void Main(string[] args)
{
    Type type = typeof(Customer);
    MethodInfo[] methodInfo = type.GetMethods();
    Console.WriteLine("The Customer class methods are:--");
    foreach (MethodInfo temp in methodInfo)
    {
        Console.WriteLine(temp.Name);
    }
    Console.Read();
}
```

注意，你可能会看到一些额外的方法名称，例如 Equals、ToString、GetType 和 GetHashCode。这是因为这些方法是从名为 Object 的类继承而来的，而且正如你所知，.NET 中的所有类都将派生自该类，因为 Object 是所有事物的基类。

下面的代码展示了如何遍历方法属性。如果你为方法定义了自定义属性，可以在 MethodInfo 类的实例中使用 GetCustomAttributes 方法来获取方法属性：

```
foreach (MethodInfo temp in methodInfo)
{
    foreach (Attribute attribute in temp.GetCustomAttributes(true))
    {
        //You usual code will go here
    }
}
```

如果你使用属性来装饰应用程序中的业务对象，可以使用 C# 反射来反射类型，获取类型方法的属性，然后执行所需的任何操作。

## C# Type 类

C# Type 类用于表示接口类型、类类型、数组类型、枚举类型、值类型等的类型声明。它位于 System 命名空间中并继承自 System.Reflection.MemberInfo 类。

以下是 Type 类的更重要属性列表：

| 属性 | 描述 |
|---|---|
| Assembly | 获取类型的程序集 |
| AssemblyQualifiedName | 获取程序集限定类型的名称 |
| Attributes | 获取与指定类型关联的属性 |
| BaseType | 获取父类型或基类型 |
| Name | 获取指定类型的完全限定名称 |
| IsAbstract | 用于检查类型是否为抽象类型 |
| IsArray | 用于检查类型是否为数组类型 |
| IsClass | 用于检查类型是否为类类型 |
| IsEnum | 用于检查类型是否为枚举类型 |
| IsInterface | 用于检查类型是否为接口类型 |
| IsNested | 用于检查类型是否为嵌套类型 |
| IsPrimitive | 用于检查类型是否为原始类型 |
| IsPointer | 用于检查类型是否为指针类型 |
| IsNotPublic | 用于检查类型是否不是公共类型 |
| IsPublic | 用于检查类型是否为公共类型 |
| IsSealed | 用于检查类型是否为密封类型 |
| IsSerializable | 用于检查类型是否为可序列化类型 |
| MemberType | 用于检查类型是否为嵌套类型的成员类型 |
| Module | 获取类型的模块 |
| Name | 获取类型的名称 |
| Namespace | 获取类型的命名空间 |

### C# Type 方法

下面你可以找到更重要的 Type 类方法列表：

| 方法 | 描述 |
|---|---|
| GetConstructors() | 这将返回该类型的全部公共构造函数 |
| GetConstructors(BindingFlags) | 这将返回具有指定 BindingFlags 的该类型的所有构造函数 |
| GetFields() | 这将返回该类型的所有公共字段 |
| GetFields(BindingFlags) | 这将返回具有指定 BindingFlags 的该类型的所有字段 |
| GetMembers() | 这将返回该类型的全部公共成员。 |
| GetMembers(BindingFlags) | 这将返回具有指定 BindingFlags 的该类型的所有成员 |
| GetMethods() | 这将返回该类型的公共方法 |
| GetMethods(BindingFlags) | 这将返回具有指定 BindingFlags 的该类型的所有方法 |
| GetProperties() | 这将返回该类型的所有公共属性 |
| GetProperties(BindingFlags) | 这将返回具有指定 BindingFlags 的该类型的所有属性 |
| GetType() | 这将获取当前类型 |
| GetType(String) | 这将获取指定名称的类型 |

我们将以一系列示例结束，以便你可以看到其中一些是如何工作的：

## Get Type

```
using System;
public class ReflectionExample
{
    public static void Main()
    {
        int a = 10;
        Type type = a.GetType();
        Console.WriteLine(type);
    }
}
```

输出结果为：

System.Int32

## Get Assembly

```
using System;
using System.Reflection;
public class ReflectionExample
{
    public static void Main()
    {
        Type t = typeof(System.String);
        Console.WriteLine(t.Assembly);
    }
}
```

输出结果为：

mscorlib, Version=4.0.0.0, Culture=neutral,
PublicKeyToken=b77a5c561934e089

## Print Type Information

```
using System;
using System.Reflection;
public class ReflectionExample
{
    public static void Main()
    {
        Type t = typeof(System.String);
        Console.WriteLine(t.FullName);
        Console.WriteLine(t.BaseType);
        Console.WriteLine(t.IsClass);
        Console.WriteLine(t.IsEnum);
        Console.WriteLine(t.IsInterface);
    }
}
```

输出结果为：

System.String
System.Object
true
false
false

## Print Constructors

```
using System;
using System.Reflection;
public class ReflectionExample
{
    public static void Main()
    {
        Type t = typeof(System.String);

        Console.WriteLine("Constructors of {0} type...", t);
        ConstructorInfo[] ci = t.GetConstructors(BindingFlags.Public | BindingFlags.Instance);
        foreach (ConstructorInfo c in ci)
        {
            Console.WriteLine(c);
        }
    }
}
```

输出结果为：

Constructors of System.String type...

Void .ctor(Char*)
Void .ctor(Char*, Int32, Int32)
Void .ctor(SByte*)
Void .ctor(SByte*, Int32, Int32)
Void .ctor(SByte*, Int32, Int32, System.Text.Encoding)
Void .ctor(Char[], Int32, Int32)
Void .ctor(Char[])
Void .ctor(Char, Int32)

## Print Methods

```
using System;
using System.Reflection;
public class ReflectionExample
{
    public static void Main()
    {
        Type t = typeof(System.String);
        Console.WriteLine("Methods of {0} type...", t);
        MethodInfo[] ci = t.GetMethods(BindingFlags.Public | BindingFlags.Instance);
        foreach (MethodInfo m in ci)
        {
            Console.WriteLine(m);
        }
    }
}
```

输出结果为：

Methods of System.String type...
Boolean Equals(System.Object)
Boolean Equals(System.String)
Boolean Equals(System.String, System.StringComparison)
Char get_Chars(Int32)
Void copyTo(Int32, char[], Int32, Int32)
Char[] ToCharArray()
....

## Print Fields

```
using System;
using System.Reflection;
public class ReflectionExample
{
    public static void Main()
    {
        Type t = typeof(System.String);

        Console.WriteLine("Fields of {0} type...", t);
        FieldInfo[] ci = t.GetFields(BindingFlags.Public | BindingFlags.Static | BindingFlags.NonPublic);

        foreach (FieldInfo f in ci)
        {
            Console.WriteLine(f);
        }
    }
}
```

输出结果为：
Fields of System.String type...
System.String Empty
Int32 TrimHead
Int32 TrimTail
Int32 TrimBoth
Int32 charPtrAlignConst
Int32 alignConst

## 匿名函数

匿名函数是没有名称的函数，在 C# 中有两种类型：

- Lambda 表达式
- 匿名方法

我们使用 lambda 表达式来创建匿名函数。

lambda 表达式是一个匿名函数，它有一系列运算符或表达式。每个 lambda 表达式都必须使用 lambda 运算符 =>，它表示“变为”或“转到”。

输入参数位于运算符左侧，表达式或代码块位于右侧并使用输入参数。通常，lambda 表达式用于代替委托，如果你还记得的话，委托是一种用于引用方法或用作谓词的类型。

### 表达式 Lambda

- Parameter => expression
- Parameter-list => expression
- Count => count + 2;
- Sum => sum + 2;
- n => n % 2 == 0

lambda 运算符用于将 lambda 表达式分为两部分——输入参数和 lambda 的主体。这里有一个简单的例子：

```
using System;
using System.Collections.Generic;
using System.Linq;
public static class demo
{
    public static void Main()
```

