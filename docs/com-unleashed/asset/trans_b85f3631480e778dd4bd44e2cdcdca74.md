
## 线程同步

从服务器角度来看，在决定线程模型之后，必须考虑并发问题。实际上，如果选择单线程线程模型，就不必考虑任何并发问题。如果选择套间线程模型，只需针对全局数据考虑并发问题。如果选择自由线程模型，则必须针对每对象数据和全局数据考虑并发问题。

但什么是每对象数据，什么是全局数据？每对象数据是仅属于当前对象局部的数据。最常见的每对象数据类型是非静态 C++ 类成员。所有分配在栈或堆上的函数局部数据也是每对象数据。所有不是每对象数据的数据都是全局数据。但如果没有一些例外，这个定义并不十分完整。

例如，不使用 COM+ 也可以让外部线程直接访问非静态 C++ 类成员数据。这类数据虽然是每对象数据，但必须作为全局数据对待，因为多个 STA 可能访问该数据。

### 线程本地存储

线程本地存储（TLS）是一种特殊的存储类型，它将访问限制在当前一个线程。如果只有一个线程可以访问线程本地存储，就不可能产生并发问题。使用 TLS，可以为每个线程关联一定数量的内存。因此，每个线程都有自己的存储，并且只能由该线程访问。对于线程本地存储的任一种实现，这可能会也可能不会缓解并发问题。有时很难确定线程本地存储的某一种实现是否存在并发问题。有时最好假定所有线程本地存储都是全局数据，并消除所有可能的并发问题。这可能会导致应用程序出现瓶颈。如果确实出现瓶颈，我建议通过重新设计应用程序来消除并发问题。

可能出现的一个问题是，假定自由线程对象总是具有相同的线程上下文。这显然是一个不正确的假定。

### 消除并发问题

Windows API 有大量函数可用于消除并发问题。这些结构中最基本的是临界区。还存在其他并发结构，包括互斥量、信号量和事件。

**清单 7.11 续**

```cpp
{
    switch (msg.message)
    {
    case MYMESSAGE:
        /////////////////////////////////////////////////
        // TODO
        // Add background processing code here
        //
        ::EnterCriticalSection(&m_csToProtect);
        std::cout << "Hello World from Thread Number: "
                  << ::GetCurrentThreadId() << std::endl;
        ::LeaveCriticalSection(&m_csToProtect);
    default:
        break;
    };
    return 0;
}

int Pool::DoWork()
{
    DWORD dw = m_qidThread.front();
    ::PostThreadMessage(dw, MYMESSAGE, 0, 0);
    m_qidThread.pop();
    m_qidThread.push(dw);
    return 0;
}
```

清单 7.11 中的代码与前面清单 7.6 中展示的线程池类似。为了保障多个线程同时写入 cout 的安全，请将 cout 例程放在临界区中，以消除任何并发问题。

还有一个我尚未提到的并发问题。例如以下代码：

```cpp
void Function( void )
{
    Pool p;
    p.DoWork();
    p.DoWork();
    p.DoWork();
}
```

如果 DoWork() 运行时间很长，p 可能会在最后一次 DoWork() 结束之前、但在临界区被删除之后被销毁。启动和结束多线程代码总是很难完美实现。

如果在没有临界区的情况下运行清单 7.12 中的代码，标准输出中会产生一些可怕的输出（见清单 7.13）。这是因为各个线程在 cout 命令执行到一半时被换出。然后下一个线程在上一个线程完成之前开始写入其输出。这种情况会持续下去，直到产生非常特别的输出。

**清单 7.12**  线程安全检查

```cpp
int main(int argc, char* argv[])
{
    Pool thread;
    Sleep(1000);
    for (int i=0;i<20;i++)
    {
        thread.DoWork();
    }
    Sleep(2000);
    return 0;
}
```

**清单 7.13**  未同步输出

```
HelloWorld!HelloWorld!HelloWorld!HelloWorld! o o o! ow WoW oW oWo oWofr
orWorWorWorWorWorWorWorWorWorWorWorWorWorWorWorWorWorWorWor
omomomom o mo md TmT mT h h hT hTNrNrFrThThruereherhermearearaeabadedae
...
Hello World! from Thread Number: 472
Hello World! from Thread Number: 402
Hello World! from Thread Number: 522
Hello World! from Thread Number:
Hello World! from Thread Number: 508
Hello World! from Thread Number: 502
Hello World! from Thread Number: 358
Hello World! from Thread Number: 373
Hello World! from Thread Number: 258
Hello World! from Thread Number: 552
```

