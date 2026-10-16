

```
}
```

最后，我们可以发起一次搜索：

```cpp
void find_cheap_red()
{
    assert(goods.size()%grain==0);
    // no match found

    Record *p=pfind(goods, [](Record& r) { return r.price<200 && r.color==Color::red; });
    cout << "record " << *p << '\n';
}
```

这种并行 find() 的第一个版本首先生成大量任务，然后按顺序等待它们。与 std::find_if() 一样，它报告匹配的第一个元素；也就是说，它找到匹配的具有最低索引的元素。这可能没问题，但：

- 我们可能最终会等待大量找不到任何内容的任务（也许只有最后一个任务找到了内容）。
- 我们可能会丢弃大量可能有用的信息（也许有上千项符合我们的条件）。

第一个问题可能没有听起来那么糟糕。假设（有些鲁莽地）启动一个线程的成本为零，并且我们拥有的处理单元数量与任务数量一样多；那么我们仍然会在大约处理一个任务所需的时间内得到结果。也就是说，我们有可能在检查 50,000 条记录所需的时间内得到结果，而不是数百万条。如果我们有 N 个处理单元，结果将以 N*50000 条记录的批次交付。如果直到向量的最后一部分才找到记录，时间大约为 vr.size()/(N*grain) 个单位。

与其按顺序等待每个任务，我们可以尝试按任务完成的顺序查看结果。也就是说，我们可以使用 wait_for_any()（§42.4.4）。例如：

```cpp
template<typename Pred>
Record* pfind_any(vector<Record>& vr, Pred pr)
{
    vector<future<Record*>> res;
    for (int i = 0; i!=vr.size(); i+=grain)
        res.push_back(async(find_rec<Pred>,ref(vr),i,i+grain,pr));

    for (int count = res.size(); count; --count) {
        int i = wait_for_any(res,microseconds{10}); // find a completed task
        if (auto p = res[i].get()) // did the task find a match?
            return p;
    }
    return nullptr; // no match found
}
```

一个 **get()** 会使它的 **future** 无效，因此我们无法两次查看部分结果。

我使用 **count** 来确保在所有任务都报告完毕后不再继续查找。除了这一点，**pfind_any()** 与 **pfind()** 一样简单。**pfind_any()** 相对于 **pfind()** 是否有性能优势取决于很多因素，但关键的观察是，为了（潜在地）获得并发的优势，我们必须使用稍微不同的算法。像 **find_if()** 一样，**pfind()** 返回其第一个匹配项，而 **pfind_any()** 返回它首先找到的匹配项。通常，某个问题的最佳并行算法是顺序解决方案思想的变体，而不是顺序解决方案的简单重复。

在这种情况下，显而易见的问题是“但你真的只需要一个匹配吗？” 鉴于并发，找到所有匹配项更有意义。做到这一点很容易。我们需要做的只是让每个任务返回一个 **vector** 的匹配项，而不是仅仅一个简单的匹配项：

```cpp
template<typename Pred>
vector<Record*> find_all_rec(vector<Record>& vr, int first, int last, Pred pr) {
    vector<Record*> res;
    for (int i=first; i!=last; ++i)
        if (pr(vr[i]))
            res.push_back(&vr[i]);
    return res;
}
```

这个 **find_all_rec()** 或许比原始的 **find_rec()** 更简单。现在我们只需要以合适的次数启动 **find_all_rec()** 并等待结果：

```cpp
template<typename Pred>
vector<Record*> pfind_all(vector<Record>& vr, Pred pr)
{
    vector<future<vector<Record*>>> res;
    for (int i = 0; i!=vr.size(); i+=grain)
        res.push_back(async(find_all_rec<Pred>,ref(vr),i,i+grain,pr));
    vector<vector<Record*>> r2 = wait_for_all(res);
    vector<Record*> r;
    for (auto& x : r2) // merge results
        for (auto p : x)
            r.push_back(p);
    return r;
}
```

如果我只是返回一个 **vector<vector<Record*>>**，这个 **pfind_all()** 将会是最简单的并行化函数。然而，通过将返回的 **vectors** 合并成一个，**pfind_all()** 成为了一类常见且流行的并行算法的例子：

- [1] 创建要运行的多个任务。
- [2] 并行运行任务。
- [3] 合并结果。

当发展成一个框架，使得并发执行的细节完全被隐藏时，这就是通常被称为 map-reduce [Dean,2004] 的基本思想。示例可以这样运行：

```cpp
void find_all_cheap_red()
{
    assert(goods.size()%grain==0);

    auto vp = pfind_all(goods,
        [](Record& r) { return r.price<200 && r.color==Color::red; });
    for (auto p : vp)
        cout << "record " << *p << '\n';
}
```

