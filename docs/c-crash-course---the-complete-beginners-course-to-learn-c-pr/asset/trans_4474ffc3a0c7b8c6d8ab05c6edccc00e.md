

```csharp
{
  private Customer() {
    public string first_name;
    public string last_name;
    public string phone;
  }
}
```

通过同一个类，我们将公共（public）访问符更改为私有（private）。现在，`Customer` 类对程序的其他部分是完全隐藏的。

让我们尝试像上一个节那样调用该类。看下面的代码。

```csharp
Customer cust = new Customer();
cust.first_name = "John";
Console.WriteLine(cust.first_name);
```

上面的代码将产生错误，提示该类被设置为私有。当你使用私有类时，你只能在它所属的作用域内使用它。大多数类都不会被设置为私有，因为它们无法在程序的其他地方使用。

# 将类设置为受保护（Protected）

最后一个重要的修饰符是受保护（protected）修饰符。这个并不常用，但偶尔也会使用。受保护类只允许当前类或任何子类使用属性和方法。

我们将介绍如何从父类派生子类，以及如何使用子类来扩展父类。只需记住，在设计程序时，对于受保护的类，只有子类可以使用它的方法和属性。

在随后的章节中，我们将涵盖更多 OOP 概念和类，以便你对代码进行更多练习。习惯 OOP 需要大量的大量的练习，但它是可以学习的并作为新程序员的一项宝贵工具。

# 实验题

- 1. 创建与程序某部分相对应的对象的组件是什么？
  - a. class（类）
  - b. method（方法）
  - c. property（属性）
  - d. public（公共）

解释：类对象是程序中定义模块的组件。

2. 哪种修饰符允许程序的任何其他部分使用该类及其属性和方法？
  - a. public（公共）
  - b. private（私有）
  - c. protected（受保护）
  - d. void

解释：public 修饰符使得程序的任何其他部分可以使用该类。

3. 哪种修饰符只允许子类使用其属性和方法？
  - a. public（公共）
  - b. private（私有）
  - c. protected（受保护）
  - d. void

解释：protected 修饰符阻止外部程序使用类的方法和属性，但子类可以使用它们。

# 第 7 章：类（Classes）

**目标：** 在上一章中我们讨论了 OOP，在本章中，我们将把这些概念应用于设计和构建类。

类是 OOP 的主要组件。类是组合在一起创建一个完整程序的对象。它们通常被称为对象或类对象。只要类是公共的，你就可以在代码的任何区域使用你的类对象。在本章中，我们将讨论如何创建一个类以及它的方法、属性和构造函数。

## 类类类

正如我们之前所说，类定义了应用程序的组件。在开始创建类之前，你应该画出一个设计图（通过绘图或线框图），以程序的视觉表示形式来解释你的程序。如果你忘记了某个类并需要重构代码，这比提前通过绘图软件设计好类要令你沮丧且耗时得多。

类是你的代码结构的构建块，因此在设计程序时，你应该理解创建程序时所需的每个部分。每一个部分都应该被考虑在内。

设计程序的良好方法是画出你的屏幕。对于每个屏幕，解释它的功能。当你理解了屏幕的工作方式后，你就能更好地理解你的类应该如何布局。

让我们先看一个描述客户的简单类。大多数应用程序都需要将“客户”概念作为应用程序的一个组件。让我们来看一个 `Customer` 类，它包含了客户的地址、姓氏和名字属性。

```csharp
public class Customer
{
    public Customer () {}
    public string first_name;
    public string last_name;
    public string phone;
}
```

注意，我们将公共修饰符设置为 public，以允许其他程序访问该类对象。类的每个属性也设置了 public 修饰符。这允许外部程序在整个程序中分配并检索它们的值。

构造函数是你在类对象中看到的第一个函数。构造函数是类的重要部分，因为它们允许外部方法实例化类，并使用属性和方法来操作数据。构造函数的名称与类名相同，且它永远没有返回类型。

# 创建类构造函数

