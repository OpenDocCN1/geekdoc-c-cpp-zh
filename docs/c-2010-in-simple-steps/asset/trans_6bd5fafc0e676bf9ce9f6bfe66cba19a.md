
为了访问类的成员数据和成员函数，您需要声明该类的一个对象。在 C# 中声明对象的语法是：

```
<className> <objectName> = new <className>();
```

C# 提供了多种定义类的方式，例如提供不同的访问级别、从其他类继承特性，以及在对象实例化或销毁时让您指定和控制代码的行为和输出。要在您的 C# 应用程序中实现所有这些功能，您需要了解以下概念：

- 访问修饰符
- 方法
- 构造函数和析构函数
- 部分类
- 静态类
- 扩展方法

让我们在以下各节中详细了解这些内容。

## 介绍访问修饰符

可以使用访问修饰符指定类成员或类型的可访问性级别。访问修饰符有助于避免数据和方法与现有代码混杂，同时保护类的对象免受外部干扰。它通过定义一定的作用域以受限的方式访问数据和方法来保护对象。您可以使用访问修饰符声明类及其方法。然而，一个方法只能包含一个修饰符。C# 中使用的不同类型的访问修饰符列在表 4.1 中：

表 4.1：C# 中的访问修饰符

| 访问修饰符 | 描述 | 语法 |
|---|---|---|
| Public | 对类内部和外部的成员提供公共访问权限，没有任何限制。 | class SampleClass
{
    public int x; // No access
    // restrictions.
} |
| Protected | 提供受保护的成员访问权限。您可以从声明它们的类或从派生自声明它们的类的类访问受保护成员。 | class A
{
    protected int x = 123;
} |
| Internal | 提供对当前程序集中成员的访问权限。如果在定义它的程序集之外访问具有 internal 访问修饰符的成员，则应用程序会生成错误。 | public class BaseClass
{
    // Only accessible within the
    // same assembly
    internal static int x = 0;
} |
| Private | 提供对在声明它们的类主体内成员的访问权限。 | class Employee
{
    private int i;
    double d; // private access by default
} |
| Protected internal | 提供对可见于当前程序集或派生自声明它们的类的类型的成员的访问权限。 | namespace MyAssembly //current
//assembly
{
  public class One
  {
    protected internal int Method()
    {
      //method code
    }
  }
  public class Two : One
  {
    public int Add()
    {
      One obj = new One();
      return obj.Method();
    }
  }
} |

> **Note**
> 
> *程序集是一组一个或多个文件作为一个单元使用。它构成部署的单一单元，是 .NET 应用程序的主要构建块。*

接下来，让我们讨论方法以及如何在 C# 中使用它们。

## 使用方法

C# 中的方法是一段包含一系列语句以执行操作的代码块。C# 中的每个操作都在方法的上下文中执行。方法可以在类或结构内部声明。

> **Note**
> 
> *结构是一种值类型，由构造函数、常量、数据成员、方法等组成。您可以使用 struct 关键字在 C# 中创建结构。您将在后面的章节中详细了解 C# 中的结构。*

方法声明通常包括指定访问级别、返回值、方法名称和方法的参数的访问修饰符。所有这些组合在一起称为方法的签名。

以下代码片段显示了如何声明方法：

```csharp
class Passenger
{
    public void Title() { }
    public void Name(int age) { }
    public int Address(int houseno, int pincode)
    {
        //Some code
    }
}
```

前述代码片段包含三个方法，即 Title()、Name() 和 Address()。这些方法的参数用括号括起来并用逗号分隔。如果您传递一组空括号，则意味着该方法不需要参数。

构造函数和析构函数是 C# 程序中每个类的特殊方法。每个类都有自己的构造函数和析构函数，当类的实例被创建或销毁时会自动调用它们。构造函数在您访问类时初始化所有类成员，而析构函数在对象不再需要时销毁分配给类成员的值。

### Note

> 您将在本章后面详细了解构造函数和析构函数。

现在，让我们学习如何在 C# 程序中定义然后调用方法。

## 定义方法

如前所述，方法由一系列语句组成。这些语句构成方法体，并在调用方法时执行。方法通常定义类的行为并允许程序员将程序逻辑分离为不同的单元。您可以始终将一些信息传递给方法，执行一条或一组指令，然后从中返回值。

