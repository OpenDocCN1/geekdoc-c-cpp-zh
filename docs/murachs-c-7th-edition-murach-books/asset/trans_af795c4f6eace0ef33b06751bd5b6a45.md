

## 测试对象类型和属性的方法（C# 6.0 及更早版本）

```csharp
public static decimal GetDiscountPercent(Object o) {
    decimal discountPercent = .0m;
    if (o.GetType() == typeof(Product)) {
        Product p = (Product) o;
        if (p.Category == ".NET")
            discountPercent = .1m;
        else if (p.Category == "Java")
            discountPercent = .2m;
    }
    return discountPercent;
}
```

## 使用模式匹配的方法（C# 7.0 及以后）

### 使用 if 语句测试对象类型

```csharp
private static decimal GetDiscountPercent(Object o) {
    decimal discountPercent = .0m;
    if (o is Product p) {
        if (p.Category == ".NET")
            discountPercent = .1m;
        else if (p.Category == "Java")
            discountPercent = .2m;
    }
    return discountPercent;
}
```

### 使用 switch 语句测试对象类型和属性

```csharp
private static decimal GetDiscountPercent(Object o) {
    switch (o) {
        case Product p when p.Category == ".NET":
            return .1m;
        case Product p when p.Category == "Java":
            return .2m;
        default:
            return .0m;
    }
}
```

### 使用 not 运算符的模式（C# 9.0 及以后）

```csharp
if (o is not null) { // code to execute goes here }
```

然而，它也可以用来检查对象是否不是特定类型，如下所示：

```csharp
if (o is not Product) { // code goes here }
```

### 描述

- C# 7.0 引入了 *模式匹配*，让你可以使用 if 或 switch 语句来测试传递给方法的对象类型。
- 要使用 if 语句测试对象类型，你使用 *is 运算符* 编写 *is 表达式*。该表达式还会将对象分配给指定类型的变量。
- 要使用 switch 语句测试对象类型，你编写对象类型和你想要将其分配到的变量。你还可以编写 *when* 子句来测试对象的属性或字段是否具有特定值。
- 从 C# 9.0 及以后，你可以在模式中使用 *not 运算符*。

## 如何使用属性模式

在第 5 章中，你学习了如何使用 switch 表达式代替仅根据表达式的值返回值的 switch 语句。然后，在第 6 章中，你学习了如何在表达式体方法中使用 switch 表达式。现在，图 12-20 显示了如何使用 C# 8.0 的一项新功能 property patterns 与 switch 表达式一起使用。属性模式是你在上一张图中学到的模式匹配功能的扩展。

该图中的第一个示例显示了一个方法，类似于你在上一张图中看到的方法，它接受一个通用对象并返回折扣百分比。但是，与其使用 if 或 switch 语句，此示例使用 switch 表达式来测试传递给方法的对象类型。为此，它只需在 case 中命名要测试的对象类型。例如，此示例中的前两个 case 测试对象是否为 Product 对象。

在对象类型之后，你编写属性模式。该模式包括属性名称后跟冒号、正在测试的值以及包围的大括号。在此示例中，属性模式测试 Product 对象的 Category 属性是否具有特定值，如上一张图所示。如果你将此方法与上一张图中执行相同功能的那些方法进行比较，你会看到使用属性模式的方法要简单得多。

关于此 switch 表达式你还应注意的一点是，它以 discard 结尾。当你使用属性模式与 switch 表达式时这是必需的，因为属性模式必须返回非空值。

第二个示例显示你可以使用 switch 表达式来测试不止一种类型的对象。在这里，前四个 case 测试 Product 对象，而接下来的两个 case 测试 Vendor 对象。虽然你在到目前为止的示例中尚未看到 Vendor 对象的用法，但你需要知道的是，这些对象是从 Vendor 类创建的，该类包含与 Product 类定义相似的属性、方法和构造函数。

请注意，在此示例中，用于测试 Vendor 对象的 case 的属性模式测试的属性与用于测试 Product 对象的 case 不同。你还可以测试同一对象的不同属性，并且你可以使用单个属性模式测试同一对象的两个或多个属性，如 Vendor 对象的第二个 case 所示。换句话说，你可以使用带有属性模式的 switch 表达式来测试任何对象的任何属性。这对于对象是否相关是成立的。

