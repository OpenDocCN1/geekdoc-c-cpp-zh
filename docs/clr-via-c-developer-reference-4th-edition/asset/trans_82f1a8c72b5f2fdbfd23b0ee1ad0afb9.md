
使用 C# 的 `fixed` 语句比分配固定的 GC 池更高效。其原理是 C# 编译器会在 `bytes` 局部变量上产生一个特殊的“固定（pinned）”标记。在垃圾回收期间，GC 会检查该根节点的内容，如果根不为空，它就知道在压缩阶段不要移动该变量所引用的对象。C# 编译器生成 IL 来初始化一个 IL 指令，在 `fixed` 块对象的地址处将 `bytes` 局部变量设回 `null`；编译器会生成 IL 直到 `fixed` 块结束，此时变量不再引用任何对象，从而允许对象在下一次垃圾回收时发生移动。

现在，让我们来谈另外两个标志：`Weak` 和 `WeakTrackResurrection`。这些标志可以用于与原生代码交互的场景，也可以用于仅使用托管代码的场景。`Weak` 标志在对象被确定为垃圾回收时通知你；但不保证对象的内存一定会被回收。`WeakTrackResurrection` 标志在对象的内存被回收时通知你。两者相比，`Weak` 标志的使用频率远比 `WeakTrackResurrection` 高得多。我从未在实际应用中见过这种 `WeakTrackResurrection` 标志。

假设 Object-A 定期调用 Object-B 的方法。然而，Object-A 持有 Object-B 引用的事实阻止了 Object-B 被垃圾回收，在某些场景下这并不是我们想要的；我们希望如果 Object-B 在托管堆中仍然存，Object-A 才调用它的方法。要实现这种场景，请使用 `GCHandle.Alloc` 并传递 Object-B 的引用和 `Weak` 标志。现在 Object-A 只持有返回的 `GCHandle` 实例而不是 Object-B。

此时，如果没有根节点持有它，Object-B 就可以被垃圾回收。当 Object-A 想调用 Object-B 的方法时，它会查询 `GCHandle` 的只读 `Target` 属性。如果该属性返回非空值，则 Object-B 仍然存活。Object-A 然后将返回的结果转换为 Object-B 的类型并调用方法。如果 `Target` 属性返回 `null`，则 Object-B 已被回收（但尚未终结），Object-A 将不会尝试调用该方法。此时，Object-A 的代码可能会调用 `GCHandle.Free` 来释放 `GCHandle` 实例。

由于处理 `GCHandle` 类型可能有些繁琐（因为需要提升权限在内存中保持或固定对象），`System` 命名空间包含了 `WeakReference<T>` 类来帮助你。

```csharp
public sealed class WeakReference<T> : ISerializable where T : class {
    public WeakReference(T target);
    public WeakReference(T target, bool trackResurrection);
    public void SetTarget(T target);
    public bool GetTarget(out T target);
}
```

这个类本质上只是 `GCHandle` 实例的面向对象的封装：逻辑上，它的构造函数调用了 `GCHandle.Alloc`，`GetTarget` 方法查询 `GCHandle` 的 `Target` 属性，`SetTarget` 方法设置 `GCHandle` 的 `Target` 属性，而它的 `Finalize` 方法对其进行保护。此外，使用 `WeakReference<T>` 类不需要特殊选项，因为该类只支持弱引用；它不支持通过 `GCHandleType.Normal` 或 `Pinned` 分配的 `GCHandle` 实例所提供的行为。`WeakReference<T>` 类的缺点是它的实例必须分配在堆上。`WeakReference<T>` 类比 `GCHandle` 实例要重得多。

**重要** 当开发者开始学习弱引用时，他们会立即认为自己正处于缓存场景中。例如，他们会认为构造一组包含大量数据的对象并对这些对象创建弱引用是很酷的特性。当程序需要数据时，程序检查弱引用以查看包含数据的对象是否还在，如果在，程序就使用它；程序将获得高性能。然而，如果发生了垃圾回收，包含数据的对象就会被销毁，程序必须重新创建数据，程序性能就会降低。

这样做的问题在于：垃圾回收并非只在内存满或接近满时发生。相反，每当某代（满时就会发生垃圾回收。因此，对象被逐内存的频率比预期的要高，你的应用程序性能受到很大影响。

弱引用可以在缓存场景中有效使用，但构建一个能够在内存消耗和速度之间找到平衡的良好缓存算法是非常复杂的。基本上，你希望缓存对所有对象都持有强引用，然后当你发现内存紧张时，将强引用转换为弱引用。CLR 没有提供机制来通知应用程序内存变紧张。但某些人通过调用 Win32 `GlobalMemoryStatus` 函数并返回 `MEMORYSTATUS` 结构的 `dwMemoryLoad` 成员取得了成功。如果该成员报告的值高于 80，说明内存正变得紧张，你可以根据使用的是最近最少使用（LRU）算法、最经常使用（MFU）算法或其他算法开始将字符串转换为弱引用。

开发者经常希望将一段数据与另一个实体关联。例如，你可以将数据与线程或 AppDomain 关联。使用 `System.Runtime.CompilerServices.ConditionalWeakTable<TKey, TValue>` 类也可以将数据与单个对象关联，它如下：

```csharp
public sealed class ConditionalWeakTable<TKey, TValue>
    where TKey : class where TValue : class {
        public ConditionalWeakTable();
        public void Add(TKey key, TValue value);
        public TValue GetValue(TKey key, CreateValueCallback<TKey, TValue> createValueCallback);
        public bool TryGetValue(TKey key, out TValue value);
        public TValue GetGetValue(TKey key);
        public TValue GetOrCreate(TKey key);
        public bool Remove(TKey key);

        public delegate TValue CreateCallback(TKey key); // 嵌套委托
    
```

如果你想与一个或多个对象关联任意数据，可以创建类的实例。然后调用 `Add` 方法，传递对象作为键以及你想与对象关联的数据。如果尝试对同一个对象添加多次，`Add` 方法将抛出 `ArgumentException`；要更改与对象关联的值，你必须移除键并重新添加。注意此类是线程安全的，因此多个线程可以并发使用，尽管该类的性能并不理想；你应该测试该类的性能以查看它是如何工作的。

当然，表内部存储了传入作为键的对象的 `WeakReference`；这确保了表不会强制保持对象存活。但 `ConditionalWeakTable` 类特殊之处在于，只要由键标识的对象在内存中，值就保证保留在内存中。因此这比普通的 `WeakReference` 更强大，因为如果是后者，即使键对象持续存在，值也可能被回收。`ConditionalWeakTable` 类可以用于实现 XAML 的依赖属性机制。它也可以用于动态语言动态地与对象关联数据。

这里是演示使用 `ConditionalWeakTable` 类的代码。它允许你对任何对象调用 `GCWatch` 扩展并传入 `String` 标签。每当特定对象被垃圾回收时，它会在控制窗口通知你。

```csharp
internal static class GCWatcher {
// 注意：字符串和 MarshalByRefObject 对象要小心
    private readonly static ConditionalWeakTable<Object, String> s_cwt = new ConditionalWeakTable<Object, String>();
    // ... 实现代码 ...
}
```

```csharp
private sealed class NotifyWhenGc<T> {
    private readonly T m_value;

    internal NotifyWhenGc(T value) { m_value = value; }
    public override string ToString() { return m_value.ToString(); }
    ~NotifyWhenGc() { Console.WriteLine("GC: " + m_value); }
}
```
