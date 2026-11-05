

## 16. 委托：像变量一样传递函数

C# 中的委托是指向方法的类型安全指针。它们允许你将方法作为参数传递，或将方法存储在变量中。

下面是一个基本示例，说明如何定义委托、将其关联到方法并调用它。

[代码示例]

```
using System;

class Program
{
    // Define a delegate type that takes two integers and returns an integer
    delegate int Operation(int x, int y);

    // Method to add two numbers
    static int Add(int a, int b)
    {
        return a + b;
    }

    static void Main()
    {
        // Create a delegate instance and point it to the Add method
        Operation op = Add;

        // Call the method via the delegate
        int result = op(5, 3);
        Console.WriteLine(result); // Output: 8
    }
}
```

[执行结果]

delegate int Operation(int x, int y); 声明一个委托类型，该类型期望一个具有两个 int 参数并返回 int 的方法。

Operation op = Add; 将委托绑定到 Add 方法。

op(5, 3) 通过委托间接调用 Add(5, 3)。

这在功能上类似于 C++ 中的函数指针，但具有类型安全性且更安全。

实际用例包括：

- 将逻辑传入方法（例如用于排序的比较规则）。
- 实现事件系统（委托是 C# 事件的核心）。
- 在运行时动态接入不同的行为。

### [补充]

委托是 C# 中事件的基础。

Action<>、Func<> 和 Predicate<> 是内置泛型委托，可简化委托的使用。

匿名方法和 lambda 表达式也可以分配给委托。

委托支持解耦——你的代码变得更灵活、更易于测试。

## 17. 使用委托和事件实现观察者模式

在 C# 中，事件使用委托实现观察者模式，该模式允许对象在发生某事时通知多个订阅者。

下面是一个基本示例，说明事件和委托如何工作以通知多个监听器有关更改。

[代码示例]

```csharp
using System;

// Define a delegate type
public delegate void NotificationHandler(string message);

// Publisher class
class Publisher
{
    // Declare an event using the delegate
    public event NotificationHandler OnNotify;
    public void DoSomething()
    {
        Console.WriteLine("Publisher is doing something important...");
        // Notify all subscribers
        OnNotify?.Invoke("Something happened in Publisher!");
    }
}

// Subscriber class
class Subscriber
{
    private string _name;
    public Subscriber(string name)
    {
        _name = name;
    }
    // Method that matches the delegate signature
    public void Respond(string message)
    {
        Console.WriteLine($"{_name} received: {message}");
    }
}

// Main execution
class Program
{
    static void Main()
    {
        Publisher pub = new Publisher();
        Subscriber sub1 = new Subscriber("Alice");
        Subscriber sub2 = new Subscriber("Bob");
        // Subscribe to the event
        pub.OnNotify += sub1.Respond;
        pub.OnNotify += sub2.Respond;
        // Trigger the event
        pub.DoSomething();
    }
}
```

[执行结果]

Publisher is doing something important...
Alice received: Something happened in Publisher!
Bob received: Something happened in Publisher!

## 18. 使用 async 和 await 实现非阻塞代码

C# 支持使用 async 和 await 进行异步编程，以避免阻塞主线程，尤其是在 Web 请求或文件访问等 I/O 操作期间。

下面是一个简单示例，模拟异步等待任务完成而不会冻结应用。

[代码示例]

```
using System;
using System.Threading.Tasks;
class Program
{
static async Task Main()
{
Console.WriteLine("Starting...");
// Call an async method and await its completion
string result = await DoWorkAsync();
Console.WriteLine($"Result: {result}");
Console.WriteLine("Done.");
}
// Asynchronous method
static async Task<string> DoWorkAsync()
{
Console.WriteLine("Working...");
// Simulate delay (e.g., downloading, processing)
await Task.Delay(2000); // 2 seconds
return "Work complete!";
}
}
```

[执行结果]

Starting...
Working...
（2 秒后出现结果）
Result: Work complete!
Done.

使用 async 和 await 时，代码看起来是同步的，但在底层异步运行：

- 方法前面的 async 告诉编译器此方法可能会异步运行。
- await 会暂停执行，直到等待的任务完成，但不会阻塞主线程。
- Task.Delay() 类似于 Thread.Sleep()，但不会阻塞——它在等待时将控制权交还给运行时。
- 这在 UI 应用或服务器中尤其有用，因为阻塞主线程会导致应用冻结或造成延迟。
- 关键优势：可读且易于维护的异步代码。

### [补充]

async 方法必须返回 Task、Task<T> 或 void（仅限事件处理程序）。

## 19. 在 C# 中使用任务进行异步编程

TAP（基于任务的异步模式）是在 C# 中编写异步代码的标准方式。它使用 async 和 await 简化并发。

下面是一个简单示例，它异步获取数据，并使用 Task 和 await 等待结果。

[代码示例]

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;
class Program
{
    // Main method must return Task if marked async
    static async Task Main()
    {
        Console.WriteLine("Starting async operation...");
        // Call an asynchronous method
        string data = await GetDataAsync();
        Console.WriteLine("Data received:");
        Console.WriteLine(data);
    }
    // Async method that returns a Task<string>
    static async Task<string> GetDataAsync()
    {
        using HttpClient client = new HttpClient();
        // Await a non-blocking network call
        string result = await client.GetStringAsync("https://example.com");
        return result;
    }
}
```

[执行结果]

Starting async operation...

Data received:

```
<!doctype html><html>...<body>Example Domain...</body></html>
```

async 将方法标记为异步。

await 会暂停执行，直到等待的任务完成——而不会阻塞线程。

HttpClient.GetStringAsync() 是非阻塞的，并返回一个 Task<string>。

此模式可让你保持应用响应性（例如，UI 保持流畅，或后端不会冻结）。

async 方法必须返回 Task 或 Task<T>（返回 void 的事件处理程序除外）。

现代 C# 中的 Main() 现在可以是 async Task Main()（如上所示）。

### [补充]

TAP 取代了 APM（异步编程模型）和 EAP（基于事件的异步模式）等较旧模型。

你可以串联多个 async 调用，并且使用 try-catch 进行错误处理可与 await 自然配合。

应避免在 Task 上使用 .Result 或 .Wait()，除非绝对必要，因为它们可能导致死锁。

## 20. 在 C# 中使用 lock 防止竞态条件

C# 中的 lock 关键字用于确保一次只有一个线程访问某个代码块，从而防止竞态条件。

下面是一个示例，它使用 lock 从多个线程安全地递增计数器。

[代码示例]

```csharp
using System;
using System.Threading;
class Program
{
static int counter = 0; // Shared data
static object locker = new object(); // Lock object
static void Main()
{
Thread[] threads = new Thread[10];
// Create and start 10 threads
for (int i = 0; i < 10; i++)
{
threads[i] = new Thread(IncrementCounter);
threads[i].Start();
}
// Wait for all threads to finish
foreach (var thread in threads)
{
thread.Join();
}
Console.WriteLine("Final counter value: " + counter);
}
static void IncrementCounter()
{
    for (int i = 0; i < 1000; i++)
    {
        lock (locker)
        {
            // Only one thread can access this at a time
            counter++;
        }
    }
}
}
```

[执行结果]

Final counter value: 10000

如果不使用 lock，多个线程可能同时读取和写入 counter，导致结果不正确（竞态条件）。

lock (locker) 确保任意时刻只有一个线程可以执行其中的代码。

locker 必须是私有的、非空引用类型对象。它不应是值类型或可公开访问的对象。

Join() 用于在打印结果之前等待线程完成。

### [补充]

lock 是 Monitor.Enter() 和 Monitor.Exit() 的语法糖。

