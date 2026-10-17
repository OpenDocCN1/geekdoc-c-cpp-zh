
## 构造函数中的字段初始化

让我们详细查看构造函数在调用后做了什么。我们知道，调用时会为每个字段分配内存，并用默认值初始化该内存。如果字段是基本类型，我们将赋值新值。如果字段是引用类型（例如我们的字段 `name`），构造函数将将其初始化为 `null`。然后它将创建相应的对象，并在最后为字段赋值。

```java
public class Collar
{
    private int size;
    public Collar()
    {
}
}
```

```java
public class Dog
{
    private string name;
    private int age;
    private double length;
    private Collar collar;
    public Dog()
    {
        this.name = "Sharo";
        this.age = 3;
        this.length = 0.5;
        this.collar = new Collar();
    }
    // ... 类的其余部分 ...
}
```

## 内存中的表示

让我们遵循构造函数被调用后的步骤。我们知道，调用时会为每个字段分配内存，并用默认值初始化内存。首先在堆中为相应字段分配内存，并用字段类型的默认值初始化内存。例如，考虑 `Dog` 类的示例：

```java
public class Dog {
    private string name;
    Dog() {
        Console.WriteLine("this.name has value of: \"" + this.name + "\"");
        // ... 这里没有其他代码 ...
    }
    // ... 类的其余部分 ...
}
```

尝试创建此类类型的新对象时，控制台将显示：
this.name has value of: ""

## 534 C# 计算机编程基础

![](img/251ffe19d2b15f8a8f566ab01924bb12_534_0.png)

## 14. 定义类

![](img/251ffe19d2b15f8a8f566ab01924bb12_536_0.png)

然后创建 **Collar** 对象。我们的构造函数（`Dog` 类）调用类的构造函数，为对象分配内存：

```java
public class Collar
{
    private int size;
    public Collar()
{
```

```java
public class Dog
{
    private string name;
    private int age;
    private double length;
    private Collar collar;
    public Dog()
    {
        this.name = "Sharo";
        this.age = 3;
        this.length = 0.5;
        this.collar = new Collar();
    }
    // ... 类的其余部分 ...
}
```

接下来，构造函数将用类型的默认值对其初始化。`Collar` 的 size 没有显式赋值，因此它将取默认值（int 为 0）：之后，类构造函数返回的新创建对象的引用**将被赋值给字段。**

最后，类型为 **Dog** 的新对象的引用将赋值给 Main() 方法中的局部变量 myDog**。

## 537 C# 计算机编程基础

![](img/251ffe19d2b15f8a8f566ab01924bb12_537_0.png)

## 字段的初始化顺序

为了避免混淆，让我们解释类字段初始化的顺序，无论我们是否在构造函数中为它们赋值并初始化了它们。

首先在堆中为相应字段分配内存，并用字段类型的默认值初始化内存。例如，考虑 `Dog` 类的示例：

```java
public class Dog {
    private string name;
    Dog() {
        Console.WriteLine("this.name has value of: \"" + this.name + "\"");
        // ... 这里没有其他代码 ...
    }
    // ... 类的其余部分 ...
}
```

当我们尝试创建此类类型的新对象时，控制台将显示：
this.name has value of: ""

## 539 C# 计算机编程基础

![](img/251ffe19d2b15f8a8f566ab01924bbbb12_539_0.png)

# 第 14 章。定义类

this.name 的值为：""

在按照相应类型的默认值对字段进行初始化后，CLR（公共语言运行时）的第二步是：如果在在声明字段时设置了值，则为该字段赋值该值。

因此，如果我们更改了 `Dog` 类中声明字段 `name` 的代码行，它将首先被初始化为 `null`，然后会被赋值为 `"Rex"`。

```cs
private string name = "Rex";
```

相应地，对于该类的每一个新对象的创建过程：

```cs
static void Main()
{
    Dog dog = new Dog();
}
```

后续将打印以下内容：

this.name 的值为："Rex"

只有在执行了类字段初始化的这两个步骤（默认值初始化以及程序员在声明字段时可能设置的值）之后，该类的构造函数才会被调用。此时，字段将获得在构造函数体中设置的值。

## 声明带参数的构造函数

在上一节中，我们看到了如何给字段设置除默认值以外的值。然而，在声明构造函数时，我们往往不知道各个字段将取什么值。为了解决这个问题，类似于带参数的方法，字段将被赋值为构造函数体中提供给它们的值。例如：

```cs
public Dog(string dogName, int dogAge, double dogLength)
{
    name = dogName;
    age = dogAge;
    length = dogLength;
    collar = new Collar();
}
```

