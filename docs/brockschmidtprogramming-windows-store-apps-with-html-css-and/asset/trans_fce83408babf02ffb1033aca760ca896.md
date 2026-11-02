
想象一下，如果所有已完成的处理器在每次调用之间都做了其他工作，这会是什么样子！在所有大括号和缩进中很容易迷路。

因此，真正的 Promise 也可以以一种使顺序操作更清晰、更易于管理的方式进行链式调用。当涉及两个以上的操作时，链式调用通常是首选方法。

## 链式调用 Promise

链式调用之所以成为可能，是因为 Promises/A 规范对 then 函数提出的一些要求：

> > *这个函数 [then] 应返回一个新的 promise，当给定的 [completedHandler] 或 errorHandler 回调完成时该 promise 得到兑现。回调处理器返回的值是返回的 promise 的兑现值。*

解析出来，这意味着 then 的任何实现都必须返回一个 promise，其结果是传给 then 的已完成处理器的返回值。凭借这一特性，我们可以以链式方式编写消费者代码，避免缩进噩梦：

```javascript
operation1().then(function (result1) {
    return operation2(result1);
}).then(function (result2) {
    return operation3(result2);
}).then(function (result3) {
    return operation4(result3);
}).then(function (result4) {
    return operation5(result4);
}).then(function (result5) {
    //And so on
});
```

这种结构使序列更易于阅读，通常也更易于使用。从一个操作到下一个操作存在某种显而易见的流程，其中链中每个 promise 的返回值至关重要。将此应用于上一节中的嵌套示例（仅保留已完成处理器），我们得到以下内容：

```javascript
getBreadCount().then(function (count) {
    return calculateIntegerSum(count, 500);
}).then(function (sum) {
    console.log("calculated sum = " + sum);
});
```

从概念上讲，当我们像这样编写链式 promise 时，可以方便地将一个已完成处理器的返回值视为链中下一个 then 所涉及的 promise：calculateIntegerSum 的结果会作为参数 sum 出现在下一个已完成处理器中。我们在第 2 章中详细讨论过这一概念。

然而，在 `getDesiredCount.then` 返回时，我们甚至还没有开始 `calculateIntegerSum`。这意味着从 `getDesiredCount.then` 返回的 promise 是另一个中间 promise。该中间体有自己的 `then` 方法，可以接收自己的已完成、错误和进度处理器。但它并不是直接等待某个任意异步操作完成，而是等待传给 `getDesiredCount.then` 的已完成处理器的结果。也就是说，中间 promise 是创建它的 promise 的子项或从属项，这样它就可以管理与父级已完成处理器的关系。

回顾上一节中场景 5 的代码，你会看到我们的 `then` 实现都没有返回任何内容（因此根据规范是不完整的）。要使其正确需要什么？

为了简化问题，暂时不考虑对 `then` 的多次调用，像 `NumberPromise` 这样的 promise 类可能看起来像这样：

~~~
var NumberPromise = function () {
    this._value = 1000;
    this.then = function (completedHandler) {
        setTimeout(valueAvailable, 100, this._value);
        var that = this;

        function valueAvailable(value) {
            var retVal = completedHandler(value);
            that._innerPromise.complete(retVal);
        }

        var retVal = new InnerPromise();
        this._innerPromise = retVal;
        return retVal;
    }
}
~~~

这里，`then` 创建了一个 promise 实例，我们将已完成处理器给出的内容传递给它。额外的 `InnerPromise.complete` 方法是私有的通信通道，通过它我们可以告诉内部 promise 现在可以兑现自己，这意味着它会调用在自己的 `then` 中接收到的已完成处理器。

因此 `InnerPromise` 可能看起来像这样（这还不完整）：

