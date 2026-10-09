
```
dispatch_queue_t notifyQueue = dispatch_get_main_queue();
dispatch_group_notify(dispatchGroup,
notifyQueue,
{
// 任务完成后继续处理
});
```

应该将 `notify` 回调放入队列的队列完全取决于具体情况。在这里，我展示了使用主队列，这是一个相当常见的用例。但它也可以是任何自定义串行队列或全局并发队列之一。

在这个示例中，分发到的队列对于所有任务都是同一个。但事实并非如此。你可能想让某些任务具有更高的优先级，但仍将它们全部分到同一个 `dispatch` 组中，并在全部完成后通知你：

```
dispatch_queue_t lowPriorityQueue =

dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_LOW, 0);
dispatch_queue_t highPriorityQueue =
dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_HIGH, 0);
dispatch_group_t dispatchGroup = dispatch_group_create();
```

```
for (id object in lowPriorityObjects) {
dispatch_group_async(dispatchGroup,
lowPriorityQueue,
^{ [object performTask]; });
}}
```

```
for (id object in highPriorityObjects) {
dispatch_group_async(dispatchGroup,
highPriorityQueue,
^{ [object performTask]; });
}}
```

```
dispatch_queue_t notifyQueue = dispatch_get_main_queue();
dispatch_group_notify(dispatchGroup,
notifyQueue,
{
// 任务完成后继续处理
});
```

与前面的示例中将任务提交到并发队列不同，你反而可以使用 `dispatch` 组来跟踪提交到不同串行队列的多个任务。然而，如果所有任务都排在同一个串行队列上，那么组就没有特别用了。因为任务无论如何都是串行执行的，你只需要在队列任务后再队列另一个 `block` 即可，这等同于 `dispatch` 组的 `notify` 回调 `block`：

```
dispatch_queue_t queue =
dispatch_queue_create("com.effectiveobjectivec.queue", NULL);

for (id object in collection) {
    dispatch_async(queue,
        ^{ [object performTask]; });
}
```

## 第 45 条：使用 `dispatch_once` 实现线程安全的单次代码执行

单例设计模式在 Objective-C 世界中并不陌生——它通常通过一个类似于 `sharedInstance` 的类方法来实现，该方法返回类的单例实例，而不是每次都专门分配新实例。对于名为 `EOClass` 的类，其共享实例方法的一种常见实现如下：

```objc
@implementation EOClass

+ (id)sharedInstance {
    static EOClass *sharedInstance = nil;
    @synchronized(self) {
        if (!sharedInstance) {
            sharedInstance = [[alloc] init];
        }
    return sharedInstance;
    }
}
@end
```

我发现单例模式引发了巨大的争议，尤其是在 Objective-C 中。线程安全性是争议的焦点。上面的代码将单例实例封装在一个同步块中以确保它是线程安全的。无论好坏，这种模式被广泛使用，而这种代码也随处可见。

然而，GCD 引入了一个让单例实例实现变得简单得的功能。该函数如下：

```objc
void dispatch_once(dispatch_once_t token, dispatch_block_t block);
```

该函数接收一个特殊的 `dispatch_once_t` 类型（我称之为 "token"）和一个 `block`。该函数确保对于给定的 `token`，`block` 将被执行且仅执行一次。在第一次执行时，最重要的是，它是完全线程安全的。注意，传递的 `token` 对于每个需要执行一次的 `block` 来说必须是完全同一个。这通常意味着要在静态或全局作用域中声明 `token` 变量。

使用此函数重写单例共享实例方法的方法所示：

# 第 6 章：Blocks 与 Grand Central Dispatch

```objc
+ (id)sharedInstance {
    static EOClass *sharedInstance = nil;
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken,^{
        sharedInstance = [[self alloc] init];
    });
    return sharedInstance;
}
```

`dispatch_once` 简化了代码并完全确保了线程安全，你甚至不需要考虑锁定或同步。这一切都在 GCD 内部被处理了。`token` 被声明为 `static` 是因为每次都需要是完全相同的 `token`。在静态作用域中定义变量意味着编译器会确保在每次运行 `sharedInstance` 方法时，而不是创建一个新变量，而是每次都复用同一个变量。

此外，`dispatch_once` 效率更高。它没有使用每次运行代码都会获取锁的重量级同步机制，而是通过对 `dispatch` `token` 的原子访问来指示代码是否已经运行。在 Mac OS X 10.8.2 机器上的简单基准测试显示，使用 `@synchronized` 方法访问 `sharedInstance` 方法与 `dispatch_once` 方法相比，`dispatch_once` 的速度提升了近一倍。

