
### 第 117.3 节：Parallel.Invoke

并行调用方法或操作（并行区域）

```csharp
static void Main()
{
    string[] urls =
    {
        "www.stackoverflow.com",
        "www.google.net",
        "www.facebook.com",
        "www.twitter.com"
    };

    System.Threading.Tasks.Parallel.Invoke(
        () => PingUrl(urls[0]),
        () => PingUrl(urls[1]),
        () => PingUrl(urls[2]),
        () => PingUrl(urls[3])
    );
}

void PingUrl(string url)
{
    var ping = new System.Net.NetworkInformation.Ping();

    var result = ping.Send(url);

    if (result.Status == System.Net.NetworkInformation.IPStatus.Success)
    {
        Console.WriteLine(string.Format("{0} is online", url));
    }
}
```

## 第 118 章：使变量线程安全

### 第 118.1 节：在 Parallel.For 循环中控制对变量的访问

```csharp
using System;
using System.Threading;
using System.Threading.Tasks;

class Program
{
    static void Main( string[] args )
    {
        object sync = new object();
        int sum = 0;
        Parallel.For( 1, 1000, ( i ) => {
            lock( sync ) sum = sum + i; // lock is necessary

            // As a practical matter, ensure this 'parallel for' executes
            // on multiple threads by simulating a lengthy operation.
            Thread.Sleep( 1 );
        } );
        Console.WriteLine( "Correct answer should be 499500.  sum is: {0}", sum );
    }
}
```

仅执行 sum = sum + i 而不使用 lock 是不够的，因为读-改-写操作不是原子的。一个线程会在读取 sum 的当前值之后，但在将修改后的值 sum + i 写回 sum 之前，覆盖 sum 的任何外部修改。

## 第 119 章：Lock 语句

### 第 119.1 节：在 lock 语句中抛出异常

以下代码将释放锁。不会有问题。在幕后，lock 语句的工作方式类似于 `try` `finally`

```csharp
lock(locker)
{
    throw new Exception();
}
```

