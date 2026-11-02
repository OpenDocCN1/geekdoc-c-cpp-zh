

- 9. 如果承诺未能兑现，消费者就只能尽力应对！

牢记这些内容，接下来我们来看看这些关系如何体现在代码中。

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_664_0.png)

图 A-2 完整的承诺关系。

## Promise 构造（核心关系）

要实现发起者与消费者之间承诺的核心关系，我们需要满足以下条件：

- 一种创建承诺并将其关联到相关结果的方式。
- 一种告知消费者结果何时可用的方式，这意味着需要某种回调函数传入消费者。

第一个要求通常意味着发起者会定义某种对象类，在内部封装获取结果所需的流程。异步 API 会创建此类的一个实例，并将其返回给调用方。

对于第二个要求，我们有两种实现方式。一种是在 Promise 对象上设置一个简单属性，由消费者将回调函数赋给该属性。另一种是在 Promise 上提供一个方法，消费者通过该方法传入回调函数。两者之中，后一种方式（使用方法）能让发起者更灵活地兑现承诺，因为在消费者赋予回调之前——这也称为订阅 Promise——发起者可以暂缓启动底层工作。你知道的，有些工作你明明知道得做，却总是迟迟不动手，直到有人真的给你定下期限！调用方法会告诉发起者，消费者现在确实需要结果了。94 在此之前，Promise 对象可以一直处于待命状态。

在 JavaScript 社区中逐渐形成的 Promise 定义，即 CommonJS/Promises A（WinJS 和 WinRT 遵循的规范）中，满足第二个要求的方法称为 *then*。事实上，这就是 Promise 的定义：一个拥有名为 'then' 的属性，且该属性值为函数的对象。

就是这样。实际上，WinJS 的静态函数 WinJS.Promise.is 用于测试给定对象是否为 Promise，其实现如下：

```javascript
is: function Promise_is(value) {
    return value && typeof value === "object" && typeof value.then === "function";
}
```

**注意** 第 3 章中我们还看到了一个非常相似的函数，名为 *done*，WinJS 和 WinRT 的 Promise 使用它来处理错误。这不是 Promises A 规范的一部分，但 Windows Store 应用会用到它。

在核心关系中，*then* 接受一个参数：由消费者实现的回调函数，称为完成处理程序。（它也称为已兑现处理程序，但我更喜欢前一种说法。）下面说明它如何融入前面展示的核心关系图中（编号保持一致）：

- 1. 消费者调用某个返回 Promise 的 API。相关 API 通常会定义所请求对象的类型。例如，在 WinRT 中，Geolocator.getGeolocationAsync 方法会返回一个 Promise，其结果是 Geoposition 对象。
- 2. 发起者通过实例化其用于执行工作的类来创建 Promise。只要该对象有一个 *then* 方法，就可以包含所需的其他方法和属性。再次强调，根据定义，Promise 必须有一个名为 *then* 的方法，但这既不要求也不禁止它拥有其他方法和属性。
- 3. 消费者收到 Promise 并希望了解其是否兑现后，会调用 *then* 来订阅该 Promise，并将完成处理程序作为第一个参数传入。Promise 必须在内部保留此函数（除非结果已经可用，见下文）。请再次注意，`then` 可以由任意数量的消费者多次调用，而 Promise 必须维护所有这些完成处理程序的列表。

94 当然，这个方法也可以是属性设置器；这里的要点是，对象需要某种方法作为触发额外操作的机制，而被动属性（非设置器）并不具备这种能力。

在此我还想分享一个小技巧。克里斯·塞尔斯曾在微软短暂担任过我的经理，他多次用这个方法对付我。对于我欠他的某项交付成果，他会问：“你什么时候能完成？”如果我说不知道，他就会问：“你什么时候能知道自己什么时候能完成？”如果我还是答不上来，他就会问：“你什么时候能知道自己什么时候能知道什么时候能完成？”如此循环往复，直到他从我这里得到某种明确的承诺！

