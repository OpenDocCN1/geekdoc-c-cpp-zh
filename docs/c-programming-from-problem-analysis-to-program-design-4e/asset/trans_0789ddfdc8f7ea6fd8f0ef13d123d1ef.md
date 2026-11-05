
```csharp
private void btnTravel_Click(object sender, EventArgs e)
{
    // GetStartLocation(), GetDestination() and
    // DetermineMiles() methods all defined as
    // abstract methods in ITraveler interface
    txtBxFrom.Text =
        aStudent.GetStartLocation();
    txtBxTo.Text =
        aStudent.GetDestination();
    txtBxMiles.Text =
        aStudent.DetermineMiles().ToString();
    txtBxFrom.Visible = true;
    txtBxTo.Visible = true;
    txtBxMiles.Visible = true;
    lblHeading.Visible = true;
    lblMiles.Visible = true;
    lblFrom.Visible = true;
    lblTo.Visible = true;
}
```

GetStartLocation()、GetDestination() 和 DetermineMiles() 是 ITraveler 接口的成员。当 Student 类实现此接口时，这些方法的主体必须编写。请注意，对这些方法的调用与任何其他调用相似。实例化 Student 类对象的类不会区分这些方法、从另一个类继承的方法或最初在 Student 类中定义的方法。

## .NET Framework 接口

接口在 .NET Framework 中发挥着重要作用。诸如 Array 类、ArrayList 类、Hashtable 类、Stack 类和 Queue 类之类的集合类实现了许多接口。.NET 包含这些类以便您管理数据集合。设计类以实现接口为它们提供了通用功能。例如，.NET Array 类是一个抽象类，用作支持数组的语言实现的基础类。如果您查阅 .NET 文档，会发现 Array 类的签名显示它实现了多个接口（ICloneable、IList、ICollection 和 IEnumerable）。

C# 和其他 .NET 语言必须扩展此基础 Array 类，以在其语言中添加单个数组的构造。这包括为接口方法定义实现细节的要求。对于您这样的开发人员，所有这些都在幕后进行。但是，此基础类 Array 提供了操作数组的方法，例如遍历元素、搜索、向数组添加元素、复制、克隆、清除、从数组中删除元素、反转元素和排序。如果仔细检查此功能，您会发现其中很大一部分之所以存在，是因为接口所强制执行的契约。克隆功能作为实现 ICloneable 的一部分被契约化。IList 接口要求为 Add()、Clear()、Remove()、Insert() 以及其他方法提供实现细节。ICollection 接口有一个 CopyTo() 方法。IEnumerable 接口有一个名为 GetEnumerator() 的方法，它返回一个可以遍历集合的枚举器。

部分集合类的签名在示例 11–23 中显示。

### 示例 11.23

```
public abstract class Array : ICloneable, IList, ICollection,
                             IEnumerable
public class ArrayList : IList, ICollection, IEnumerable, ICloneable
public class Queue : ICollection, IEnumerable, ICloneable
public class Stack : ICollection, IEnumerable, ICloneable
public class Hashtable : IDictionary, ICollection, IEnumerable,
    ISerializable, IDeserializationCallback, ICloneable
```

请注意，每个集合类都实现了 ICloneable。Array 类是集合中唯一一个抽象类。Hashtable 类是唯一实现 IDeserializationCallback 接口的类。建议您查阅这些类和接口的文档。通过这样做，您可以看到面向对象开发的真正威力。在查阅文档时，您会注意到它不仅包括必须实现的方法，还提供了类的描述并以多种语言展示示例。

文档提供了指向类的链接，以便您可以深入挖掘并发现更多信息。

> **注意**
> 
> .NET Framework 类库和 Visual Studio 最强大的功能之一是可用的庞大文档库。除了语法之外，它还包括教程和功能使用示例。

Hashtable 类通过将具有指定键值对的元素添加到集合中来实现 Add()。ArrayList 类通过将对象添加到集合末尾来实现 Add()。Add() 的含义是否会根据所使用的对象类型而不同？这就是多态背后的思想——下一节的主题。

