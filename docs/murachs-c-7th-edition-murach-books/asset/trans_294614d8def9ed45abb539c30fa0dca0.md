

## 一个使用整数作为索引的只读索引器

```
private List<Product> products;

public Product this[int i]
{
    get { return products[i]; }
}
```

## 使用表达式体的相同索引器

```
public Product this[int i] => products[i];
```

## 具有表达式体 get 和 set 访问器的索引器

```
public Product this[int i]
{
    get => products[i];
    set => products[i] = value;
}
```

## 使用这些索引器的代码

```
ProductList products = new ProductList();
products.Add("C#", "Murach's C#", 59.50m);
Product p1 = products[0];
products[i] = new Product(code, description, price);
```

## Description

- 如果索引器是只读的并且只是返回一个表达式的值，则可以将其作为表达式体索引器编写。表达式体索引器是在 C# 6.0 中引入的。
- 要编写表达式体索引器，您需要编写访问修饰符、返回类型和 this 关键字，然后是 lambda 运算符和要返回的表达式。
- 如果索引器的 get 访问器只是返回一个表达式，并且 set 访问器执行单个语句，则访问器可以作为表达式体访问器编写。表达式体 get 和 set 访问器是在 C# 7.0 中引入的。
- 要编写表达式体 get 访问器，您需要编写 get 关键字，然后是 lambda 运算符和要返回的表达式。
- 要编写表达式体 set 访问器，您需要编写 set 关键字，然后是 lambda 运算符和要执行的语句。
- 您可以使用重构将使用代码块的 get 和 set 访问器转换为表达式体访问器。这与对其他属性的操作方式相同。

## How to throw an argument exception

当您编写属性和方法时，通常最好检查传递给属性或方法的参数，以确保它们是有效的。然后，如果参数无效，则应抛出异常以通知类的用户发生了错误。例如，当您编写索引器时，您可能希望检查索引参数是否在有效范围内。

图 13-5 显示了应如何处理参数异常。在这里，第一个索引器的 get 访问器检查传递给它的 int 值是否在有效范围内。如果 int 值小于零或大于或等于列表中的产品数量，则索引器会抛出异常。否则，int 值将用于从产品列表中返回指定的 Product 对象。

第二个索引器的工作方式与第一个索引器类似，但它接受一个字符串来指定产品的代码。首先，get 访问器检查字符串是否包含超过四个字符。如果是，则索引器会抛出异常。否则，foreach 循环将产品代码与列表中每个产品的产品代码进行比较。如果产品代码匹配，则 get 访问器将从列表中返回 Product 对象。否则，get 访问器返回 null 值。

正如您在第 7 章中学到的，throw 语句和 throw 表达式指定要抛出的异常对象。.NET 在本图中列出了三个异常类作为标准异常，您可以在验证参数时使用它们。例如，如果参数超出属性可接受的值范围，则应抛出 ArgumentOutOfRangeException。如果尝试将属性设置为 null 值而属性需要一个值，则应抛出 ArgumentNullException。对于任何其他参数错误，应抛出 ArgumentException。

请注意，这三个异常都有一个接受 message 参数的构造函数。您可以使用此参数提供指示数据有问题的错误消息。但是，由于 ArgumentOutOfRangeException 已包含描述问题的错误消息，因此您可以只指定超出范围的参数名称。

当您编写使用抛出参数异常的属性或方法的语句时，您可能会认为应该将语句放在 try-catch 语句中，以便在发生异常时捕获它。但我们不建议这样做。相反，您应该在将数据传递给属性或方法之前验证数据。例如，本图中显示的 if 语句在将产品代码传递给第二个索引器之前检查用户输入的产品代码的长度。这样，异常就不应该发生。

那么为什么要在类中包含验证代码呢？因为如果您设计类使其可重用，就不能总是指望其他程序员验证他们传递给类的数据。通过包含此验证代码，您使类完全自包含。

## 一个检查范围并抛出参数异常的索引器

```
public Product this[int i]
{
    get
    {
        if (i < 0 || i >= products.Count)
        {
            throw new ArgumentOutOfRangeException(i.ToString());
        }
        return products[i];
    }
    ...
}
```

## 一个验证数据并抛出参数异常的索引器

```
public Product this[string code]
{
    get
    {
        if (code.Length > 4)
        {
            throw new ArgumentException(
                "Maximum length of Code is 4 characters.");
        }
        foreach (Product p in products)
        {
            if (p.Code == code)
                return p;
        }
        return null;
    }
}
```

## Three argument exceptions

| Exception | Description |
|---|---|
| ArgumentOutOfRangeException(message) | Use when the value is outside the acceptable range of values. |
| ArgumentNullException(message) | Use when the value is null and a null value is not allowed. |
| ArgumentException(message) | Use when the value is invalid for any other reason. |

## An if statement that validates data before setting a property value

```
Product p = null;
if (txtCode.Text.Length <= 4)
    p = products[txtCode.Text];
```

## Description

- 如果类检测到无效参数，它应使用描述错误的 message 参数抛出三个参数异常之一。
- 所有参数异常都是 System 命名空间的一部分。

## How to work with delegates and events

除了字段、属性、索引器、方法和构造函数之外，类还可以定义委托和事件。

## How to define and use a delegate

图 13-6 显示了如何定义和使用委托。委托是从类创建的，可以引用具有特定返回类型和参数列表的方法，这些构成委托的签名。因此，您可以将委托视为指向具有给定签名的方法的指针。因此，可以通过委托间接调用方法。

在许多情况下，您将使用委托将事件处理程序连接到事件上。但是，您也可以在没有事件的情况下使用委托。本图中显示的示例将帮助您了解其工作原理。

要定义委托，您首先编写 public 和 delegate 关键字，后跟返回类型、委托的名称和参数列表。例如，本图中在 ProductList 类中定义了一个名为 ChangeHandler 的委托，其返回类型为 void，并且有一个 ProductList 参数。然后，您可以使用该委托与任何具有相同返回类型和参数的方法，这些构成委托的签名。

在本图中，PrintToDebug() 方法具有与 ChangeHandler 委托相同的签名。如您所见，此方法是在应用程序的主窗体中编写的。然后，在创建 ProductList 对象并向其添加产品后，从窗体的 Load 事件处理程序中调用它。

要使用 ChangeHandler 委托，您首先创建委托对象。这与实例化任何类型的对象的工作方式相同。在这种情况下，由于委托是在 ProductList 类中声明的，因此委托的名称会与该类一起限定。您还指定在实例化它时委托使用的 方法。在本图中，这是 PrintToDebug() 方法。请注意，创建委托对象的语句是在类级别编写的，因此可以从类的任何位置访问它。因此，它使用的方法被声明为 static。

实例化委托后，您可以调用它并传递方法所需的所有参数。在此示例中，只传递了 PrintToDebug() 方法所需的 ProductList 对象。这会导致产品列表中的所有产品都打印到输出窗口的 Debug 部分，并附带一条消息，指示产品列表已更改。

尽管本图中提供的示例并不现实，但它应该让您了解委托的工作原理。例如，您可能有一个按钮的 Click 事件处理程序，它添加用户在窗体上输入的产品，然后调用委托。更有可能的是，您将使用委托将事件处理程序连接到事件，如下一图所示。