- 4. 与此同时，发起者会努力兑现承诺。例如，WinRT 的 `getGeolocationAsync` API 会从设备传感器获取信息，或使用基于 IP 地址的方法来估算用户的位置。
- 5. 发起者获得结果后，会让 Promise 对象将结果传递给所有完成处理程序（通过 `then` 接收）。
- 6. 消费者在完成处理程序中按自己的需要处理数据。

如你所见，Promise 归根结底*只是一种编程结构*，用于管理消费者与发起者之间的关系，仅此而已。事实上，它不一定涉及任何异步工作：Promise 也可以用于已经确定的结果。在这种情况下，Promise 只是增加了完成处理程序这一层，通常会在第 3 步中通过 `then` 提供给 Promise 后立即调用，而不是等到第 5 步。虽然这会给已知值带来额外开销，但它能让同步和异步结果以相同方式处理，这对异步编程大有裨益。

为了说明 Promise 的核心构造，并展示异步操作，我们来看几个示例。这些示例使用了一个简单的 Promise 类，来自配套内容中的 Promises 示例。

**不要照着我接下来展示的做法来** 自己实现一个功能完备的 Promise 类会相当复杂，因为你需要处理许多细节，例如 `then` 必须返回另一个 Promise。因此，务必使用 `WinJS.Promise` 类，或使用其他完整实现 Promises A、并能让你轻松为自己的异步操作创建可靠 Promise 的库。这里展示的示例仅用于教学，因为它们并未实现完整规范。

## 示例 #1：一个空 Promise！

假设我们有一个函数 `doSomethingForNothing`，它通过 Promise 返回一个空对象 `{ }` 作为结果：

```
//Originator code
function doSomethingForNothing() {
    return new EmptyPromise();
}
```

稍后我们会介绍 `EmptyPromise` 类。首先，假设 `EmptyPromise` 符合定义，并提供一个接受完成处理程序的 `then` 方法。消费者可以这样使用这个 API：

```javascript
//Consumer code
var promise = doSomethingForNothing();
promise.then(function (results) {
  console.log(JSON.stringify(results));
});
```

输出如下：

{ }

**示例中的 App.log** 虽然这里的代码片段使用了 console.log，但 Promises 示例使用了一个名为 App.log 的函数，它接入 WinJS.log 机制，并将输出直接显示在应用画布上。这样做只是为了让运行中的示例应用能够显示有意义的输出。

为了简洁起见，消费者代码可以缩短为 `doSomethingForNothing().then(function (results) { ... });`，但为了清晰起见，我们会显式写出 Promise。还要注意，传递给完成处理程序的参数（上例中的 results）可以随意命名。代码由你编写，一切由你掌控。

顺着上面的消费者代码看，我们调用了 promise.then，随后某个时候会调用匿名完成处理程序。这个“某个时候”究竟要等多久，取决于相关操作的性质。

假设 doSomethingForNothing 已经知道它会返回一个空对象作为结果。那么，EmptyPromise 可以这样实现（请不要对面向对象 JavaScript 的最佳写法发表意见）：

```javascript
//Originator code
var EmptyPromise = function () {
  this._value = {};
  this.then = function (completedHandler) {
    completedHandler(this._value);
  }
}
```

发起者对这个构造函数使用 new 后，会得到一个拥有 then 方法的对象，该方法接受一个完成处理程序。由于这个 Promise 已经知道结果，其 then 实现只需直接调用给定的完成处理程序。无论 then 被调用多少次，这种做法都行得通，即使消费者将这个 Promise 传递给了另一个消费者也是如此。95

95 再次说明，规范规定 then 的返回值必须是一个 Promise，并且该 Promise 会在完成处理程序返回时兑现。这是导致 Promise 实现相当复杂的因素之一。显然，我们在这里忽略了定义中的这一部分！