最后，我们必须考虑并行化的努力是否值得。为此，我在我的测试中添加了简单的顺序版本：

```cpp
void just_find_cheap_red()
{
    auto p = find_if(goods.begin(),goods.end(),
        [](Record& r) { return r.price<200 && r.color==Color::red; });
    if (p!=goods.end())
        cout << "record " << *p << '\n';
    else
        cout << "not found\n";
}

void just_find_all_cheap_red() {
    auto vp = find_all_rec(goods,0,goods.size(),
        [](Record& r) { return r.price<200 && r.color==Color::red; });
    for (auto p : vp)
        cout << "record " << *p << '\n';
}
```

对于我的简单测试数据和我的（相对）简单的笔记本电脑，只有四个硬件线程，我没有发现任何一致或显著的性能差异。在这种情况下，async() 不成熟实现中线程创建的成本主导了并发的影响。如果我现在需要显著的并行加速，我会基于预先创建的一组线程和一个工作队列实现我自己的 async() 变体，类似于 Sync_queue (§42.3.4) 的 packaged_tasks (§42.4.3)。请注意，这种重大的优化可以在不更改我的基于任务的并行 find() 程序的情况下完成。从应用程序的角度来看，用优化版本替换标准库的 async() 是一个实现细节。

### 42.5 Advice

- [1] A thread is a type-safe interface to a system thread; §42.2.
- [2] Do not destroy a running thread; §42.2.2.
- [3] Use join() to wait for a thread to complete; §42.2.4.
- [4] Consider using a guarded_thread to provide RAII for threads; §42.2.4.
- [5] Do not detach() a thread unless you absolutely have to; §42.2.4.
- [6] Use lock_guard or unique_lock to manage mutexes; §42.3.1.4.
- [7] Use lock() to acquire multiple locks; §42.3.2.
- [8] Use **condition_variable** to manage communication among **thread**s; §42.3.4.
- [9] Think in terms of tasks that can be executed concurrently, rather than directly in terms of **thread**s; §42.4.
- [10] Value simplicity; §42.4.
- [11] Return a result using a **promise** and get a result from a **future**; §42.4.1.
- [12] Don’t **set_value()** or **set_exception()** to a **promise** twice; §42.4.2.
- [13] Use **packaged_task**s to handle exceptions thrown by tasks and to arrange for value return; §42.4.3.
- [14] Use a **packaged_task** and a **future** to express a request to an external service and wait for its response; §42.4.3.
- [15] Don’t **get()** twice from a **future**; §42.4.4.
- [16] Use **async()** to launch simple tasks; §42.4.6.
- [17] Picking a good granularity of concurrent tasks is difficult: experiment and measure; §42.4.7.
- [18] Whenever possible, hide concurrency behind the interface of a parallel algorithm; §42.4.7.
- [19] A parallel algorithm may be semantically different from a sequential solution to the same problem (e.g., **pfind_all()** vs. **find()**); §42.4.7.
- [20] Sometimes, a sequential solution is simpler and faster than a concurrent solution; §42.4.7.

## 43 The C Standard Library

> *C is a strongly typed, weakly checked language.*
> — D. M. Ritchie

- Introduction
- Files
- The printf() Family
- C-Style Strings
- Memory
- Date and Time
- Etc.
- Advice

### 43.1 Introduction

The standard library for the C language is with very minor modifications incorporated into the C++ standard library. The C standard library provides quite a few functions that have proven useful over the years in a wide variety of contexts – especially for relatively low-level programming.

There are more C standard-library functions than are presented here; see a good C textbook, such as “Kernighan and Ritchie” [Kernighan,1988] or the ISO C standard [C,2011], if you need to know more.

### 43.2 Files

The <cstdio> I/O system is based on files. A file (a FILE*) can refer to a file or to one of the standard input and output streams: stdin, stdout, and stderr. The standard streams are available by default; other files need to be opened:

**File Open and Close**

| Function | Description |
| --- | --- |
| `f=fopen(s,m)` | Open a file stream for a file named `s` with the mode `m`. `f` is the `FILE*` for the opened file if successful or `nullptr`. |
| `x=fclose(f)` | Close file stream `f`; return 0 if successful. |

A file opened with fopen() must be closed by fclose() or the file will remain open until the operating system closes it. If that is a problem (is considered a leak), use an fstream (§38.2.1). A mode is a C-style string containing one or more characters specifying how a file is to be opened (and used after opening):

**File Modes**

| Mode | Meaning |
| --- | --- |
| `"r"` | Reading |
| `"w"` | Writing (discard previous contents) |

