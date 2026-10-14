

## 提示

请记住，在方法中声明的变量默认不会被初始化。然而，类中的字段会根据其类型自动初始化为 0、false 或 null。尽管如此，提供显式的字段初始化方式仍然是良好的实践。

## 命名和可访问性

许多组织都有自己的内部风格，要求开发人员在编写代码时遵循。这一风格的一部分通常涉及为标识符命名制定的规则。这些规则的目的通常是为了使代码更易于维护。以下建议相当常见，与基于类成员可访问性的字段和方法命名约定有关；然而，C# 并未强制执行这些规则：

- 公共的标识符应以大写字母开头。例如，Area 以 A 开头（而不是 a），因为它是公共的。这种系统被称为 PascalCase 命名方案（因为它最早在 Pascal 语言中使用）。
- 非公共的标识符（包括局部变量）应以小写字母开头。例如，radius 以 r 开头（而不是 R），因为它是私有的。这种系统被称为 camelCase 命名方案。

### 注意

一些组织仅对方法使用 camelCase 方案，并采用以下划线字符开头命名私有字段的约定，例如 _radius。然而，本书中的示例对私有方法和字段使用 camelCase 命名。

对此规则只有一个例外：类名应以大写字母开头，并且构造函数必须与所属类名完全一致；因此，私有构造函数也必须以大写字母开头。

## 重要

不要声明两个仅在大小写上不同的公共类成员。如果这样做，使用其他不区分大小写的语言（如 Microsoft Visual Basic）的开发人员可能无法将你的类集成到他们的解决方案中。

## 使用构造函数

当你使用 new 关键字创建对象时，运行时需要使用类的定义来构造该对象。运行时必须从操作系统获取一段内存，用类定义的字段填充它，然后调用构造函数执行所需的任何初始化。

构造函数是一种特殊的方法，在你创建类的实例时自动运行。它与类同名，可以接受参数，但不能返回值（甚至不是 void）。每个类都必须有一个构造函数。如果你不编写一个，编译器会自动为你生成一个默认构造函数。（然而，编译器生成的默认构造函数实际上什么也不做。）你可以很容易地编写自己的默认构造函数。只需添加一个不返回值且与类同名的方法即可。以下示例展示了带有默认构造函数的 Circle 类，该构造函数将 radius 字段初始化为 0：

Click here to view code image

```
class Circle
{
    private int radius;

    public Circle() // default constructor
    {
        radius = 0;
    }

    public double Area()
    {
        return Math.PI * radius * radius;
    }
}
```

### 注意

在 C# 用语中，*default* 构造函数是指不接受任何参数的构造函数。无论是编译器生成还是你编写的，它仍然是默认构造函数。你也可以编写非默认构造函数（即 *确实* 接受参数的构造函数），你将在下一节“重载构造函数”中看到。

在此示例中，构造函数被标记为 *public*。如果省略此关键字，构造函数将为 private（就像其他任何方法和字段一样）。如果构造函数为 private，则无法在类外部使用，这会阻止你从 *Circle* 类之外的方法创建 *Circle* 对象。你可能因此认为私有构造函数没有太大价值。它们确实有其用途，但超出了当前讨论的范围。

添加了公共构造函数后，你现在可以使用 *Circle* 类并调用其 *Area* 方法。请注意你如何使用点表示法在 *Circle* 对象上调用 *Area* 方法：

Click here to view code image

```
Circle c;
c = new Circle();
double areaOfCircle = c.Area();
```

## 重载构造函数

你几乎完成了，但还不完全。你现在可以声明一个 *Circle* 变量，用它引用一个新创建的 *Circle* 对象，然后调用其 *Area* 方法。然而，还有一个最后的问题。所有 *Circle* 对象的面积将始终为 0，因为默认构造函数将半径设置为 0，并且它保持为 0；*radius* 字段是私有的，在初始化后没有简单的方法可以更改其值。构造函数只是一种特殊类型的方法，它——像所有方法一样——可以被重载。就像有多个版本的 *Console.WriteLine* 方法，每个版本接受不同的参数一样，你也可以编写构造函数的不同版本。因此，你可以在 *Circle* 类中添加另一个带有指定半径参数的构造函数，如下所示：

Click here to view code image

```
class Circle
{
    private int radius;

    public Circle() // default constructor
    {
        radius = 0;
    }

    public Circle(int initialRadius) // overloaded constructor
    {
        radius = initialRadius;
    }

    public double Area()
    {
        return Math.PI * radius * radius;
    }
}
```

### 注意

类中构造函数的顺序无关紧要；你可以按自己感觉最舒适的顺序定义构造函数。

然后你可以在创建新的 *Circle* 对象时使用此构造函数，例如以下代码：

```
Circle c;
c = new Circle(45);
```

当你构建应用程序时，编译器会根据你为 new 运算符指定的参数确定应调用哪个构造函数。在此示例中，你传递了一个 *int*，因此编译器生成调用接受 *int* 参数的构造函数的代码。

你应该注意 C# 语言的一个重要特性：如果为类编写了自己的构造函数，编译器将不会生成默认构造函数。因此，如果你编写了接受一个或多个参数的构造函数，并且也想要一个默认构造函数，你必须自己编写默认构造函数。

## 部分类

一个类可以包含许多方法、字段和构造函数，以及后续章节中讨论的其他项。一个功能强大的类可能会变得相当庞大。使用 C#，你可以将类的源代码拆分到单独的文件中，以便将大型类的定义组织成更易于管理的较小部分。此功能被 Visual Studio 2015 用于通用 Windows 平台（UWP）应用，其中开发人员可以编辑的源代码与 Visual Studio 在表单布局更改时生成的代码分开维护。

当你将类拆分到多个文件时，你使用 partial 关键字在每个文件中定义类的各个部分。例如，如果 Circle 类被拆分到两个文件 circ1.cs（包含构造函数）和 circ2.cs（包含方法和字段）之间，circ1.cs 的内容如下所示：

Click here to view code image

```
partial class Circle
{
    public Circle()  // default constructor
    {
        this.radius = 0;
    }

    public Circle(int initialRadius) // overloaded constructor
    {
        this.radius = initialRadius;
    }
}
```

circ2.cs 的内容如下所示：

Click here to view code image

```
partial class Circle
{
    private int radius;

    public double Area()
    {
        return Math.PI * this.radius * this.radius;
    }
}
```

当你编译拆分到单独文件中的类时，必须向编译器提供所有文件。

在下面的练习中，你将声明一个类来模拟二维中的点

