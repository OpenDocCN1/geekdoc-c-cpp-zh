
```
0004: |00260360
普通 JIT 生成的代码
BasicStack`[[System.-Canon, mscorlib]].Push(System.-Canon)
00260360 57 push edi
00260361 56 push esi
00260362 8b7104 mov esi, dword ptr ecx[4]
00260365 8b7908 mov edi, dword ptr ecx[8]
00260368 8d4701 lea eax, [edi]
0026036b 8b910b mov dword ptr ecx[8], eax
002603d0 53 push edx
00260370 8b mov ecx,esi
00260371 8bd mov edx,edi
00260373 e8f4cb38 call !JIT_Stelem (70ecfc)
00260378 5e pop esi
00260379 59 pop edi
0026037a c3 ret

0004: |002603c0
普通 JIT 生成的代码
BasicStack`1[[System.Int32, mscorlib]].Push(Int32)
002603c0 57 push ebp
002603c1 56 push esi
002603c2 8b7104 mov esi, dword ptr ecx[4]
002603c5 8b7908 mov edi, dword ptr ecx[8]
002603c8 8d4701 lea eax,[edi+1]
002603cb 949108 mov dword ptr ecx[8],eax
002603ce 3b7e04 cmp edi, dword ptr [ecx+4] (wait, checking logic: cmp edi, [ecx+4])
002603d1 7307 ja
002603d3 8954e8 mov dword ptr [esi+4],edx
002603d7 57 pop esi
002603d8 5f pop edi
002603d9 c3 ret
002603da e877446 call !JIT_RngFail(70874856)
002603dc

普通 JIT 生成的代码
BasicStack`1[[System.Double, mscorlib]].Push(Double)
00260420 56 push esi
00260421 8b7104 mov edx, dword ptr ecx+4]
00260424 8b7908 mov esi, dword ptr ecx+8]
00260427 8d4701 lea eax,[esi+1]
0026042a 949108 mov dword ptr ecx+8],eax
0026042d 3b7e04 cmp edi, dword ptr [ecx+4]
00260430 730c ja
0026043e dd44208 fid qword ptr [esp+8]
00260436 d8cf208 fstp qword ptr [edx+8]
0026043a 57 pop esi
0026043b c8 ret
0026043e e8134467 call !JIT_RngFail(70874856)
00260443
```

我们已经看到 .NET 泛型实现在编译时是完全类型安全的。仍然需要确定的是在泛型集合中使用值类型时是否存在装箱（boxing）代价。事实上，因为 JIT 编译器会为每个泛型参数为值类型的泛型编译一个特殊的体，因此不需要装箱。

总结来说，与 Java 泛型或 C++ 模板相比.NET 泛型具有显著优势。泛型约束机制与 C 提供的野蛮增长相比相当有限，但跨程序集共享泛型带来的灵活性以及按需生成代码（并共享它）的性能收益是巨大的。

## 集合

.NET Framework 拥有大量的集合，本章的目的并不是回顾其中的每一个一个——这项任务最好交给文档。然而，在选择集合时（特别是对于性能敏感型代码），需要考虑一些非显易见的因素。我们将在本节中探索这些因素。

**注意** 某些开发者警惕使用内置数组以外的任何集合。数组非常灵活、不可缩放，并且难以高效地实现某些操作，但它们以具有其他集合实现中最小的开销而闻。只要你有良好的测量工具（如第 2 章考虑的），就不应该害怕使用内置集合。本节将讨论的集合内部实现细节也将有助于泛型。一个例子：在 `foreach` 循环中迭代 `List<T>` 比在 `for` 循环慢得多，因为枚举必须验证在循环过程中底层集合没有被更改。

首先，回想 .NET 4.5 分类的集合（不包括并发集合，我们将单独讨论）以及它们的运行时性能特征。比较集合的插入、删除和查找性能是找到你需求最佳候选的合理方法。下表仅列出了泛型集合（非泛型对应项在 .NET 2.0 中被替换）：

表 5-1. .NET Framework 中的集合

| 集合 | 详情 | 插入时间 | 删除时间 | 查找时间 | 排序 | 索引访问 |
|---|---|---|---|---|---|---|
| `List<T>` | 自动可缩放数组 | O(1)* | O(n) | O(n) | 否 | 是 |
| `LinkedList<T>` | 双向 | O(1) | O(1) | O(n) | 否 | 否 |
| `Dictionary<K,V>` | 哈希表 | O(1) | O(1) | O(1) | 否 | 否 |
| `HashSet<T>` | 哈希表 | O(1) | O(1) | O(1) | 否 | 否 |
| `Queue<T>` | 自动循环数组 | 摊销 O(1) | O(1) | | 否 | 否 |
| `Stack<T>` | 自动可缩放数组 | 摊销 O(1) | | | 否 | 否 |
| `SortedDictionary<K,V>` | 红黑树 | O(log n) | O(log n) | O(log n) | 是（键） | 否 |
| `SortedList<K,V>` | 排序可缩放数组 | O(n)** | O(n) | O(log n) | 是（键） | 是 |
| `SortedSet<T>` | 红黑树 | O(log n) | O(log n) | O(log n) | 是 | 否 |

* “摊销”在这种情况下我们的意思是某些操作可能花费 O(n) 时间，但大多数操作将花费 O(1) 时间，使得 n 次操作的平均时间为 O(1)。
** 除非数据按排序插入，在这种情况下为 O(1)。

前者是通过具有 $n$ 个节点的 $n$ 个元素的二叉搜索树实现的，后者则是基于包含 $n$ 个元素的连续数组实现的。在 32 位系统上，在排序集中存储 $n$ 个大小为 $s$ 的值类型需要 $(20+s)n$ 字节的存储，而列表只需要 $n$ 字节。

- 某些集合对元素有额外要求，以获得良好的性能。例如，正如我们在第 3 章看到的，哈希表的实现要求哈表元素具有良好的哈希码。

- 摊还代价为 O(1) 的集合在执行良好时，与真正的 O(1) 成本集合几乎没有区别。毕竟，很少有程序员（以及程序！）会警惕 `List<T>.Add` 可能会产生巨大的内存分配开销，并且运行时间与元素数量成正比。摊还时间分析非常有用的工具；它已被用于证明许多算法和集合的优越性。

- 空间权衡（ubiquitous-space tradeoff）存在于集合设计中，甚至存在于 .NET Framework 中包含哪些集合的选择中。`SortedList<K,V>` 以线性插入和删除为代价，提供了非常紧凑且顺序的元素存储；而 `Dictionary<K,V>` 占用空间更多是非顺序的，但所有操作都具有对数级界限。

> 注意：没有更好的机会来提到字符串了，字符串也是一种简单的集合类型——字符的集合。最初，`System.String` 类被实现为不可变的、不可调整大小的字符数组。对字符串的所有操作都会导致新对象的创建。这就是为什么通过拼接成千上万短字符串来创建长字符串是非常无效的。`System.Text.StringBuilder` 类解决了这些问题，它的实现类似于 `List<T>`，并在发生更改时将其内部存储翻倍。每当你需要从大量（或未知）的小字符串构造字符串时，请使用 `StringBuilder` 进行中间操作。

集合类的丰富性可能让人目不应接，但在某些情况下，没有任何内置集合是合适的。我们稍后考虑几个例子。在 .NET 4.0 之前，对内置集合的一个常见抱怨是缺乏线程安全：表 5-1 中的没有任何集合可以安全多线程并发访问。在 .NET 4.0 中，`System.Collections.Concurrent` 命名空间引入了全新的、专为并发编程环境设计的集合。

## 并发集合

随着 .NET 4.0 中任务并行库（Task Parallel Library）的出现，对线程安全集合的需求变得更加迫。在第 6 章中，我们将看到几个从多个线程并发访问数据源或输出缓冲区的动机示例。现在，我们本着之前学过的标准（非线程安全）集合相同的精神，关注可用的并发集合及其性能特征。

### 第 5 章 集合与泛型

表 5-2. .NET Framework 中的并发集合

| 集合 | 最相似的 | 详细信息 | 同步 |
|---|---|---|---|
| `ConcurrentStack<T>` | `Stack<T>` | 单链表¹ | 无锁 (CAS)，自旋时采用指数级退避 |
| `ConcurrentQueue<T>` | `Queue<T>` | 数组段的链表 (32 个元素)² | 无锁 (CAS)，在出队刚入队列的项时进行短暂自旋 |
| `ConcurrentBag<T>` | | 线程本地列表，工作窃取³ | 本地列表通常无，工作窃取使用 Monitor |
| `Dictionary<K,V>` | `Dictionary<K,V>` | 哈希表：哈桶和链表⁴ | 对于更新：针对每组哈希桶使用 Monitor（与其他哈桶独立） |

对“详细信息”列的说明：
1. 在第 6 章中，我们将看到一个使用 CAS 的无锁栈的实现，而 CAS 是我们单元中的原子原语。
2. `ConcurrentQueue<T>` 类管理一个数组段的链表，这允许它以较低的开销模拟无界队列。入队和出队仅涉及指向数组段的原子指针。在几个位置需要同步，例如，确保项在线程完成入队操作之前不会被出队。然而，同步是基于 CAS 的。
3. `ConcurrentBag<T>` 类管理一个没有特定顺序的项列表。项存储在线程本地列表中；在线程本地列表中添加或删除项是在列表头部完成的，通常通常同步同步。当线程需要来自其他列表的项时，它会从列表尾部窃取，这仅在列表中少于三个项时才会引起竞争。
4. `Dictionary<K,V>` 使用了带锁的哈希表实现（每个哈桶上挂着链表，作为桶结构的通用描述，另见第 3 章）。锁在桶级别通过锁进行管理，锁的数量限制由构造函数的 `concurrencyLevel` 参数决定。所有读取操作不需要任何锁，但所有变变操作都是原子的（例如，向挂载在哈桶上的列表插入新项）。

大多数并发集合与其非线程安全的对应版本相似，但 `ConcurrentDictionary<K,V>` 类具有成员，可以极大减少所需的锁数量，并解决粗心访问字典时可能出现的竞态条件：

```csharp
// 以下代码使用 AddOrUpdate 方法来确保在添加项或更新现有项时进行正确的同步：

