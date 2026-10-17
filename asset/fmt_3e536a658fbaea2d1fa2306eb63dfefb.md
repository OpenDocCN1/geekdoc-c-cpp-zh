
```
        return bathrooms;

    }

    set {

        bathrooms = value;

    }

}

public decimal RentPerMonth {

    get {

        return rentPerMonth;

    }

    set {

        if (value > 0M)

            rentPerMonth = value;

    }

}

}

//General Methods --------------------------------

}
```

三种建筑类型中的每一种都以类似于下面的代码行开头：
`class clsApartment : clsBuilding`

这建立了图 16-1 所示的“是一个（is a）”关系。（这与你通过本书看到的几乎每个表单类定义中的 `: Form` 没有区别。）通过使用这种语法将每个派生类连接到基类，你可以在所有派生类中使用 `clsBuilding` 中的 `PropertySummary()`。

还有一点：派生类不能继承构造函数。你必须为派生类编写一个构造函数。如果基类没有默认构造函数，派生类的构造函数必须使用 `base` 关键字调用基类构造函数，如 `clsApartment` 所示：

```csharp
public clsApartment(string addr, decimal price, decimal price,
decimal tax, decimal insur, DateTime time,
int type :
base(addr, price, payment, tax,
insur, date, type);
```

这里使用 `base` 关键字是为了将用于构造 `clsApartment` 对象的参数传递给 `clsBuilding` 构造函数。（该概念与用于多个构造函数使用的这种结构类似。）

# 基类不是派生类

派生类使用基类方法的能力是一个单向关系。也就是说，派生类可以调用基类方法，但基类不能直接调用派生类方法。例如，假设 `clsCommercial` 一个名为 `HouseCleaning()` 的公共方法。如果 `MyBldg` 是一个 `clsBuilding` 对象，你不能使用：

```csharp
myBldg.HouseCleaning(); // Error!!
```

编译器会抛出错误并通知你找不到 `HouseCleaning()` 的定义。即使你对 `HouseCleaning()` 方法使用 `public` 访问修符，这个结论也是正确的。你无法执行基类-派生方法调用的原因是图 16-1 所示的“是一个”关系是一条单行道。也就是说，`clsCommercial` 对象假设拥有 `clsBuilding` 对象的所有属性和方法，但 `clsBuilding` 对象并不假设拥有 `clsCommercial` 对象的所有属性和方法。

# 抽象类

如前面提到的，基类通常用作派生类之间共享的所有属性的存储。然而，基类可能是非抽象的，实例化其中一个基类是没有意义的。例如，你可能会创建一个名为 `clsDeciduous` 的树类，它具有 `leafColor`、`barkStyle`、`maxHeight` 和 `ringCount` 属性。派生类必须是 `clsOak`、`clsMaple`、`clsWillow` 等。问题在于，即使所有派生类都有叶子、树皮高度和年轮计数，但有许多具有这些特征的树，使得实例化 `clsDeciduous` 对象是没有意义的。只有在派生类中找到的细节结合基类，才有足够的信息使对象变得有用。

为了防止基类的实例化，请使用 `abstract` 关键字：

```csharp
public abstract class clsDeciduous
{
  // The class code...
```

如果类是通过 `abstract` 关键字定义的（如下所示），则你无法实例化该类的对象。这意味着像下面这条语句会引起编译器错误，告诉你不能实例化抽象类的对象：

```csharp
clsDeciduous myLeafTree = new clsDeciduous();
```

如果你不能实例化类的对象，为什么要使用它呢？

通过使用 `abstract` 关键字定义类，你是在告诉该类的用户两件事：第一，他们不能实例化该类的对象，这提醒了他们第二个原因。第二，更重要的一点是，用户必须定义派生类来捕捉基类中体现的功能。事实上，如果你使用 `abstract` 关键字定义一个方法，派生类必须实现它。

如果一个类是通过 `abstract` 关键字定义的（如下所示），你无法实例化该类的对象。这意味着像下面这条语句会引起编译器错误，告诉你不能实例化抽象类的对象：

```csharp
clsDeciduous myLeafTree = new clsDeciduous();
```

如果你不能实例化类的对象，为什么要使用它呢？

通过使用 `abstract` 关键字定义类，你是在告诉该类的用户两件事：第一，他们不能实例化该类的对象，这提醒了他们第二个原因。第二，更重要的一点是，用户必须定义派生类来捕捉基类中体现的功能。事实上，如果你使用 `abstract` 关键字定义一个方法，派生类必须实现它。

