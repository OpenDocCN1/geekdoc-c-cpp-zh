

### 清单12.9（续）

```java
public static final int THRESHOLD = 1000;
private double[] values;
private int from;
private int to;
private DoublePredicate filter;

public Counter(double[] values, int from, int to, DoublePredicate filter)
{
    this.values = values;
    this.from = from;
    this.to = to;
    this.filter = filter;
}

protected Integer compute()
{
    if (to - from < THRESHOLD)
    {
        int count = 0;
        for (int i = from; i < to; i++)
        {
            if (filter.test(values[i])) count++;
        }
        return count;
    }
    else
    {
        int mid = (from + to) / 2;
        var first = new Counter(values, from, mid, filter);
        var second = new Counter(values, mid, to, filter);
        invokeAll(first, second);
        return first.join() + second.join();
    }
}
}
```

## 12.7 异步计算

到目前为止，我们的并发计算方法都是将任务分解，然后等待所有部分完成。但等待并不总是一个好主意。在以下小节中，你将了解如何实现无等待（即异步）计算。

### 12.7.1 可完成的 Future

当你有一个 future 对象时，你需要调用 `get` 来获取值，这会阻塞直到值可用。`CompletableFuture` 类实现了 `Future` 接口，并提供了第二种获取结果的机制。你可以注册一个 `callback`，一旦结果可用，它就会被（在某个线程中）调用并传入结果。

```java
CompletableFuture<String> f = ...;
f.thenAccept(s -> Process the result string s);
```

这样，你就可以在结果可用时非阻塞地处理结果。有少数 API 方法会返回 `CompletableFuture` 对象。例如，你可以使用实验性的 `HttpClient` 类异步获取网页，你将在第二卷的第 4 章中遇到这个类：

```java
HttpClient client = HttpClient.newHttpClient();
HttpRequest request = HttpRequest.newBuilder(URI.create(urlString)).GET().build();
CompletableFuture<HttpResponse<String>> f = client.sendAsync(
      request, BodyHandlers.ofString());
```

如果有一个方法能够生成现成的 `CompletableFuture` 那就太好了，但大多数时候，你需要自己创建。要以异步方式运行任务并获取 `CompletableFuture`，你不能直接将其提交给执行器服务。相反，你应该调用静态方法 `CompletableFuture.supplyAsync`。下面是不借助 `HttpClient` 类来读取网页的方法：

```java
public CompletableFuture<String> readPage(URL url)
{
   return CompletableFuture.supplyAsync(() ->
      {
         try
         {
            return new String(url.openStream().readAllBytes(), "UTF-8");
         }
         catch (IOException e)
         {
            throw new UncheckedIOException(e);
         }
      }, executor);
}
```

如果省略执行器，任务将在默认执行器（即 `ForkJoinPool.commonPool()` 返回的执行器）上运行。你通常不会希望这样做。

> **警告：** 请注意，`supplyAsync` 方法的第一个参数是 `Supplier<T>`，而不是 `Callable<T>`。这两个接口都描述了无参数且返回值类型为 `T` 的函数，但 `Supplier` 函数不能抛出受检异常。从上面的代码可以看出，这并非一个明智的选择。

`CompletableFuture` 可以通过两种方式完成：要么带有结果，要么带有未捕获的异常。为了处理这两种情况，可以使用 `whenComplete` 方法。所提供的函数会以结果（如果没有则为 `null`）和异常（如果没有则为 `null`）为参数被调用。

```java
f.whenComplete((s, t) -> {
    if (t == null) { Process the result s; }
    else { Process the Throwable t; }
});
```

`CompletableFuture` 之所以被称为 *可完成（completable）*，是因为你可以手动设置完成值。（在其他并发库中，这样的对象被称为 *承诺（promise）*。）当然，当你使用 `supplyAsync` 创建 `CompletableFuture` 时，完成值会在任务完成时隐式设置。但显式设置结果会带来额外的灵活性。例如，两个任务可以同时计算一个答案：

```java
var f = new CompletableFuture<Integer>();
executor.execute(() ->
    {
        int n = workHard(arg);
        f.complete(n);
    });
executor.execute(() ->
    {
        int n = workSmart(arg);
        f.complete(n);
    });
```

若要改为用异常完成 future，请调用

```java
Throwable t = ...;
f.completeExceptionally(t);
```

