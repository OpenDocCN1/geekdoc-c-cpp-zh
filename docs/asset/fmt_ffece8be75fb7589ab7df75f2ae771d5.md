
本章提醒你类和接口之间的区别，并描述如何最好地将两者结合使用，以保护客户端代码免受实现更改的影响，并促进多态性。

它还涵盖了接口的多功能性，以及它们如何成为现代软件解决方案中无处不在的工具。这包括一些强大的设计模式，当正确应用（并结合本书中的其他模式）时，这些模式会产生极其灵活的代码，并能够适应敏捷项目所拥抱的不断变化的需求。

然而，接口本身并不是万灵药。明智地使用接口当然可以为项目带来帮助，但接口必须以正确的方式应用。本章探讨了一些常见的接口滥用。

## 什么是接口？

接口定义类具有的行为，但不定义这些行为如何实现。

接口是独立于类的构造，但它们需要类提供工作代码来实现接口。

接口由其语法定义——即接口的语言构造方面：`interface`关键字及其所暗示和包含的一切。但它们也由其特性定义：它们所代表和支持的概念。

### 语法

接口是使用`interface`关键字定义的。它们可以像类一样包含属性、方法和事件。但是，接口的任何元素都不能指定访问修饰符：实现类必须将接口实现为`public`。清单3-1展示了一个接口的声明以及可能的实现。

#### 清单3-1 声明并实现一个接口

单击此处查看代码图像

```csharp
public interface ISimpleInterface
{
    void ThisMethodRequiresImplementation();

    string ThisStringPropertyNeedsImplementingToo
    {
        get;
        set;
    }

    int ThisIntegerPropertyOnlyNeedsAGetter
    {
        get;
    }

    public event EventHandler<EventArgs> InterfacesCanContainEventsToo;
}
//...
public class SimpleInterfaceImplementation : ISimpleInterface
{

    public void ThisMethodRequiresImplementation()
    {

    }

    public string ThisStringPropertyNeedsImplementingToo
    {
        get;
        set;
    }

    public int ThisIntegerPropertyOnlyNeedsAGetter
    {
        get
        {
            return this.encapsulatedInteger;
        }
        set
        {
            this.encapsulatedInteger = value;
        }
    }

    event EventHandler<EventArgs> InterfacesCanContainEventsToo = delegate {};
```

```csharp
private int encapsulatedInteger;
}
```

`.NET Framework`不支持类的多继承概念，但它支持单个类实现多个接口。

对于类可以实现接口的数量没有限制；一个类上真正有意义的接口数量更多是一个实际问题。清单3-2扩展了前面的示例，在实现类上实现了第二个接口。

#### 清单3-2 单个类可以实现多个接口

单击此处查看代码图像

```csharp
public interface IInterfaceOne
{
    void MethodOne();
}
//...
public interface IInterfaceTwo
{
    void MethodTwo();
}
//...
public class ImplementingMultipleInterfaces : IInterfaceOne, IInterfaceTwo
{
    public void MethodOne()
    {
    }

    public void MethodTwo()
    {
    }
}
```

虽然单个类可以实现多个接口，但一个接口也可以由不同的类多次实现。

### 多继承

有些语言支持从多个基类继承的概念。特别是`C++`允许这种构造。然而，`.NET Framework`语言不允许这样做，如果类试图继承两个或更多类，编译器将生成警告，如图3-1所示。

![](img/65c1bad7a6b3cffae8cbb79664f0708b_115_0.png)

**图3-1** 编译器阻止多继承。

### 菱形继承问题

不允许多继承的一个原因是菱形继承问题。当一个类继承两个或更多类时，就会出现这个问题。如果这些基类中的每一个都包含相同的方法，应该使用哪一个？图3-2显示了该问题的统一建模语言（UML）图。

![](img/65c1bad7a6b3cffae8cbb79664f0708b_115_1.png)

**图3-2** 显示菱形继承问题的UML图。

在这种情况下，类`AttemptedMultipleInheritance`应该继承哪个版本的`RootMethod()`——是`BaseClassOne`从`RootClass`继承的那个，还是`BaseClassTwo`从`RootClass`继承的那个？由于这种歧义，`.NET Framework`不允许类的多继承。

