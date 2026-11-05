

将包含类型的实例的 `this` 作为嵌套类型的构造函数参数传递。下面的示例

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

展示了这种技术。C 的实例创建 Nested 的实例，并将自身的 `this` 传递给 Nested 的构造函数，以便后续访问 C 的实例成员。

> **JON SKEET** 规范中的这一节乍看之下可能有些奇怪：为什么要费心规定你不能做什么？为什么有人会期望从嵌套类型的实例访问包含类型的实例？嗯，在 Java 中，内部类正是这样工作的。要实现类似 C# 的嵌套类型行为，你需要将嵌套类型声明为 static——这与 C# 中的静态类完全不同！

### 10.3.8.5 对包含类型的私有成员和受保护成员的访问

嵌套类型可以访问其包含类型可访问的所有成员，包括包含类型中声明为私有和受保护可访问性的成员。下面的示例

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

展示了一个类 C，其中包含嵌套类 Nested。在 Nested 内部，方法 G 调用 C 中定义的静态方法 F，而 F 具有私有声明可访问性。

> > **JON SKEET** 同样，这种行为与 Java 中的行为不同：在 Java 中，外部类型可以访问嵌套类型的私有成员，但反过来不行。我认为 C# 的做法更合理。它还允许一些不错的模式，例如创建一个带有私有构造函数的抽象类：所有派生类都必须嵌套在该抽象类中。奇怪的是，我发现这种行为的主要用例是模拟 Java 枚举。

嵌套类型还可以访问其包含类型的基类型中定义的受保护成员。在下面的示例中

```csharp
using System;

class Base
{
    protected void F() {
        Console.WriteLine("Base.F");
    }
}

class Derived: Base
{
    public class Nested
    {
        public void G() {
            Derived d = new Derived();
            d.F();          // Okay
        }
    }
}
class Test
{
    static void Main() {
        Derived.Nested n = new Derived.Nested();
        n.G();
    }
}
```

嵌套类 Derived.Nested 通过 Derived 的实例调用 Derived 的基类 Base 中定义的受保护方法 F。

### 10.3.8.6 泛型类中的嵌套类型

泛型类声明可以包含嵌套类型声明。封闭类的类型参数可以在嵌套类型中使用。嵌套类型声明可以包含仅适用于该嵌套类型的附加类型参数。

泛型类声明中包含的每个类型声明都隐式地是泛型类型声明。编写对泛型类型中嵌套的类型的引用时，必须指定包含它的构造类型，包括其类型实参。但是，在外部类内部，嵌套类型可以不加限定地使用；构造嵌套类型时，可以隐式使用外部类的实例类型。下面的示例展示了引用由 Inner 创建的构造类型的三种不同且正确的方式；前两种是等效的：

```csharp
class Outer<T>
{
    class Inner<U>
    {
        public static void F(T t, U u) {...}
    }

    static void F(T t) {
        Outer<T>.Inner<string>.F(t, "abc");   // These two statements
        Inner<string>.F(t, "abc");            // have the same effect

        Outer<int>.Inner<string>.F(3, "abc"); // This type is different

        Outer.Inner<string>.F(t, "abc");      // Error: Outer needs type arg
    }
}
```

尽管这是一种糟糕的编程风格，但嵌套类型中的类型参数可以隐藏外部类型中声明的成员或类型参数：

```csharp
class Outer<T>
{
    class Inner<T>    // Valid: hides Outer's T
    {
        public T t;   // Refers to Inner's T
    }
}
```

## 10.3.9 保留成员名称

为了便于底层 C# 运行时实现，对于每个为属性、事件或索引器的源成员声明，实现必须根据成员声明的种类、名称和类型保留两个方法签名。如果程序声明了签名与这些保留签名之一匹配的成员，则属于编译时错误，即使底层运行时实现并未使用这些保留。

保留名称不会引入声明；因此它们不参与成员查找。但是，声明所关联的保留方法签名确实参与继承（§10.3.3），并且可以用 `new` 修饰符隐藏（§10.3.4）。

保留这些名称有三个目的：

- 它允许底层实现使用普通标识符作为方法名，以 get 或 set 访问 C# 语言功能。
- 它允许其他语言互操作，使用普通标识符作为方法名，以 get 或 set 访问 C# 语言功能。
- 它通过使保留成员名称的具体细节在所有 C# 实现中保持一致，帮助确保一个符合规范的编译器接受的源能被另一个编译器接受。

析构函数（§10.13）的声明也会导致保留一个签名（§10.3.9.4）。

### 10.3.9.1 为属性保留的成员名称

对于类型为 T 的属性 P（§10.7），保留以下签名：

```
T get_P();
void set_P(T value);
```

即使属性是只读或只写的，这两个签名也都会保留。

> > **BILL WAGNER** 尽管你可以编写名为 `get_<something>` 和 `set_<something>` 的方法，但如果 `<something>` 不是属性名，则不推荐使用这种技术。避免这样做将最大限度地减少将来更新代码的需要。

在下面的示例中

```csharp
using System;

class A
{
    public int P {
        get { return 123; }
    }
}

class B: A
{
    new public int get_P() {
        return 456;
    }

    new public void set_P(int value) {
    }
}

class Test
{
    static void Main() {
        B b = new B();
        A a = b;
        Console.WriteLine(a.P);
        Console.WriteLine(b.P);
        Console.WriteLine(b.get_P());
    }
}
```

类 A 定义了只读属性 P，因此保留了 get_P 和 set_P 方法的签名。类 B 派生自 A，并隐藏了这两个保留签名。该示例产生以下输出：

```
123
123
456
```

### 10.3.9.2 为事件保留的成员名称

对于委托类型为 T 的事件 E（§10.8），保留以下签名：

```
void add_E(T handler);
void remove_E(T handler);
```

### 10.3.9.3 为索引器保留的成员名称

对于类型为 T、参数列表为 L 的索引器（§10.9），保留以下签名：

```
T get_Item(L);
void set_Item(L, T value);
```

即使索引器是只读或只写的，这两个签名也都会保留。此外，成员名称 Item 也会保留。

### 10.3.9.4 为析构函数保留的成员名称

对于包含析构函数（§10.13）的类，保留以下签名：

```
void Finalize();
```

## 10.4 常量

常量是一种类成员，表示一个常量值——一个可以在编译时计算的值。常量声明引入一个或多个给定类型的常量。

```
constant-declaration:
    attributes_opt constant-modifiers_opt const type constant-declarators ;
```

```
constant-modifiers:
    constant-modifier
    constant-modifiers constant-modifier
```

- new
- public
- protected
- internal
- private

```
constant-declarators:
    constant-declarator
    constant-declarators , constant-declarator
```