## 注意事项

- 线程安全的单次代码执行是一常见任务。GCD 通过 `dispatch_once` 函数提供了一个易于使用的工具。
- `token` 应该在静态或全局作用域中声明，以确保传递给每个需要执行一次的 `block` 的同一个 `token`。

## 第 46 条：避免使用 `dispatch_get_current_queue`

在使用 GCD 时，特别是当分发到各种队列时，确定当前正在执行的是哪个队列是常见的。例如，Mac OS X 和 iOS 中的 UI 工作都需要在主线程上执行，这等同于 GCD 中的主队列。有时，有必要确定当前的 GCD 代码是否在主队列上执行。阅读文档时，你会遇到以下函数：

```objc
dispatch_queue_t dispatch_get_current_queue();
```

## 第 46 条：避免使用 `dispatch_get_current_queue`

文档记录该函数返回当前正在执行的队列。这确实是该函数的功能，但应该谨慎对待。事实上，从 iOS 6.0 版本开始，它现在已正式被弃用。但在 Mac OS X 10.8 版本中尚未被弃用。尽管如此，在 Mac OS X 上也应避免使用。

该方法的一种常见典型反模式是：将当前队列与特定队列进行比较，试图规避同步分发时可能发生的死锁。考虑以下访问器方法，它们使用队列来同步对实例变量的访问（参见第 41 条）：

```objc
(NSString*)someString {
    NSString *localSomeString;
    dispatch_sync(_syncQueue, ^{
        localSomeString = _someString;
    });
    return localSomeString;
}
```

```objc
(void)setSome(NSString*)someString {
    dispatch_async(_syncQueue, ^{
        _someString = someString;
    });
}
```

你可能在该模式中遇到的问题是 `getter` 中的死锁。如果 `getter` 是从与用于同步的队列（示例中的 `_syncQueue`）相同的队列中调用的，将因为 `dispatch_sync` 在 `block` 执行完成之前不会返回。但如果 `block` 的目标队列是当前队列，那么该 `block` 将永远没有机会运行，因为 `dispatch_sync` 将继续阻塞，等待队列可用以运行目标 `block`。这是一个非重入性方法的示例。

在读过 `dispatch_get_current_queue` 的文档后，你可能会认为通过检查当前队列是否为同步队列来使方法可重入是安全的，如果是，则直接执行 `block` 而不是进行分发：

```objc
(NSString*)someString {
    NSString *localSomeString;
    dispatch_sync(_syncQueue, ^{
        localSomeString = _someString;
    });
```

# 第 6 章：Blocks 与 Grand Central Dispatch

```objc
if (dispatch_get_current_queue() == _syncQueue) {
    // 直接执行 block
} else {
    dispatch_sync(_syncQueue, ^{
        localSomeString = _someString;
    });
}
return localSomeString;
}
```

## 第 46 条：避免使用 `dispatch_get_current_queue`

在这种情况下，正确的解决方案是访问器不需要被改为可重入。相反，你应该确保用于同步的队列永远不要尝试访问属性；永远不要调用 `someString`。队列应该只用于属性的同步。分发队列是非常轻量级的，因此创建多个队列以确保同步队列仅用于一个属性的同步是没问题的。

前面的示例可能看起来稍显刻意，但另一个需要注意的是，队列可能会在你没有预料的情况下导致此问题。队列被排列成层级结构，这意味着在某个队列上入的 `block` 将在其父队列中执行。层级结构中的最后一个队列始终是全局队列之一。为了说明一个简单的层次结构，请参见图 6.4。

在队列 B 或 C 上的 `block` 随后被调度在队列 A 上运行。因此，排在队列 A、B 和 C 上的 `block` 将互斥执行。然而，排在队列 D 上的 `block` 将与 A（因此是 B 和 C）并行运行，因为 A 和 D 的目标队列是并发队列。并发队列根据系统资源（如 CPU 核心数）在多个线程上并行执行 `block`。

```objc
dispatch_queue_t queueA = create("com.objective.queueA", NULL);
dispatch_queue_t queueB = create("com.objective.queueB", NULL);
```

```objc
dispatch_sync(queueA, ^{
    dispatch_sync(queueB, ^{
        // 死锁
    });
});
```

这在内部分发到 `queueA` 时将总是死锁，因为它将等待外部 `dispatch_sync` 完成，而外部在内部 `dispatch_sync` 完成之前本身不会完成。现在考虑使用 `dispatch_get_current_queue` 放入相同的检查：