# 多态

第16章提到多态是面向对象编程的三支柱之一。当时我回避了这个话题，说多态这个词来自希腊语，意思是“多种形状”。现在你理解了继承，就可以完全欣赏多态了。

与其坚持“多种形状”的概念，也许应该将其修改为“多种消息”。本质上，多态意味着你可以向不同的类发送相同的消息，每个类都会正确响应。

## 尝试使用多态

考虑以下示例。在我住的地方，如果下雪超过2，你就出去扫雪。程序的示例如图16-3所示。

注意公寓和商业建筑给了电话号码，但对于住在家里的人没有提供。假设是作为合同的一部分，租户需要自己扫雪。

你下载的代码已经包含了 `RemoveSnow` 方法。这个练习只是解释了如何实现多态。

## 如何工作

你首先需要修改基类以处理除雪消息。添加到 `clsBuilding` 中的代码如下：

```csharp
public virtual string RemoveSnow()
{
    return whichType[buildingType] +
        ": No snow removal service available.";
}
```

## virtual关键字

`clsBuilding` 中的除雪方法 `RemoveSnow()` 是通过 `virtual` 关键字定义的。`virtual` 关键字用于标识该方法可以在派生类中被重写。换句话说，虚拟方法可以在任何派生自此基类的类被不同的定义替换。

如果你参考图16-1，你可以看到为 `clsApart` 和 `clsCommercial` 对象提供了 `RemoveSnow()` 方法。这两个类的代码如下：

```csharp
public override string RemoveSnow() // clsApart
{
    return "Apartment: Call John's Snow Removal: 859.444.7654";
}
```

```csharp
public override string RemoveSnow() // clsCommercial
{
    return "Commercial: Call Acme Snow Plowing: 803.234.5566";
}
```

图 16-1 也显示了 `clsHome` 类没有 `RemoveSnow()` 方法。租房的人在签署租赁合同时已被告知，他们需要负责清理积雪。

### override 关键字

正如你可能猜到的那样，`override` 关键字与 `virtual` 关键字是相辅相成的。`virtual`（虚方法）告诉代码的阅读者该方法可以被重写，而 `override` 关键字则告诉该方法正在重写其继承类中的某个方法。

通常情况下，派生类会重写基类定义的虚方法。然而，你可以定义一个新的类 `clsRecreational`，可能为 `clsFrontage`、`boatRamp`、`availableFishingTackle` 等带有新的属性。该类的定义如下：

```csharp
public class clsRecreational : clsHome
{
    // 类代码
}
```

你可以根据需要不断扩展类定义。（如果你想防止某个类被继承，请在类定义中使用 `sealed`（密封）关键字作为修饰符，例如 `public sealed clsLastClass`。使用 `sealed` 关键字意味着不允许从该类进行进一步派生。）

但在大多数情况下，你是在使用 `override` 来对应基类中定义的虚方法。

### 发送清理积雪的消息

`frmMain` 的用户界面现在包含一个发布清理积雪消息的按钮。每个类都负责确定具体的操作方法。清理积雪消息的按钮点击代码如下：

```csharp
private void btnRemoveSnow_Click(object sender, EventArgs e)
{
    lstMessages.Items.Add(myapp.RemoveSnow());
    lstMessages.Items.Add(myComm.RemoveSnow());
    lstMessages.Items.Add(myHome.RemoveSnow());
    lstMessages.Items.Add("*");
}
```

每个派生类都通过调用 `RemoveSnow()` 方法发送相同的消息。然而，消息是由任何选择附加到方法调用上的派生类进行分派的。

注意，`clsHome` 虽然没有 `RemoveSnow()` 方法，但它仍然显示了以下消息：

> Home: No snow service available.

正如你无疑已经想出来的那样，由于 `clsHome` 没有 `RemoveSnow()` 方法，因此使用了基类中的 `RemoveSnow()` 方法。在其他情况下，`clsHome` 选择不重写 `RemoveSnow()` 方法，而是使用基类中写的“默认”方法。

继承和多态行为的优之处在于，每个对象都知道如何对调用的任何事件或方法做出特定的反应，尽管这些对象共享相同的方法名。

初看之下，继承似乎有点令人生畏。然而，如果你在不确定发生什么的地方设置若干断点并运行程序，你就能快速理解代码在做什么。单步执行程序是深入理解程序在执行时实际在做什么的绝佳方法。

