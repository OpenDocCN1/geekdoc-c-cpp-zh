

## 如何编码构造函数

默认情况下，当你使用 new 关键字创建用户定义类的实例时，C# 会为新对象中的所有实例变量分配默认值。如果这不是你想要的，你可以编写一个在对象从类创建时执行的特殊方法，称为构造函数。图 12-9 展示了如何做到这一点。

要创建构造函数，你需要声明一个与类同名的 public 方法。例如，Product 类的构造函数必须命名为 Product。在构造函数内部，你初始化实例变量，并包含在对象从类创建时想要执行的任何其他语句。请注意，构造函数不得声明返回类型。

本图中的第一个示例是一个不提供任何参数的构造函数，因此在创建类实例且未指定任何参数时调用。因为该构造函数没有可执行语句，所以它只是将所有实例变量初始化为默认值（不包括只读变量和在声明时已初始化的变量）。各种数据类型的默认值在此图中列出。

在某些情况下，类可能未定义任何构造函数。例如，你可能忘记编写构造函数。或者，你可能在另一个类中编写一个类（参见第 16 章）并且未为该类声明构造函数。在这种情况下，C# 编译器会生成一个等效于第一个示例中所示构造函数的默认构造函数。

本图中的第二个构造函数显示你可以像重载方法一样重载构造函数。在这里，定义了一个接受三个参数的构造函数。该构造函数使用传递给参数的值来初始化实例变量。当对象创建时设置初始值时，常使用此技术。

第三个构造函数展示了你如何为 Product 类提供一个仅接受产品代码作为参数的构造函数。然后，它调用名为 ProductDB 的数据库类中的 GetProduct() 方法来检索指定产品的数据。数据检索后，构造函数使用它来初始化实例变量。

请注意，第二个和第三个构造函数都使用 this 关键字来引用正在初始化的属性。虽然这不是必需的，但它能清楚地表明所引用的属性是在当前类中定义的，而不是在另一个类中定义的。另请注意，如果你编写了像这些示例中的构造函数，编译器将不会生成默认构造函数。在这种情况下，你需要编写像第一个示例中那样的构造函数。

本图还展示了执行此处所示三个构造函数的语句。第一个语句执行不带参数的构造函数。第二个语句执行带三个参数的构造函数。第三个语句执行带一个参数的构造函数。虽然你以前见过类似的语句，但现在你应该更好地理解它们的工作原理。

### 一个不带参数的构造函数

```
public Product()
{
}
```

### 一个带三个参数的构造函数

```
public Product(string code, string description, decimal price)
{
    this.Code = code;
    this.Description = description;
    this.Price = price;
}
```

### 一个带一个参数的构造函数

```
public Product(string code)
{
    Product p = ProductDB.GetProduct(code);
    this.Code = p.Code;
    this.Description = p.Description;
    this.Price = p.Price;
}
```

### 调用这些构造函数的语句

```
Product product1 = new Product();
Product product2 = new Product("C#", "Murach's C#", 59.50m);
Product product3 = new Product(txtCode.Text);
```

### 实例变量的默认值

| Data type | Default value |
|---|---|
| All numeric types | 0 |
| Boolean | false |
| Char | null |
| Object | null |
| Date | 12:00 a.m. on January 1, 0001 |

### Description

- 构造函数的名称必须与类的名称相同。此外，构造函数必须始终使用 public 访问修饰符声明，并且不能指定返回类型。
- 要编写带参数的构造函数，请在类名后的括号内为每个参数编写数据类型和名称。
- 类的名称与其参数列表组合形成构造函数的签名。每个构造函数必须具有唯一的签名。
- 如果构造函数未为实例变量分配值并且该变量在声明时未初始化，则该变量将被分配如上所示的默认值。

## 一个包含静态成员的类

```
{
    private static string lineEnd = "\n";

    public static string LineEnd
    {
        get { return lineEnd; }
        set { lineEnd = value; }
    }

    public static string IsPresent(string value, string name)
    {
        string msg = "";
        if (value == "")
        {
            msg += name + " is a required field." + LineEnd;
        }
        return msg;
    }
}
```

### 使用静态成员的代码

```
string errorMessage = "";
errorMessage += Validator.IsPresent(txtCode.Text, txtCode.Tag.ToString());
errorMessage += Validator.IsPresent(txtDescription.Text, txtDescription.Tag.ToString());

if (errorMessage != "")
    MessageBox.Show(errorMessage, "Entry Error");
```

### Validator 类的 using 指令

```
using static ProductMaintenance.Validator;
```

### Description

- 静态成员是字段、属性或方法，可以在不创建类的实例的情况下访问。要定义静态成员，你使用 static 关键字。
- 静态属性和方法只能引用其他静态成员或在属性或方法内部声明的变量。
- 使用 public 关键字声明的常量隐式为静态。你不能在常量声明上编写 static 关键字。
- 如果你从类创建对象，则不能通过对象的变量引用静态成员。你只能通过类名引用静态成员。
- 如果类仅包含静态成员，你可以在类声明中使用 static 关键字将类声明为静态类。这可以防止程序员意外地向类添加非静态成员或从类创建对象。
- C# 6.0 引入了一个 using 指令，让你可以在不命名类型的情况下引用类型的静态成员。

## 产品维护应用程序

现在你已经学习了创建类的基本技能，接下来的主题将介绍一个产品维护应用程序，该应用程序维护一个简单的产品文件。如你所见，此应用程序除了启动程序并运行第一个表单的两个表单类和 Program 类之外，还使用了三个用户定义的类。

图 12-11 描述了产品维护应用程序的操作。如你所见，此应用程序使用两个表单。主表单在列表框中显示存储在文件中的产品列表。用户可以使用此表单添加或删除产品。

如果用户单击“添加产品”按钮，则会以对话框形式显示“新产品”表单。然后，用户可以输入新产品的数据并单击“保存”按钮将产品添加到文件中。产品保存后，产品维护表单中的列表框将被刷新，以便包含新产品。用户也可以单击“新产品”表单上的“取消”按钮来取消添加操作。

要删除产品，用户在列表中选择产品并单击“删除产品”按钮。然后会显示一个对话框以确认操作。如果操作得到确认，则产品将被删除，并且列表框将被刷新，以便不再包含已删除的产品。

本图还显示了“新产品”表单上三个文本框的 Tag 属性是如何设置的。正如你马上就会看到的，数据验证类的方法使用这些文本框的 Tag 属性，如果用户输入了错误数据，则显示有意义的错误消息。