> **注意：** 在多线程中对同一个 future 调用 `complete` 或 `completeExceptionally` 是安全的。如果 future 已经完成，这些调用将没有效果。

`isDone` 方法会告诉你一个 `Future` 对象是否已经完成（正常完成或发生异常）。在前面的例子中，`workHard` 和 `workSmart` 方法可以利用该信息，在另一个方法已经确定结果时停止工作。

> **警告：** 与普通 future 不同，当你调用 `CompletableFuture` 的 `cancel` 方法时，其计算不会被中断。取消只是将 `Future` 对象设置为以 `CancellationException` 异常完成。一般来说，这是合理的，因为 `CompletableFuture` 可能没有一个专门负责其完成的线程。然而，这种限制也适用于 `applyAsync` 等方法返回的 `CompletableFuture` 实例，而这些实例原则上是可以被中断的。

### 12.7.2 组合可完成的 Future

非阻塞调用是通过回调实现的。程序员为任务完成后的动作注册一个回调。当然，如果下一个动作也是异步的，那再下一个动作就会在不同的回调中。即使程序员按照“先做第1步，再做第2步，然后做第3步”的思路思考，程序逻辑也可能分散在“回调地狱”中。当需要添加错误处理时，情况会更糟。假设第2步是“用户登录”。由于用户可能输错凭据，你可能需要重复该步骤。试图在一组回调中实现这样的控制流，或者在其实现后理解它，可能相当具有挑战性。

`CompletableFuture` 类通过提供一种将异步任务 *组合* 成处理流水线的机制来解决这个问题。

例如，假设我们要从网页中提取所有图片。假设我们有一个方法 `public CompletableFuture<String> readPage(URL url)`，它会在网页文本可用时返回该文本。如果方法 `public List<URL> getImageURLs(String page)` 能返回 HTML 页面中图片的 URL，你就可以安排它在页面可用时被调用：

```java
CompletableFuture<String> contents = readPage(url);
CompletableFuture<List<URL>> imageURLs = contents.thenApply(this::getImageURLs);
```

`thenApply` 方法也不会阻塞。它会返回另一个 future。当第一个 future 完成时，其结果会被传递给 `getImageURLs` 方法，该方法的返回值将成为最终结果。

```java
CompletableFuture<List<URL>> imageURLs = readPage(url)
    .exceptionally(ex -> "<html></html>")
    .thenApply(this::getImageURLs)
```

你可以用同样的方式设置超时限制：

```java
CompletableFuture<List<URL>> imageURLs = readPage(url)
    .completeOnTimeout("<html></html>", 30, TimeUnit.SECONDS)
    .thenApply(this::getImageURLs)
```

或者，你也可以在超时时抛出异常：

```java
CompletableFuture<String> f = readPage(url).orTimeout(30, TimeUnit.SECONDS);
```

表12.3中返回 `void` 的方法通常用于处理流水线的末端。

### 表12.3 向 `CompletableFuture<T>` 对象添加动作

| 方法 | 参数 | 描述 |
|---|---|---|
| `thenApply` | `T -> U` | 将函数应用于结果。 |
| `thenAccept` | `T -> void` | 类似于 `thenApply`，但结果为 `void`。 |
| `thenCompose` | `T -> CompletableFuture<U>` | 对结果调用函数并执行返回的 future。 |
| `handle` | `(T, Throwable) -> U` | 处理结果或错误并产生新的结果。 |
| `whenComplete` | `(T, Throwable) -> void` | 类似于 `handle`，但结果为 `void`。 |
| `exceptionally` | `Throwable -> T` | 根据错误计算出结果。 |
| `completeOnTimeout` | `T, long, TimeUnit` | 在超时的情况下，将给定的值作为结果返回。 |
| `orTimeout` | `long, TimeUnit` | 在超时的情况下抛出一个 `TimeoutException`。 |
| `thenRun` | `Runnable` | 执行 `Runnable`，结果为 `void`。 |

现在让我们来看看组合多个 future 的方法（见表12.4）。

前三个方法会并发运行一个 `CompletableFuture<T>` 和一个 `CompletableFuture<U>` 动作，并组合结果。

接下来三个方法会并发运行两个 `CompletableFuture<T>` 动作。只要其中一个完成，其结果就会被传递，另一个结果则被忽略。