## 扩展方法 (EXTENSION METHODS)

继承为你提供了一种避免重复代码的方法（如果没有父子关系，可能会代码重复）。当然，使用继承要求你能够访问类的源代码。然而，扩展方法允许你在没有源代码的情况下扩展类的功能。

你可以将扩展方法看作是静态方法，你在没有该类源代码的情况下将其授予现有类。理解扩展方法最简单的方法是通过下一个“尝试一试 (Try It Out)”中的示例。

假设你有一个程序，需要验证用户输入了有效的社会安全号码 (SSN)。有效的 SSN 格式为 `ddd-dd-dd`，这意味着一个三数字字段、两个数字字段、另一个连字符，最后是四位数字序列。你想要扩展 `String` 类以添加一个检查有效 SSN 的方法。图 16-4 显示了你即将编写的程序的示例运行情况。下一节将介绍如何使用扩展方法的示例。

![](img/4329bd7a4f8df07a)

## 使用扩展方法

**尝试一试 (TRY IT OUT)**：使用扩展方法

在 `clsExtension` 类中，我们使用 `this` 关键字来扩展 `string` 类。如下如 `LISTING 16-4` 所示：

```csharp
using System;
using System.Text.RegularExpressions;
namespace StringMethods
{
    public static class clsExtension
    {
        public static bool CheckSSN(this string str)
        {
            int len = str.Length;
            Regex pattern = null;
            if (len == 9)
            {
                pattern = new Regex(@"\d{3}-\d{2}-\d{4}");
            }
            else
            {
                return false;
            }
            return pattern.IsMatch(str);
        }
    }
}
```

在 `LISTING 16-5` 中，我们看到如何在程序中使用扩展方法：

```csharp
using System;
using System.Windows.Forms;
using StringMethods;
public class frmMain : Form
{
    private Label label;
    private Label lblResult;
    private TextBox txtSSN;
    private Button btnVerify;
    private Button btnClose;
    #region Windows 代码
    public frmMain()
    {
        InitializeComponent();
    }
    [STAThread]
    public static void Main()
    {
        frmMain main = new frmMain();
        Application.Run(main);
    }
    private void btnVerify_Click(object sender, EventArgs e)
    {
        string str = txtSSN.Text;
        if (str.CheckSSN())
            lblResult.Text = "Valid";
        else
            lblResult.Text = "Invalid";
    }
    private void btnClose_Click(object sender, EventArgs e)
    {
        Close();
    }
    #endregion
}
```

```cs
else
lblResult.Text = "Invalid";
```

你可以使用与任何其他字符串方法相同的语法来调用你的验证方法。
等一下。

`CheckValidSSN()` 的签名期望传递一个字符串。啊，是的，但签名中的关键字告诉方法，调用引用的是当前对象。因此，扩展方法已经可以访问正在测试的字符串，而不需要传递该字符串。调用根据字符串的内容返回 true 或 false，并显示相应的标签。

扩展方法为你提供了一种方便的方法，可以在不使用继承的情况下扩展类的功能。如果你曾想过“我真希望这个类能够做……”，你可能考虑编写一个扩展方法。当你为字符串模式或数据值编写重复的测试时，这一点尤为真实。

### 总结

本章完成了你对面向对象编程三大支柱的学习：封装、继承和多态。整个过程中，书中强调了将数据封装在类或方法内部的重要性。在本章中，你学习了 `protected` 访问修饰符允许你封装数据，同时根据需要将其与派生类共享。你还学习了多态如何让每个派生类以适合自身的方式对消息做出反应。最后，你看到了扩展方法如何通过“挂载”新方法来扩展类的功能，而无需使用继承。

### 练习

你可以在附 A 中找到以下练习的答案。

- 1. 一家高尔夫俱乐部想要建立一个会员计划，可以向其成员发送邮件、电子邮件和投票票。会员包括初级、普通和高级高尔夫会员，以及一项不包含高尔夫球的社交会员。问题是，初级和社交会员不允许对俱乐部事务进行投票。此外，社交会员不应该收到有关高尔夫锦赛的邮件，因为他们不允许使用球场，只能使用泳池和餐厅设施。如果你编写这个程序，你会如何组织它？

- 2. 假设你在程序中看到以下代码：
```java
public clsJunior(string addr, int status, decimal minimum)
    : base(addr, status, minimum)
```
