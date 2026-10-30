

查询数据通常需要快速完成，并且可以只提供较少的事务一致性保证：为了提高响应速度，允许出现幻读或不可重复读可能是可以接受的权衡。不过，命令处理通常要求具备事务一致性，因此需要使用不同的层来处理命令和查询。有时，命令和查询的数据访问层也可能不同。命令可能需要完全符合 ACID（ACID 代表原子性、一致性、隔离性和持久性）的数据库，而查询则可能只需简单的文档存储即可。文档存储会通过命令层发布的事件进行异步更新，从而使查询读取具有最终一致性。

## 结论

本章说明了依赖关系的组织在创建软件应用程序时所构成的重大挑战。项目的长期健康状况、适应性，以及项目是否能够存续，都依赖于对依赖关系进行合理管理。如果开发人员不加审慎地创建相互引用的类，就会形成类似意大利面的混乱交叉依赖，这会严重影响团队以一致且可预测的方式交付业务价值的能力。

依赖关系必须在所有层面上进行管理：从彼此交互的单个类和方法，到程序集引用，再到组件的高层架构。开发人员必须始终保持警惕，确保无关的依赖关系不会泄漏到其方法、类、程序集或层之外。

从某种意义上说，本章为本书其余部分的大量内容奠定了基础。本书内容为可维护、可适应的代码提供了坚实基础，并在每一章中不断得到强化。如果你的程序集包含意大利面式的引用关系，并且你的层没有隐藏其基础设施依赖，那么无论你尝试遵循其他什么模式或实践，代码都会变得更难测试、修改和理解。

## 接口和设计模式

完成本章后，你将能够：

- 定义接口，并识别接口与类之间的差异。
- 使用接口应用设计模式，例如适配器模式和策略模式。
- 通过鸭子类型、混入和流式接口理解接口的多功能性。
- 识别接口的局限性，并实现相应的变通方案。
- 发现接口常见的反模式和滥用方式。

接口是 Microsoft .NET Framework 开发中的一种强大构造。虽然 `interface` 关键字非常简单，但它所代表的是一种非常强大的范式。正确使用接口时，它们会为代码提供扩展点，使代码具备适应性。然而，接口也存在一些不太理想的用法，而且这些用法仍然被广泛采用。

本章将重申类与接口之间的差异，并说明如何最好地结合使用二者：既保护客户端代码，使其免受实现变更的影响，又促进多态性。

本章还将介绍接口的多功能性，以及接口如何成为现代软件解决方案中无处不在的工具。本章将演示一些强大的设计模式；如果正确应用这些模式（并结合本书中的其他模式），就能生成非常灵活、能够适应敏捷项目不断变化需求的代码。

然而，接口本身并不是万能药。适当使用接口确实可以帮助项目，但必须以正确的方式应用接口。本章还将探讨接口的一些常见滥用方式。

### 什么是接口？

接口定义了类所具有的行为，但不定义这些行为的实现方式。接口作为一种独立于类的构造存在，但它要求类提供用于实现该接口的工作代码。

接口由其语法定义，也就是接口的语言构造部分：`interface` 关键字以及该关键字所隐含和包含的一切内容。但接口也由其特性定义，即它们所代表并启用的概念。

### 语法

接口使用 `interface` 关键字定义。与类一样，接口可以包含属性、方法和事件。但是，接口中的任何元素都不能指定访问修饰符：实现类必须以 `public` 方式实现接口。代码清单 4-1 展示了接口的声明以及一种可能的实现方式。

代码清单 4-1 声明并实现接口。

```
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

    event EventHandler<EventArgs> InterfacesCanContainEventsToo;
}
// ...
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
    }

    public event EventHandler<EventArgs> InterfacesCanContainEventsToo = delegate ( );

    private int encapsulatedInteger;
}
```

.NET Framework 不支持类的多重继承概念，但支持一个类实现多个接口。

一个类能够实现的接口数量没有限制；一个类上真正合理的接口数量更多是一个实践层面的问题。代码清单 4-2 扩展了前面的示例，使实现类实现第二个接口。

# 代码清单 4-2 一个类可以实现多个接口。

```
public interface IInterfaceOne
{
    void MethodOne();
}
// . . .
public interface IInterfaceTwo
{
    void MethodTwo();
}
// . . .
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

一个类可以实现多个接口，而一个接口也可以由不同的类实现。

### 多重继承

某些语言支持从多个基类继承的概念。尤其是 C++，允许这种构造。不过，.NET Framework 语言不允许这样做；如果一个类试图继承两个或更多类，编译器就会生成警告，如图 4-1 所示。

> 2 类“ TheInterface.AttemptedMultipleInheritance”不能拥有多个基类：“TheInterface.BaseClassOne”和“BaseClassTwo”

图 4-1 编译器阻止多重继承。

### 菱形继承问题

不允许多重继承的原因之一是菱形继承问题。当同一个类继承两个或更多类时，就会出现这一问题。如果这些基类中都包含相同的方法，那么应该使用哪一个方法？图 4-2 展示了这一问题的统一建模语言（UML）图示。

![](img/f852e0a12c174e64d91a8e1a05146eab_144_0.png)

图 4-2 展示菱形继承问题的 UML 图。

在这种情况下，类 `AttemptedMultipleInheritance` 应该继承哪个版本的 `RootMethod()`：是 `BaseClassOne` 从 `RootClass` 继承的版本，还是 `BaseClassTwo` 从 `RootClass` 继承的版本？由于存在这种歧义，.NET Framework 不允许类的多重继承。

### 显式实现

接口也可以以*显式*方式实现。显式接口实现不同于前面示例中展示的隐式接口实现。代码清单 4-3 展示了之前的同一个示例类，但这一次它以显式方式实现接口。

**代码清单 4-3** 显式实现接口。

```
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

要使用显式实现的接口，客户端必须持有一个指向接口实例的引用；仅持有指向接口实现的引用是不够的。代码清单 4-4 将对此进行更详细的探讨。

