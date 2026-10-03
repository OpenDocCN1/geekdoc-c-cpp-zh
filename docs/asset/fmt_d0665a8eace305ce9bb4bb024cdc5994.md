
## PlaceOrders 方法

在表单代码后文件中添加 `PlaceOrders` 方法；它将订单添加到 `orders` 队列中，并为每个订单分配一个唯一的订单 ID 和从菜单中随机选择的菜肴。

为了能够取消 `while` 循环订单，可以使用传递给方法的 `CancellationToken` 实例的 `IsCancellationRequested` 属性，以检查是否已通过点击 Cancel 按钮发出了取消请求。

使用 `try/catch` 块忽略任何异常，并且仅在没有抛出异常时才在 `try` 块中将订单添加到队列。

添加 `Thread.Sleep(300)` 方法来模拟注册订单需要一段时间。使用 `Random` 类生成从 1 到菜单集合中项目数量的随机数；此 ID 将被用于从 `menu` 集合中获取菜肴。

创建一个新的 `Order` 实例，并将订单 ID 和菜肴传递给其构造函数；将订单添加到 `orders` 队列。

将订单 ID 加 1。

- 在表单代码后文件中添加一个带有 `CancellationToken` 参数 `token` 的私有 void 方法 `PlaceOrders`。
- 添加一个带有 `orderId` 变量的 `while` 循环并将其赋值为 1。
- 添加一个只要 `token` 未被取消就一直迭代的 `while` 循环。
- 在 `while` 循环中使用 `try/catch` 块忽略任何异常。
- 添加 `Thread.Sleep(300)` 方法来模拟注册订单需要一段时间。
- 使用 `Random` 类生成从 1 到菜单集合中项目数量的随机数；此 ID 将被用于从 `menu` 集合中获取菜肴。
- 创建一个新的 `Order` 实例并将订单 ID 和菜肴传递给其构造函数；将订单添加到 `orders` 队列。
- 将订单 ID 加 1。

`PlaceOrders` 的完整代码如下：

```csharp
private void PlaceOrders(CancellationToken token)
{
    int orderId = 1;
    while (!token.IsCancellationRequested)
    {
        try
        {
            Thread.Sleep(300);
            Random random = new Random();
            int idx = random.Next(1, menu.Count + 1);
            Dish dish = menu.First(m => m.Id == idx);
            Order order = new Order(orderId, dish);
            orders.Enqueue(order);
            orderId++;
        }
        catch { }
    }
}
```

## ProcessOrders 方法

在表单代码后文件中添加 `ProcessOrders` 方法；它将从 `orders` 队列中提取订单并在列表框中显示服务员名称。只要没有发出取消请求就一直迭代的 `while` 循环将使用传递给方法的 `CancellationToken`。在每次迭代中，服务员将尝试从 `orders` 队列中提取一个订单；如果成功，将把人员名称添加到订单中，并调用 `Action<string>` 委托来显示信息。为了进行跨线程调用，你需要使用表单的 `BeginInvoke` 方法。

- 在代码后文件中添加一个带有 `string` 参数 `name` 和 `CancellationToken` 参数 `token` 的方法 `ProcessOrders` 方法。
- 添加一个 `Action<string>` 委托 `AddToList`。
- 添加一个 `Order` 变量 `order`，用于从 `orders` 队列中提取下一个订单。
- 添加一个只要 `token` 参数未发出取消请求就一直迭代的 `while` 循环。
- 在 `while` 循环中添加一个 `if` 语句，当成功从 `orders` 队列中提取订单时执行。
- 在 `if` 块中将人员名称添加到订单。
- 从列表框调用方法的 `BeginInvoke` 方法来激活 `Action<string>` 委托，该委托调用提取出的 `order` 对象的 `OrderInfo` 值。

`ProcessOrders` 的完整代码如下：

```csharp
private void ProcessOrders(string name, CancellationToken token)
{
    Action<string> AddToList = orderInfo => 1stOrders.Items.Add(orderInfo);
    Order order;
    while (!token.IsCancellationRequested)
    {
        if (orders.Dequeue(out order))
        {
            order.Waiter = name;
            this.BeginInvoke(AddToList, new object[] { order.OrderInfo });
        }
    }
}
```

