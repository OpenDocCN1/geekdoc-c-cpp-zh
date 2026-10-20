

## 声明变量为结构类型并为其赋值值的代码

```csharp
// Create an instance of the Product structure
Product p;

// Assign values to each instance variable
p.Code = "C#";
p.Description = "Murach's C#";
p.Price = 59.50m;

// Call a method
string msg = p.GetDisplayText("\n");
```

## 使用默认构造函数初始化实例变量的代码

```csharp
Product p = new Product();
```

## 使用接受参数的构造函数初始化实例变量的代码

```csharp
Product p = new Product("C#", "Murach's C#", 59.50m);
```

## 创建并比较两个结构的代码

```csharp
Product p1 = new Product("C#", "Murach's C#", 57.50m);
Product p2 = new Product("C#", "Murach's C#", 57.50m);
bool isEqual = p1.Equals(p2); // isEqual is true

p2.Price = 59.50m;
isEqual = p1.Equals(p2); // isEqual is false
```

## 复制结构并更改值的代码

```csharp
Product product = new Product("C#", "Murach's C#", 57.50m);
Product copy = product;
copy.Price = 59.50m;
```

描述

- 当你用结构类型声明一个变量时，会创建一个该结构的实例。如果你不使用 new 关键字创建实例，实例变量不会被初始化。
- 要创建结构的实例并将其实例变量初始化为默认值，可使用 new 关键字配合默认构造函数。
- 要通过调用接受参数的构造函数来创建结构的实例，必须使用 new 关键字。
- 在初始化结构的所有实例变量之前，不能调用其任何属性或方法。
- 你可以使用赋值运算符（=）来复制一个结构，就像复制任何值类型一样。
- 与类不同，结构不能被其他类继承。有关继承如何工作，请参阅第 14 章。

> 图 12-25 如何使用结构

## 如何创建和使用记录

图 12-26 显示了创建记录的语法。此语法与创建类或结构的语法类似。记录可以拥有类或结构相同类型的全部成员，包括字段、属性、方法和事件。与结构不同，记录支持继承，类似于类。

本图中的第一个示例展示了一个 Product 记录。这与本章前面介绍的 Product 类和 Product 结构示例类似。该记录定义了三个属性、一个设置这些属性值的构造函数，以及一个名为 GetDisplayText() 的公共方法。

像类一样，记录定义了一个引用类型。然而，记录处理相等比较的方式像结构。换句话说，会比较记录每个属性的值。如果它们都相同，比较结果返回 true。否则返回 false。在下一章，你将学习从类创建的对象如何处理比较。目前你只需要知道，默认情况下，记录的 Equals() 方法的工作方式与从类创建的对象的 Equals() 方法不同。

本图中的第二个代码示例演示了其工作原理。这里，两个属性值相同的记录存储在名为 p1 和 p2 的变量中。因此，当第一个 Equals() 方法比较这两个变量时，返回 true。然而，当代码更改 p2 记录的 Price 属性时，两个变量的属性存储的值不再匹配。所以当第二个 Equals() 方法比较这两个变量时，返回 false。

你也可以创建只包含只读属性的记录，如本图中的第二个语法所示。这与你在图 12-24 中看到的只读结构类似，只是只读记录不能包含方法。要创建只读记录，你将一组属性传递给类似构造函数的语句。请注意，因为这是一个语句，所以以分号结尾。

正如你在前一图中看到的，你可以通过将其赋给新变量来复制结构。然而，这对引用类型不起作用。那是因为引用类型的变量存储的是对对象的引用，而不是对象本身。因此，如果你将变量复制到另一个变量，两个变量都引用同一个对象。然后，如果你使用一个变量更改属性，该更改也会反映在另一个变量中。

因此，要复制引用类型，你需要创建对象的新实例，然后将原始对象的属性值赋给新对象。本图中的最后一个示例展示了两种方法。第一种，你可以将原始对象的值赋给副本，并更改你想要的任何值。这适用于类或记录。第二种，你可以使用 with 关键字配合包含要更改的属性值的花括号。在本图中，例如，最后一条语句创建了 Product 对象的副本，但更改了 Price 属性的值。或者，如果你想在不更改任何属性的情况下复制对象，可以将花括号留空。这仅适用于记录。

