

## 如何创建委托
### 使用匿名方法
```
ProductList.ChangeHandler myDelegate =
delegate (ProductList products)
{
    Debug.WriteLine("The products list has changed!");
    for (int i = 0; i < products.Count; i++) { ... }
};
myDelegate(products);
```
### 使用 lambda 表达式
```
ProductList.ChangeHandler myDelegate = products =>
{
    Debug.WriteLine("The products list has changed!");
    for (int i = 0; i < products.Count; i++) { ... }
};
myDelegate(products);
```

## 如何绑定事件
### 使用匿名方法
```
products.Changed += delegate (ProductList products)
{
    Debug.WriteLine("The products list has changed!");
    for (int i = 0; i < products.Count; i++) { ... }
};
```
### 使用 lambda 表达式
```
products.Changed += products =>
{
    Debug.WriteLine("The products list has changed!");
    for (int i = 0; i < products.Count; i++) { ... }
};
```

## 描述
- *匿名方法* 是没有名称的方法。当你创建委托时，如果不想指定命名方法，可以使用匿名方法。如果方法只在一个地方被调用，这有助于简化代码。
- *lambda 表达式* 与匿名方法类似，但它使用 lambda 运算符而不是 delegate 关键字。
- 你也可以将匿名方法或 lambda 表达式绑定到事件。当你这样做时，应将代码放在类构造函数中，或如果类是窗体，则放在 Load 事件处理程序中。

## 如何重载运算符
图 13-2 中的 ProductList 类使用了重载运算符。具体来说，该类重载了 + 和 - 运算符，以便你可以使用这些运算符向产品列表添加产品或从产品列表中移除产品，而不是使用 Add() 和 Remove() 方法。以下主题解释了如何实现此类重载运算符。

### 对运算符重载的介绍
图 13-9 提供了有关 *运算符重载* 的一些基本信息。首先，你应该知道你可以重载一元和二元运算符。图中所列的是最常见的可重载运算符。

C# 为内置类型如 decimal、int、string 和 DateTime 定义了这些运算符的含义。然而，对于用户定义的类型，如上一章中介绍的 Product 类或本章中介绍的 ProductList 类，这些运算符要么未定义，要么以可能不适合该类的方式定义。例如，+ 运算符未为用户定义的类型定义，但 == 运算符已定义。默认情况下，如果你使用 == 运算符比较两个对象变量，则它们在引用同一对象时才被视为相等。

使用运算符重载，你可以为你的类创建自己的 C# 运算符实现，使其适合你的类。例如，Product 类的 == 运算符更合适的定义是，如果两个 Product 变量引用具有相同 Code、Description 和 Price 属性的对象，则认为它们相等。

正如本图顶部所示的语法，你使用 operator 关键字声明运算符。在运算符声明中，你指定返回类型，该类型指示操作返回的对象类型。在大多数情况下，返回类型与包含声明的类相同（例如 Product 类中的 Product）。然后，你指定要定义的运算符，后跟一个或两个操作数，具体取决于运算符是一元还是二元运算符。

请注意，运算符始终声明为 static。这样，它们就可以正确处理 null 操作数。当你看到重载 == 运算符的代码时，这将更有意义。

重载运算符通常依赖于类中定义的方法。例如，在图 13-10 中，你会看到 ProductList 类的 + 运算符使用类的 Add() 方法将产品添加到列表中。然后，在图 13-11 中，你会看到 Product 类的 == 和 != 运算符通过重写 Object 类的 Equals() 方法来实现，该方法由所有其他类继承。

### 重载一元运算符的语法
```
public static returnType operator unary-operator(type operand)
```

### 重载二元运算符的语法
```
public static returnType operator
    binary-operator(type-1 operand-1, type-2 operand-2)
```

### 你可以重载的常见运算符
#### 一元运算符
```
+ - ! ++ -- true false
```

#### 二元运算符
```
+ - * / % & | == != > < >= <=
```

### Object 类的 Equals() 方法
| 方法 | 描述 |
|---|---|
| Equals(object) | 返回一个布尔值，指示当前对象是否引用与指定对象相同的实例。如果这不是你想要的，你可以像图 13-11 所示那样重写此方法。 |
| Equals(object1, object2) | Equals() 方法的静态版本，用于比较两个对象以确定它们是否引用同一实例。 |

### Object 类的 GetHashCode() 方法
| 方法 | 描述 |
|---|---|
| GetHashCode() | 返回一个整数值，用于在哈希表中标识对象。如果重写 Equals() 方法，则必须同时重写 GetHashCode() 方法。 |

