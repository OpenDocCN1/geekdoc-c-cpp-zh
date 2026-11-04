
```csharp
public interface IObserver<in T> {
    void OnCompleted();
    void OnError(Exception error);
    void OnNext(T value);
}
```

最后一个方法最容易理解，它对应着我们传统意义上的事件处理器。每当事件源引发一个事件时，就会调用这个方法。请注意接口中泛型的使用，它用来表示事件参数，这些参数携带了事件所发出的数据。

## 泛型协变与逆变（再讨论）

`IObservable<T>` 和 `IObserver<T>` 接口都在其泛型参数 `T` 上使用了新的 .NET 4 和 C# 4.0 泛型协变和逆变注解。我们可以尝试通过两种方式来理解这些注解。

首先是机械式的方式，像编译器一样查看代码。对于 `IObserver<T>`，请注意 `T` 只出现在输入位置，即作为 `OnNext` 的参数。因此，该接口可以使用 `in` 关键字标记为逆变。对于 `IObservable<T>`，情况则要复杂一些。因为 `IObserver<T>` 用在 `Subscribe` 方法的输入位置，你可能会认为它也应当被标记为逆变。这时事情会很快变得违反直觉。当在输入位置使用逆变类型时，变体会发生翻转：`T` 在 `IObservable<T>` 上变成了协变。你可以把这与布尔逻辑中的双重否定规则进行类比。

直觉方法可能效果更好。很明显，数据是被送入 `IObserver<T>` 对象的，因此将其标记为逆变是合理的，因为它会通过输入位置充当数据的接收者。另一方面，`IObservable<T>` 产生数据并将其输入观察者。生产是一种导出或输出的行为，因此该类型应当是协变的。

如果一开始没能理解这些，也不用担心：即使是最聪明的语言设计者，在琢磨这个问题时偶尔也会遇到困难。

`OnError` 方法用于向观察者发出信号，表明事件源遇到了某些问题。这使得处理异步发生的错误变得容易得多（例如，在与 Web 服务通信时发生网络错误）。在经典事件的世界中，没有直接渠道将这些信息传递给用户，处理此类异常情况变得非常麻烦。

最后，`OnCompleted` 方法表示事件源不会再产生任何进一步的数据（例如，因为底层操作已完成）。当你需要确知某个事件不再产生数据时（例如，解除观察者的挂钩），这会非常有用。经典的 .NET 事件不会引发此类通知。

## 拉取与推送

`IObservable<T>` 和 `IObserver<T>` 接口乍看起来可能有点奇怪，但实际上它们与众所周知的 `System.Collections.Generic` 接口 `IEnumerable<T>` 和 `IEnumerator<T>` 密切相关。事实上，它们是数学对偶。你觉得这相当抽象是正常的，但其实相当简单。请跟我来。

回顾我们关于语句的讨论，`IEnumerable<T>` 的主要用途是 `foreach` 循环语句。集合实现该接口，允许我们逐个拉取其中的数据。实际上，消费者处于控制地位，这使其成为一种交互式机制。为了从源中拉取数据，消费者通过调用 `MoveNext` 和 `Current` 向枚举器请求更多数据：

```csharp
IEnumerable<T> source = ...;
using (IEnumerator<T> sourceEnumerator = source.GetEnumerator()) {
    while (sourceEnumerator.MoveNext()) { // Do you have more?
        T item = sourceEnumerator.Current; // Give it to me!
        // Do something with the item; could break out as well...
    }
} // Calls Dispose, telling the source we're done fetching data.
```

基于 `IEnumerable<T>` 和 `IEnumerator<T>` 消费数据源的方法如图 18.31 所示。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_923_0.png)

图 18.31 枚举数据源基于交互式对话。

事件源则恰恰相反，基于响应式方法。现在是源告诉消费者数据可用，并将其推送给消费者。事件处理器（即观察者）的作用是对数据到来的事件做出反应：