## C# 计算机编程基础

同样，调用带参数的构造函数的方式与调用带参数的方法相同——所需的值以列表的形式提供，元素之间用逗号分隔：

```cs
static void Main()
{
    Dog myDog = new("Moby", 2, 0.4); // 传递参数
    Console.WriteLine("My dog " + myDog.name + 
    " is " + myDog.age + " year " + myDog.old. + 
    " and has length: " + myDog.length + " m.");
}
```

执行此 `Main()` 方法的结果如下：

| 我的狗 Moby 今年 2 岁。它的长度是：0.4 米。 |

在 C# 中，类的构造函数数量没有限制。唯一的要求是它们的签名必须不同（关于什么是签名，我们已经在“方法”章节中解释过）。

## 构造函数参数的作用域

类比方法参数列表中变量的作用域，一个构造函数参数列表中的变量的作用域从构造函数的起始左括号一直延伸到结束右括号，即贯穿整个构造函数体。

很多时候，当我们声明一个带参数的构造函数时，可以将参数列表中的变量命名为与要初始化的字段相同的名称。例如，让我们考虑 `Dog` 类的构造函数：

```cs
public Dog Dog(string name, int age, double length)
{
    name = name;
    age = age;
    length = length;
    collar = new Collar();
}
```

编译并执行上面声明的 `Main()` 方法：

| 我的狗 0 岁。它的长度是：0 米。 |

很奇怪，不是吗？在这一事实中，结果并不那么尴尬。解释如下：构造函数参数列表中变量作用的作用域，与构造函数中同名字段的作用域重叠了。因此，我们没有给字段赋值任何值，因为在实践中我们无法访问它们。例如，我们没有给字段赋值，而是我们在构造函数体中没有对字段的访问权限。例如：

```cs
age = age;
```

正如我们在“字段与局部变量”节中看到的，为了避免这个问题，我们应该使用 `this` 关键字给字段赋值：

```cs
public Dog(string name, int age, double length)
{
    name = name;
    age = age;
    length = length;
    collar = new Collar();
}
```

现在，让我们再次执行 `Main()` 方法：

```cs
static void Main()
{
    Dog myDog = new("Moby", 2, 0.4);
    Console.WriteLine("My dog " + myDog.name + 
    " is " + myDog.age + " year " + myDog.old. + 
    " and has length: " + myDog.length + " m.");
}
```

输出结果将是：我的狗 Moby 今年 2 岁。它的长度是：0.4 米

## 带变长参数的构造函数

类似于带参数的方法，带变长参数的构造函数调用以相同的方式进行——所需的值以列表的形式提供，元素之间用逗号分隔：

- 1. 当我们声明带变长参数的构造函数时，必须使用 `params` 关键字。
- 2. 带变长参数的构造函数允许有其他参数。
- 3. 变长参数必须位于参数列表的最后。

考虑一个类的构造函数声明，它描述了如下内容：

```cs
public Lecture(string subject, params string[])
{
    // 变量的初始化
}
```

声明中的第一个参数是科目名，后续参数是学生姓名。这里是构造该类的示例：

```cs
Lecture lecture = new Lecture("Biology", "Peter", "Steven");
```

在在上一个示例中，我们看到根据创建我们类对象的需要，我们可以声明构造函数的多个变体。很容易发现，构造函数的大部分代码是重复的。这让我们思考是否有一种替代方法，可以让一个已经正在执行初始化的构造函数被其他构造函数复用以执行相同的初始化。另一方面，在章节开头提到，构造函数无法以这种方式被调用

方法通过 `new` 关键字进行调用。应该有某种方法——否则会有大量不必要的重复代码。

在 C# 中，存在一种机制，使得一个构造函数可以调用同一个类中定义的另一个构造函数。这同样通过 `this` 关键字来实现，但通过在声明构造函数时的语法结构：

```
[<modifiers>] <class_name>([parameters_list_1])
: this([parameters_list_2])
```

在声明构造函数的已知形式（上述声明的第一行），我们可以添加一个冒号，后面跟上关键字 `this`，然后是圆括号。如果我们想要调用的构造函数带有参数，我们需要在括号中添加一个需要提供的参数列表 `parameters_list_2`。

以下是关于构造函数重载章节中代码的写法，现在我们不再重复每个每个字段的初始化，而是调用同一类中声明的构造函数：

