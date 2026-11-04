
泛型约束不足以表达在泛型类型参数上存在某个运算符的要求。如果我们有接口作为运算符契约的容器，那么基于接口的泛型约束就可以派上用场。

基于运算符进行约束的能力长期以来一直是一个请求，但人们担心这可能会变成一个无底洞，不同约束机制的数量会随着版本的发布不断增长。只有未来才能告诉我们，是否会有足够的动力来设计、实现、测试并记录这样一个特性。如果你对此有明确的需求，请大声而清晰地表达出来，确保 .NET 语言团队能够听到。与此同时，也请务必看看 F#，在 F# 中数值数据类型得到了某种不同的处理，尤其是当你发现自己回到科学计算领域时。

## 基类约束

不仅接口可用于将类型参数限制为仅那些实现它的类型，基类也可以用来强制执行类似的关系。你可以约束一个类型参数，使得只有指定基类的子类才能用于实例化该参数：

```
class FruitMixer<T> where T : Fruit {
    private T[] _ingredients;
    public FruitMixer(params T[] ingredients) {
        _ingredients = ingredients;
    }
}
```

约束的强制过程与我们所见过的接口约束类似。下面这段代码可以正常工作，原因显而易见：每一个 Jonagold 都是一个 Apple。

```
var appleMixer = new FruitMixer<Apple>(new Jonagold());
```

请注意，泛型与众所周知的“在期望较少特定类型的地方传入更特定类型的对象”的能力相辅相成。即使用于创建 `FruitMixer<Apple>` 实例的构造函数被类型化为接收 Apple 的 params 数组，我们也可以放入更派生类型的元素，例如 Jonagold。但是，当你尝试使用不从 Fruit 派生的类型来构造泛型类型时，在编译时就会遇到麻烦：

```
var cementMixer = new CementMixer<Cement>();
```

为泛型类型的使用者添加约束，为声明泛型类型的一方提供了更多保证。因为我们保证只会获得 Fruit 派生的类型，所以我们可以依赖 Fruit 类型上定义的方法：

```
class FruitMixer<T> where T : Fruit {
    private T[] _ingredients;

    public FruitMixer(params T[] ingredients) {
        _ingredients = ingredients;
    }

    public Juice MakeJuice() {
        var juice = new Juice();

        foreach (T ingredient in _ingredients)
            juice += ingredient.Squeeze();

        return juice;
    }
}
```

## 默认构造函数约束

除了基于接口或基类表达的泛型约束之外，还有一些其他技术可用。其中之一是 `new` 约束，它表达了为某个类型参数提供默认构造函数的要求：

```
class Factory<T> where T : new() {
    ...

    public T CreateInstance() {
        return new T();
    }
}
```

显然，前面 `Factory<T>` 类型的 `CreateInstance` 方法相对于从外部直接实例化对象而言，并没有提供任何价值。它仅仅是一种方式，用以展示在参数被适当约束的情况下，预期的构造函数语法如何与类型参数配合使用。从外部来看，这个类型的使用方式如下：

```
var factory = new Factory<int>();
var zero = factory.CreateInstance();
```

事实证明，`Int32` 类型有一个默认构造函数（返回默认值 0），所以这可以正常工作。相反，没有默认构造函数的类型在用作泛型参数 `T` 时会被拒绝。图 15.19 显示了这种情况下产生的编译时错误。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_754_0.png)

图 15.19 违反默认构造函数约束。

当需要实例化参数类型的对象时（例如，提供默认存储或重置某种存储中的项），默认构造函数约束就派上了用场。以服务对象池为例来考虑这种情况。在基本层面上，一个对象池可能看起来像这样：

```
class ServicePool<T> : IService where T : IService, new() {
    private List<T> _objects;

    public ServicePool(int min, int max) { /* TODO */ }
}
```

```
// Any IService interface would do, so we just give a simple example here.
interface IService
{
    void TransferFunds(string sourceAccount, string targetAccount, decimal amount);
}
```

在类型层面，`ServicePool<T>` 实现了某个服务接口，将该功能暴露给外部世界。为了提供此服务，它将所有请求委托给实现相同接口的工作对象。这就解释了类型定义及其约束：

```
class ServicePool<T>
    : IService    // expose the service to the outside
    where T : IService,  // need to be able to delegate to a worker
        new()           // need to be able to instantiate workers as needed
```

该对象池负责确保在任何时候都有一定数量的工作对象处于待命状态。它通过利用默认构造函数约束，创建由类型参数 `T` 指定的工作类型实例来实现这一点。

每当对对象池服务接口的请求到达时，请求会被转发给一个可用工作对象，同时以某种方式将该工作对象标记为已占用。这意味着必须使用一种不同的、最好是线程安全的数据结构来跟踪已占用或可用（空闲）的工作对象。当请求完成时，该工作对象可以被返还到空闲列表，准备服务其他请求。图 15.20 显示了与对象池的交互序列。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_755_0.png)

图 15.20 对象池交互序列。

可能会出现这样的情况：当没有空闲工作对象可用时，请求到达了。如果尚未达到最大工作对象数的阈值，对象池可以选择创建更多工作对象实例，再次使用默认构造函数约束。这种按需实例化工作对象的过程如图 15.21 所示。

还可以实现其他机制以尽可能保持池的高效（例如，当服务池的工作负载下降时，从池中移除工作对象）。这可能有助于减少资源消耗（例如，当工作对象保持与另一台提供服务的机器的开放连接时）。并且，通过使（引用类型的）对象不可达，它也可以从托管堆中回收。

## 泛型对 CLS 的影响

公共语言规范（CLS）是 .NET 真正实现跨语言互操作性的关键。通过让多种语言遵循一套规则，就可以在类型及其使用方面获得完整保真的集成。

当 CLS 在早期的 .NET 1.0 时代被引入时，许多语言实现了“CLS 角色”（有关更多信息，请参阅第 1 章“介绍 .NET 平台”）。为了使 .NET 2.0 及更高版本中的泛型成为一流的 .NET Framework 特性，CLS 必须扩展额外的规则，以确保在处理此类类型时的跨语言互操作性。

鉴于泛型带来的巨大好处，不得不给语言实现者增加额外负担被认为是一种不错的权衡。万岁！

![](img/a16f85e62ce9bdc527f4b09dbfe26092_756_0.png)

图 15.21 对象池交互序列。

显然，我们都想知道 `new T()` 调用在底层是如何实现的。首先，注意泛型约束机制已启用，以供跨语言使用。如图 15.22 所示，`.ctor T` 部分揭示了约束贯穿编译过程，一直进入元数据，供其他语言检查。

在 `new T()` 被编译的地方，有更有趣的事情发生。事实上，我选择展示一个带有 `CreateInstance` 方法的 `Factory<T>` 并非随意之举，因为它为我们稍后讨论泛型方法提供了一个很好的起点。让我们看看 `CreateInstance` 内部发生了什么，如图 15.23 所示。

