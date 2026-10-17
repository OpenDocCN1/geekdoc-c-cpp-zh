
你可以看到，编译器要求重写 `Object.Equals` 和 `Object.GetHashCode` 方法。
`.NET Framework` 类 `System.Object` 定义了以下方法：

- `Equals(object)` 方法——确定调用对象是否与参数所引的对象是同一个对象。如果对象相同则返回 true，否则返回 false。你可以在类中重写此方法，以比较两个对象内容的相等性。`Equals(object, object)` 方法会调用 `Equals(object)` 来计算其结果。
- `GetHashCode()` 方法——返回一个与调用对象相关的哈希值。该哈希值可以用于任何采用哈希作为访问存储对象手段的算法。

如果你重载了 `--` 运算符，你需要重写 `Equals(object)` 和 `GetHashCode()`，因为 `--` 运算符和 `Equals(object)` 方法的功能相同。当重写 `Equals()` 时，为了兼容性，你还需要重写 `GetHashCode()`。

在 `OverloadEqual0pr.cs` 中添加 `Equals` 和 `GetHashCode` 方法后（如列表 10.8 所示），程序如列表 10.9 所示。只有粗体代码是新添加的，其余部分与列表 10.8 相同。

### 列表 10.9 OverloadEqual0pr.cs 文件中的程序代码

```cs

using System;

class Product {

    int qty;

    public Product() {

        qty=0;

    }

    public Product(int x) {

        qty=x;

    }

    public static bool operator == (Product op1, Product op2) {

        if(op1.qty == op2.qty) return true;

        else return false;

    }

```

## 第 10 章运算符重载

```cs

public static bool operator != (Product op1, Product op2)

{

    return !(op1==op2);

}

public override bool Equals(Object obj) {

    if (obj == null || GetType() != obj.GetType()) return false;

    Product p = (Product)obj;

    return qty.Equals(p.qty);

}

public override int GetHashCode() {

    return qty.GetHashCode();

}

public int getQuantity() {

    return qty;

}

class OverloadEqualExpr {

    static void Main() {

        Product p1 = new Product(10);

        Product p2 = new Product(50);

        if(p1==p2)

            Console.Write("Product p1 is equal to p2 i.e. (0) is equal to (1)",

            p1.getQuantity(), p2.getQuantity());

        else

            Console.Write("Product p1 is not equal to p2 i.e. (0) is not equal to (1)",

            p1.getQuantity(), p2.getQuantity());

    }

}

```

输出：

Product p1 is not equal to p2 i.e. 10 is not equal to 50

你可以看到 Product 对象 `p1` 的 `qty` 成员值设置为 10，而 Product 对象 `p2` 的值设置为 50。当你遇到 `p1==p2` 时，重载的 `==` 运算符被调用，对象 `p1` 和 `p2` 作为参数传递给它。在方法内部，比较传递对象的 `qty` 成员值。由于值 10 和 50（赋值给 `qty` 成员的值）不相等，方法返回布尔值 `false`。随后，屏幕上显示消息 `Product p1 is not equal to p2 i.e. 10 is not equal to 50`。

## 转换运算符重载

强制转换意味着将一种类型的值转换为另一种数据类型，以便用于计算或进一步处理。强制转换提供的数据类型转换可以是隐式的，也可以是显式的。

强制转换意味着将一种类型的值转换为另一种数据类型，以便用于计算或进一步处理。强制转换提供的数据类型转换可以是隐式的，也可以是显式的。

隐式转换意味着将一种类型的值转换为另一种数据类型，以便用于计算或进一步处理。强制转换提供的数据类型转换可以是隐式的，也可以是显式的。

显式转换意味着将一种类型的值转换为另一种数据类型，以便用于计算或进一步处理。强制转换提供的数据类型转换可以是隐式的，也可以是显式的。

隐式转换意味着将一种类型的值转换为另一种数据类型，以便用于计算或进一步处理。强制转换提供的数据类型转换可以是隐式的，也可以是显式的。

显式转换意味着将一种类型的值转换为另一种数据类型，以便用于计算或进一步处理。强制转换提供的数据类型转换可以是隐式的，也可以是显式的。

## 第 10 章 运算符重载

```csharp

public static implicit operator int(Inches inchObject)

{

    return inchObject.inch/12;

}

public override string ToString()

{

    return (this.inch.ToString());

}

class ConversionOverload

{

    public static void Main()

    {

        Inches inc=new Inches(24);

        int feet1=inc;

        Console.WriteLine("Inches in feet becomes ({0})", feet1);

        int feet2=5;

        Inches inchObj = (Inches) feet2;

        Console.WriteLine("*({0}) feet becomes ({1}) in inches", feet2, inchObj.ToString());

    }

}

```