ConcurrentDictionary<string, int> expenses = ...;

expenses.AddOrUpdate("ParisExpenses", currentAmount, (key, amount) => amount + currentAmount);
```

`AddOrUpdate` 方法保证了复合操作“添加或更新”周围的必要同步。

## 缓存考虑

选择正确的集合不仅关乎其性能，但布局对应用程序往往更为关键。现代系统带有三级缓存：L1、L2 和 L3。当处理器尝试访问内存时，首先检查数据是否已在 L1 缓存中。如果是，从 L2 满足需要 10 个周期。同样，从 L3 满足需要 40 个周期。最后，如果数据不在任何缓存层级中，处理器将等待主内存（这是昂贵的）。当处理器访问内存时，读取的不是单个字节或字，而是一个缓存行。在单元从缓存中驱出之前，访问同一行上的任何字都不会再次触发缓存缺失。

尽管这种描述没有证明 SRAM 和 DRAM 操作的硬件复杂性，但它为讨论数据布局如何影响算法提供了足够的思考空间。我们现在考虑一个涉及单核心缓存的简单示例：假设任务是遍历大型集合并对其进行聚合。以下是两种替代方案；一种数据来自 `LinkedList<int>`，另一种来自整数数组 (`int[]` 两种内置集合）。

```csharp
LinkedList<int> numbers = new LinkedList<int>(Enumerable.Range(0, 20000000));