## OpenRestaurant 方法

此方法将启动一个任务，该任务将订单添加到订单队列，并启动服务员和女员在服务客户时从订单队列中取出订单时使用的任务。

必须为 `CancellationToken` 变量创建一个令牌，该令牌将作为参数传递给任务方法，从而能够取消正在运行的任务并关闭餐厅。

- 在表单的代码后（code-behind）中添加一个名为 `OpenRestaurant` 的无参数私有 void 方法。
- 使用 `ct = cts.Token;` 为 `CancellationToken` 变量创建一个令牌。
- 添加一个执行 `PlaceOrders` 方法的任务，并传入 `CancellationToken` 变量。
  `Task.Run(() => PlaceOrders(ct));`
- 添加三个执行 `ProcessOrders` 方法的任务，并传入服务员或女员的名字（Carl, Mary 和 Lisa）以及 `CancellationToken` 变量。
  `Task.Run(() => ProcessOrders("Carl", ct));`

`OpenRestaurant` 方法的完整代码如下：

```csharp
private void OpenRestaurant()
{
    ct = cts.Token;
    Task.Run(() => PlaceOrders(ct));
    Task.Run(() => ProcessOrders("Carl", ct));
    Task.Run(() => ProcessOrders("Lisa", ct));
    Task.Run(() => ProcessOrders("Mary", ct));
}
```

## btnStart_Click 事件

当用户点击按钮时，餐厅打开并使用 Task 调用了 `OpenRestaurant` 方法。按钮在被点击后应该设为禁用状态。

- 在表单的代码后中找到 `btnStart_Click` 事件。
- 添加一个 `try/catch` 块，其中 `catch` 块忽略所有异常。
- 添加一个执行 `OpenRestaurant` 方法的任务。
- 禁用按钮。

`btnStart_Click` 事件的完整代码如下：

```csharp
private void btnStart_Click(object sender, EventArgs e)
{
    try
    {
        Task.Run(() => OpenRestaurant());
        btnStart.Enabled = false;
    }
    catch
    {
    }
}
```

## btnCancel_Click 事件

点击此将通过调用 `CancellationSource` 实例上的 `Cancel` 方法来关闭餐厅。按钮在被点击后应该设为禁用状态。

- 在表单的代码后中找到 `btnCancel_Click` 事件。
- 添加一个 `try/catch` 块，其中 `catch` 块忽略所有异常。
- 调用 `CancellationSource` 实例上的 `Cancel` 方法。
- 禁用按钮。

`btnCancel_Click` 事件的完整代码如下：

```csharp
private void btnCancel_Click(object sender, EventArgs e)
{
    try
    {
        cts.Cancel();
        btnCancel.Enabled = false;
    }
    catch
    {
    }
}
```

## 18. Async（异步）

### 介绍

当你希望在启动操作的线程之外执行某个操作，且不想等待初始线程完成时，异步操作就是答案。

.NET Framework 4.5 比以前更容易创建异步操作；在后台创建任务的操作，以及 `async` 关键字让你能够在不阻塞线程的情况下创建异步操作，而 `await` 关键字则等待结果，这一切都在同一个方法内完成。

### async 和 await

在 .NET Framework 4.5 中，引入了 `async` 和 `await` 关键字；它们让编写异步操作变得简单得多。你使用 `await` 关键字来挂起带有 `async` 修饰符的方法执行，直到一个长时间运行的任务完成；在异步方法挂起期间，主线程可以继续它的工作。

使用 `async` 和 `await` 运行异步操作的独特之处在于，它们允许你在单个线程上运行异步操作；这使得它们在从异步操作更新 GUI 时特别有用。

### 阻塞 GUI 线程

当执行此代码时，GUI 线程将被阻塞，直到 Task 完成。

```csharp
public partial class Form1 : Form
{
    private void btnBlockingUIThread_Click(object sender, EventArgs e)
    {
        Task<string> task = Task.Run<string>(() =>
        {
            Thread.Sleep(5000);
            return "Finished";
        });

        // 阻塞 UI 线程，直到任务完成。
        lbl1Result.Text = task.Result;
    }
}
```

