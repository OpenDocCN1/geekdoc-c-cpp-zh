

num = i;
}

public int GetNum() {
    return num;
}
}

// A generic derived class.
class Gen<T> : NonGen {
    T ob;
    public Gen(T o, int i) : base (i) {
        ob = o;
    }
    // Return ob.
    public T GetOb() {
        return ob;
    }
}
// Create a Gen object.
class HierDemo3 {
    static void Main() {
        // Create a Gen object for string.
        Gen<String> w = new Gen<String>("Hello", 47);
        Console.Write(w.GetOb() + " ");
        Console.WriteLine(w.GetNum());
    }
}

程序的输出如下所示：

```
Hello 47
```

在程序中，注意 Gen 如何在以下声明中继承 NonGen：

```
class Gen<T> : NonGen {
```

因为 NonGen 不是泛型的，所以没有指定类型参数。因此，尽管 Gen 声明了类型参数 T，但 NonGen 不需要它（也不能使用它）。因此，NonGen 被 Gen 以正常方式继承。没有特殊条件适用。

## 在泛型类中重写虚方法

泛型类中的虚方法可以像其他任何方法一样被重写。例如，考虑以下程序，其中虚方法 GetOb() 被重写：

```
// Overriding a virtual method in a generic class.
using System;
```

```csharp
// A generic base class.
class Gen<T> {
    protected T ob;

    public Gen(T o) {
        ob = o;
    }

    // Return ob. This method is virtual.
    public virtual T GetOb() {
        Console.Write("Gen's GetOb(): ");
        return ob;
    }
}

// A derived class of Gen that overrides GetOb().
class Gen2<T> : Gen<T> {

    public Gen2(T o) : base(o) { }

    // Override GetOb().
    public override T GetOb() {
        Console.Write("Gen2's GetOb(): ");
        return ob;
    }
}

// Demonstrate generic method override.
class OverrideDemo {
    static void Main() {

        // Create a Gen object for int.
        Gen<int> iOb = new Gen<int>(88);

        // This calls Gen's version of GetOb().
        Console.WriteLine(iOb.GetOb());

        // Now, create a Gen2 object and assign its
        // reference to iOb (which is a Gen<int> variable).
        iOb = new Gen2<int>(99);

        // This calls Gen2's version of GetOb().
        Console.WriteLine(iOb.GetOb());
    }
}
```

输出如下所示：

Gen's GetOb(): 88
Gen2's GetOb(): 99

正如输出所确认的那样，对于类型为 Gen2 的对象会调用 GetOb() 的重写版本，但对于类型为 Gen 的对象会调用基类版本。

注意另一件事：这行代码

```
iOb = new Gen2<int>(99);
```

是有效的，因为 iOb 是类型为 Gen<int> 的变量。因此，它可以引用类型为 Gen<int> 的任何对象，或从 Gen<int> 派生的任何类的对象，包括 Gen2<int>。当然，由于类型不匹配，iOb 不能用于引用类型为 Gen2<double> 的对象，例如。

## 重载使用类型参数的方法

使用类型参数的方法可以被重载。然而，规则比不使用类型参数的方法更为严格。一般来说，使用类型参数作为参数数据类型的方法可以被重载，只要两个版本的签名不同。这意味着它们的参数类型和/或数量必须不同。然而，类型差异的判定不是基于泛型类型参数，而是基于在创建构造类型时为类型参数替代的类型参数。因此，可以以“看起来正确”的方式重载使用类型参数的方法，但不会在所有特定情况下都有效。

例如，考虑这个泛型类：

```csharp
// Ambiguity can result when overloading methods that
// use type parameters.
//
// This program will not compile.

using System;

// A generic class that contains a potentially ambiguous
// overload of the Set() method.
class Gen<T, V> {
    T ob1;
    V ob2;

    // ...

    // In some cases, these two methods
    // will not differ in their parameter types.
    public void Set(T o) {
        ob1 = o;
    }

    public void Set(V o) {
        ob2 = o;
    }
}

class AmbiguityDemo {
    static void Main() {
        Gen<int, double> ok = new Gen<int, double>();
```