该图中的第三个示例与第一个示例类似，只是它接受 Product 对象而不是通用对象。因此，不需要测试对象类型。但是，它只能与 Product 对象一起使用。

### 属性模式的语法

```text
{ property: value[, property: value]... }
```

### 使用 switch 表达式与属性模式测试对象类型和属性的方法

```csharp
private static decimal GetDiscountPercent(Object o) => o switch
{
    Product { Category: ".NET" } => .1m,
    Product { Category: "Java" } => .2m,
    _ => .0m
};
```

### 测试两种对象类型的方法

```csharp
private static decimal GetDiscountPercent(Object o) => o switch
{
    Product { Category: ".NET" } => .1m,
    Product { Category: "Java" } => .2m,
    Product { Category: "Web" } => .3m,
    Product { Category: "Mainframe" } => .4m,
    Vendor { DiscountType: "Quantity" } => .2m,
    Vendor { DiscountType: "Terms", Terms: 30 } => .3m,
    _ => .0m
};
```

### 测试特定类型对象的方法

```csharp
private static decimal GetDiscountPercent(Product p) => p switch
{
    { Category: ".NET" } => .1m,
    { Category: "Java" } => .2m,
    _ => .0m
};
```

### 描述

- C# 8.0 引入了一种新的模式匹配类型，称为 *属性模式*。你可以使用属性模式与 switch 表达式来测试对象的属性或公共字段是否具有特定值。
- 属性模式由属性或公共字段的名称组成，后跟冒号和模式的值，所有内容都用大括号括起来。你还可以使用属性模式通过用逗号分隔来测试两个或多个属性或公共字段的值。
- 要测试传递给方法的对象类型，你在属性模式前加上类型的名称。

## 如何生成代码存根

除了你刚刚学习用于创建类的技能外，你还可以使用 Visual Studio 的一项功能 live code analysis 来为类及其成员生成代码存根。此功能可以帮助你根据使用该类的代码快速生成类的起始代码。然后，你可以根据需要稍后增强该类的代码。

图 12-21 显示了 Generate From Usage 功能的工作原理。在这里显示的第一个屏幕中，你可以看到我从名为 Product 的类声明了一个名为 product 的变量。但是，由于 Product 类不存在，Visual Studio 将其标记为语法错误。然后，我使用类名的 Quick Actions 菜单中的第一个命令显示一个子菜单，并使用子菜单中的第一个命令生成该类。第二个屏幕类似，但在这种情况下，我为名为 GetPrice() 的方法生成了一个存根。

当你将指针指向用于生成类或成员的 Quick Actions 菜单中的命令时，Visual Studio 会显示将生成的代码，如图所示。如你所见，类的代码由 namespace 语句、class 语句和构造函数组成。请注意，类使用 internal 访问修饰符声明，这将访问限制为当前 C# 程序集。

方法代码由方法声明和单个语句组成。该语句抛出一个异常，指出该方法尚未实现。然后，你可以用实现该方法的代码替换此语句。

与类一样，此方法也包含 internal 访问修饰符。此外，由于调用 GetPrice() 方法的语句将返回值分配给 decimal 变量，因此该方法返回 decimal 值。最后，由于该语句将字符串传递给该方法，因此该方法使用字符串参数定义。

在此示例中，Product 类是在新文件中创建的。你还可以使用 Quick Actions 菜单中的第二个命令将类添加到当前文件并跟在当前类之后，并使用第三个命令将类嵌套在当前类中。你将在第 16 章中了解有关嵌套类的更多信息。

最后，与其像第一个示例中的语句那样自动从语句生成类声明，你可以使用 Quick Actions 子菜单中的第四个命令显示 Generate Type 对话框。此对话框让你指定要生成的代码。例如，你可以使用它来指定类的不同访问修饰符。虽然此对话框在此未显示，但你不应该在使用它时遇到任何困难。

在大多数情况下，你将使用 IntelliSense 的标准补全模式来输入类或成员的名称。这是本书迄今为止你所学到的模式。当你输入未定义的类或成员名称时，你可能希望改用建议模式。在此模式下，完成列表仍会显示，但当前项是轮廓而不是高亮显示。然后，要提交你输入的名称，你输入语句中的下一个字符或按 Enter 键。这有助于防止 IntelliSense 插入不需要的文本。要在补全模式和建议模式之间切换，你可以使用本图中描述的两种技术之一。