输出：
In feet becomes 2
5 feet becomes 60 in inches

你可以看到创建了一个名为 `inc` 的 `Inches` 对象。值 24 被赋值给 `Inches` 对象 `inc` 的 `inch` 成员。`inc` 对象被赋值给 `int` 类型的变量 `feet1`，这导致了**隐式转换运算符方法**的调用。该隐式转换运算符方法将 `inch` 成员中的值除以 12 并返回结果。
定义了一个名为 `feet2` 的 `int`，并初始化值为 5。通过调用**显式转换运算符方法**，将该 `int` 值显式转换为 `Inches` 对象。在显式转换运算符方法中，创建了一个名为 `inchObj` 的 `Inches` 对象。提供的 `feet` 参数乘以 12 并赋值给 `inch` 对象的 `inch` 成员。`inchObj` 对象返回到 `Main` 方法，在方法中显示了 `feet` 和 `inches` 值。

这里是关于显式和隐式转换的另一个快速示例。列表 10.11 中的 `ConversionOvr.cs` 程序解释了隐式和显式转换。该程序定义了一个名为 `BookInfo` 的类，它包含两个数据成员 `qty` 和 `rate`，其中 `qty` 是 `int` 类型，`rate` 是 `double` 类型。`qty` 和 `rate` 分别代表书籍的数量和价格。当 `BookInfo` 对象被赋值给 `float` 变量时，会隐式地将对象内容转换为 `float`。换句话说，程序通过将对象的 `qty` 和 `rate` 成员相乘返回书籍的总金额。`BookInfo` 对象通过简单地乘以 `qty` 和 `rate` 成员并返回结果，将隐式转换为 `float`。

同样，一个 `float` 值可以被显式转换为 `BookInfo` 对象。该 `float` 值被赋值给 `BookInfo` 对象的 `rate` 成员，`qty` 成员被设置为默认值 10。假设新 `BookInfo` 对象的 `qty`（数量）为 10，该 `float` 值可以显式转换为 `BookInfo` 对象（赋值给 `BookInfo` 对象的 `rate` 成员）。

+ 10.11 ConversionOv.cs 文件中的代码

```csharp

using System;

class BookInfo

{

    int qty;

    float rate;

    public BookInfo()

    {

    }

    public BookInfo(int q, float r)

    {

        this.qty = q;

        this.rate = r;

    }

    public static implicit operator float(BookInfo bk)

    {

        return bk.qty * bk.rate;

    }

    public static implicit operator BookInfo(float value)

    {

        BookInfo bkinfo = new BookInfo();

        bkinfo.qty = 10; //假设默认数量

        bkinfo.rate = value;

        return bkinfo;

    }

    public override string ToString()

    {

        return string.Format("Quantity={0} and Rate={1}", this.qty, this.rate);

    }

}

class ConversionOv

{

    public static void Main(string[] args)

    {

        BookInfo book = new BookInfo(10, 12.99f);

        float amt = book;

        Console.WriteLine("Total amount of the books is {0}", amt);

        float price = 15.25f;

        BookInfo bkinfo = (BookInfo)price;

        Console.WriteLine(bkinfo.ToString());

    }

}

```

输出：
Total amount of the books is 129.9
Quantity=10 and Rate=15.25

你可以看到创建了一个名为 `book` 的 `BookInfo` 对象。值 10 和 12.99 被赋值给 `BookInfo` 对象的 `qty` 和 `rate` 成员。`book` 对象被赋值给 `float` 变量 `amt`，导致了隐式转换运算符方法的调用。该隐式转换运算符方法将 `qty` 和 `rate` 成员的值相乘，并返回书籍的总金额。

定义了一个名为 `price` 的 `float`，并初始化值为 15.25。通过调用显式转换运算符方法，该 `float` 被显式转换为 `BookInfo` 对象。在显式转换运算符方法中，创建了一个名为 `bkinfo` 的 `BookInfo` 对象。该 `float` 值被赋值给对象的 `rate` 成员。对象的 `qty` 成员被设置为默认值 10。在对 `qty` 和 `rate` 成员赋值后，`bkinfo` 对象被返回到 `Main` 方法，在方法中显示了数量和速率值。

## 总结

在本章中，你看到了运算符重载允许你如何在自定义类型（结构体和类）中使用运算符。你学习了在添加对象时实现二元运算符重载、添加常量以及数字。你发现了实现一元运算符重载、相等性比较运算符。最后，你学习了实现转换运算符重载、创建隐式转换运算符以及显式转换运算符。