```csharp
IObservable<T> source = ...;
using (source.Subscribe(item => { /* Do something with the item */ })) {
    // While observing events, you can do other stuff.
    // Or you could call the Dispose method in a different place later.
} // Calls Dispose, telling the source we're done receiving events.
```

在前面的代码中，我使用了 `IObservable<T>` 上的一个扩展方法，它允许将观察者的 `OnNext` 调用作为 lambda 表达式传入，从而无需仅仅为了注册事件处理器而实现 `IObserver<T>` 接口。

基于 `IObservable<T>` 和 `IObserver<T>` 对事件源做出响应的方法如图 18.32 所示。

警告：请勿在家中尝试。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_924_0.png)

图 18.32 观察事件源需要观察者做出响应。

总而言之，从 `IEnumerable<T>` 检索数据时，你主动获取一个枚举器对象，并开始一段类似这样的对话：你还有下一个条目给我吗？有！请把它给我……这是非常交互式的。而对于 `IObservable<T>`，你则被动得多，你会这样说：只要有条目可用，就通过这个方法把它推送给我，让我观察它。

对偶是一个非常深刻的属性，能产生许多有用的结果。从数学角度讲，对偶一侧拥有某些属性，必然意味着对偶另一侧也拥有类似属性。在 `IObservable<T>` 与 `IEnumerable<T>` 的关系中，有一个地方能明显看到这一点，那就是两个领域上 *组合子* 的定义。简单来说，组合子将一个领域中的一个或多个输入对象组合成同一领域中的一个输出对象。你可能已经猜到了，LINQ 的标准查询运算符就是此类组合子。

为了说明这一点，请思考下面这些在 `IEnumerable<T>` 上定义为扩展方法的 LINQ to Object 查询运算符。我们将在专门讨论 LINQ 的章节中详细阐述这些运算符，尤其是第 20 章“语言集成查询内幕”，其中有一整节名为“标准查询运算符”。

```csharp
IEnumerable<T> Where<T>(this IEnumerable<T> source, Func<T, bool> predicate);
IEnumerable<R> Select<T, R>(this IEnumerable<T> source, Func<T, R> project);
```

正如你所见，（大多数）这些运算符接受一个处于 `IEnumerable` “领域”中的对象，并返回一个这样的对象作为结果。由于两个世界之间存在深刻的对偶性，我们可以轻松地将前面的签名转换为 `IObservable<T>`：

```csharp
IObservable<T> Where<T>(this IObservable<T> source, Func<T, bool> predicate);
IObservable<R> Select<T, R>(this IObservable<T> source, Func<T, R> project);
```

这些运算符与 `IEnumerable<T>` 上对应的运算符一样有意义。例如，给定一个产生 `T` 类型条目的*事件源*，你可以使用 `Where` 运算符应用过滤，从而获得一个只包含通过过滤条件条目的*事件源*。使用这些运算符时，用户无需担心所有实现细节，包括正确释放 `IObserver<T>` 订阅。

### 查询运算符在哪里？

.NET 4 没有随附 `IObservable<T>` 的查询运算符。由于各种发布限制，这些运算符作为 Rx 的一部分带外发布，而 Rx 仍处于测试阶段。尽管如此，关键的 `IObservable<T>` 和 `IObserver<T>` 接口在 .NET 4 中是可用的，因此组件可以开始依赖它们。

如果我们想在 `CountDown` 类上实现 `IObservable<uint>`，可以进行如下映射：

- `Tick` 事件通过对已订阅观察者调用 `OnNext` 来实现。
- `Finished` 事件对应于对这些观察者调用 `OnCompleted`。

一旦我们这样做了，用户就可以按如下方式订阅计时器的事件（使用 Rx 提供的扩展 `Subscribe` 方法）：

```csharp
var countDown = new CountDown(5);
var unsubscribe = countDown.Subscribe(
    seconds => { Console.WriteLine(seconds + " seconds remaining."); },
```
