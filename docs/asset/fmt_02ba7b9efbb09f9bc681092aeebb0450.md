
实现 `mixin` 的另一种方法是使用 Re-motion Re-mix 等第三方库。Re-mix 允许你通过运行时配置指定在创建某个目标类的新实例时要组合哪些类。与 Impromptu Interface 一样，它即时生成一个新类型，该类型满足 mixin 请求上的所有接口，并且该类型的每个实例在调用接口方法时都会委托给 mixin 的实例。接口和一些示例实现显示在清单 3-29 中。

### LISTING 3-29 The disparate interfaces to be combined as a mixin.

Click here to view code image

```
public interface ITargetInterface
{
    void DoSomething();
}
//...
public class TargetImplementation : ITargetInterface
{
    public void DoSomething()
    {
        Console.WriteLine("ITargetInterface.DoSomething()");
    }
}
//...
public interface IMixinInterfaceA
{
    void MethodA();
}
//...
public class MixinImplementationA : IMixinInterfaceA
{
    public void MethodA()
    {
        Console.WriteLine("IMixinInterfaceA.MethodA()");
    }
}
//...
public interface IMixinInterfaceB
{
    void MethodB(int parameter);
}
//...
public class MixinImplementationB : IMixinInterfaceB
{
    public void MethodB(int parameter)
    {
        Console.WriteLine("IMixinInterfaceB.MethodB({0})", parameter);
    }
}
//...
public interface IMixinInterfaceC
{
void MethodC(string parameter);
}
// ...
public class MixinImplementationC : IMixinInterfaceC
{
    public void MethodC(string parameter)
    {
        Console.WriteLine("IMixinInterfaceC.MethodC(\"{0}\")", parameter);
    }
}
```

请注意，没有任何一个类实现了所有这些接口。相反，下一步是配置 Re-mix，以便当它被要求提供 `TargetImplementation` 的实例时，它将返回一个包含所有接口和类组合的 mixin。Listing 3-30 显示了这样的配置。

### LISTING 3-30 Instructing Re-mix how to construct TargetImplementation instances.

Click here to view code image

```
var config = MixinConfiguration.BuildFromActive()
    .ForClass<TargetImplementation>()
    .AddMixin<MixinImplementationA>()
    .AddMixin<MixinImplementationB>()
    .AddMixin<MixinImplementationC>()
    .BuildConfiguration();

MixinConfiguration.SetActiveConfiguration(config);
```

不幸的是，你不能简单地在 `TargetImplementation` 上调用 `new` 并期望得到一个 mixin。相反，你必须要求 Re-mix 创建一个 `TargetImplementation` 实例，以便它可以按你的规范构建一个新类型并实例化它。Listing 3-31 显示了它是如何做到这一点的——幸运的是，这很简单。

### LISTING 3-31 Re-mix is in charge of creating mixins.

Click here to view code image

```
ITargetInterface target = ObjectFactory.Create<TargetImplementation>(ParamList.Empty)
```

Re-mix 的一个限制是，你不能——也不可能——知道 `ObjectFactory.Create` 返回的实例的确切类型。你所知道的是它是一个 `TargetImplementation` 的子类实例。这对客户端来说有点坏消息，因为在编译时你唯一能保证 `TargetImplementation` 满足的接口就是 `ITargetInterface`。因此，mixin 的客户端必须通过使用 `is` 和 `as` 进行类型嗅探来将 mixin 强制转换为期望的接口。Listing 3-32 突出了这个问题。

### LISTING 3-32 Type-sniffing is bad practice but necessary for using mixins.

Click here to view code image

```
public class MixinClient
{
    public MixinClient(ITargetInterface target)
    {
        this.target = target;
    }

    public void Run()
    {
        target.DoSomething();

        var targetAsMixinA = target as IMixinInterfaceA;
        if(targetAsMixinA != null)
        {
            targetAsMixinA.MethodA();
        }

        var targetAsMixinB = target as IMixinInterfaceB;
        if(targetAsMixinB != null)
        {
            targetAsMixinB.MethodB(30);
        }

        var targetAsMixinC = target as IMixinInterfaceC;
        if(targetAsMixinC != null)
        {
            targetAsMixinC.MethodC("Hello!");
        }
    }

    private readonly ITargetInterface target;
}
```

