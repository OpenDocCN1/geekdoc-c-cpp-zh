

// . . .
public class MixinImplementationB : IMixinInterfaceB
{
    public void MethodB(int parameter)
    {
        Console.WriteLine("IMixinInterfaceB.MethodB({0})", parameter);
    }
}
// . . .
public interface IMixinInterfaceC
{
    void MethodC(string parameter);
}
// . . .
public class MixinImplementationC : IMixinInterfaceC
{
    public void MethodC(string parameter)
    {
        Console.WriteLine("IMixinInterfaceC.MethodC(\"{0}\")", parameter);
    }
}
```

请注意，并没有一个类实现所有这些接口。相反，下一步是配置 Re-mix，以便当它被要求提供 TargetImplementation 的实例时，它将返回一个包含所有接口和类组合的混入。清单 4-31 显示了这样的配置。

**LISTING 4-31** Instructing Re-mix how to construct TargetImplementation instances.

```
var config = MixinConfiguration.BuildFromActive()
    .ForClass<TargetImplementation>()
    .AddMixin<MixinImplementationA>()
    .AddMixin<MixinImplementationB>()
    .AddMixin<MixinImplementationC>()
    .BuildConfiguration();

MixinConfiguration.SetActiveConfiguration(config);
```

不幸的是，你不能简单地在 TargetImplementation 上调用 new 并期望得到一个混入。相反，你必须要求 Re-mix 创建一个 TargetImplementation 实例，以便它可以根据你的规范构建一个新类型并实例化它。清单 4-32 显示了它是如何做到这一点的——幸运的是，这很简单。

**LISTING 4-32** Re-mix is in charge of creating mixins.

Re-mix 的一个限制是，你无法——也不能——知道 ObjectFactory.Create 返回的实例的确切类型。你所知道的是，它是 TargetImplementation 的一个子类的实例。这对客户端来说有点坏消息，因为在编译时你唯一能保证 TargetImplementation 满足的接口是 ITargetInterface。因此，混入的客户端必须通过使用 is 和 as 进行类型嗅探，将混入强制转换为期望的接口。清单 4-33 突出了这个问题。

**LISTING 4-33** Type-sniffing is bad practice but necessary for using mixins.

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

将混入应用于解决方案时效果最好，当类型嗅探已经存在或必要时。这在某些库和框架中是正确的。例如，Prism（Windows Presentation Foundation/Model-View-ViewModel 库）使用类型嗅探，并且客户端类所需的功能可以分离到不同的实现中，并通过混入重新组合。

## Fluent interfaces

如果一个接口从其一个或多个方法中返回自身，则称该接口为流畅接口。这允许客户端将调用链接在一起，如清单 4-34 所示。

**LISTING 4-34** Fluent interfaces allow method chaining.

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

这提高了可读性，因为它避免了对接口实例的重复引用。它是实现配置或有限状态机的越来越流行的方式，如第 10 章“接口隔离”所述。

流畅接口也很容易实现。类所要做的就是从方法中返回 this。因为类已经是接口的实现，所以通过返回 this，类只返回其自身的接口部分，从而隐藏了其余的实现。清单 4-35 显示了本示例中使用的 IFluentInterface 的定义和实现。

**LISTING 4-35** Implementing a simple fluent interface is easy.

```
public interface IFluentInterface
{
    IFluentInterface DoSomething();

    IFluentInterface DoSomethingElse();

    void ThisMethodIsNotFluent();
}
// . . .
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

请注意，接口的一个方法不是流畅的——它返回 void。如果一个方法返回的不是接口，它就不是流畅的。客户端所做的任何方法链调用都将被对非流畅方法的调用所中断。

## Conclusion

在本章中，你已经了解了接口是什么以及为什么它们是编写自适应代码的关键方面。它们是多态性的催化剂，使你能够在类族中封装变化。它们是设计模式生长的根基。然而它们实际上什么都不做。

记住，没有伴随实现，接口是无用的。但没有接口，实现及其相关的依赖关系就会渗透并污染你的代码，使其难以维护和扩展。恰当地放置的接口充当服务代码肮脏的实现细节与干净、结构良好的客户端之间的防火墙。

接口还具有其他更专业的特性，例如鸭子类型和混入。这些很少使用，但在正确的上下文中应用时，它们可以简化否则复杂的代码并增加适应性的额外维度。

本章奠定的基础将在你体验本书其余部分中接口的无处不在时具有重要意义。

## Testing

**After completing this chapter, you will be able to**

- Define different kinds of application testing and choose between techniques.
- Write code in a test-first fashion, focusing on implementing only that which the tests demand.
- Understand the different types of testing that can improve aspects of a software product.
- Diagnose problems created by testing anti-patterns, which reduce code adaptiveness.

软件质量不仅限于代码的质量以及它对变化的适应性。它也是衡量软件是否准确满足其需求的标准。测试是一系列可以用来确保这种软件质量的实践的统称。

单元测试是编写测试其他代码的代码的学科。单元测试是源代码，因此可以编译和执行。随着每个单元测试的运行，它会以简单的 true 或 false 报告测试的成功或失败，通常是绿色或红色视觉指示。如果所有单元测试都通过，则它们所测试的生产代码被认为正在工作，满足其需求。如果甚至一个单元测试失败——可能有数千个——则整体生产代码被认为未满足其需求。

当你在尽可能早的阶段进行单元测试时——也就是说，在编写任何生产代码之前——你创建了一个安全网来捕获更改代码时出现的任何后续错误。如果一个单元测试从通过状态转变为失败状态，你就知道你上次所做的更改导致代码损坏。编写单元测试然后改进代码以获得更好的设计的过程创造了一个正反馈循环，在此过程中代码质量提高，同时你也在同时取得实现新功能进展。

### Unit testing

在某种程度上，单元测试应被视为每个程序员日常纪律的强制性部分。理想的情况是，生产代码——构成软件产品基础的代码——完全是为验证应用程序行为而编写的测试的结果。本章后面你将学习如何通过测试驱动开发来实现这一点，但请记住，目标是在务实与纯粹主义之间取得平衡。最好是交付一些东西并接受一些