```csharp
// 无参数
public Dog()
  : this("Ax1") // 调用构造函数
{
  // 此处可以添加更多代码
}

// 单参数
public Dog(string name)
  : this(name, 1) // 调用构造函数
{
}

// 双参数
public Dog(string name, int age)
  : this(name, age, 0.3) // 调用构造函数
{
// 三参数
public Dog(string name, int age, double length)
  : this(name, age, length, new Collar()) // 调用构造函数
{
// 四参数
public Dog(string name, int age, double length, Collar collar) {
    this.name = name;
    this.age = age;
    this.length = length;
    this.collar = collar;
}
```

如上面示例中第一个构造函数的注释所示，如果有必要，在调用带有特定参数的其他构造函数之外，每个构造函数都可以在其体中添加代码，执行额外的初始化或其他操作。

# 默认构造函数

考虑以下问题：如果我们不在类中声明构造函数会发生什么？我们如何从该类型创建对象呢？

恰好，当一个类没有任何构造函数时，这个问题由 C# 解决。当我们不不声明构造函数时，编译器会为我们创建一个，并将其用于创建像我们的类这样的对象。这种构造函数被称为默认隐式构造函数，它不会有任何参数并且是空的（即除了对象字段的默认置零之外，它什么都不做）。

> 当我们不在给定的类中声明任何构造函数时，编译器将创建一个，的默认隐式构造函数。

例如，让我们声明 `Collar` 类，不在其中声明任何构造函数：

```csharp
public class Collar {
    private int size;
    public int Size {
        return size;
    }
}
```

虽然我们没有显式声明无参数构造函数，但我们可以通过以下方式创建该类的对象：

```csharp
Collar collar = new Collar();
```

# 默认构造函数

默认无参数构造函数如下：

```
<access_level> <class_name>() {}
```

我们应该知道默认构造函数的命名始终与类 `<class_name>` 相同，它的参数列表和体始终为空。如果类中没有构造函数，编译器会添加一个。默认构造函数通常是公共的或受保护的。

> 默认构造函数始终没有参数。

为了确保默认构造函数始终没有参数，让我们尝试通过设置参数来调用默认构造函数：

```csharp
Collar collar = new Collar(5);
```

编译器将显示以下错误信息：

```
'Collar' 不包含接受 1 个参数的构造函数
```

# 默认构造函数是如何工作的？

正如我们所猜测的，默认构造函数在创建我们的类对象时唯一做的事情就是将类的字段置零。例如，如果在 `Collar` 类中没有声明任何构造函数，我们从它创建一个对象，稍后尝试打印 `size` 字段中的值：

```csharp
static void Main()
{
  Collar collar = new Collar();
  Console.WriteLine("Collar's size is: " + collar.Size);
}
```

结果将是：

```
Collar's size is: 0
```

我们看到对象 `collar` 的 `size` 字段保存的值只是整数类型 - int 的默认值。

# 何时默认构造函数不会创建？

我们必须知道，如果在给定的类中至少声明了一个构造函数，那么编译器就不会创建默认构造函数。

为了研究这一点，请考虑以下示例：

```csharp
public Collar(int size)
    : this()
{
    this.size = size;
}
```

假设这是 `Collar` 类中唯一的构造函数。我们尝试调用其中一个无参数的构造函数，希望编译器为我们创建了一个无参数的构造函数。在我们尝试编译后，我们会发现我们尝试的操作是不可能的。编译器会显示：

```
Collar 不包含接受 0 个参数的构造函数
```

关于默认构造函数的规则是：

> 如果我们在给定的类中至少声明了一个构造函数，编译器就不会创建默认构造函数。

# 默认构造函数与无参数构造函数的区别

在结束本节之前，我们将澄清重要的一点：

> 虽然默认构造函数和无参数构造函数在签名上相似，但它们完全不同。

区别在于，默认构造函数是由编译器在没有构造函数的情况下创建的，而无参数构造函数是我们声明的。

此外，正如之前提到的，默认构造函数始终是公共或受保护的，取决于类的修饰符，而无参数构造函数取决于我们。

## 属性

在面向对象编程的世界中，有一个名为属性的元素，它介于字段和方法之间，用于更好地保护类的状态。在某些面向对象编程语言中，如 C#、Delphi / Pascal、Visual Basic、Python 和其他，属性是语言的一部分。其他语言如 Java 不属性概念，为了此目的程序员应该声明一对方法。

# C# 中的属性 – 示例介绍

使用属性是一种良好的实践，也是面向对象编程概念的重要部分。编程中属性的是通过声明来实现此功能的。

考虑一个示例。我们再次有一个 `Dog` 类，描述一只狗。狗的一个特征是，例如它的颜色。对狗的“颜色”属性的访问及其相应的修改可以通过方式完成：

```csharp
// 获取（读取）属性
string color = dogInstance.Color;

// 设置（修改）属性
dogInstance.Color = "black";
```
