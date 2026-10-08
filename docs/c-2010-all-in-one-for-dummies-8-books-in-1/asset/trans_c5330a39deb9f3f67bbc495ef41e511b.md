

## 174 泛型类：编写你自己的泛型

```csharp
Console.WriteLine(
  "向队列中添加随机数量 (0 - 20) 的随机包");
Package pack;
PackageFactory fact = new PackageFactory();
// 你想要一个小于 20 的随机数。
int numToCreate = rand.Next(20); // 0 - 20 之间的随机整数
Console.WriteLine("Creating packages: {}", numToCreate);
for (int i = 0; i < numToCreate; i++)
{
  Console.WriteLine("Generating and adding random package ({}), {})", i, i);
```

- Priority 枚举 -- 定义了一组优先级
- 与优先级 1, 2, 3, ... 不同，这些有具体的名称。
- 有关枚举的信息，
- 请参阅文章 Enumerating the Charms of the Enum
- enum Priority

```csharp
enum Priority
{
  Low, Medium, High
}
```

``` 

IPriorizable 接口 -- 定义了优先级排序的能力。
// 定义一个自定义接口：可以添加到
// PriorityQueue 的类必须实现此接口。
```csharp
interface IPriorizable
{
  Priority priority { get; } // 接口中属性的示例
}
```

```csharp
// PriorityQueue -- 一个泛型优先级队列类
// 添加到队列的类型“必须”实现 IPriorizable 接口。
class PriorityQueue<T> where T : IPriorizable
```

```csharp
// Queues -- 底层队列：全部是泛型的！
private Queue<T> _queueHigh = new Queue<T>();
private Queue<T> _queueMedium = new Queue<T>();
private Queue<T> _queueLow = new Queue<T>();
```

```csharp
// Enqueue -- 优先排序并添加到正确的队列；类型为 T 的项。
// 该项必须知道自己的优先级。
public void Enqueue(T item)
{
    switch (item.Priority) // 要求 IPriorizable 以确保此优先级。
    {
        case Priority.High:
            _queueHigh.Enqueue(item);
            break;
        case Priority.Medium:
            _queueMedium.Enqueue(item);
            break;
        case Priority.Low:
            _queueLow.Enqueue(item);
            break;
        default:
            throw new ArgumentOutOfRangeException(
                item.Priority.ToString(),
                "bad priority in PriorityQueue.Enqueue"
            );
    }
}
```

```csharp
// Dequeue -- 从可选最高优先级队列获取 T。
public T Dequeue()
{
    // 找到带有项的高优先级队列。
    Queue<T> queueTop = TopQueue();
    if (queueTop != null && queueTop.Count > 0)
    {
        return queueTop.Dequeue();
    }
    // 如果都为空，返回 null（你可以抛出异常）。
    return default(T); // 这是什么？见讨论部分。
}
```

```csharp
// TopQueue -- 带有项的底层队列的优先级是什么。
private Queue<T> TopQueue()
{
    if (_queueHigh.Count > 0) // 高优先级队列中有任何
        return _queueHigh;
    if (_queueMedium.Count > 0) // 中优先级队列中有任何
        return _queueMedium;
    if (_queueLow.Count > 0) // 低优先级队列中有任何
        return _queueLow;
    // 全部为空，返回一个空队列。
}
```

```csharp
// IsEmpty -- 检查是否有可出队的项。
public bool IsEmpty()
{
    // 如果所有队列都为空则返回 true
    return (_queueHigh.Count == 0) && (_queueMedium.Count == 0) &&
           (_queueLow.Count == 0);
}
```

```csharp
// Count - 队列中共有多少项。
public int Count // 一个只读属性。
{
    return _queueHigh.Count + _queueMedium.Count + _queueLow.Count;
}
```

PriorityQueue 稍微有点长，你可以看看这个。

```csharp
static void Main(string[] args)
{
    Console.WriteLine("创建一个优先级队列:");
    PriorityQueue<Package> pq = new PriorityQueue<Package>();
    Console.WriteLine();
    // 向队列中添加随机数量 (0 - 20) 的随机包：
    Package pack;
    PackageFactory fact = new PackageFactory();
    // 你想要一个小于 20 的随机数。
    Random rand = new Random();
    int numToCreate = rand.Next(20); // 0 - 20 之间的随机整数
    for (int i = 0; i < numToCreate; i++)
    {
        Console.WriteLine("正在生成并添加随机包 {}", i);
        pack = fact.CreatePackage();
        Console.WriteLine("添加的优先级为 {0}", pack.Priority);
        pq.Enqueue(pack);
    }

    Console.WriteLine("看看我们得到了什么:");
    int count = pq.Count;
    Console.WriteLine("收到的包: {0}", count);

    Console.WriteLine("移除随机数量的包 (0 - 20): {0}");
    int numToRemove = rand.Next(count);
    Console.WriteLine("正在移除 {0} 个包，{0}", numToRemove);
    for (int i = 0; i < numToRemove; i++)
    {
        pack = pq.Dequeue();
        if (pack != null)
        {
            Console.WriteLine("发出的包优先级为 {0}", pack.Priority);
        }
    }
    // 看看有多少包被“发货了”。
    Console.WriteLine("发出了 {0} 个包", count - pq.Count);
}

class Package : IPriorizable {
    // 优先级
    private Priority _priority;

    // 构造函数
    public Package(Priority priority) {
        _priority = priority;
    }

    // 返回优先级
    public Priority Priority() {
        return _priority;
    }
}

class PackageFactory {
    // 随机生成器
    Random _rand = new Random();

    // CreatePackage 方法选择一个优先级，
    // 然后创建一个该优先级的包。
    public Package CreatePackage() {
        // 需要 0, 1 或 2 (小于 3 的值)。
        int rand = _rand.Next(3);
        // 将 int 转换为枚举很笨拙，但它避免了
        // 使用 ifs 或 switch 语句。
        return new Package((Priority)rand);
    }
}
```