```objc
dispatch_sync(queueA, ^{
    dispatch_sync(queueB, ^{
        dispatch_block_t block = ^{ /* */ };
        if (dispatch_get_current_queue() == queueA) {
            block();
        } else {
            dispatch_sync(queueA, block);
        }
    });
});
```

然而，这也会导致死锁，因为 `dispatch_get_current_queue` 返回的是当前队列，在前面的示例中将是 `queueB`。因此，同步分发到 `queueA` 的操作仍然会发生，导致死锁，和之前一样。

## 第 6 章：Block 与全局中央调度 (GCD)

由于队列的层次结构，当前队列与准备同步派发的队列之间的等性检查可能并不总是有效。例如，入队队列 C 上的 Block 会返回队列 C 作为当前队列，因此它可能认为自己可以安全地异步派发到队列 A。事实上，这会导致像以前一样的死锁。

如果一个 API 允许你指定在哪个队列上调度回调 Block，但内部使用了串行同步队列，且其目标队列设置为回调队列，则可能会出现这个问题。在此类 API 的调用者代码中，假设回调 Block 中通过 `dispatch_current_queue` 返回的当前队列始终等于它给出的队列将是错误的。事实上，返回的将是内部的同步队列。

为了解决这个问题，最佳方法是使用 GCD 的队列特定数据函数，这些函数允许你将任意数据以键值对的形式与队列关联。最重要的一点是，如果在检索数据时某个键没有关联数据，系统将向上遍历层次结构，直到找到数据或到达根节点。这种用法可能并不显而易见，请考虑这个示例：

```
dispatch_queue_t queueA =
    dispatch_queue_create("com.objectivec.queueA", NULL);
    dispatch_queue_t queueB =
    dispatch_queue_create("com.objectivec.queueB", NULL);
    dispatch_queue_set_target_queue(queueB, queueA);
```

```
static int kQueueSpecific;
CFString queueSpecificValue = CFSTR("queueA");
dispatch_queue_set_specific(queueA,
    &kQueueSpecific,
    (void*)queueSpecificValue,
    (dispatch_function_t)CFRelease);
dispatch_sync(queueB, {
    dispatch_block_t block = ^{NSLog("@No deadlock!")};
    block();
```

```
CFString retrievedValue =
    dispatch_get_specific(&kQueueSpecific);
if (retrievedValue) {
    block();
} else {
    dispatch_sync(queueA, block);
}
});
```

## 第 46 条：避免使用 `dispatch_get_current_queue`

在这个示例中创建了两个队列。队列 B 的目标队列设置为队列 A，而 A 的目标队列保持为默认优先全局队列。然后，使用以下函数在队列 A 上设置了一个队列特定值：

```
void dispatch_queue_set_specific(dispatch_queue_t queue,
                             const void *key,
                             void *context,
dispatch_function_t destructor);
```

该函数接收一个要设置数据的目标队列，随后是键和 t 值。键和值都是不透明的 `void` 指针。对于键，需要记住的是它们是通过 t 指针的值进行比较的，而不是通过内容。队列特定数据的行为与 `NSDictionary` 对象不同，后者比较的是对象的等效性键。队列特定数据的行为更像关联引用（参见第 10 条）。值（在函数原型中称为 `context`）也是 `void` 指针。因此，它们可以完全是你想要的任何内容。然而，你可以对对象进行任何需要的内存管理。这使得在 ARC 环境下将 Objective-C 对象作为值非常困难。在示例中，使用 CoreFoundation 字符串作为值，因为 ARC 不负责任何 CoreFoundation 对象内存的管理。因此，此类对象是良好的队列特定数据，因为它们可以根据需要无缝桥接（toll-free bridged）到相应的 Objective-C 类。

该函数的最后一个参数是析构函数，它在给定键持有的对象被移除时（是因为队列被释放或为该键设置了新值）运行执行。`dispatch_function_t` 定义如下：

```
typedef void (*dispatch_function_t)(void*)
```

因此，析构函数必须是一个接受单个指针作为唯一参数并返回 `void` 的函数。在示例中，提供了 `CFRelease`，尽管也可以提供一个名为 `CFRelease` 的自定义函数来清理值并执行任何其他必要的清理。

因此，队列特定数据提供了一个简单な机制，用于解决 `dispatch_get_current_queue` 的常见陷阱之一。`dispatch_get_queue` 的其他常见用途包括调试。在这些情况下，只要代码不被编译到发布版本中就是安全的。访问当前队列的特定需求无法通过其他函数涵盖，最好向 Apple 提交功能请求。

## 注意事项