~~~
var InnerPromise = function (value) {
    this._value = value;
    this._completedHandler = null;
    var that = this;

    //Internal helper
    this._callComplete = function (value) {
        that._completedHandler && that._completedHandler(value);
    }

    this.then = function (completedHandler) {
~~~

    if (that._value) {
        that._callComplete(that._value);
    } else {
        that._completedHandler = completedHandler;
    }
};
//This tells us we have our fulfillment value
this.complete = function (value) {
    that._value = value;
    that._callComplete(value);
}
```

也就是说，我们提供自己的 `then`（仍然不完整），如果值已经已知，它会调用给定的处理器；否则它会保存已完成处理器（仅支持一个这样的处理器）。然后我们假设当父 promise 从其持有的已完成处理器获得返回值时，会调用 `complete` 方法。当这种情况发生时，这个 `InnerPromise` 对象就可以兑现自己。

到目前为止一切顺利。然而，当传给 `complete` 的参数本身就是一个 promise 会怎样？这意味着这个 `InnerPromise` 必须等待另一个 promise 完成，使用另一个已完成处理器。只有这样它才能兑现自己。因此我们需要在 `InnerPromise` 内部做类似这样的事情：

//Test if a value is a promise
function isPromise(p) {
    return (p && typeof p === "object" && typeof p.then === "function");
}

//This tells us we have our fulfillment value
this.complete = function (value) {
    that._value = value;

    if (isPromise(value)) {
        value.then(function (finalValue) {
            that._callComplete(value);
        });
    } else {
        that._callComplete(value);
    }
}

我们现在进展顺利。有了这个实现，链式调用 `getDesiredCount` 和 `calculateIntegerSum` 的消费者代码工作得很好，其中传给第二个已完成处理器的 `sum` 值正是计算返回的结果。

但我们仍然有一个问题：`InnerPromise.then` 本身并没有返回一个 promise，正如它应该做的那样，这意味着链在这里就断了。因此，我们无法在序列上链式调用另一个操作。

`InnerPromise.then` 应该返回什么？嗯，在我们已经拥有兑现值的情况下，我们可以直接返回自己（在变量 `that` 中）。否则我们需要再创建一个 InnerPromise，其连接方式与我们在 NumberPromise 内部所做的相同。

~~~javascript
this._callComplete = function (value) {
    if (that._completedHandler) {
        var retVal = that._completedHandler(value);
        that._innerPromise.complete(retVal);
    }
}

this.then = function (completedHandler) {
    if (that._value) {
        var retVal = that._callComplete(that._value);
        that._innerPromise.complete(retVal);
        return that;
    } else {
        that._completedHandler = completedHandler;
    }

    //Create yet another inner promise for our return value
    var retVal = new InnerPromise();
    this._innerPromise = retVal;
    return retVal;
};
~~~

有了这个，InnerPromise 支持我们所寻找的链式调用。你可以在 Promises 示例的场景 6 中看到这一点。在此场景中，你会在页面上找到两个按钮。第一个运行此精简的消费者代码：

~~~javascript
getDesiredCount().then(function (count) {
    return calculateIntegerSum(count, 500);
}).then(function (sum1) {
    console.log("calculated first sum = " + sum1);
    return calculateIntegerSum(sum1, 500);
}).then(function (sum2) {
    console.log("calculated second sum = " + sum2);
});
~~~

其中输出为：

~~~
calculated first sum = 499500
calculated second sum = 124749875250
~~~

第二个按钮运行相同的消费者代码，但为 promise 使用了显式的变量。它还打开了来自 promise 类内部的嘈杂日志记录，以便我们可以看到正在发生的一切。为此，每个 promise 类都标记有标识符，以便我们可以跟踪它们各自的身份。我不会展示代码，但输出如下：

~~~
p1 obtained, type = NumberPromise
InnerPromise1 created
p1.then returned, p2 obtained, type = InnerPromise1
InnerPromise1.then called
InnerPromise1.then creating new promise
InnerPromise2 created
p2.then returned, p3 obtained, type = InnerPromise2
~~~