```
Gen<int, int> notOK = new Gen<int, int>();
ok.Set(10); // is valid, type args differ
notOK.Set(10); // ambiguous, type args are the same!
}
```

让我们仔细检查这个程序。首先，注意 Gen 声明了两个类型参数：T 和 V。在 Gen 内部，Set() 是基于类型为 T 和 V 的参数重载的，如下所示：

```
public void Set(T o) {
    ob1 = o;
}
public void Set(V o) {
    ob2 = o;
}
```

这看起来合理，因为 T 和 V 看起来是不同的类型。然而，这种重载会产生潜在的歧义问题。

按 Gen 的写法，并没有要求 T 和 V 实际上是不同的类型。例如，按原则上完全正确地构造 Gen 对象如下所示：

```
Gen<int, int> notOK = new Gen<int, int>();
```

在这种情况下，T 和 V 都将被 int 替换。这使得 Set() 的两个版本相同，这当然是一个错误。因此，当稍后在 Main() 中尝试对 notOK 调用 Set() 时，会报告编译时歧义错误。

一般来说，只要没有导致冲突的构造类型，就可以使用类型参数重载方法。重要的是要理解类型约束不参与重载解析。因此，类型约束不能用于消除歧义。像方法一样，使用类型参数的构造函数、运算符和索引器也可以被重载，规则相同。

## 如何实例化泛型类型

在使用泛型时经常提出的一个问题是，使用泛型类是否会导致运行时代码膨胀。简单的答案是否定的。原因是 C# 以高度有效的方式实现泛型，仅在需要时创建新的构造类型。以下是该过程的工作方式。

当泛型类编译为 MSIL 时，它保留了所有类型参数的泛型形式。在运行时，当需要类的特定实例时，JIT 编译器会构造类的特定可执行代码版本，其中类型参数被类型参数替换。使用相同类型参数的类的每个实例都将使用相同的可执行代码版本。

例如，给定一个名为 Gen<T> 的泛型类，那么所有 Gen<int> 对象都将使用相同的可执行代码。因此，代码膨胀减少，只有程序中实际使用的类版本才会被创建。当需要不同的构造类型时，会编译类的新版本。

一般来说，对于类型参数为值类型（如 int 或 double）的每个构造类型，都会创建一个泛型类的新可执行版本。因此，Gen<int> 的每个对象将使用一个版本的 Gen，而类型为 Gen<double> 的每个对象将使用另一个版本的 Gen，每个版本的 Gen 都针对特定的值类型进行定制。然而，对于类型参数为引用类型的所有情况，只有一个泛型类版本。这是因为所有引用的大小（以字节为单位）相同。因此，只需要一个版本来处理所有类型的引用。这种优化也减少了代码膨胀。

## 一些泛型限制

使用泛型时需要记住以下几个限制：

- 属性、运算符、索引器和事件不能是泛型的。然而，这些项可以在泛型类中使用，并且可以使用该类的泛型类型参数。
- extern 修饰符不能应用于泛型方法。
- 指针类型不能用作类型参数。
- 如果泛型类包含静态字段，则每个构造类型都有该字段的自己的副本。这意味着同一构造类型的每个实例共享相同的静态字段。然而，不同的构造类型共享该字段的不同副本。因此，静态字段不被所有构造类型共享。

## 关于泛型的最终想法

泛型是 C# 的强大扩展，因为它们简化了类型安全、可重用代码的创建。尽管泛型语法乍一看可能有点令人不知所措，但它很快就会变得得心应手。同样，学习如何以及何时使用约束需要一些练习，但随着时间的推移会变得更容易。泛型现在是 C# 编程不可或缺的一部分。掌握这一重要特性所付出的努力是值得的。

