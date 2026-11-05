
## 10.3 类成员

当字段、方法、属性、事件、运算符或构造函数声明包含 static 修饰符时，它声明一个静态成员。此外，常量或类型声明会隐式声明一个静态成员。静态成员具有以下特征：

-   当静态成员 M 在形式为 E.M 的 *成员访问* (§7.6.4) 中被引用时，E 必须表示包含 M 的类型。E 表示实例是编译时错误。
-   静态字段标识一个存储位置，由给定封闭类类型的所有实例共享。不管创建了多少个给定封闭类类型的实例，静态字段永远只有一个副本。
-   静态函数成员（方法、属性、事件、运算符或构造函数）不作用于特定实例，并且在这种函数成员中引用 `this` 是编译时错误。

当字段、方法、属性、事件、索引器、构造函数或析构函数声明不包含 static 修饰符时，它声明一个实例成员。（实例成员有时称为非静态成员。）实例成员具有以下特征：

-   当实例成员 M 在形式为 E.M 的 *成员访问* (§7.6.4) 中被引用时，E 必须表示包含 M 的类型的实例。E 表示类型是绑定时错误。
-   类的每个实例都包含该类的所有实例字段的单独集合。
-   实例函数成员（方法、属性、索引器、实例构造函数或析构函数）作用于类的给定实例，并且该实例可以作为 `this` (§7.6.7) 访问。

下面的示例说明了访问静态成员和实例成员的规则：

```csharp
class Test
{
    int x;
    static int y;

    void F() {
        x = 1;                 // Okay: same as this.x = 1
        y = 1;                 // Okay: same as Test.y = 1
    }

    static void G() {
        x = 1;                 // Error: cannot access this.x
        y = 1;                 // Okay: same as Test.y = 1
    }
}
```

## 10. 类

```csharp
static void Main() {
    Test t = new Test();    // Okay
    t.x = 1;                // Error: cannot access static member through instance
    t.y = 1;                // Error: cannot access instance member through type
    Test.x = 1;             // Okay
    Test.y = 1;
}
```

F 方法显示，在实例函数成员中，可以使用简单名称 (§7.6.2) 访问实例成员和静态成员。G 方法显示，在静态函数成员中，通过简单名称访问实例成员是编译时错误。Main 方法显示，在成员访问 (§7.6.4) 中，实例成员必须通过实例访问，而静态成员必须通过类型访问。

## 10.3.8 嵌套类型

在类或结构声明内声明的类型称为嵌套类型。在编译单元或命名空间内声明的类型称为非嵌套类型。

> JON SKEET 我听说“顶层类型”这个短语比“非嵌套类型”使用得更频繁——我毫不怀疑我自己也传播了这种非标准术语。考虑到绝大多数类型都是非嵌套的，描述性术语感觉应该是积极的，而不是仅仅是嵌套的缺失。这就是我的借口，顺便说一下，其他人也可以借用。

在示例

```csharp
using System;
class A
{
    class B
    {
        static void F() {
            Console.WriteLine("A.B.F");
        }
    }
}
```

中，class B 是嵌套类型，因为它是在 class A 内声明的，而 class A 是非嵌套类型，因为它是在编译单元内声明的。

> BRAD ABRAMS 我不太喜欢在可重用的库中公开可访问的嵌套类型。嵌套类型的可发现性不是很好。更重要的是，我们已经有一个分组机制——命名空间——应该用来表示相关的类型。

## 10.3.8.1 完全限定名

嵌套类型的完全限定名 (§3.8.1) 为 S.N，其中 S 是声明类型 N 的类型的完全限定名。

## 10.3.8.2 声明的可访问性

非嵌套类型可以具有 public 或 internal 声明的可访问性，并且默认具有 internal 声明的可访问性。嵌套类型也可以具有这些形式的声明可访问性，另外还取决于包含类型是类还是结构，还可以有一种或多种额外的声明可访问性形式：

