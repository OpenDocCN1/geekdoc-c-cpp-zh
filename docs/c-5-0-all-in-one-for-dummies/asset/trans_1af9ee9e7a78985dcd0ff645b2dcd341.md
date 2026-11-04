
## Book II 第 11 章：使用命名参数和可选参数提高生产力

并且城市，你可以将城市名称默认为你的城市，使该参数变为可选。

```
public static string searchForPhoneNumber(string name, string city = "Columbus")
(...)
```

在 C# 3.0 中，你通过搜索方法的两个重载实现来实现这一点。其中一个包含名称和城市作为参数。第二个仅将名称作为参数。它在方法体中设置城市并调用第一个方法。代码如下所示：

```
public static string searchForPhoneNumber(string name, string city) {...}
public static string searchForPhoneNumber(string name) {
    string city = "Columbus";
    return searchForPhoneNumber(name, city);
}
```

这个的典型例子是 addit 方法。它很愚蠢，但它说明了多个重载的现实。所以，在此之前你有这个：

```
public static int addit(int z, int y)
{
    return z + y;
}
public static int addit(int z, int y, int x)
{
    return z+y+x;
}
public static int addit(int z, int y, int x, int w)
{
    return z + y + x + w;
}
public static int addit(int z, int y, int x, int w, int v)
{
    return z + y + x + w + v;
}
```

使用可选参数，你现在有这个：

```
public static int addit(int z, int y, int x = 0, int w = 0, int v = 0)
{
    return z + y + x + w + v;
}
```

如果你需要加两个数字，你可以轻松完成。

```
int answer = addit(10, 4);
```

如果你需要加四个数字，也不会有任何问题。

```
int answer = addit(10, 4, 5, 12);
```

那么为什么可选参数很危险呢？因为有时默认值会产生意外的后果。例如，你不想创建一个 divideit 方法并将参数默认为 0。有人可能会调用它并得到一个无法调试的除零错误。在方法体内将 additall 中的可选值设置为 1 是不好的。

```
    public static int additall(int z, int y, int x = 0, int w = 0, int v = 1)
    {
        //You CLEARLY don't want this
        return z + y + x + w + v;
    }
```

有时问题可能非常微妙，因此请谨慎使用可选参数。例如，假设你有一个基类，然后有一个派生类实现基类，像这样：

```
    public abstract class Base
    {
        public virtual void SomeFunction(int x = 0)
        {
            [...]
        }
    }

    public sealed class Derived : Base
    {
        public override void SomeFunction(int x = 1)
        {
            [...]
        }
    }
```

**如果声明一个新实例会发生什么？**

```
    Base ex1 = new Base();
    ex1.SomeFunction ();            // SomeFunction (0)

    Base ex2 = new Derived();
    ex2.SomeFunction ();            // SomeFunction (0)

    Derived ex3 = new Derived();
    ex3.SomeFunction ();            // SomeFunction (1)
```

这里发生了什么？根据你如何实现类，可选参数的默认值设置不同。第一个例子 ex1 是 Base 的实现，默认的可选参数为 0。在第二个例子中，ex2 被强制转换为 Derived 类型（这是合法的，因为 Derived 是 Base 的子类），默认值也为 0。然而，在第三个例子中，Derived 被直接实例化，默认值是 1。这不是特别预期的行为，尽管我必须承认我不确定在这种情况下 *什么* 是预期行为。不管怎么说，这都是一个陷阱，需要注意。

### 引用类型

引用类型，正如 Book 1 所讨论的，是存储对实际数据的引用而不是数据本身的变量。引用类型通常被称为对象，尽管这有点不准确，因为 .NET Framework 中的一切都是对象。

新的引用类型通过以下方式实现

- Class
- Interface
- Delegate

这些需要在使用之前构建；class 本身不是引用类型，但 Calendar 类是。

.NET Framework 中有三种内置引用类型：

- String （谁知道为什么这不是静态类型）
- Object
- Dynamic

你可以像传递静态类型一样将引用类型传递给方法。它仍然被视为参数。你在方法内部像使用任何其他变量一样使用它。

但引用类型可以像静态类型一样传递吗？让我们试试。例如，如果你为我们的 Calendar 类有一个 Schedule 方法，你可以传入 CourseId，也可以传入整个 Course。一切都取决于你如何构建应用程序。

```
public class Course
{
    public int CourseId;
    public string Name;
    public Course(int id, string name)
    {
        CourseId = id;
        Name = name;
    }
}
public class Calendar
{
    public static void Schedule(int courseId)
    {
    }
    public static void Schedule(Course course)
    {
        //Something interesting happens here
    }
}
```

在这个例子中，你为 Schedule 有一个重载方法——一个接受 CourseId，一个接受 Course 引用类型。第二个是引用类型，因为 Course 是一个类，而不是像 CourseId 的 Integer 那样的静态类型。

如果想让第二个 Schedule 方法支持可选的 Course 参数怎么办？比如，如果你只是想在省略参数时默认创建一个新的 Course。这就类似于将静态整数设置为“0”或类似的东西，对吧？

```
public static void Schedule(Course course = new Course())
{
    //Implementation here
}
```

然而这是不允许的。Visual Studio 只允许在静态类型上使用可选参数，编译器会告诉你这一点。如果你想这样做，你必须在 Schedule 方法中接受 CourseId，并在方法体中构造一个新的 Course。

### 输出参数

正如 Book I 所讨论的，输出参数是方法签名中的参数，它们实际上会更改用户传入给它们的变量的值。参数引用原始变量的位置，而不是创建“工作副本”。

输出参数在方法签名中用 out 关键字声明。你可以有任意多个（好吧，在合理范围内），尽管如果你使用超过几个，你可能应该使用其他东西（也许是一个通用列表？）。

一个输出参数在方法声明中可能看起来像这样：

```
public static void Schedule(int courseId, out string name, out DateTime scheduledTime)
{
    name = "something";
    scheduledTime = DateTime.Now;
}
```

按照规则，你应该能够通过预设值使这些参数中的一个变为可选。但，唉，它不起作用，如图 11-1 所示。

与引用参数不同，输出参数不支持默认值是有意义的。输出参数就是输出，设置值应该在方法体内发生。

请记住可选参数的目的——解决对大量重载方法的需求。因为输出参数根本不期望传入值，所以为其提供默认值对程序员没有好处。

![](img/80ff26f06fc9ab951e1cd4257b867366_425_0.png)

图 11-1：Visual Studio 对默认可选参数值的错误。

### 查看命名参数

与可选参数的概念相伴的是命名参数。如果你有多个默认参数，你需要一种方法告诉编译器你提供的是哪个参数！

例如，查看本章前面 additall 方法，在实现可选参数之后：

```
public static int additall(int z, int y, int x = 0, int w = 0, int v = 0)
{
    return z + y + x + w + v;
}
```

显然，在此实现中参数的顺序无关紧要，但如果这在类库中，你可能不知道参数顺序不是问题！你如何告诉编译器跳过 x 和 w 如果你想提供 v？在过去，你会这样做：

```
int answer = additall(3,7, , ,4);
```

幸运的是，你现在不必再这样做了。现在，有了命名参数，你可以说

```
int answer = additall(z:3, y:7, v:4);
```

非可选参数不必命名，因为位置是假设的，因为它们无论如何都是必需的。尽管如此，将它们命名是良好的实践。如果你跳过命名，你会有这个：

```
int answer = additall(3, 7, v:4);
```

你必须承认这有点更难阅读。人们必须回到方法签名才能弄清楚发生了什么。
