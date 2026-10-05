

# Product 类的代码

图 12-3 显示了 Product 类的完整代码，其成员在图 12-2 中描述过。如你所示，它以一个带有 `public` 公共访问修饰符的类语句开头。该访问修饰符允许其他类访问该类。

类块中的代码定义了 Product 类的成员。在本章的其余部分，你将学习如何编写像所示代码的代码。现在，我将展示这段代码的预览，以便让你对它的工作原理有一个大致的了解。

该类中的前三个语句是三个类变量（字段）的声明。正如你稍后将看到的，这些字段被用于存储 `Code`、`Description` 和 `Price` 属性的数据。由于这些变量是由 `private` 私有访问修饰符定义的，因此无法在类外部引用它们。

在字段之后是 Product 类的两个构造函数的声明。第一个构造函数不接受任何参数，它创建 Product 类的实例并将其字段初始化为默认值。第二个构造函数创建类的实例，并使用通过 `code`、`description` 和 `price` 参数传递的值进行初始化。

接下来是 Product 类的三个属性的声明。属性提供了对三个字段中存储的值的访问。在每个属性声明内部，有两个代码块分别用于获取和设置属性的值。

最后是 `GetDisplayText` 方法的声明，它接受一个名为 `sep` 的字符串参数。该方法返回一个字符串，将 `code`、`description` 和 `price` 值连接起来，并通过 `sep` 参数传递的值分隔。

注意，你始终使用 `public` 访问修饰符来标识可以从其他类访问的属性和方法。相比之下，你使用 `private` 访问修饰符声明你不希望从其他类访问的字段。例如，字段只能通过类定义的属性进行访问。你也可以使用 `private` 访问修饰符编写你不希望从其他类访问的属性和方法。

# Product 类

```csharp
using System;

namespace ProductMaint
{
    public class Product {
        private string code;
        private string description;
        private decimal price;

        public Product(){}
        public Product(string code, string description, decimal price) {
            this.Code = code;
            this.Description = description;
            this.Price = price;
        }

        public string Code {
            get {
                return code;
            }
            set {
                code = value;
            }
        }

        public string Description {
            get {
                return description;
            }
            set {
                description = value;
            }
        }

        public decimal Price {
            get {
                return price;
            }
            set {
                price = value;
            }
        }

        public string GetDisplayText(string sep) {
            return code + sep + price.ToString("*c") + sep + description;
        }
    }
}
```

图 12-3 Product 类的代码

# 实例化是如何工作的

从类创建对象的过程被称为实例化。图 12-4 描述了实例化是如何工作的。在这里，你可以看到 Product 类的两个实例。每个实例代表一个不同的 Product 对象。因为两个实例都是从同一个类创建的，所以它们具有相同的属性。然而，实例在每个属性上具有不同的值。例如，`product1` 对象的 `Code` 属性值为 `CS10`，但 `product2` 对象的 `Code` 值为 `VB10`。

图中的第一个代码示例显示了你如何创建这两个对象实例。在这里，第一行代码声明了两个类型为 `Product` 的变量 `product1` 和 `product2`。接下来的两行创建了对象。为了实现这一点，它们使用了 `new` 关键字，类类名以及传递给构造函数并用于初始化对象的值。

图中的第二个代码示例显示了创建相同对象实例的另一种方法。这段代码使用了对象初始化器（object initializers）功能。对象初始化器允许你创建对象的实例并对其赋值，而无需显式调用构造函数。要做到这一点，你在类名后跟随一个用大括号括起来的列表，指定你想初始化的属性或公共字段的名称，以及你想赋值给这些属性或字段的值。

对象初始化器的优点之一是它们允许你在单个语句中创建对象并对其赋值。为了说明这一点，假设 `Product` 类没有接受 `code`、`description` 和 `price` 的构造函数。在这种情况下，你必须使用以下代码来创建类的实例并对其赋值，而不使用对象初始化器：

```sharp
product1 = new Product();
product1.Code = "CS10";
product1.Description = "Murach's C# 2010";
product1.Price = 54.5;
```

然而，这个功能在你编写 LINQ 查询表达式时最有用，你将在第 23 章学习如何这样做。

到此时，重要的是意识到一个类定义了一个引用类型（reference type）。这意味着用于访问对象的变量包含存储对象的内存位置的地址，而不是对象本身。换句话说，`product1` 变量持有对 `Product` 对象的引用，而不是一个真实的 `Product` 对象。

# 从 Product 类实例化的两个 Product 对象

product1
Code=CS10
Description=Murach's C# 2010
Price=54.50

product2
Code=VB10
Description=Murach's Visual Basic 2010
Price=54.50

# 创建这两个对象实例的代码

```sharp
product1, product2;
product1 = new Product("CS10","Murach's C# 2010", 54.50m);
product2 = new Product("VB10","Murach's Visual Basic 2010", 54.50m);
```

# 创建对象实例的另一种方法

```sharp
product1 = new Product {Code = "CS10",
Description = "Murach's C# 2010", Price = 54.50m};
product2 = new Product {Code = "VB10",
Description = "Murach's Visual Basic 2010", Price = 54.50m};
```

# 说明

- 当实例化对象时，会执行构造函数来初始化组成对象的数据。如果类没有提供构造函数，则会执行默认构造函数。
- 组成对象的数据有时被称为对象的状态（state）。一旦对象实例化，它的状态就可以改变。
- 每当你更改属性或公共字段的值时，对象的状态就会改变。调用影响对象内部存储的方法时，状态也会改变。
- 应用程序可以创建同一类的两个或多个实例。每个实例都是具有独立状态的实体。如果你更改了一个对象状态，从同一类创建的对象不受影响。
- 对象初始化器允许你在单个语句中创建对象的实例并对其赋值，而无需显式调用构造函数。
- 类定义了一个引用类型。这意味着用于访问从类实例化的对象的变量包含对象的地址，而不是对象本身。

# 如何创建类

现在你已经学习了组成类的成员，并看到了 Product 类的代码，你已经准备好学习创建和使用你自己的类的基本技能。接下来的主题将介绍这些技能。

# 如何向项目添加类文件

要创建用户自定义类，首先要向项目添加类文件。要做到这一点，你可以使用图 12-5 所示的对话框。当你完成此对话框后，类文件将出现在解决方案管理器中，扩展名为 `.cs`。

当你向项目中添加类时，Visual Studio 会自动生成类声明。然后你可以通过添加字段、属性、方法以及类所需的任何其他成员来完成该类。