让我们考虑一个简单的例子，以便更好地理解方法的概念。假设您需要找到数字 10 的平方。您也许可以按以下代码片段所示编写代码：

```
int square = 10 * 10;
```

现在考虑一种需要从用户接受输入的情况。前面的代码片段将不再满足目的。然而，使用方法，您可以相当轻松地执行此任务。

让我们执行以下步骤创建一个名为 CreatingMethod 的控制台应用程序，并学习如何在 C# 程序中定义方法：

- 1. 单击 开始→所有程序→Microsoft Visual Studio 2010→Microsoft Visual Studio 2010 以打开 Visual Studio 2010 集成开发环境（IDE）。
- 2. 在 Visual Studio 2010 IDE 中，从菜单栏选择 文件→新建→项目 选项以打开 新建项目 对话框。
- 3. 在 新建项目 对话框中，在 已安装模板 窗格中选择 Visual C# 选项，并在中间窗格中选择 控制台应用程序 选项。
- 4. 在 名称 文本框中输入 CreatingMethod 以指定应用程序的名称，并在 位置 下拉组合框中指定应用程序的适当位置。在我们的例子中，我们选择了默认位置，即 D:\C# 2010 Applications。
- 5. 单击 确定 按钮。CreatingMethod 应用程序已创建。
- 6. 在 Program.cs 文件中，将清单 4.1 中给出的突出显示的代码片段添加到 Program 类内部：

### 清单 4.1：显示定义方法的代码

```csharp
public static int GetSquare()
{
    int num, square = 0;
    Console.WriteLine("Enter an integer number");
    num = Convert.ToInt32(Console.ReadLine());
    square = num * num;
    return square;
}
```

在清单 4.1 中，定义了一个方法 GetSquare()。声明了两个局部整数变量 num 和 square，并将其初始化为值 0。Console.WriteLine() 语句用于提示用户输入一个整数。变量 square 被赋值为用户输入的数字的平方。然后返回变量 square 中包含的值。

## 调用方法

在 C# 中，在代码中定义方法后，您需要调用它以实现代码并执行程序的逻辑。调用方法类似于从计算机上的不同位置访问文件。您可以在应用程序的 Program 类的 Main() 方法中调用方法。

现在让我们学习如何在定义后调用方法。我们将调用清单 4.1 中定义的方法。执行以下步骤以调用本章 定义方法 部分中创建的 CreatingMethod 应用程序中定义的 GetSquare() 方法：

- 1. 将清单 4.2 中给出的突出显示的代码片段添加到 CreatingMethod 应用程序中 Program 类的 Main() 方法：

### 清单 4.2：调用方法

```csharp
static void Main(string[] args)
{
    Console.WriteLine("The square of the number is " + Program.GetSquare());
    Console.WriteLine("\nPress ENTER to quit...");
    Console.ReadLine();
}
```

- 2. 按 F5 键运行 CreatingMethod 应用程序。应用程序的输出显示如下图所示 Fig.C#-4.1：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_109_0.png)

Fig.C#-4.1

- 3. 输入一个数字并按键盘上的 Enter 键。输出显示如下图所示 Fig.C#-4.2：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_109_1.png)

Fig.C#-4.2

如 Fig.C#-4.2 所示，当您输入数字 21 时，其平方被计算并显示在屏幕上。现在，让我们研究如何在 C# 中向方法传递参数。

## 传递参数

在 C# 中，使用 params 关键字，您可以在 C# 应用程序中定义方法参数。您可以使用 params 关键字接受可变数量的参数。params 关键字在方法的形参列表中占据最后一个位置。要创建接受可变数量参数的方法，您可以执行以下步骤：

- 1. 重复本章 定义方法 部分的步骤 1 到 3。
- 2. 在 名称 文本框中输入 PassingParameters 以指定应用程序的名称，并在 位置 下拉组合框中指定应用程序的适当位置。在我们的例子中，我们选择了默认位置，即 c:\users\temp\documents\visual studio 2010\Projects。
- 3. 单击 确定 按钮。PassingParameters 应用程序已创建。
