

同样地，在代码开发过程中，我们可能会以相同的方式遇到多种数据类型。例如，代码中有一堆字符串。我们可以利用列表的内置功能对其执行某些操作。不仅如此，代码中还有一个整数列表，我们可以完全自由地使用内置列表功能来运行操作。

那么，设想一下，如果我们需要实现一个用户自定义的功能，并且它需要能兼容并适用于所有基本数据类型和用户自定义数据类型。因此，我们需要开发一个类似于 List（C# 集合中自带的那种）的泛型类，并且它应包含与列表相同的方法（Add、AddRange、Where 等）。这些方法还必须能与新类所支持的相同数据类型集合一起工作。

那么，如何创建一个在运行时指定数据类型并执行其中方法的用户自定义类呢？C# 提供了一项名为泛型（Generics）的功能，为我们解答了这个问题。

## 什么是泛型

泛型是一种允许用户使用占位符定义类和方法的类。泛型是在 C# 语言 2.0 版本中引入的。使用泛型的基本思想是让类型（Integer、String 等，以及用户自定义类型）成为类、方法和接口的参数。集合的一个主要限制是缺乏编译时类型检查。这实际上意味着你可以将任何对象放入集合中，因为 C# 编程语言中的所有类都派生自 object 基类。这实际上损害了类型安全性，并与 C# 作为一种类型安全语言的基本定义相矛盾。不仅如此，使用集合还会以隐式和显式类型转换的形式带来显著的性能开销，而这是向集合添加对象或从集合检索对象所必需的。

为了彻底解决类型安全问题，.NET 框架提供了泛型来创建具有类型占位符的结构、类、方法和接口。泛型通常用于为引用类型和值类型创建类型安全的集合。.NET 框架在 System.Collections.Generic 命名空间中提供了大量的接口和类来实现泛型集合。

### 泛型的特性

泛型是一种可以在很多方面增强程序的技术，例如：

- 它允许你提高代码性能、代码复用性和类型安全性。
- 你可以创建自己的泛型方法、类、接口和委托。
- 你可以创建泛型集合类。.NET Framework 类库在 System.Collections.Generic 命名空间中包含许多新的泛型集合类。
- 你可以在运行时获取泛型数据类型中使用的类型信息。

与传统非泛型类型相比，泛型类型有以下一些重要特征，使其显得特别：

- 类型安全。
- 性能。
- 二进制代码复用。

### 类型安全

泛型最重要的特性之一是类型安全。对于非泛型的 ArrayList 类，如果使用对象，任何类型都可以添加到集合中，这有时会导致严重问题。下面的示例展示了将字符串、整数和一个对象添加到 ArrayList 类型的集合中：

```cs
ArrayList obj = new ArrayList();
obj.Add(50);
obj.Add("Dog");
obj.Add(new TestClass());
```

现在，如果该集合通过 foreach 语句以整数元素进行遍历，编译器会接受这段代码，但由于集合中的所有元素并非都是整数，运行时就会发生异常：

```cs
foreach(int i in obj)
{
    Console.WriteLine(i);
}
```

编程中的经验法则是，错误应该尽早被发现。对于泛型类 `Test<T>`，泛型类型 T 定义了允许的类型。通过 `Test<int>` 的定义，只能将整数类型添加到集合中。编译器不会编译以下代码，因为 Add() 方法包含无效参数：

```cs
Test<int> obj = new Test<int>();
obj.Add(50);
obj.Add("Dog");        // compiler error
obj.Add(new TestClass());   // compiler error
```

### 性能

泛型的另一个关键特性是性能。使用非泛型集合类处理值类型时，一旦值类型被转换为引用类型，通常会产生装箱和拆箱的开销。

在下一个示例中，ArrayList 类存储对象，而 Add() 方法以整数参数被调用。因此，整数会被装箱。当使用 foreach 语句从 ArrayList 读取值时，就会发生拆箱：¹

```cs
ArrayList obj = new ArrayList();
obj.Add(50);      // boxing - convert value type to reference type
int x = (int)obj[0]; // unboxing
foreach(int i in obj)
{
    Console.WriteLine(i);   // unboxing
}
```

泛型比其他集合（如 ArrayList）更快。

与其使用对象，不如将 `TestClass<T>` 类的泛型类型定义为 int，这样编译器动态生成的类内部就会使用 int 类型。因此，装箱和拆箱不再发生，如下所示：

```cs
TestClass<int> obj = new TestClass<int>();
obj.Add(50);      // No boxing
int x = obj[0]; // No unboxing
foreach(int i in obj)
{
    Console.WriteLine(i);      // No unboxing
}
```

### 二进制代码复用

泛型提供了一种源代码复用。一个泛型类可以被定义一次，并用许多不同的类型进行实例化。泛型可以在一种支持 CLR 的语言中定义，并从另一种 .NET 语言中使用。下面的 `TestClass<T>` 分别使用 int 和 string 类型实例化：

```cs
TestClass<int> obj = new TestClass<int>();
obj.Add(50);

TestClass<string> obj1 = new
TestClass<string>();
obj1.Add("hello");
```

### 泛型方法

虽然大多数开发者通常会使用基类库中已有的泛型类型，但你当然也可以构建自己的泛型成员和自定义泛型类型。

这个示例的主要目标是构建一个交换（swap）方法，它可以通过单一类型参数对任何可能的数据类型（基于值或基于引用）进行操作。由于交换算法的性质，传入的参数将通过 ref 关键字以引用方式传递：

```cs
using System;
using System.Collections.Generic;

namespace GenericApp
{
    class Program
    {
        // Generic method
        static void Swap<T>(ref T a, ref T b)
        {
            T temp;
            temp = a;
            a = b;
            b = temp;
        }
        static void Main(string[] args)
        {
            // Swap of two integers.
            int a = 40, b = 60;
            Console.WriteLine("Before swap: {0}, {1}", a, b);
            Swap<int>(ref a, ref b);
            Console.WriteLine("After swap: {0}, {1}", a, b);
            Console.ReadLine();
        }
    }
}
```

### 泛型类和方法

C# 也有并非针对特定类型设计，而是可以用于任何常规类型的类和方法。

我们通常使用 `<>` 尖括号来实现这一目的。假设我们用 `<T>` 设置了一个类或方法，并在方法或类内部对 `T` 执行各种操作。当我们在调用时加上整数类型——`<int>`，那么在编译期间，类或方法内部的 `T` 就会被替换为 int。让我们在这里看看泛型类：

```cs
using System;
class Generic<T>
{
    private T genericVariable;
    public Generic(T genericValue)
    {
        this.genericVariable = genericValue;
    }
    public void Display()
    {
        Console.WriteLine(this.genericVariable);
    }
}
class Test
{
    static void Main(string[] args)
```

```cs
{
    this.genericVariable = genericValue;
}
public void Display()
{
    Console.WriteLine(this.genericVariable);
}
```

让我们再看一个示例：

```cs
using System;
class Generic<T, U>
{
    public T GenericVariableFirst
    {
        get;
        set;
    }
    public U GenericVariableSecond
    {
        get;
        set;
    }
}
class Test
{
    static void Main(string[] args)
    {
        Generic<int, string> g = new Generic<int, string>();
        g.GenericVariableFirst = 10;
        g.GenericVariableSecond = "abc";
        Console.WriteLine(g.GenericVariableFirst);
```