### 显式实现

接口也可以被*显式*实现。显式接口实现不同于隐式接口实现，前面的示例展示的是隐式接口实现。清单3-3显示了之前相同的示例类，但这次它显式实现了其接口。

#### 清单3-3 显式实现接口

单击此处查看代码图像

```csharp
public class ExplicitInterfaceImplementation : ISimpleInterface
{
    public ExplicitInterfaceImplementation()
    {
        this.encapsulatedInteger = 4;
    }

    void ISimpleInterface.ThisMethodRequiresImplementation()
    {
        encapsulatedEvent(this, EventArgs.Empty);
    }

    string ISimpleInterface.ThisStringPropertyNeedsImplementingToo
    {
        get;
        set;
    }

    int ISimpleInterface.ThisIntegerPropertyOnlyNeedsAGetter
    {
        get
        {
            return encapsulatedInteger;
        }
    }

    event EventHandler<EventArgs> ISimpleInterface.InterfacesCanContainEventsToo
    {
        add { encapsulatedEvent += value; }
        remove { encapsulatedEvent -= value; }
    }

    private int encapsulatedInteger;
    private event EventHandler<EventArgs> encapsulatedEvent;
}
```

要使用显式实现的接口，客户端必须拥有对接口实例的引用——对接口实现的引用是不够的。清单 3-4 进一步详细探讨了这一点。

#### LISTING 3-4 当显式实现时，接口方法在类实例上不可见。

Click here to view code image

```
public class ExplicitInterfaceClient
{
    public ExplicitInterfaceClient(ExplicitInterfaceImplementation implementationReference, ISimpleInterface interfaceReference)
    {
        // Uncommenting this will cause compilation errors.
        //var instancePropertyValue =
        //implementationReference.ThisIntegerPropertyOnlyNeedsAGetter;
        //implementationReference.ThisMethodRequiresImplementation();
        //implementationReference.ThisStringPropertyNeedsImplementingToo = "Hello";
        //implementationReference.InterfacesCanContainEventsToo += EventHandler;

        var interfacePropertyValue =
            interfaceReference.ThisIntegerPropertyOnlyNeedsAGetter;
        interfaceReference.ThisMethodRequiresImplementation();
        interfaceReference.ThisStringPropertyNeedsImplementingToo = "Hello";
        interfaceReference.InterfacesCanContainEventsToo += EventHandler;
    }

    void EventHandler(object sender, EventArgs e)
    {
    }
}
```

显式实现只有在你想要避免签名冲突时才真正有用，当类已经拥有必须由接口实现的 方法签名时。

可在 `.NET Framework` 中定义 的每个方法都有特定的方法签名。此签名有助于将方法区分 为唯一，并区分已被重写的方法。方法 的签名由其名称和参数列表组成。请注意，方法的访问级别、返回值、抽象或密封状态都会影响方法签名。清单 3-5 显示了各种方法签名，其中一些会冲突。如果方法在上述所有标准上都相等，则方法签名会冲突。没有类、接口或结构可以包含具有冲突签名的方法。

#### LISTING 3-5 其中一些方法具有相同的签名。

Click here to view code image

```
public class ClashingMethodSignatures
{
    public void MethodA()
    {
    }

    // This would cause a clash with the method above:
    //public void MethodA()
    //{
    //}

    // As would this: return values are not considered
    //public int MethodA()
    //{
    //    return 0;
    //}

    public int MethodB(int x)
    {
        return x;
    }

    // There is no clash here: the parameters differ.
    // This is an overload of the previous MethodB.
    public int MethodB(int x, int y)
    {
        return x + y;
    }
}
```

属性由于没有参数列表，仅通过其名称区分。因此，如果两个属性具有相同的名称，则其签名会冲突。

想象一下清单 3-6 中所示的类，该类需要实现上述接口 `InterfaceOne`。

#### LISTING 3-6 此类需要实现的接口将导致方法签名冲突。

Click here to view code image

```
public class ClassWithMethodSignatureClash
{
    public void MethodOne()
```

#### LISTING 3-9 显式实现接口以避免冲突的方法签名。

Click here to view code image