如果在有临界区的情况下运行同一个清单 7.12，输出会更易读（见清单 7.14）。

**清单 7.14**  同步输出

```
Hello World! from Thread Number: 492
Hello World! from Thread Number: 353
Hello World! from Thread Number: 465
Hello World! from Thread Number: 518
Hello World! from Thread Number: 450
Hello World! from Thread Number: 510
Hello World! from Thread Number: 435
Hello World! from Thread Number: 416
Hello World! from Thread Number: 69
Hello World! from Thread Number: 452
Hello World! from Thread Number: 492
Hello World! from Thread Number: 353
Hello World! from Thread Number: 465
Hello World! from Thread Number: 518
Hello World! from Thread Number: 450
Hello World! from Thread Number: 510
Hello World! from Thread Number: 435
Hello World! from Thread Number: 416
Hello World! from Thread Number: 69
Hello World! from Thread Number: 452
```

临界区对象作为进程本地或线程本地对象存在，因此只会限制对与临界区对象具有相同上下文的资源的访问。如果临界区对象被实例化为非单例类的非静态成员，则不能用于限制对全局对象的访问。如果临界区是全局对象，则可用于限制对非单例类的非静态成员的访问，但这种临界区限制性太强，因为它会防范对数据成员每个实例的当前访问。

> **注意**
> 
> 我所说的“临界区限制性太强”是什么意思？创建一个临界区，并用这一个临界区解决多个并发问题，是相当方便的。但这可能会在临界区中造成瓶颈。有时更倾向于创建多个临界区，每个并发问题一个，而不是在多个并发访问全局资源的问题之间共享一个临界区。

如果从 CComCriticalSection 或 CComAutoCriticalSection 类继承，ATL 会自动在类中实现一个临界区对象。所有 ATL 对象都通过关联实现一个 CComAutoCriticalSection 对象。你的 ATL 对象具有名为 Lock() 和 Unlock() 的方法，这些方法被重定向到派生自 CComAutoCriticalSection 类的成员对象。清单 7.15 展示了 CComObjectRootEx 类的定义，所有 ATL 对象都派生自该类。

**清单 7.15**  `CComObjectRootEx` 的定义

```cpp
template <class ThreadModel>
class CComObjectRootEx : public CComObjectBase
{
public:
    typedef ThreadModel _ThreadModel;
    typedef _ThreadModel::AutoCriticalSection _CritSec;
    typedef CComObjectLockT<_ThreadModel> ObjectLock;

    ULONG InternalAddRef()
    {
        ATLASSERT(m_dwRef != -1L);
        return _ThreadModel::Increment(&m_dwRef);
    }
    ULONG InternalRelease()
    {
        ATLASSERT(m_dwRef > 0);
        return _ThreadModel::Decrement(&m_dwRef);
    }

    void Lock() { m_critsec.Lock(); }
    void Unlock() { m_critsec.Unlock(); }
private:
    _CritSec m_critsec;
};
```

`_CritSec` typedef 被定义为 `_ThreadModel::AutoCriticalSection`。根据 `_ThreadModel` 的类型定义，它被定义为 `CComAutoCriticalSection` 或 `CComFakeCriticalSection`。如果你的对象是自由线程的，则实现 `CComAutoCriticalSection`，否则实现 `CComFakeCriticalSection`。

### 瑞士军刀

所有这些 typedef 都相当令人困惑，因为 Microsoft 试图创建一个通用临界区，当线程模型不需要它时它什么都不做。这种通用设计通常会导致代码令人困惑。而它确实如此。

Microsoft 的一项设计考虑是让程序员编写其类时无需关心所使用的线程模型。为了少数将来某天会利用此特性的程序员，Microsoft 创建了多层 typedef 来迷惑我们其余的人。

这种过度设计有时被称为瑞士军刀设计模式。Microsoft 使用瑞士军刀设计模式的另一个例子是 MFC 的 `CString` 类。我认为 CString 类有一个方法可以将字符串翻译成 40 种不同的语言。我可能错了。
