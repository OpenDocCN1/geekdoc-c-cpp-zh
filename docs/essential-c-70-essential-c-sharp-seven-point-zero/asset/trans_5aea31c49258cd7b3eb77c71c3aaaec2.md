

public class Program
{
    private static async Task WriteWebRequestSizeAsync(
        string url)
    {
        try
        {
            WebRequest webRequest =
                WebRequest.Create(url);
            WebResponse response =
                await webRequest.GetResponseAsync();
            using (StreamReader reader =
                new StreamReader(
                    response.GetResponseStream()))
            {
                string text =
                    await reader.ReadToEndAsync();
                Console.WriteLine(
                    FormatBytes(text.Length));
            }
        }
        catch (WebException)
        {
            // ...
        }
        catch (IOException)
        {
            // ...
        }
        catch (NotSupportedException)
        {
            // ...
        }
    }

    public static void Main(string[] args)
    {
        string url = "http://www.IntelliTect.com";
        if (args.Length > 0)
        {
            url = args[0];
        }

        Console.Write(url);

        Task task = WriteWebRequestSizeAsync(url);

        while (!task.Wait(100))
        {
            Console.Write(".");
        }

        // ...
    }
}

注意观察 Listing 19.13 和 Listing 19.15 之间的细微差异。首先，我们将 Web 请求功能的主体重构为一个新方法（*WriteWebRequestSizeAsync()*），并在方法的声明中添加了新的上下文关键字 *async*。装饰了该关键字的方法必须返回 *void*、*Task*、*Task<T>*，或者如 C# 7.0 中的 *ValueTask<T>*，9

在这种情况下，由于方法主体没有返回数据，但我们仍然希望具备向调用者返回有关异步活动的信息的能力，*WriteWebRequestSizeAsync()* 返回 *Task*。注意方法名的后缀是 *Async*；这个后缀并非必要，但通过这种方式标记异步方法是一种惯例，以便识别其异步行为。最后，在同步方法存在异步等价版本的所有位置，我们在调用异步版本之前插入新的上下文关键字 *await*。

注意，Listing 19.13 和 19.15 之间没有其他变化。异步方法版本似乎仍然返回与之前相同的数据类型——尽管实际上每个方法都返回一个 *Task<T>*。这并不是通过某种神奇的隐式类型转换实现的，*也不是*。*GetResponseAsync()* 的声明如下：

```csharp
public virtual Task<WebResponse> GetResponseAsync() { ... }
```

在调用点，我们将返回值赋值给 *WebResponse*：

```csharp
WebResponse response = await webRequest.GetResponseAsync()
```

*async* 上下文关键字扮演着关键角色，它向编译器发出信号，表明编译器应将表达式重写为一个状态机，以表示我们在 Listing 19.14 中看到的（以及更多的）所有控制流。

还要注意到 Listing 19.15 中相较于 Listing 19.14 的 *try/catch* 逻辑改进。在 Listing 19.15 中，没有捕获 *AggregateException*。*catch* 子句继续捕获预期的确切异常类型，无需解包内部异常。为了做到这一点，*await* 重写逻辑会获取任务中的第一个异常并抛出该异常——因此，被捕获的就是该异常。（相比之下，当你调用任务的 *Wait()* 方法时，异常会被收集到一个 *AggregateException* 中，并抛出该聚合异常。）其目的是让异步代码尽可能看起来像同步代码。

9. 从技术上讲，你还可以返回任何实现了 *GetAwaiter* 方法的类型。请参阅本章后面标题为“Awaiting Non-Task<T> or Values”的高级主题。

为了更好地解释控制流，Table 19.2 在单独的列中显示了每个任务，以及在每个任务上发生的执行过程。表格有助于消除一些重要的误解：

- **误解 #1：** 使用 `async` 关键字装饰的方法在被调用时会自动在工作线程上执行。这绝对是错误的；该方法正常执行，在调用线程上运行，如果实现中没有等待任何未完成的可等待任务，它将在同一线程上同步完成。是该方法的实现负责启动任何异步工作。仅仅使用 `async` 关键字并不会改变方法代码的执行位置。此外，从调用者的角度来看，对 `async` 方法的调用也没有什么特别之处；它是一个返回类型为 `Task` 的方法，被正常调用，并正常返回其返回类型的对象。
- **误解 #2：** `await` 关键字会导致当前线程阻塞，直到被等待的任务完成。这也绝对是错误的。如果你希望当前线程阻塞直到任务完成，请调用 `Wait()` 方法，正如我们之前描述的那样。事实上，`Main` 线程在等待其他任务完成时反复这样做。每次执行 `task.Wait(100)` 时，它都会阻塞。然而，一旦该调用完成，`while` 循环的主体与其他任务并发执行——而不是同步执行。`await` 关键字评估其后的表达式（通常类型为 `Task` 或 `Task<T>`），将延续体（continuation）添加到结果任务中，然后 *立即* 将控制权返回给调用者。任务的创建已启动了异步工作；`await` 关键字意味着开发人员希望该方法的调用者在此线程上继续执行其工作，同时异步工作被处理。在该异步工作完成后的某个时间点，执行将从 `await` 表达式后的控制点恢复。

事实上，`async` 关键字存在的主要原因有两个。首先，它向代码读者非常清晰地表明，后续的方法将被编译器自动重写。其次，它告知编译器，方法中 *await* 上下文关键字的使用应被视为异步控制流，而不是普通标识符。

## TABLE 19.2: 各任务内的控制流

| 描述 | Main() 线程 | GetResponseAsync() 任务 | ReadToEndAsync() 任务 |
| :--- | :--- | :--- | :--- |
| 执行正常进入 Main 并一直运行到第一个 Console.Write(url) 语句。调用了 WriteWebRequestSizeAsync()，因此控制流正常进入该方法。WriteWebRequestSizeAsync() 内的指令正常执行（仍在 Main() 线程上），包括调用 WebRequest.Create(url)。 | string url = "http://www.IntelliTect.com"; if (args.Length > 0) { url = args[0]; } Console.Write(url); Task task = WriteWebRequestSizeAsync(url); WebRequest webRequest = WebRequest.Create(url); | | |
| 第一个 await 修饰符开始生效，生成一个新的 Task，GetResponseAsync() 将在其中执行。假设它没有几乎瞬间执行完毕，控制流返回到 Main() 并开始执行 while 循环。一旦 GetResponseAsync() 任务完成，在同一任务内的执行继续，将所述任务的结果隐式赋值给 response 变量。然后从响应实例化 StreamReader。 | while (!task.Wait(100)) { Console.Write("."); } | WebResponse response = await webRequest.GetResponseAsync(); StreamReader reader = new StreamReader(response, GetResponseStream()); | |
| 当发生另一个 await 时，又创建了一个任务，这次是为了执行 ReadToEndAsync()。（在此期间，Main 的 while 循环继续执行。）一旦 ReadToEndAsync() 任务完成，结果被赋值给 text，然后其 Length 在控制台上显示。最后，task.Wait() 返回 true，进程执行完毕。 | | | string text = (await reader.ReadToEndAsync()); Console.WriteLine(FormatBytes(text.Length)); |

# 基于 Task 的异步模式

4.9

827