## 描述
- 你使用 *operator* 关键字在类内 *重载运算符*。例如，你可能在 ProductList 类中重载 + 运算符，以便它可用于向列表添加产品。你也可能在 Product 类中重载 == 和 != 运算符，以便你可以比较两个 Product 对象是否包含相同的数据，而不是是否引用同一实例。
- 你可以重载上面所示的所有一元和二元运算符，以及本书中未介绍的一些运算符。当你重载二元运算符时，*operand-1* 是运算符左侧的操作数，*operand-2* 是运算符右侧的操作数。
- *重载运算符* 始终是 static，以便它们可以正确处理 null 操作数。
- 当你重载 == 和 != 等关系运算符时，你需要提供自己的 Equals() 和 GetHashCode() 方法版本。有关详细信息，请参阅图 13-11。

### 重载 + 运算符的 ProductList 类的一部分
```
public class ProductList
{
    private List<Product> products;

    public void Add(Product p)
    {
        products.Add(p);
    }

    public static ProductList operator + (ProductList pl, Product p)
    {
        pl.Add(p);
        return pl;
    }
    .
    .
}
```

### 使用 ProductList 类的 + 运算符的代码
```
ProductList products = new ProductList();
Product p = new Product("C#", "Murach's C#", 59.50m);
products = products + p;
```

### 使用 + 运算符的另一种方式
```
products += p;
```

### 使用表达式体运算符的代码
```
public ProductList Add(Product p)
{
    products.Add(p);
    return this;
}

public static ProductList operator + (ProductList pl, Product p) =>
    pl.Add(p);
```

## 描述
- 你可以重载内置算术运算符，使其在定义它们的类创建的对象上执行自定义函数。
- 你应仅重载对类有意义的算术运算符。例如，为 ProductList 类重载 + 运算符作为向产品列表添加产品的方式是合理的。但为此类重载 * 或 / 运算符是没有意义的。
- 你不会单独重载 += 或 -= 运算符。相反，这些运算符由重载的 + 和 - 运算符自动处理。
- 仅返回表达式或执行单个语句的运算符可以作为 *表达式体运算符* 编码。表达式体运算符在 C# 6.0 中可用。

## 如何重载关系运算符
图 13-11 显示，重载关系运算符通常比重载算术运算符更困难。在这里，第一个示例展示了如何为 Product 类实现 == 运算符，以便你可以根据值而不是对象引用比较产品。将要比较的两个对象作为参数传递给此运算符。

运算符首先使用 Object 类的 Equals() 方法检查两个对象是否等于 null。此 Equals() 方法的实现基于引用，而不是值。因此，它允许你测试对象是否为 null。这种测试是必要的，以防止重载的 == 运算符在其中一个操作数为 null 时抛出异常。

如果两个操作数都为 null，则 == 运算符返回 true。如果第一个操作数为 null 但第二个操作数不为 null，则返回 false。如果第一个操作数不为 null，则 == 运算符调用第一个操作数的 Equals() 方法将其与第二个操作数进行比较，然后返回比较结果。

请注意，Equals() 方法的声明包含 override 关键字。这意味着它重写了 Object 类定义且每个类都继承的 Equals() 方法。在下一章中，你将学习如何使用继承。然后，你将能够理解这段代码的工作原理。

Equals() 方法首先测试传递给它的对象，在本例中为 == 运算符的第二个操作数，以判断其是否为 null。如果此对象为 null，则 Equals() 方法返回 false。这是有意义的，因为没有任何对象应被视为等于 null。

如果传递给 Equals() 方法的对象不为 null，则此方法将其转换为名为 p 的 Product 对象。然后，它将自己的 Code、Description 和 Price 值与 p 对象的 Code、Description 和 Price 值进行比较。如果三个属性都相等，则返回 true。否则，返回 false。

当你重载比较运算符时，你还必须重载执行相反操作的运算符。例如，如果你重载 == 运算符，你还必须重载 != 运算符。同样，如果你重载 < 运算符，你还必须重载 > 运算符。图中使用来实现 Product 类的 != 运算符的代码也显示在此处。正如你所见，此运算符以 == 运算符为基础定义。这样可以确保这些运算符返回一致的结果。

当你重载 == 运算符时所需的最后一个方法是 GetHashCode() 方法。与 Equals() 方法一样，此方法重写 Object 类定义的 GetHashCode() 方法。对于 GetHashCode() 方法的主要要求是，对于 Equals() 方法认为相等的任意两个对象，它必须始终返回相同的值。实现此目的最简单的方法是将 Equals() 方法中用于比较的值组合成一个字符串，然后返回该字符串的哈希码。

本图中的第二个示例展示了如何使用 == 运算符比较两个 Product 对象。首先，从 Product 类创建两个名为 p1 和 p2 的对象变量，其值相同。然后，产品