int sum = 0;

for (LinkedListNode<int> curr = numbers.First; curr != null; curr = curr.Next()) {
    sum += curr.Value;
}

int[] numbers = Enumerable.Range(0, 20000000).ToArray();

for (int curr = 0; curr < numbers.Length; ++curr) {
    sum += numbers[curr];
}
```

在上述系统中，第二种代码运行速度比第一种快 2 倍。这是一个不可忽视的差异。图 5-3: 显示缓存层级的 Intel i7 架构图。

### 第5章 集合与泛型

```assembly
; x86 assembly for the second loop, assume 'sum' is in EAX and 'numbers' is in ECX

mov edi, dword ptr [ecx+4]    ; numbers.Length
test edi, edi
z LOOP_END
xor edx, edx                 ; loop index
LOOP_BEGIN:
add eax, dword ptr [ecx+edx*4+8]    ; sum += numbers[i], no bounds check
inc edx
cmp esi, edx
jg LOOP_BEGIN
LOOP_END:
```

考虑到这两个循环的这种代码生成（排除用于遍历数组的 SIMD 指令优化，数组在内存中是连续的），通过检查执行的指令很难解释性能差异。事实上，我们必须分析这段代码的访问模式才能得出任何可靠的结论。

在两个循环中，每个整数只被访问一次，缓存似乎并不关键，因为没有可重用的数据可以从缓存命中中获益。尽管如此，数据在内存中的布局方式仍然影响程序的性能——这并不是因为数据被重用，而是因为它们进入内存的方式。在访问元素时，缓存行开头的缓存缺失会带入 16 个连续整数（缓存行 = 64 字节）。由于数组访问是顺序的，接下来的 15 个元素现在已经在缓存中，无需发生缓存缺失即可访问。这几乎是一个理想的场景，缓存比例为 1:16。相反，当访问链表时，缓存行开头的缓存缺失最多带入 3 个链表节点，缓存缺失比例为 1:4（一个节点包含一个后置指针、一个指针和一个整数数据，在 32 位系统上占用 12 字节；引用类型头使每个节点增加到 20 字节）。

较高的缓存缺失率是上述两种情况性能差异的原因。此外，我们假设了一个理想场景，即所有链表节点都顺序放置在内存中，这只有在它们同时分配且期间没有其他分配发生的情况下才可能，而这种情况非常不利。如果列表节点在内存中的分布密度较低，缓存缺失率将会更高，性能也会糟糕。

结论性的示例展示了缓存相关影响的另一个方面，即分分块（blocking）乘法算法。矩阵乘法（我们将在第 6 章讨论 C++ AMP 时再次遇到）因为元素被重用了多次。以下是朴素的实现：

```c
public static int[] MultiplyNaive(int[] a, int[] b) {
    int[] c = new int[N, N];
    for (int i = 0; i < N; ++i) {
        for (int j = 0; j < N; ++j) {
            for (int k = 0; k < N; ++k) {
                c[i, j] += a[i, k] * b[k, j];
            }
        }
    }
    return c;
}
```