下一章将关注委托和事件。你将学习委托、委托实例化委托调用。你还将学习多路委托。最后，你将学习处理事件。

# 第 11 章 委托与事件

本章主题包括：

- 委托引言
- 多路委托
- 协变与逆变
- 泛型委托类型
- 匿名方法
- 委托与接口的区别
- 事件处理

## 委托引言

委托是一个 `.NET` 类，它封装了一个方法并存储方法的地址或引用。它定义了委托实例可以调用的类型。它定义了方法的签名（方法的返回类型、参数数量及其类型）。使用委托的第一步是声明它们。

## 声明委托

确定可以被委托引用的方法。在类或命名空间中使用 `delegate` 关键字并指定要调用方法的签名来声明委托。声明委托的语法如下：`delegate <返回类型> <委托名称> <参数列表>`以下语句声明了一个名为 `Calculate` 的委托，它引用返回 `int` 类型并接受两个类型参数的方法：

```csharp

delegate int Calculate(int x, int y);

```

可以使用访问修饰符 `public`、`private` 和 `protected` 控制委托的可见性。声明委托后，你可以实例化它来封装方法。然后你可以像通过普通实例调用一样通过委托调用该方法。

## 调用引用的方法

假设你的委托实例 `r` 所指向的 `Rect` 方法如下：

```c

static int Rect (int x, int y)

{

  return x * y;

}

```

你可以看到 `Rect` 方法与委托的方法签名相匹配。它接受两个 `int` 类型的参数。接下来的语句通过委托实例 `r` 调用了 `Rect` 方法：

`r(5,8);`

前面的语句实际上与 `r.Rect(5,8);` 相同。

你可以看到，委托实例就像普通方法一样被调用。以下是委托的特性：

-   委托允许你引用一个方法，并让你能够在运行时实现任何所需的功能。
-   每个委托类型都描述了它所封装的方法的参数数量、类型以及返回值的类型。
-   一旦声明了委托类型，就必须创建一个委托对象并与特定的方法关联。
-   定义委托就像定义一个新类。委托被实现为派自 `System.MulticastDelegate` 的类，而该类又派自基类 `System.Delegate`。
-   只要签名与委托匹配，委托就可以调用任何方法。这使得委托成为匿名调用的理想选择。
-   委托是面向对象、类型安全且安全的。在定义委托时，你需要指定它将指向的方法的完整签名。
-   对于静态方法，委托对象封装了要调用的方法。
-   委托对象同时封装了一个实例和该实例上的一个方法。
-   委托变量在运行时被分配一个方法。这对于编写插件方法非常有用。

列表 11.1 所示的 `Delegate.cs` 程序演示了委托类型的使用。该程序声明了一个名为 `Calculate` 的委托，它可以引用任何返回 `int` 类型并接受两个 `int` 类型参数的方法。该程序展示了如何创建委托实例、引用所需的方法并调用增强的方法。

## 列表 11.1 Delegate1.cs 中的程序代码

```csharp

using System;

delegate delegate Calculate(int x, int y);

class Delegate1

{

    static int Rect(int x, int y)

    {

        return x * y;

    }

    static void Main()

    {

        Calculate r = Rect; //等同于 Calculate r = new Calculate(Rect);

        Console.WriteLine("Area of rectangle is " + r(5,8));

    }

}

```

## 输出：

Area of rectangle is 400

你可以看到声明了一个 `Calculate` 委托，它接受两个整数参数并返回 `int` 类型的数据。定义了一个 `Rect` 方法，它接受两个 `int` 类型的参数并返回 `int` 类型。在 `Main()` 方法中，创建了一个名为 `r` 的 `Calculate` 委托实例。委托实例 `r` 调用了 `Rect` 方法，并传递了两个参数 5 和 8。`Rect` 方法的结果显示在屏幕上。

如之前提到的，只要签名与委托匹配，委托就可以指向或引用任何方法。列表 11.2 所示的 `Delegate.cs` 程序解释了委托如何指向两个方法。该程序声明了一个名为 `FunDelegate` 的委托，它可以引用任何返回 `int` 类型的方法。定义了两个静态方法 `AddNum` 和 `MultNum`，它们分别返回所提供参数的和和乘积。这两个方法与委托的签名相同（都接受两个 `int` 类型的参数并返回 `int`）。

## 列表 11.2 Delegate2.cs 中的程序代码

```csharp

using System;

delegate int FuncDelegate(int m, int n);

class Delegate2

{

    public static int AddNum(int p, int q)

    {

        return p+q;

    }

    public static int MultNum(int p, int q)

    {