## 创建记录的语法（C# 9.0 及更高版本）

```csharp
public record RecordName
{
    record members...
}
```

## 一个 Product 记录

```csharp
public record Product
{
    public Product(string code, string description, decimal price) {...}

    public string Code { get; set; }
    public string Description { get; set; }
    public decimal Price { get; set; }

    public string GetDisplayText(string sep) =>
        Code + sep + Price.ToString("C") + sep + Description;
}
```

## 创建并比较两个记录实例的代码

```csharp
Product p1 = new Product("C#", "Murach's C#", 57.50m);
Product p2 = new Product("C#", "Murach's C#", 57.50m);
bool isEqual = p1.Equals(p2);              // isEqual is true

p2.Price = 59.50m;
isEqual = p1.Equals(p2);                    // isEqual is false
```

## 创建仅包含只读属性的记录的语法

```csharp
public record RecordName(propertyList);
```

## 一个只读 Product 记录

```csharp
public record Product(string Code, string Description, decimal Price);
```

## 复制只读记录的实例并更改值的代码

```csharp
Product product = new Product("C#", "Murach's C#", 57.50m);
```

## 通过将原始值传递给副本的构造函数

```csharp
Product copy1 = new Product(product.Code, product.Description, 59.50m);
```

## 使用 with 关键字

```csharp
Product copy2 = product with { Price = 59.50m };
```

描述

- *record* 是一种像类一样的引用类型。与类不同，记录的 Equals() 方法比较其属性的值。这像结构一样工作。
- 记录可以包含与类相同的类型成员，可以被继承，并且你可以使用对象初始值设定项创建记录的实例。
- 你可以通过将属性列表传递给记录来创建只包含只读属性的记录，但不能对这种类型的记录使用对象初始值设定项。
- 你可以使用 *with* 关键字复制记录并更改一个或多个属性值。

![](img/844f608d10a44654833ea5efc8a2e7a7_445_0.png)

## 视角

到目前为止，你可能在想为什么要付出额外努力将应用程序划分为类。答案有两点。首先，将代码划分为类使得在两个或多个应用程序中重用代码变得更容易。例如，任何需要处理 Products 文件中数据的应用程序都可以使用 Product 和 ProductDB 类。其次，使用类有助于将应用程序的业务逻辑和数据库处理与用户界面分离。这可以简化应用程序的开发，并使其在以后更容易维护和增强。

现在你已经对类的使用有了介绍，可以继续两种不同的方式。如果你已经对类的使用感到舒适，可以阅读本节的下一章到第四章，以了解更多关于面向对象编程的知识。这将为你理解 .NET 类的工作方式以及创建自己的复杂类提供背景知识。

另一方面，如果你刚开始编程并且对类的使用不熟悉，你可能想跳到第 4 或 5 节，在那里你将看到业务类在其他应用程序中的使用。正如你在这些节的章节中会看到的，本章已经为你提供了开发大多数业务类和应用程序所需的技能。然后，当你对类的使用更熟悉时，可以返回到本节的最后四章。

## 术语

- multi-layered architecture
- three-layered architecture
- presentation layer
- database layer
- middle layer
- business layer
- domain layer
- business class
- business object
- three-tiered architecture
- object
- property
- method
- member
- class
- instantiation
- object initializer
- encapsulation
- data hiding
- constructor
- state
- reference type
- class file
- field
- instance variable
- read-only field
- public field
- get accessor
- getter
- set accessor
- setter
- read/write property
- read-only property
- write-only property
- signature
- overloaded method
- static member
- auto-implemented property
- expression-bodied property
- lambda operator
- expression-bodied accessor
- expression-bodied constructor
- type of operator
- pattern matching
- is operator
- not operator
- property pattern
- live code analysis
- feature
- suggestion mode
- completion mode
- Class View window
- CodeLens feature
- Peek Definition
- window
- Go To Definition
- feature
- structure
- read-only structure
- record

