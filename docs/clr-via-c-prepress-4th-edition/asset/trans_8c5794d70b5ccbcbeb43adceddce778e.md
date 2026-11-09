

![](img/3f2c86949cdef7e2f9e27c37c607b28e_541_0.png)

**图 21-15** 第二次垃圾回收后托管堆的状态。

## 手动监控和控制对象的生存期

CLR 为每个 AppDomain 提供一个 GC 句柄表。该表允许应用程序监控对象的生存期或手动控制对象的生存期。创建 AppDomain 时，该表为空。表中的每个条目由托管堆上对象的引用和一个标志组成，该标志指示你是想监控还是控制该对象。应用程序通过下面显示的 System.Runtime.InteropServices.GCHandle 类型在表中添加和移除条目。

```csharp
// This type is defined in the System.Runtime.InteropServices namespace
public struct GCHandle {
   // Static methods that create an entry in the table
   public static GCHandle Alloc(object value);
   public static GCHandle Alloc(object value, GCHandleType type);

   // Static methods that convert a GCHandle to an IntPtr
   public static explicit operator IntPtr(GCHandle value);
   public static IntPtr ToIntPtr(GCHandle value);

   // Static methods that convert an IntPtr to a GCHandle
   public static explicit operator GCHandle(IntPtr value);
   public static GCHandle FromIntPtr(IntPtr value);

   // Static methods that compare two GCHandles
   public static Boolean operator ==(GCHandle a, GCHandle b);
   public static Boolean operator !=(GCHandle a, GCHandle b);

   // Instance method to free the entry in the table (index is set to 0)
   public void Free();

   // Instance property to get/set the entry's object reference
   public object Target { get; set; }

   // Instance property that returns true if index is not 0
   public Boolean IsAllocated { get; }

   // For a pinned entry, this returns the address of the object
   public IntPtr AddrOfPinnedObject();

   public override Int32 GetHashCode();
   public override Boolean Equals(object o);
}
```

基本上，要控制或监控对象的生存期，你需要调用 GCHandle 的静态 Alloc 方法，传入要监控/控制对象的引用，以及 GCHandleType。GCHandleType 是一个标志，指示你想如何监控/控制对象。GCHandleType 类型是一个枚举类型，定义如下：

```csharp
public enum GCHandleType {
    Weak = 0,                    // Used for monitoring an object’s existence
    WeakTrackResurrection = 1,   // Used for monitoring an object’s death
    Normal = 2,                   // Used for controlling an object’s lifetime
    Pinned = 3                    // Used for controlling an object’s lifetime
}
```

现在，下面解释每个标志的含义：

- **Weak（弱）** 此标志允许你*监控*对象的生存期。具体来说，你可以检测垃圾回收器何时确定该对象已无法从应用程序代码中到达。请注意，对象的 `Finalize` 方法可能尚未执行或已经执行，因此该对象可能仍在内存中。
- **WeakTrackResurrection（弱跟踪复活）** 此标志允许你*监控*对象的生存期。具体来说，你可以检测垃圾回收器何时确定该对象已无法从应用程序代码中到达。请注意，对象的 `Finalize` 方法（如果存在）肯定已经执行，并且该对象的内存已被回收。
- **Normal（普通）** 此标志允许你*控制*对象的生存期。具体来说，你是在告诉垃圾回收器，即使应用程序中可能没有引用该对象的根，该对象也必须保留在内存中。当垃圾回收运行时，该对象的内存可以被压缩（移动）。不带 `GCHandleType` 标志的 Alloc 方法假定指定了 `GCHandleType.Normal`。
- **Pinned（固定）** 此标志允许你*控制*对象的生存期。具体来说，你是在告诉垃圾回收器，即使应用程序中可能没有引用该对象的根，该对象也必须保留在内存中。当垃圾回收运行时，该对象的内存不能被压缩。当你希望将内存地址交给本机代码时，这通常很有用。本机代码可以写入托管堆中的这块内存，因为它知道垃圾回收不会移动该对象。

当你调用 GCHandle 的静态 Alloc 方法时，它会扫描 AppDomain 的 GC 句柄表，查找一个可用条目，该条目中存储了你传给 Alloc 的对象引用，并且标志被设置为你传给 GCHandleType 参数的值。然后，Alloc 返回一个 GCHandle 实例给你。GCHandle 是一个轻量级值类型，包含一个实例字段 IntPtr，它指向表中条目的索引。当你想释放 GC 句柄表中的这个条目时，你获取 GCHandle 实例并调用 Free 方法（该方法还会通过将其 IntPtr 字段设置为零来使 GCHandle 实例失效）。

下面介绍垃圾回收器如何使用 GC 句柄表。当垃圾回收发生时：

