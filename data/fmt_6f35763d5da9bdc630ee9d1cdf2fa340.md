
注意 C# 的 `using` 语句支持初始化多个变量的能力，只要这些变量都是同一种类型。它还支持直接使用一个已经初始化的变量。有关此主题的更多信息，请参阅《C# 程序员参考》中的“Using 语句”主题。

`using` 语句也适用于实现了 `IDisposable` 接口的值类型。这允许你创建一个极其高效且实用的机制，来封装用于开始和结束操作所需的代码。例如，假设你想通过使用 `Mutex` 来锁定一段代码。`Mutex` 也实现了 `IDisposable` 接口，对它调用 `Dispose` 可以释放原生资源；这与锁本身无关。为了简化 `Mutex` 锁定和解锁的语法，你可以定义一个封装了 `Mutex` 对象锁定和解锁的值类型。下面的 `MutexLock` 结构就是此类示例，`Main` 方法演示了如何使用 `MutexLock`：

```csharp
using System;
using System.Threading;

// 此值类型封装了互斥锁锁定和解锁
internal struct MutexLock : IDisposable {
    private readonly Mutex m_mutex;

    // 此构造函数获取互斥锁的锁
    public MutexLock(Mutex m) {
        m_mutex = m;
        m_mutex.WaitOne();
    }

    // 此 Dispose 方法释放互斥锁的锁
    public void Dispose() {
        m_mutex.ReleaseMutex();
    }
}

public static class Program {
    public static void Main() {
        // 构建一个互斥锁对象
        Mutex m = new Mutex();

        // 锁定互斥锁，执行某些操作，然后解锁
        using (new MutexLock(m)) {
            // 在此处执行某些线程安全的操作...
        }
    }
}
```

# 一个有趣的依赖问题

`System.IO.FileSystem` 类型允许用户打开文件进行读写。为了提高性能，该类型的实现使用了内存缓冲区。只有当缓冲区满时，该类型才会将缓冲区的内容刷新到文件中。`FileStream` 仅支持写入字节。如果你想写入字符和字符串，可以使用 `System.IO.StreamWriter`，如下面的代码所示：

```csharp
FileStream fs = new FileStream("Data.dat", FileMode.Create);
StreamWriter sw = new StreamWriter(fs);
sw.Write("Hi here");
```

```csharp
// 下面调用 Close 是你应该做的。
sw.Close();
// 注意：StreamWriter.Close 会关闭 FileStream;
// FileStream 不需要显式关闭。
```
