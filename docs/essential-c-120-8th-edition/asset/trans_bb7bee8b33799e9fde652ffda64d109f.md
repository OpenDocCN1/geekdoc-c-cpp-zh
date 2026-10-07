

# 第 20 章：基于任务的异步模式

.Unwrap()
.ContinueWith(antecedent) =>

```csharp
int textOccurrenceCount = antecedent.Result;
Console.WriteLine(
  $"{Environment.NewLine}{findText} appears {textOccurrenceCount} times at URL '{url}';");

try {
  while (!task.Wait(100)) {
    Console.Write(".*");
  }
} catch (AggregateException exception) {
  exception.Flatten();
  try {
    exception.Handle(innerException => {
      // 重新抛出异常而不是使用
      // 对类型进行判断
      ExceptionDispatchInfo.Capture(innerException)
      .Throw();
      return true;
    });
  } catch (HttpRequestException) {
    // ...
  } catch (IOException) {
    // ...
  }
}
```

```csharp
private static async Task<int> CountOccurrencesAsync(byte[] downloadData, string findText) {
```

# 使用 TPL 异步调用高延迟操作

```csharp
// ...
}
```

相关的输出基本上与输出 20.1 相同，不同在于“Downloading...” 和“Searching...” 之后预计会有额外的点号，这取决于这些操作执行所需的时间。

当执行列表 20.2 时，它会在文件下载期间，向控制台打印“Downloading...”并带有额外的点号；“Searching....” 发生的情况也是类似的。结果不再是简单地在控制台打印四个点号（....），而是列表 20.2 也会在下载文件和搜索其文本所需的任何时间内持续打印点号。

遗憾的是，这种异步性伴随着中断执行流的相关代码。异步版本的代码并不是简单地在调用 `HttpClient.GetByteArrayAsync(url)` 之后紧跟计数次数的语句（调用 `CountOccurrences()` 的异步版本），而是需要 `ContinueWith()` 语句、为了简便起见而调用的 `Unwrap()` 方法，以及一套复杂的 `try/catch` 处理系统。细节在“高级主题：TPL 异步请求的复杂性”中概述。在此可以说，你将非常感激带有 `async/await` 的基于任务的异步模式。

# 高级主题

# TPL 异步请求的复杂性

第一个 `ContinueWith()` 语句确定了在 `HttpClient.GetByteArrayAsync(url)` 之后要执行的内容。注意第一个 `ContinueWith()` 中的返回语句返回了 `CountOccurrencesAsync(downloadData, findText)`，它返回另一个任务，特别是 `Task<int>`。因此，第一个 `ContinueWith()` 语句的返回类型是 `Task<Task<byte[]>>`。

2. 引入于 C# 5.0。

因此有了 `Unwrap()` 调用：如果没有它，第二个 `ContinueWith()` 语句中的 `antecedent` 也是 `Task<Task<byte>>`，这本身就说明了复杂性。结果是，必须调用两次 `Result`——一次直接针对 `antecedent`，第二次针对 `Task<byte[]>.Result` 属性的 `antecedent.Result`。后一次调用会阻塞后续执行，直到 `GetByteArrayAsync()` 操作完成。为了避免 `Task<Task<TResult>>` 结构，我们在第二次调用 `ContinueWith()` 之前先调用 `Unwrap()`，从而剥离了外层的 `Task` 并适当处理任何错误或取消请求。

然而，复杂性并不仅限于任务和 `ContinueWith()`：异常处理为复杂性增加了一个全新的维度。正如前面提到的，由于异步操作可能会遇到多个异常，TPL 通常会抛出 `AggregateException` 异常。但是，由于我们在 `ContinueWith()` 块内部调用了 `Result` 属性，我们可能也会在工作线程内部抛出 `AggregateException`。

正如你在前面的章节中学习到的样，有多种方法处理这些异常：

- 1. 我们可以为所有返回任务的*异步方法*以及每个 `ContinueWith()` 方法调用添加后续任务。然而，这样做将阻止我们使用流式 API（在其中 `ContinueWith()` 语句被一个接一个地链联）。此外，这将迫使我们将异常处理逻辑深度嵌入执行流中，而不是简单地依赖于 `await`。

- 2. 我们可以使用 `try/catch` 块包裹每个委托体。不幸的是，这种方法也不理想。首先，从 `antecedent.Result` 触发的异常会抛出 `AggregateException`，我们需要解包它们来单独处理。其次，每个委托体都需要一个独立的 `try/catch` 处理器，即使某些块的异常类型是相同的。第三，`Main` 对 `Wait()` 的调用仍然可能抛出异常，因为没有方法将后者包裹在 `try/catch` 块中。 

- 3. 在列表 20.2 中，我们并不捕捉 `GetByteArrayAsync()` 抛出的异常，而是完全依赖包裹 `Main.Wait()` 的 `try/catch` 块。考虑到异常将 `AggregateException`，在 `catch` 块中，我们通过调用 `AggregateException.Handle()` 来处理异常。这些异常随后会被异常处理器捕获并进行相应的处理。然而，在处理 `AggregateException.InnerExceptions` 之前，我们首先调用 `AggregateException.Flatten()`。这一步确保了所有异常都移动到了第一层并移除了 AggregateException。

如列表 20.2 所示，选项 3 可能是首选方法，因为它大多数情况下将异常处理保持在执行流之外。这并没有消除处理的复杂性，而是减少了它在常规执行流中的出现。

总之，尽管列表 20.2 的异步版本与列表 20.1 的同步版本逻辑执行流几乎相同，两个版本都尝试从服务器下载资源。如果下载成功，则返回结果；如果下载失败，则查询异常类型以确定正确的行动方案。显然，列表 20.2 的异步版本比列表 20.1 对应的同步版本更难阅读、理解和修改。与使用标准流语句的同步版本不同，异步版本被迫创建多个 Lambda 表达式以委托的形式表示后续逻辑。

而且这还是一个相对简单的示例，特别是我们还没有列出 `CountOccurrencesAsync()` 的实现。想象一下，如果异步代码包含（例如）一个在操作失败时重试三次的循环、尝试连接多个不同的服务器、获取一个资源集合而不是单个资源，或者所有这些可能的情况同时发生。将这些功能添加到同步版本中是直观的，但在异步版本中并不清楚如何做到。

# 使用 async 和 await 的基于任务的异步模式

为了解决复杂性问题，列表 20.3 也提供了异步执行，但使用了基于任务的异步性，它利用了 `async/await` 特性。³通过 `async/await`，编译器处理复杂性，让开发者能够专注于业务逻辑。与其担心 `ContinueWith()` 语句、获取 `antecedent.Result`、`Unwrap()` 调用、复杂的错误处理等，`async/await` 允许你只需在代码上标记简单的语法，告知编译器应该处理这些复杂性。此外，当任务完成且额外的

+3. 引入于 C# 5.0。