将 mixin 应用于解决方案时效果最好，当类型嗅探已经存在或必要时。这在某些库和框架中是正确的。例如，Prism（Windows Presentation Foundation/Model-View-Viewmodel 库）使用类型嗅探，并且客户端类所需的功能可以分离到不同的实现中并通过 mixin 重新组合。

## Fluent interfaces

如果一个接口从其一个或多个方法中返回自身，则称该接口为 *fluent*。这允许客户端将调用链接起来，如 Listing 3-33 所示。

### LISTING 3-33 Fluent interfaces allow method chaining.

Click here to view code image

```
public class FluentClient
{
    public FluentClient(IFluentInterface fluent)
    {
        this.fluent = fluent;
    }

    public void Run()
    {
        // without using fluency
        fluent.DoSomething();
        fluent.DoSomethingElse();
        fluent.DoSomethingElse();
        fluent.DoSomething();
        fluent.ThisMethodIsNotFluent();

        // using fluency
        fluent.DoSomething()
            .DoSomethingElse()
            .DoSomethingElse()
            .DoSomething()
            .ThisMethodIsNotFluent();
    }

    private readonly IFluentInterface fluent;
}
```

这提高了可读性，因为它避免了对接口实例的重复引用。它是实现配置或有限状态机的越来越流行的方式，如第 8 章“接口隔离”所述。

实现流畅接口也很简单。类所要做的就是从方法中返回 `this`。因为类已经是接口的实现，所以通过返回 `this`，类只返回其自身的接口部分，从而隐藏了其余的实现。Listing 3-34 显示了本示例中使用的 `IFluentInterface` 的定义和实现。

### LISTING 3-34 Implementing a simple fluent interface is easy.

```
public interface IFluentInterface
{
    IFluentInterface DoSomething();

    IFluentInterface DoSomethingElse();

    void ThisMethodIsNotFluent();
}
// ...
public class FluentImplementation : IFluentInterface
{
    public IFluentInterface DoSomething()
    {
        return this;
    }

    public IFluentInterface DoSomethingElse()
    {
        return this;
    }

    public void ThisMethodIsNotFluent()
    {
    }
}
```

请注意，接口的一个方法不是流畅的——它返回 `void`。如果方法返回的不是接口，则它不是流畅的。客户端所做的任何方法链调用都将被对非流畅方法的调用所中断。

## Conclusion

在本章中，你已经了解了接口是什么以及为什么它们是编写自适应代码的关键方面。它们是多态性的催化剂，使你能够在类族中封装变化。它们是设计模式生长的根基。然而它们实际上什么都不做。

记住，接口如果没有相应的实现就毫无用处。但没有接口，实现及其相关的依赖关系就会渗透并污染你的代码，使其难以维护和扩展。恰当地放置的接口充当服务代码肮脏的实现细节与干净、结构良好的客户端之间的防火墙。

接口还具有其他更专业的特性，例如鸭子类型和 mixin。这些很少使用，但在正确的上下文中应用时，它们可以简化原本复杂冗长的代码并增加适应性的另一个维度。

本章奠定的基础将在你体验本书其余部分接口的无处不在时变得非常重要。

## Chapter 4. Unit testing and refactoring

### After completing this chapter, you will be able to

- Define unit testing and refactoring and explain why both are very useful techniques.
- Understand how unit testing and refactoring are intrinsically linked.
- Write code in a test-first fashion, focusing on implementing only that which the tests require.
- Refactor production code to improve its overall design.
- Recognize overspecified unit tests and refactor them.

本章重点介绍两种当前编程最佳实践技术：单元测试和重构。

单元测试是编写测试其他代码的代码的学科。单元测试本身作为源代码，可以被编译和执行。随着每个单元测试的运行，它会用简单的 true 或 false 报告测试的成功或失败，通常是一个绿色或红色的视觉指示。如果所有单元测试都通过，则认为它们所测试的生产代码可能正在工作。如果甚至有一个单元测试失败——可能有数千个——则认为整体生产代码肯定已损坏。