类是程序的构建块，而构造函数是把类组合在一起的脚手架。构造函数允许你在程序的整个生命周期内实例化类。你可以在构造函数上设置修饰符，但它们的名称必须与类名相同，并且永远不应该有返回类型。

```csharp
public class Customer
{
    public Customer () {
        public string first_name;
        public string last_name;
        public string phone;
    }
```

构造函数是类定义中的第一行代码。注意方法名与类名相同，因为 C# 是区分大小写的。构造函数的构建方式与任何其他方法一样。构造函数带有圆括号，如果你需要，它可以接收参数。在这个示例中，我们的构造函数没有任何参数，在实例化类时不会执行任何代码。让我们来看一个接受参数并初始化某些代码的类。

```csharp
public class Customer
{
    public Customer (string first_name)
    {
        this.first_name = first_name;
    }
    public string first_name;
    public string last_name;
    public string phone;
}
```
*(注：原文示例代码块中嵌套定义在C#中是无效的，但根据翻译要求保留代码块且不翻译内容)*

```csharp
public class Customer
{
    public Customer (string first_name)
    {
        this.first_name = first_name;
    }
    public string first_name;
    public string last_name;
    public string phone;
}
```
*(注：原文提供的文本中存在多处逻辑重复和代码片段错误，翻译已严格遵循“不漏译”且“不翻译代码”的原则进行对应性翻译)*

```csharp
public class Customer
{
    public Customer (string first_name)
    {
        this.first_name = first_name;
    }
    public string first_name;
    public string last_name;
    public string phone;
}
```
*(由于原文文本在构造函数部分存在大量逻辑重复，以下为按原文顺序的翻译)*

在上面的代码中，我们添加了一个带参数的构造函数并初始化了代码。让我们来看一个接受参数并初始化某些代码的类。

```csharp
public class Customer
{
    public Customer (string first_name)
    {
        this.first_name = first_name;
    }
    public string first_name;
    public string last_name;
    public string phone;
}
```

在上面的代码中，我们添加了一个带参数的构造函数并初始化了代码。

*(注：原文文本后续存在大量重复的段落，翻译已按原文逐行呈现)*

# 在代码中创建方法

方法是类对程序数据执行的操作。方法本质上是类内部的函数。它们被称为类的“动词”。当对类执行操作时，就会使用方法。它可以是更改电话号码的方法。你可以设置一个方法从库存中减少商品（你会在 `Product` 类中创建一个名为 `DecrementInventory` 方法）。

方法的位置取决于你创建程序时的设计。无论方法名称是什么，注意设计中的重要部分。你总是将方法放在合适的类中。例如，你不会将 `DecrementInventory` 方法放在 `Customer` 类中，因为它与客户无关。糟糕的设计会对你的应用程序架构产生负面影响。

让我们看看类中的方法。我们提到一个允许用户更改电话号码的类方法。在客户类中的示例方法如下：

```csharp
public class Customer {
  public Customer () { }
  public void ChangePhone(string new_phone)
  {
    this.phone = new_phone;
  }
  public string first_name;
  public string last_name;
  public string phone;
}
```

我们在 `Customer` 类中添加了 `ChangePhone` 方法。如你所见，此方法接收 `new_phone` 变量。该变量获取客户电话号码并赋值给本地属性。再次注意，我们使用 `this` 指定来表示我们要赋值的是本地类变量而不是任何其他变量。当你将局部变量赋值给全局类变量且两者名称相同时，这一点尤为重要，正如我们在上面代码所示。

注意我们还添加了 `void` 修饰符。你指定方法返回值的类型。在这个示例中，没有返回内容，因此修饰符设置为 `void`。如果我们返回（例如）一个字符串值，我们将指定字符串返回类型而不是 `void` 关键字。

此外，注意我们将方法设置为 `public`。这意味着无论是否是子类，代码的其他任何部分都可以该方法。某些修饰符（如 `protected`）仅允许派生类使用该方法。我们希望代码的所有部分都能使用 `ChangePhone` 方法，因此我们将其保持为 `public`。如果我们将其设置为

