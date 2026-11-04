
### Obsolete 特性

Obsolete 特性，即 System.ObsoleteAttribute 的简称，允许你将程序元素标记为过时。它的一般形式如下：

```csharp
[Obsolete("message")]
```

其中，message 在该程序元素编译时显示。下面是一个简短示例：

```csharp
// Demonstrate the Obsolete attribute.

using System;

class Test {

    [Obsolete("Use MyMeth2, instead.")]
    public static int MyMeth(int a, int b) {
        return a / b;
    }

    // Improved version of MyMeth.
    public static int MyMeth2(int a, int b) {
        return b == 0 ? 0 : a / b;
    }

    static void Main() {
        // Warning displayed for this.
        Console.WriteLine("4 / 3 is " + Test.MyMeth(4, 3));

        // No warning here.
        Console.WriteLine("4 / 3 is " + Test.MyMeth2(4, 3));
    }
}
```

编译此程序时，当在 Main() 中遇到对 MyMeth() 的调用，就会生成一条警告，提示用户改用 MyMeth2()。

Obsolete 的第二种形式如下：

```csharp
[Obsolete("message", error)]
```

其中，error 是布尔值。如果为 true，则使用过时项会生成编译错误而不是警告。当然，区别在于包含错误的程序无法编译为可执行程序。

*本页有意留空*

## 泛型

本章探讨 C# 最复杂、最强大的特性之一：*泛型*。有趣的是，尽管泛型如今已是 C# 编程不可或缺的一部分，但它们并未包含在最初的 1.0 版本中，而是由 C# 2.0 加入。

可以说，泛型的加入从根本上改变了 C# 的特性，这并非夸大其词。它不仅新增了一种语法元素，还增加了新能力，并促成了库的许多更改和升级。尽管泛型被引入 C# 已有数年，其影响仍在整个语言中持续回荡。

泛型特性之所以如此重要，是因为它使创建能够以类型安全的方式处理各种数据的类、结构、接口、方法和委托成为可能。如你所知，许多算法无论应用于何种类型的数据，在逻辑上都是相同的。例如，无论队列存储的是 **int**、**string**、**object** 类型的项，还是用户定义的类，支持队列的机制都是相同的。

在泛型之前，你可能需要为同一算法创建多个不同版本，以处理不同类型的数据。通过使用泛型，你可以定义一次解决方案，而不依赖任何特定数据类型，然后无需额外工作即可将该解决方案应用于多种数据类型。

本章介绍泛型的语法、理论和用法。它还展示了泛型如何为一些以前棘手的情况提供类型安全。完成本章后，你会想查看第 24 章，该章介绍集合。在那里你会找到许多泛型在泛型集合类中应用的示例。

### 什么是泛型？

从根本上说，*泛型* 一词意味着 *参数化类型*。参数化类型很重要，因为它们使你能够创建这样的类、结构、接口、方法和委托：其操作的数据类型被指定为参数。例如，使用泛型可以创建一个自动处理不同数据类型的单一类。对参数化类型进行操作的类、结构、接口、方法或委托称为 *泛型*，如 *泛型类* 或 *泛型方法*。

重要的是要理解，C# 一直允许你通过 **object** 类型的引用来创建通用代码。因为 **object** 是所有其他类的基类，所以 **object** 引用可以指向任何类型的对象。因此，在泛型之前的代码中，通用代码使用 **object** 引用来操作各种不同类型的对象。

```csharp
// Show the type of data used by iOb.
iOb.ShowType();

// Get the value in iOb.
int v = iOb.GetOb();
Console.WriteLine("value: " + v);

Console.WriteLine();

// Create a Gen object for strings.
Gen<string> strOb = new Gen<string>("Generics add power.");

// Show the type of data stored in strOb.
strOb.ShowType();

// Get the value in strOb.
string str = strOb.GetOb();
Console.WriteLine("value: " + str);
}
```

该程序产生的输出如下所示：