重构是逐步改进现有代码设计的过程。它类似于编写代码的各种草稿，就像我为本书编写了各种草稿一样。通过承认我们开发人员很少能第一次就做对，重构使我们能够先做最简单的事情，然后通过逐步改进，逐渐在以后到达更好的解决方案。

能够肆无忌惮地重构的自由是由单元测试实现的。当你在尽可能早的阶段进行单元测试时——即在编写任何生产代码之前——你创建了一个安全网来捕获重构代码时出现的任何后续错误。如果单元测试从通过状态转变为失败状态，你就知道你上次所做的更改导致代码损坏。编写单元测试然后重构以获得更好的设计的过程是一个上升螺旋，在此过程中代码质量提高，同时你也在实现新功能方面取得进展。

## Unit testing

在某种程度上，单元测试应被视为每个程序员日常纪律的强制性部分。对于一些开发人员来说，理想的情况是生产代码——构成软件产品基础的代码——完全是为验证应用程序行为而编写的测试的结果。本章后面你将学习如何通过测试驱动开发来实现这一点，但请记住目标是务实而不是原教旨主义：与为了编写更多单元测试而迟到的相比，交付一些东西并接受一些审慎的技术债务肯定更好。也就是说，每个项目在及时性与完整性之间的容忍度都是独特的。

有一些公认的单元测试模式和准则会导致可重复的成功。这些模式和准则不再是新事物，而是预期、尝试和测试过的。单元测试的安排和命名，以及最重要的如何确保代码的可测试性，都是主要关注点。如果忽视这些关注点，单元测试将不再与它们所测试的代码同步，测试失败将被容忍，安全网将枯竭并断裂。

### 安排、执行、断言

每个单元测试都由三个不同的部分组成：

- 测试前置条件的**安排**
- 被测**操作**的执行
- 预期行为已发生的**断言**

这三部分构成了 *安排、执行、断言*（AAA）模式。你编写的每个测试都应遵循这种模式，以便其他人能够读懂你的单元测试。

> 注意
> 
> 有些读者可能更熟悉以 *Given, When, Then* 表达的这种方式。这与安排、执行、断言直接类似，但它是这样的：*给定*某些前置条件，*当*执行测试目标时，*那么*应该发生某些预期行为。

### 安排前置条件

在执行需要测试的操作之前，你必须搭建好正在测试的场景。对于某些测试来说，这仅仅就是构造被测系统（SUT）。SUT 就是你要测试的类。如果没有该类的有效实例，你将无法测试它的任何方法。

*清单 4-1* 展示了一个测试的最小 Arrange 部分，该测试针对表示客户余额和交易的 `Account` 类。在本例中，我使用 MSTest。本章后续还将基于此示例继续展示测试的 Act 和 Assert 部分。测试方法名 `AddingTransactionChangesBalance()` 简明扼要地描述了测试的意图——确保每当添加交易到账户时，账户余额都会发生变更以包含这笔新交易。

### 清单 4-1 构造 SUT 是安排单元测试时常见的首要步骤。

单击此处查看代码图片

```
[TestClass]
public class AccountTest
{
    [TestMethod]
    public void AddingTransactionChangesBalance()
    {
        // Arrange
        var account = new Account();
    }
}
```

这里所采取的 Arrange 步骤非常简洁。这个测试的唯一前置条件就是 `Account` 类的一个新实例。你直接在测试中通过 `new` 运算符来创建它。至此，你可以继续进入 AAA 模式的下一步。

### 执行可测试的操作

既然你已经让被测系统处于适合操作的状态，就可以执行你正在测试的方法了。每个测试的 Act 阶段都应该只包含与系统的一次交互——例如，一次方法调用或属性获取/设置。这确保了测试易于阅读和编写，并且具有清晰的执行路径。

清单 4-2 展示了测试中 Act 部分的添加。与测试方法名保持一致，测试调用了 `account.AddTransaction()` 方法。

### 清单 4-2 每个 Act 阶段都应只包含与 SUT 的一次交互。

单击此处查看代码图片

```
[TestClass]
public class AccountTest
{
    [TestMethod]
    public void AddingTransactionChangesBalance()
    {
        // Arrange
        var account = new Account();

        // Act
        account.AddTransaction(200m);
    }
}
```
