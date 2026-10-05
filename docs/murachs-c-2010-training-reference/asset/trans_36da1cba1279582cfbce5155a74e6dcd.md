

# 如何使用抽象类和密封类

本章的最后两个主题展示了如何通过抽象类（abstract）和密封类（sealed）来在你创建的类中要求或限制继承的使用。

## 如何使用抽象类

抽象类是一种无法实例化的类。换句话说，它只能作为其他类可以继承的基类。图 14-17 显示了如何使用抽象类。

要声明一个抽象类，你需要在类声明中包含 `abstract` 关键字，如此图顶部的 `Product` 类所示。然后，你可以在该类中编写任何你需要的成员。此外，你还可以编写抽象方法和抽象属性。例如，这里显示的 `Product` 类包含一个名为 `GetDisplayText` 的抽象方法。如你所见，该方法的声明包含了 `abstract` 关键字，并且没有编写方法体。
你使用类似的技巧来编写抽象属性，如第二个示例所示。

当你在抽象类包含抽象属性和方法时，你必须在继承该抽象类的非抽象类中对它们进行重写（override）。此图中的第三个示例说明了这一点。在这里，你可以看到一个名为 `Book` 的类继承自 `Product` 类，并重写了该类定义的抽象 `GetDisplayText` 方法。虽然你必须重写抽象属性和方法，但你应该注意它们并没有用 `virtual` 关键字声明。因为抽象属性和方法是隐式虚方法的。

到这里，你可能会奇怪为什么要使用抽象类。为了帮助你理解，请考虑本章预介绍的 `Product Maintenance` 。该应用程序使用了两种类型的对象：`Book` 对象和 `Software` 对象。然而，没有什么可以阻止你创建 `Product` 类的实例。因此，`Product` 类层次结构实际上允许产生三种类型的对象：`Book` 对象、`Software` 对象和 `Product` 对象。

如果这不是你想要的，你可以将 `Product` 类声明为抽象类。这样，你就无法创建 `Product` 本身的实例了。相反，`Product` 类只能作为其他类的基类。

注意，这并不意味着你不能声明抽象类型的变量。它仅仅意味着你不能使用 `new` 关键字配合抽象类型来创建该类型的实例。例如，如果你将 `Product` 类声明为抽象类，你仍然可以声明一个可以持有 `Book` 或 `Software` 对象的 `Product` 变量，如下所示：

```csharp
Product p = new Book("CS10", "Murach's C# 2010",
                "Joel Murach", 54.50m);
```

然而，你将无法使用 `new` 关键字配合 `Product` 类来创建一个 `Product` 对象。

## 抽象 Product 类

```csharp
public abstract class Product {
    public string Code { get; set; }
    public string Description { get; set; }
    public decimal Price { get; set; }

    public abstract string GetDisplayText(string sep)
    // 没有编写方法体。
}
```

## 抽象只读属性

```csharp
public abstract bool Invalid {
    get; // get 访问器没有编写方法体。
}
```

## 继承自抽象 Product 的类

```csharp
public class Book {
    public string Author { get; set; }

    public override string GetDisplayText(string sep) {
        return this.Code + sep + this.Description
        + " (" + this.Author + ")" + sep + this.Price.ToString("c");
    }
}
```

### Description

- 抽象类是一种可以被其他类继承但你无法创建其对象的类。要声明抽象类，请在类声明中编写 `abstract` 关键字。
- 抽象类可以像其他类一样包含属性、方法和其他成员。此外，抽象类可以包含抽象属性和方法。
- 当你在抽象类包含抽象属性和方法时，你必须在继承该抽象类的非抽象类中对它们进行重写。
- 要创建抽象方法，请在方法声明中编写 `abstract` 关键字并省略方法体。
- 要创建抽象属性，请使用类似的技术，在属性声明中编写 `abstract` 关键字。
- 抽象方法是隐式虚式的，因此当子类继承基类时，它必须重写基类中定义的抽象方法。
- 抽象属性和方法不需要用 `virtual` 关键字声明。
- 抽象类可以作为其他类的基类，但不能创建抽象类的实例。

图 14-17 如何使用抽象类

## 如何使用密封类

与可以继承的抽象类相反，密封类（sealed class）是无法被继承的类。因为 C# 编译器不需要为继承和多态生成代码，使用密封类可以带来微小的性能收益。

图 14-18 显示了创建密封类，以及密封属性和方法。要创建密封类，请在类声明中包含 `sealed` 关键字，如图顶部的示例所示。你也可以通过在类声明中省略 `sealed` 关键字，而在特定的属性或方法上编写它。

此示例使用了 A、B、C 三个类。A 类是一个声明了虚方法 `ShowMessage` 的基类。B 类继承 A 并重写了 `ShowMessage` 方法。此外，B 类密封了该方法。然后，C 类继承 B 并尝试重写 `ShowMessage` 方法，由于 B 类密封了该方法，无法这样做。

密封方法的工作原理

```csharp
// 声明了虚方法的基类 A
public class A
{
    public void ShowMessage()
    {
        MessageBox.Show("Hello from class A");
    }
}
```

```csharp
// 继承 A 并重写且密封了方法的类 B
public class B : A
{
    public sealed override void ShowMessage()
    {
        MessageBox.Show("Hello from class B");
    }
}
```

```csharp
// 继承 B 并尝试重写其密封方法的类 C
public class C : B
{
    public override void ShowMessage() // 不允许
    {
        MessageBox.Show("Hello from class C");
    }
}
```

## 密封类的类声明

```csharp
public sealed class Book : Product
```