### 挂起执行

为了挂起执行并让 GUI 线程继续工作，你使用 `async` `await` 关键字。注意 `async` 关键字用于修饰方法头。

```csharp
public partial class Form1 : Form
{
    private async void btnAsyncAndAwait_Click(object sender, EventArgs e)
    {
        Task<string> task = Task.Run(() =>
        {
            Thread.Sleep(5000);
            return "Finished";
        });

        // 当 Task 有结果时将被调用
        lbl1Result.Text = await task;
    }
}
```

进阶阅读：“使用 Async and Await 进行异步编程 (C# 和 Visual Basic)”

### 可等待方法 (Awaitable methods)

`await` 操作符以非锁定的方式等待 Task 完成。可等待的方法对于 `void` 方法应返回 `Task`，对于返回结果的方法应返回 `Task<TResult>`；唯一的一个例外是允许返回 `void` 的事件方法。

此代码展示了一个同步方法的实现，在下一个示例中将其修改为异步方法。

```csharp
public partial class Form1 : Form
{
    private Student GetDataSynchronous()
    {
        var task = Task.Run<Student>(() =>
        {
            Thread.Sleep(3000);
            return new Student
            {
                FirstName = "Jonas"
            };
        });
        return task.Result;
    }
}
```

下面的代码展示了一个返回值的异步方法的实现。注意异步方法和事件方法必须用 `async` 关键字修饰，并在事件方法调用异步方法时使用 `await` 操作符。标签的 `Text` 属性将在异步方法完成后赋值。

```csharp
public partial class Form1 : Form
{
    private async Task<Student> GetDataAsynchronously()
    {
        var task = await Task.Run<Student>(() =>
        {
            Thread.Sleep(3000);
            return new Student { FirstName = "Jonas" };
        });
        return task;
    }

    private async void btnAwaitableMethod_Click(object sender, EventArgs e)
    {
        var student = await GetDataAsynchronously();
        lblResult.Text = student.FirstName;
    }
}
```

进阶阅读：“异步返回类型 (C# 和 Visual Basic)”

### 回调方法 (Callback methods)

你可以配置异步操作在任务完成时调用回调方法；异步方法可以将数据传递给回调方法，由该方法处理信息或更新 GUI。

必须创建一个委托来处理回调方法，并将其作为参数传递给异步方法。回调方法通常带有参数并返回 `void`；这使得在声明回调方法时 `Action<T>` 委托非常合适，因为它接受最多 16 个类型参数，T 是你想要返回类型。

在以下示例中，我们使用异步方法注册了一个新学生，并在回调方法中通过消息框向用户确认学生已添加。

当点击按钮时，使用 `await` 关键字异步调用 `EnrollStudent` 方法，并将回调方法和学生姓名作为其参数。

`EnrollStudent` 方法使用 `async` 关键字声明并返回 `Task`，使其成为异步方法。处理传入回调方法指针的参数声明为 `Action<Student>`，它将接收一个 `Student` 实例作为参数。

在 `EnrollStudent` 方法中，一个等待的 Task 将新学生添加到 `Students` 集合（或现实场景中的数据库表）中并返回 `Student` 对象。然后另一个等待的 Task 将以 `Student` 对象作为参数执行回调方法。

当这两个任务都完成后，`EnrollStudent` 方法将完成它的工作。

在 `DisplayStudentCallback` 方法中，消息框显示了新注册的学生。

```csharp
public partial class Form1 : Form
{
    List<Student> Students = new List<Student>();

    private async void btnCallbackMethod_Click(object sender, EventArgs e)
    {
        await EnrollStudent(DisplayStudentCallback, "Lisa", "Smith");
    }

    private async Task EnrollStudent(Action<Student> callback,
        string firstName, string lastName)
    {
        var student = await Task.Run(() =>
        {
            Students.Add(new Student
            {
                FirstName = firstName,
                LastName = lastName
            });
            return Students.Last();
        });

        // 异步调用回调方法。
        await Task.Run(() => callback(student));
    }

    private void DisplayStudentCallback(Student student)
    {
        MessageBox.Show($"Student enrolled: {student.FirstName} {student.LastName}");
    }
}
```