-   在类中声明的嵌套类型可以具有五种声明的可访问性形式中的任意一种（public、protected internal、protected、internal 或 private），并且与其它类成员一样，默认为 private 声明的可访问性。
-   在结构中声明的嵌套类型可以具有三种声明的可访问性形式中的任意一种（public、internal 或 private），并且与其它结构成员一样，默认为 private 声明的可访问性。

示例

```csharp
public class List
{
    // Private data structure
    private class Node
    {
        public object Data;
        public Node Next;
        public Node(object data, Node next) {
            this.Data = data;
            this.Next = next;
        }
    }

    private Node first = null;
    private Node last = null;
    // Public interface
    public void AddToFront(object o) {...}
    public void AddToBack(object o) {...}
    public object RemoveFromFront() {...}
    public object RemoveFromBack() {...}
    public int Count { get {...} }
}
```

声明了一个私有嵌套类 Node。

## 10.3.8.3 隐藏

嵌套类型可能会隐藏 (§3.7.1) 基成员。new 修饰符允许在嵌套类型声明上使用，以便可以显式表达隐藏。示例

```csharp
class Base
{
    public static void M() {
        Console.WriteLine("Base.M");
    }
}
class Derived: Base
{
    new public class M
    {
        public static void F() {
            Console.WriteLine("Derived.M.F");
        }
    }
}
class Test
{
    static void Main() {
        Derived.M.F();
    }
}
```

显示了一个嵌套类 M，它隐藏了在 Base 中定义的方法 M。

## 10.3.8.4 this 访问

嵌套类型与其包含类型在 this 访问 (§7.6.7) 方面没有特殊关系。具体来说，嵌套类型中的 this 不能用于引用包含类型的实例成员。在嵌套类型需要访问其包含类型的实例成员的情况下，可以通过将包含类型实例的 this 作为嵌套类型的构造函数参数提供来提供访问。下面的示例

```csharp
using System;
class C
{
    int i = 123;
    public void F() {
        Nested n = new Nested(this);
        n.G();
    }
    public class Nested
    {
        C this_c;
        public Nested(C c) {
            this_c = c;
        }
        public void G() {
            Console.WriteLine(this_c.i);
        }
    }
}
class Test
{
    static void Main() {
        C c = new C();
        c.F();
    }
}
```

显示了这种技术。C 的一个实例创建 Nested 的一个实例并将其自己的 this 传递给 Nested 的构造函数，以提供随后对 C 的实例成员的访问。

> JON SKEET  本规范的这一部分乍一看可能很奇怪：为什么要指定你不能做什么？为什么任何人会期望能够从嵌套类型的实例访问包含类型的实例？好吧，在 Java 中，这正是内部类的工作方式。要实现类似 C# 的嵌套类型行为，你需要将嵌套类型声明为 static——这与 C# 中的 static 类完全不同！

## 10.3.8.5 访问包含类型的私有和受保护成员

嵌套类型可以访问其包含类型可访问的所有成员，包括具有 private 和 protected 声明可访问性的包含类型的成员。示例

```csharp
using System;

class C
{
    private static void F() {
        Console.WriteLine("C.F");
    }

    public class Nested
    {
        public static void G() {
            F();
        }
    }
}

class Test
{
    static void Main() {
        C.Nested.G();
    }
}
```

显示了一个包含嵌套类 Nested 的类 C。在 Nested 内部，方法 G 调用在 C 中定义的静态方法 F，而 F 具有 private 声明的可访问性。

> > **JON SKEET** 再次，这与 Java 中的行为不同，在 Java 中，外层类型可以访问嵌套类型的私有成员，但反之则不行。我认为 C# 的方法更合理。它还允许一些不错的模式，例如创建一个具有私有构造函数的抽象类。所有派生类都必须嵌套在抽象类内。奇怪的是，我发现这种行为的主要用例是模拟 Java 枚举。

嵌套类型还可能访问其包含类型的基类型中定义的 protected 成员。在示例

```csharp
using System;

class Base
{
    protected void F() {
        Console.WriteLine("Base.F");
    }
}
```