1. 垃圾回收器标记所有可达对象（如本章开头所述）。然后，垃圾回收器扫描 GC 句柄表；所有 Normal 或 Pinned 对象都被视为根，这些对象也会被标记（包括这些对象通过其字段引用的任何对象）。
2. 垃圾回收器扫描 GC 句柄表，查找所有 Weak 条目。如果 Weak 条目引用了一个未标记的对象，则该引用标识的是一个不可达对象（垃圾），该条目的引用值会被更改为 null。
3. 垃圾回收器扫描终结列表。如果列表中的某个引用指向一个未标记的对象，则该引用标识的是一个不可达对象，该引用会从终结列表移到 freachable 队列。此时，该对象被标记，因为该对象现在被视为可达。
4. 垃圾回收器扫描 GC 句柄表，查找所有 WeakTrackResurrection 条目。如果 WeakTrackResurrection 条目引用了一个未标记的对象（现在该对象是由 freachable 队列中的条目引用的对象），则该引用标识的是一个不可达对象（垃圾），该条目的引用值会被更改为 null。
5. 垃圾回收器压缩内存，挤出不可达对象留下的空洞。Pinned 对象不会被压缩（移动）；垃圾回收器会移动它们周围的其他对象。

现在你已经理解了该机制，让我们看看何时使用它们。最容易理解的标志是 Normal 和 Pinned，所以我们先讨论这两个。这两个标志通常在与本机代码互操作时使用。

Normal 标志用于当你需要将指向托管对象的指针交给本机代码时，因为在将来的某个时刻，本机代码会回调托管代码，并将该指针传递回去。你实际上不能将指向托管对象的指针传递给本机代码，因为如果发生垃圾回收，对象可能会在内存中移动，从而使指针失效。为了解决这个问题，你可以调用 GCHandle 的 Alloc 方法，传入对象的引用和 Normal 标志。然后，你将返回的 GCHandle 实例转换为 IntPtr，并将 IntPtr 传给本机代码。当本机代码回调托管代码时，托管代码会将传入的 IntPtr 转换回 GCHandle，然后查询 Target 属性以获取托管对象的引用（或当前地址）。当本机代码不再需要该引用时，你调用 GCHandle 的 Free 方法，该方法允许将来的垃圾回收释放该对象（假设

```csharp
public Boolean TryGetTarget(out T target);
}
```

这个类实际上只是 `GCHandle` 实例的一个面向对象包装器：从逻辑上讲，其构造函数调用 `GCHandle` 的 `Alloc`，其 `TryGetTarget` 方法查询 `GCHandle` 的 `Target` 属性，其 `SetTarget` 方法设置 `GCHandle` 的 `Target` 属性，其 `Finalize` 方法（上面未显示，因为它是受保护的）调用 `GCHandle` 的 `Free` 方法。此外，代码使用 `WeakReference<T>` 类不需要特殊权限，因为该类只支持弱引用；它不支持以 `Normal` 或 `Pinned` 的 `GCHandleType` 分配的 `GCHandle` 实例所提供的行为。`WeakReference<T>` 类的缺点是必须在堆上分配它的实例。因此，`WeakReference<T>` 类比 `GCHandle` 实例更重量级。

**重要** 当开发人员开始学习弱引用时，他们立刻会想到弱引用在缓存场景中很有用。例如，他们认为可以构造一批包含大量数据的对象，然后为这些对象创建弱引用。当程序需要数据时，程序检查弱引用，看包含该数据的对象是否仍然存在；如果存在，程序就直接使用它，从而获得高性能。但是，如果发生了一次垃圾回收，包含数据的对象就会被销毁，当程序不得不重新创建数据时，程序体验到的性能就会降低。

这种技术的问题如下：垃圾回收并不仅仅在内存已满或接近满时发生。相反，只要第 0 代满了，垃圾回收就会发生。因此，对象被移出内存的频率远高于预期，应用程序的性能会大受影响。

弱引用在缓存场景中可以非常有效地使用，但构建一个好的缓存算法以在内存消耗和速度之间找到合适平衡是非常复杂的。基本上，你希望缓存对所有对象保持强引用，然后当你发现内存变得紧张时，开始将强引用转换为弱引用。目前，CLR 没有提供任何机制来通知应用程序内存变得紧张。但有些人通过定期调用 Win32 `GlobalMemoryStatusEx` 函数并检查返回的 `MEMORYSTATUSEX` 结构体的 `dwMemoryLoad` 成员取得了很大成功。如果该成员报告的值高于 80，内存就会变得紧张，你可以根据你想要最近最少使用算法、最常使用算法、基于时间的算法或其他算法，开始将强引用转换为弱引用。

开发人员经常希望将一段数据与另一个实体关联起来。例如，你可以将数据与线程或 `AppDomain` 关联。也可以使用 `System.Runtime.CompilerServices.ConditionalWeakTable<TKey, TValue>` 类将数据与单个对象关联，该类如下所示：

```csharp
public sealed class ConditionalWeakTable<TKey, TValue>
    where TKey : class where TValue : class {
    public ConditionalWeakTable();
    public void Add(TKey key, TValue value);
    public TValue GetValue(TKey key, CreateValueCallback<TKey, TValue> createValueCallback);
}
```