```
public class ClassAvoidingMethodSignatureClash : IInterfaceOne
{
    public void MethodOne()
    {
        // original implementation
    }

    void IInterfaceOne.MethodOne()
    {
        // new implementation
    }
}
```

类似地，如果一个类需要实现两个不同的、相互无关的接口，但这两个接口都包含具有相同签名的方法，你可以隐式实现它们并共享同一个方法实现。或者，如清单 3-10 所示，你可以显式实现它们——为了清晰——以区分哪个实现属于哪个接口。

#### LISTING 3-10 在实现具有通用方法签名的两个接口时，只有显式实现才足够。

Click here to view code image

```
public class ClassImplementingClashingInterfaces : IInterfaceOne, IAnotherInterfaceOne
{
    void IInterfaceOne.MethodOne()
    {

    }

    void IAnotherInterfaceOne.MethodOne()
    {
    }
}
```

### Polymorphism

能够使用一种类型 的对象并使其隐式表现为另一种类型 的能力称为 *polymorphism*。客户端代码可以与对象交互，就好像它是 一种类型一样，而实际上是另一种类型。这种程序性的障眼法是面向对象编程最重要的原则之一，并且支撑了一些最优雅、适应性最强的编程问题解决方案。

图 3-3 显示了表示车辆行为的接口，以及汽车、摩托车和快艇的可能实现类。请注意，这三种车辆类型各不相同，但由于其统一的接口，它们都表现出相同的行为。

![](img/65c1bad7a6b3cffae8cbb79664f0708b_121_0.png)

FIGURE 3-3 接口将行为传递给实现类，从而实现多态。

在此示例中，车辆被假定具有可启动和停止的发动机、某种转向装置以及加速能力。多态允许客户端代码持有对 `IVehicle` 接口的引用，并将所有具体类型视为相同。汽车的转向或加速方式与摩托车有何不同，或快艇发动机启动和停止方式与火车有何不同，对客户端来说并不重要。而这是一件非常好的事情。实际上，每当我们使用车辆时，我们都是该接口的客户端。当然，车辆的真实接口比这里所示的更为细致，但原则是相同的。你需要知道汽车发动机的内部工作原理才能启动和停止发动机吗？完全不需要。那些都是实现细节，对你驾驶知识的影响为零。这就是良好的接口设计。

本章其余部分构成的设计模式和接口功能都促进了自适应代码的创建。多态使其中每一个都对任何满足预期接口的类有用，无论该类是已经编写还是尚未构思。

### Adaptive design patterns

设计模式由 Gang of Four¹ 书籍 *Design Patterns*（Addison-Wesley Professional, 1994）普及。尽管这本书几乎有 20 年的历史了（在软件开发术语中至少相当于四个冰河时代），但它至今仍然极其相关。其中一些模式已被重新归类为反模式，但其他模式被不断使用并增强了代码的适应性。

> ¹ 因其四位作者而得名：Erich Gamma、Richard Helm、Ralph Johnson 和 John Vlissides。

良好的设计模式是接口和类之间可重用的协作，可以在许多不同的场景、跨项目、平台、语言和框架中反复应用。与大多数值得注意的最佳实践一样，设计模式是最好知道而不是不知道的理论工具。它们可能被过度使用，并且并不总是适用，有时用大量类、接口、间接和抽象使原本简单的解决方案变得复杂。

在我看来，设计模式往往要么被低估要么被高估。在某些项目中，设计模式不足，代码缺乏可辨识的结构。其他项目则过于自由地应用设计模式，在收益可忽略不计的地方添加了间接和抽象。平衡在于找到正确的地方应用正确的模式。

### The Null Object pattern

空对象模式是最常见的设计模式之一——也是最容易理解和实现的一种。其目的是让你避免意外抛出 `Null-ReferenceException` 以及大量空对象检查代码。图 3-4 中的 UML 类图显示了空对象模式的应用方式。

![](img/65c1bad7a6b3cffae8cbb79664f0708b_122_0.png)

**FIGURE 3-4** 空对象模式作为 UML 类图的演示。

[Listing 3-11](#) 显示了一些可能抛出 `NullReferenceException` 的典型代码。

**LISTING 3-11** 如果你不检查返回值是否为 null，就有抛出 NullReference-Exception 的风险。

[Click here to view code image](#)

```
class Program
```