更多内容可参见 [C# 5.0 规范](#)：

形式为的 lock 语句

```csharp
lock (x) ...
```

其中 x 是 *引用类型* 的表达式，精确等价于

```csharp
bool __lockWasTaken = false;
try {
    System.Threading.Monitor.Enter(x, ref __lockWasTaken);
    ...
}
finally {
    if (__lockWasTaken) System.Threading.Monitor.Exit(x);
}
```

只是 x 只会被求值一次。

### 第 119.2 节：简单用法

`lock` 的常见用法是临界区。

在以下示例中，`ReserveRoom` 应该从不同的线程调用。使用 `lock` 进行同步是在这里防止竞争条件的最简单方法。方法体被 `lock` 包围，这确保了两个或多个线程不能同时执行它。

```csharp
public class Hotel
{
    private readonly object _roomLock = new object();

    public void ReserveRoom(int roomNumber)
    {
        // lock keyword ensures that only one thread executes critical section at once
        // in this case, reserves a hotel room of given number
        // preventing double bookings
        lock (_roomLock)
        {
            // reserve room logic goes here
        }
    }
}
```

如果一个线程在另一个线程正在其中运行时到达 `lock` 块，前者将等待后者退出该块。

> 最佳实践是定义一个私有的用于加锁的对象，或一个私有的静态对象变量来保护所有实例共用的数据。

### 第 119.3 节：在 lock 语句中返回

以下代码将释放锁。

```csharp
lock(locker)
{
    return 5;
}
```

有关详细解释，建议参考此 SO 回答。

### 第 119.4 节：反模式和陷阱

#### 在栈分配的 / 局部变量上加锁

使用 lock 时的一个误区是在函数中使用局部对象作为锁。由于这些局部对象实例在函数的每次调用中都不同，lock 将不会按预期执行。

```csharp
List<string> stringList = new List<string>();

public void AddToListNotThreadSafe(string something)
{
    // DO NOT do this, as each call to this method
    // will lock on a different instance of an Object.
    // This provides no thread safety, it only degrades performance.
    var localLock = new Object();
    lock(localLock)
    {
        stringList.Add(something);
    }
}

// Define object that can be used for thread safety in the AddToList method
readonly object classLock = new object();

public void AddToList(List<string> stringList, string something)
{
    // USE THE classLock instance field to achieve a
    // thread-safe lock before adding to stringList
    lock(classLock)
    {
        stringList.Add(something);
    }
}
```

#### 假设加锁会限制对同步对象本身的访问

如果一个线程调用：lock(obj) 而另一个线程调用 obj.ToString()，第二个线程不会被阻塞。

```csharp
object obj = new Object();

public void SomeMethod()
{
    lock(obj)
    {
        //do dangerous stuff
    }
}

//Meanwhile on other thread
public void SomeOtherMethod()
{
    var objInString = obj.ToString(); //this does not block
}
```

#### 期待子类知道何时加锁

有时基类被设计成其子类在访问某些受保护字段时必须使用锁：

```csharp
public abstract class Base
{
    protected readonly object padlock;
    protected readonly List<string> list;

    public Base()
    {
        this.padlock = new object();
        this.list = new List<string>();
    }

    public abstract void Do();
}

public class Derived1 : Base
{
    public override void Do()
    {
        lock (this.padlock)
        {
            this.list.Add("Derived1");
        }
    }
}

public class Derived2 : Base
{
    public override void Do()
    {
        this.list.Add("Derived2"); // OOPS! I forgot to lock!
    }
}
```

使用模板方法封装加锁要安全得多：

```csharp
public abstract class Base
{
    private readonly object padlock; // This is now private
    protected readonly List<string> list;

    public Base()
    {
        this.padlock = new object();
        this.list = new List<string>();
    }

    public void Do()
    {
        lock (this.padlock) {
            this.DoInternal();
        }
    }

    protected abstract void DoInternal();
}

public class Derived1 : Base
{
    protected override void DoInternal()
    {
        this.list.Add("Derived1"); // Yay! No need to lock
    }
}
```

#### 对装箱的 ValueType 变量加锁不会同步

在以下示例中，一个私有变量在作为对象参数提供给函数时被隐式装箱，期望在该监视器资源上加锁。装箱发生在调用 IncInSync 函数之前，因此每次调用函数时装箱的实例都对应于不同的堆对象。

```csharp
public int Count { get; private set; }

private readonly int counterLock = 1;

public void Inc()
{
    IncInSync(counterLock);
}

private void IncInSync(object monitorResource)
{
    lock (monitorResource)
    {
        Count++;
    }
}
```

装箱发生在 Inc 函数中：

```
BulemicCounter.Inc:
IL_0000: nop
IL_0001: ldarg.0
IL_0002: ldarg.0
IL_0003: ldfld UserQuery+BulemicCounter.counterLock
IL_0008: box System.Int32
IL_000D: call UserQuery+BulemicCounter.IncInSync
IL_0012: nop
IL_0013: ret
```

这并不意味着装箱的 ValueType 完全不能用于监视器加锁：

```csharp
private readonly object counterLock = 1;
```

现在装箱发生在构造函数中，这对于加锁来说是可以的：

```
IL_0001:  ldc.i4.1
IL_0002:  box        System.Int32
IL_0007:  stfld      UserQuery+BulemicCounter.counterLock
```

#### 在存在更安全的替代方案时不必要地使用锁

一个非常常见的模式是在线程安全类中使用私有 List 或 Dictionary，并在每次访问时加锁：

```csharp
public class Cache
{
    private readonly object padlock;
    private readonly Dictionary<string, object> values;

    public WordStats()
    {
        this.padlock = new object();
        this.values = new Dictionary<string, object>();
    }

    public void Add(string key, object value)
    {
        lock (this.padlock)
        {
            this.values.Add(key, value);
        }
    }

    /* rest of class omitted */
}
```

如果有多个方法访问 values 字典，代码会变得很长，更重要的是，始终加锁会掩盖其意图。加锁也很容易忘记，而缺乏适当的加锁会导致难以找到的错误。

通过使用 ConcurrentDictionary，我们可以完全避免加锁：

```csharp
public class Cache
{
    private readonly ConcurrentDictionary<string, object> values;

    public WordStats()
    {
        this.values = new ConcurrentDictionary<string, object>();
    }

    public void Add(string key, object value)
    {
        this.values.Add(key, value);
    }

    /* rest of class omitted */
}
```

使用并发集合还能提高性能，因为它们或多或少都采用了无锁技术。