```
Type of T is System.Int32
value: 102

Type of T is System.String
value: Generics add power.
```

让我们仔细检查这个程序。

首先，注意下面这行如何声明 Gen。

```csharp
class Gen<T> {
```

这里，T 是类型参数的名称。此名称用作占位符，代表创建 Gen 对象时将指定的实际类型。因此，在 Gen 内每当需要类型参数时就使用 T。注意 T 包含在 < > 中。这种语法可以推广。每当声明类型参数时，都要在尖括号内指定它。因为 Gen 使用类型参数，所以 Gen 是泛型类。

在 Gen 的声明中，名称 T 没有特殊含义。任何有效标识符都可以使用，但 T 是传统做法。其他常用的类型参数名称包括 V 和 E。当然，你也可以为类型参数使用描述性名称，例如 TValue 或 TKey。使用描述性名称时，通常以 T 作为首字母。

接下来，T 用于声明一个名为 ob 的变量，如下所示：

```csharp
T ob; // declare a variable of type T
```

如前所述，T 是占位符，代表创建 Gen 对象时将指定的实际类型。因此，实例化 Gen 对象时，ob 将是绑定到 T 的类型的变量。例如，如果为 T 指定类型 string，那么在该实例中，ob 将是 string 类型。

```csharp
ob = o;
}

// Return type object.
public object GetOb() {
    return ob;
}

// Show type of ob.
public void ShowType() {
    Console.WriteLine("Type of ob is " + ob.GetType());
}

// Demonstrate the non-generic class.
class NonGenDemo {
    static void Main() {
        NonGen iOb;

        // Create NonGen object.
        iOb = new NonGen(102);

        // Show the type of data stored in iOb.
        iOb.ShowType();

        // Get the value in iOb.
        // This time, a cast is necessary.
        int v = (int) iOb.GetOb();
        Console.WriteLine("value: " + v);

        Console.WriteLine();

        // Create another NonGen object and store a string in it.
        NonGen strOb = new NonGen("Non-Generics Test");

        // Show the type of data stored in strOb.
        strOb.ShowType();

        // Get the value of strOb.
        // Again, notice that a cast is necessary.
        String str = (string) strOb.GetOb();
        Console.WriteLine("value: " + str);

        // This compiles, but is conceptually wrong!
        iOb = strOb;

        // The following line results in a runtime exception.
        // v = (int) iOb.GetOb(); // runtime error!
    }
}
```

该程序产生以下输出：

```
Type of ob is System.Int32
value: 102
```

运行时调用对象。因此，尽管在程序源代码中 ob 的类型被指定为 object，但在运行时，被引用对象的实际类型是已知的。这就是为什么如果在程序执行期间尝试无效强制转换，CLR 会生成异常。

### 具有两个类型参数的泛型类

你可以在泛型类型中声明多个类型参数。要指定两个或更多类型参数，只需使用逗号分隔的列表。例如，下面的 TwoGen 类是 Gen 类的变体，具有两个类型参数：

```csharp
// A simple generic class with two type parameters: T and V.
using System;

class TwoGen<T, V> {
    T ob1;
    V ob2;

    // Notice that this constructor has parameters of type T and V.
    public TwoGen(T o1, V o2) {
        ob1 = o1;
        ob2 = o2;
    }

    // Show types of T and V.
    public void showTypes() {
        Console.WriteLine("Type of T is " + typeof(T));
        Console.WriteLine("Type of V is " + typeof(V));
    }

    public T getob1() {
        return ob1;
    }

    public V GetObj2() {
        return ob2;
    }
}

// Demonstrate two generic type parameters.
class SimpGen {
    static void Main() {
        TwoGen<int, string> tgObj =
            new TwoGen<int, string>(119, "Alpha Beta Gamma");

        // Show the types.
        tgObj.showTypes();

        // Obtain and show values.
        int v = tgObj.getob1();
        Console.WriteLine("value: " + v);
```