## 多态

**多态** 是类能够为同名调用的方法提供不同实现的能力。您已经理解并在日常生活中使用多态，当您根据对象与动词一起使用时的情况来确定动词的真实行为时。例如，动词 "drive" 本身的含义是模糊的。驾驶汽车与钉钉子、驾驶船只或让人发疯是不同的。只有将 "drive" 置于上下文中，您才知道与之相关的行为或活动。

您在程序中也多次体验过多态的使用。一个快速的例子是 ToString() 方法。请记住，此方法被定义为 Object 类的四个方法之一。这意味着在 .NET 中的每个类，无论是用户定义还是框架类，都有一个 ToString() 方法。根据调用 ToString() 方法的对象类型，它执行不同的功能。最终结果是将某个对象转换为其字符串表示形式。将整数转换为字符串与将单个字符转换为字符串是不同的活动。您可以将其视为有多种不同的实现，而实现由调用它的对象类型决定。示例 11-24 显示了在 PresentationGUI 类中包含的对 ToString() 方法的两次调用。

### 示例 11.24

```
// Calls overridden ToString() defined in Person class
// Returns the first name, a space, and the last name
txtBxName.Text = aStudent.ToString();

// Calls ToString() defined in object class
// Returns a number representing age in string format
txtBxAge.Text = aStudent.Age.ToString();
```

正如注释所述，对 ToString() 方法的第一次调用调用了在 Person 类中定义的方法。请记住，该方法重写了对象的 ToString()。此 ToString() 实现（包含在示例 11-9 中）是将名和姓用空格连接起来。CLR 认识到应使用此方法，因为它是用 Student 对象调用的。Student 不包含 ToString() 方法的实现；因此，CLR 接下来查找它派生的类，即 Person 类。

对 ToString() 方法的第二次调用不使用 Person 类的实现。请注意，此调用是用 int 对象进行的。Age 属性返回一个 int。因此，根据发出调用的对象，调用的是 Object 类的 ToString() 方法。

多态允许在不考虑其提供特定实现的情况下调用类的方法。因此，在 .NET 中，多态通过接口、继承和抽象类的使用来实现。

## .NET 中的多态编程

正如您所见，多个类可以实现相同的接口或实现多个接口。接口描述了方法以及每个方法成员需要接收和返回的参数类型，但它将方法体实际细节留给实现接口的类。实现接口的每个类可能具有完全不同的行为。实现接口的所有类中的方法名相同，但功能可能从一个类到另一个类差异很大。

> 注意
> 
> 面向对象开发的黑盒概念在这里发挥作用。您不必知道方法是如何完成其工作的。您只需要知道要发送哪些参数（如果有），以及对象完成工作时您期望实现什么。这可能是一个返回值，也可能只是方法完成的指示。

通过继承，多态得以实现，方法是允许类重写基类成员。这使得动态绑定成为可能。CLR 根据调用方法的对象在运行时确定调用哪个方法。使用 virtual 关键字标记方法使派生类能够为该方法编写自己的功能。

> 注意
> 
> 请记住，类不必重写 virtual 方法。类可以选择使用基类的实现。

由于抽象类不能被实例化，接口和继承的特性在多态编程中都发挥作用。通过使用抽象类，从它们派生的类被迫为任何抽象方法包含实现细节。与仅提供必须实现的方法签名的接口不同，抽象类的一些或全部成员可以被实现。抽象类还可以包含数据成员、属性、事件和方法。方法可以标记为 virtual 或 abstract，也可以完全实现。使用哪个方法的决定基于发出调用的对象。

继承对于在无需为每个新应用程序重新发明轮子的情况下扩展现有类的功能非常有用。在 .NET 中，您必须记住您只有单继承。一个类可以实现多个接口，但必须为所有接口方法提供实现细节。组件编程可能是开发的未来方式。它是一种强大的技术，使您能够轻松实现对象的多个接口。所有这些高级面向对象功能的共同目标是实现多态编程。
