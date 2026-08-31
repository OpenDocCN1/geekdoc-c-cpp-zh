
# 嵌入式系统的 C++

## 介绍

面向对象代码的伟大之处在于，它可以让简单的问题看起来变得庞大且复杂。在书中，我假设读者对 `C++` 已经非常熟悉。在整本书中，我展示了 `C++11` 中一些不为人知的特性，例如类型特征、常量表达式和 `OpenMP` 支持。我得出的结论是`C++`是完美的工具。

问题可以通过许多方式解决。我提供了一种替代方案并比较了性能。

## 致谢

我要感谢我的表弟兼朋友 `Andre`。没有 `Andre` 的帮助，这本书将会单薄得多。

## C++ 代码风格

```
#define AND &&
#define OR ||
#define EQ ==
```

在所有的源代码示例中，我尽力遵循了一致的 `C/C++` 风格。在书中，我没有将大括号单独放在一行，唯一的目的是为了让代码更短。更短的代码更有可能在较小的阅读器屏幕上显示。出于同样的原因，代码本身没有注释，希望注释的缺失通过穿插的解释得到了补偿。我使用了驼峰命名法。类型和类名以大写开头，变量以小写开头，而常量则全大写并用下划线分隔。

## 软件原语

### 互斥

在多任务环境中，线程和中断会并发读写数据对象。可以使用不同的工具来同步不同上下文之间的访问，并创建线程安全的 API。可用工具包括信号量、操作系统提供的互斥锁，以及禁用中断、禁用部分中断、禁用操作系统调度器以及使用自旋锁。当我为实时操作系统或硬件提供的 API 编写封装时，我希望封装尽可能轻量。通常，我使用汇编指令的数量来衡量封装的开销。指令数量是 CPU 周期或执行时间的良好估计。

```cpp
class LockDummy {
public:
    LockDummy() {
        cout << "Locked context" << endl;
    }
    ~LockDummy() {
        cout << "Lock is freed" << endl;
    }
};
```

在接下来的用法示例中，`C++`符 `auto` 告诉编译器自动提供正确的类型——`C++11`编译器知道在某些情况下推导出某些变量类型。例如，`C++`编译器可以推断赋值左侧的返回类型或函数的返回类型。

在 `main()` 函数中，编译器将调用输出函数两次，不会添加任何其他代码。当变量 `myDummyLock` 的作用域结束时，锁会被释放——调用析构函数 `~LockDummy`。该作用域可以是一个 `while` 循环。我不需要在函数每次返回之前调用"unlock"。`C++`编译器会确保析构函数总是被调用，且只被调用一次（更多关于 `RAII` 的信息请参见 [1]）。这种便利的服务不会产生任何性能开销。以下代码的输出将是：

```
Locked context
Protected context
Lock is freed
```

```cpp
int testDummyLock() {
#if (__cplusplus >= 201103) // 如果 C++11 或更高版本使用 "auto"
  auto myDummyLock = LockDummySimple();
#else
    LockDummySimple myDummyLock = LockDummySimple();
#endif

  cout << "Protected context" << endl;
  return 0;
}
```

我想通过另一个例子来强调这个观点。在下面的代码中，我在锁变量的声明周围设置了一个作用域。代码的输出将是：

```
Locked context
Protected context
Lock is freed
End of main
```

```cpp
int main() {
    {
        LockDummy lock;
        cout << "Protected context" << endl;
    }
    cout << "End of main" << endl;
    return 0;
}
```

我的第二个锁是一个更真实的锁，它会禁用硬件中断。我假设有一个可以禁用和启用中断的 API。我正在对原始锁代码进行一些重构。首先，我使用模板，这是 `C++` 的一个特性，允许你声明一个对泛型操作的类。我将重用模板 `Lock` 中的代码来处理不同的同步对象。模板 `Lock` 中的代码可以操作任何实现了两个公共方法（静态方法 `get()` 和 `release()`）的结构体或类。在这里我仔细地避免了多态，我不要求同步对象属于同一个类层次结构。禁用/启用中断 API 的封装器（它可能会写入硬件）不会是操作系统信号量封装器的子类/朋友/父类/关系/派生类。

禁用和启用中断的 API 如下：

```cpp
static inline void interruptDisable(void) {
  cout << "Disable" << endl;
}

static inline void interruptEnable(void) {
  cout << "Enable" << endl;
}
```

我正在描述一个同步对象。该类实现了两个方法："get"和"release"。这两个方法都是"inline"的，这有助于优化器决定是否应该将方法的调用替换为方法的代码。最终结果将类似于在 `C` 中使用宏定义。`SynchroObject` 类中的默认构造函数是私有的，我不希望应用程序中出现这种类型的对象。到目前为止，我的 `C++`编译器还没有向我的执行文件添加任何对象代码。

```cpp
class SynchroObject {
    SynchroObject() {};
public:
    static inline void get() {
        interruptDisable();
    }
    static inline void release() {
        interruptEnable();
    }
};
```

模板类 `Lock` 可以操作任何提供 `get/release` API 的同步对象类型。模板类 `Lock` 的所有方法都是"inline"的。`C++`编译器不会向对象代码添加任何函数，而是会将对 `Lock` 方法的调用替换为同步对象的 `get/release` 代码。

```cpp
template<typename Mutex> class Lock {
public:
    inline Lock() {
        Mutex::get();
    }
    inline ~Lock() {
        Mutex::release();
    }
};
```

声明一个新类型 `MyLock`，它使用我的 `SynchroObject` 来禁用/启用中断。除了对中断启用和禁用中断 API 的调用外，我的执行文件中没有额外的数据或代码。

```cpp
typedef Lock<SynchroObject> MyLock;
```

`main()` 函数的输出将是两个单词：`Disable`, `Enable`

```cpp
int main() {
    {
        MyLock lock;
    }
    return 0;
}
```

禁用和启用中断函数的封装开销完全为零。事实上，如果我检查反汇编，我会在主程序中看到两次对打印函数的调用，外无他物。我写了一些 `C++`代码，它们被优化成了空。我获得了什么？增值价值是什么？

这段代码没有允许我在调用禁用中断后忘记启用中断。无论我的函数有多少个返回点或跳出循环的地方，`C++`编译器都会确保 `interruptEnable` 函数恰恰被调用一次。

### 并行执行

有些人在面对问题时，会想："我知道了，我将使用线程"——然后他们就出了问题。

我的系统中有一个四核 CPU。我的硬件支持 `GCC 4.8` 编译器。如果我使用编译标记 `-fopenmp` 编译下面的代码，我将得到输出 "4"：

```cpp
void testReduction(void) {
  int a = 0;
  #pragma omp parallel reduction (+:a)
    {
      a = 1;
    }
  cout << a << endl;
}
```

如果没有 `-fopenmp` 标记，输出将是 "1"。当 `C++`编译器遇到 `pragma "omp parallel"` 时，它会添加一段代码，根据系统中的核心数产生一个线程"团队"（在 `Linux POSIX pthreads` 中）。接下来的部分由线程组并行执行。

在我的系统上执行以下函数，使用 `OpenMP` 需要 ~0.179s，而不使用 `OpenMP` 则需要 ~0.322s：

```cpp
volatile uint_fast8_t myArray[(size_t)512*1024*1024];
uint_fast32_t testOpenMPLoop() {
  uint_fast32_t sum = 0;
  #pragma omp parallel for reduction(+:sum)
  for (uint64_t i=0; i < sizeof(myArray); i++)
    {
      sum += myArray[i];
    }
  return sum;
}
```

如果数组大小小于 1000 万条目，`OpenMP` 会启动，而单线程版本需要更多的时间。

我的第一个示例是一个循环缓冲区（cyclic buffer），它也被称为环形缓冲区（ring buffer）。"生产者"向循环缓冲区的"尾部"（tail）添加对象，而"消费者"则从循环缓冲区的"头部"（head）提取对象。生产者的示例可以是一个中断服务程序，它从 `UART` 设备（RS232 端口）获取字符。"消费者"则是从应用程序主循环中调用的函数，用于处理来自 `UART` 的到达命令。`CyclicBuffer` 类是一个模板类，它应该帮助优化器为给定的整数类型和 CPU 架构生成尽可能高效的代码。

```cpp
template<typename  ObjectType, typename  Lock, std::size_t  Size>

class CyclicBufferSimple {
public:
 CyclicBufferSimple();
 ~CyclicBufferSimple() {}
 inline  bool add(const ObjectType object);
 inline  bool remove(ObjectType &object);
 inline  bool isEmpty();
 inline  bool isFull();

private:
 inline size_t increment(size_t index);
 inline  void errorOverflow() {}
 inline  void errorUnderflow() {}
 ObjectType  data[Size + 1];
 size_t  head;
 size_t  tail;
};
```

如果应用程序尝试在缓冲区中存储整数以外的任何内容，`CyclicBufferSimple`构造函数会导致构建失败。对于给定 CPU 架构上大于整数尺寸的对象，可能应该有不同的 API。

```cpp
template<typename  ObjectType, typename  Lock, std::size_t  Size>

CyclicBufferSimple<ObjectType, Lock, Size>::CyclicBufferSimple() {
#if (__cplusplus >= 201103)
 static_assert(std::numeric_limits<ObjectType>::is_integer, "CyclicBuffer is intended to work only with integer types");
#elif defined(__GNUC____)
 __attribute__((unused)) ObjectType val1 = 1;
#else
 volatile ObjectType val1;
    *(&val1) = 1;
#endif
 this->head = 0;
 this->tail = 0;
}
```

有两个方法返回缓冲区状态：

```cpp
template<typename  ObjectType, typename  Lock, std::size_t  Size>
inline  bool  CyclicBufferSimple<ObjectType, Lock, Size>::isEmpty() {
 bool res = (this->head == this->tail);
 return res;
}

template<typename  ObjectType, typename  Lock, std::size_t  Size>
inline  bool  CyclicBufferSimple<ObjectType, Lock, Size>::isFull() {
 size_t tail = increment(this->tail);
 bool res = (this->head == tail);
 return res;
}
```

一个处理缓冲区索引回绕的方法：

```cpp
template<typename  ObjectType, typename  Lock, std::size_t  Size>
inline  size_t  CyclicBufferSimple<ObjectType, Lock, Size>::increment(size_t index) {
 if (index < Size) {
 return (index + 1);
} else {
 return 0;
    }
}
```

循环缓冲区的添加/删除 API：

```cpp
template<typename  ObjectType, typename  Lock, std::size_t  Size>
inline  bool  CyclicBufferSimple<ObjectType, Lock, Size>::add(const ObjectType object) {
 Lock lock;
 if (!isFull()) {
 data[this->tail] = object;
 this->tail = increment(this->tail);
 return  true;
} else {
        errorOverflow();
 return  false;
    }
}

template<typename  ObjectType, typename  Lock, std::size_t  Size>
inline  bool  CyclicBufferSimple<ObjectType, Lock, Size>::remove(ObjectType &object) {
 Lock lock;
 if (!isEmpty()) {
object = data[this->head];
 this->head = this->increment(this->head);
 return  true;
} else {
        errorUnderflow();
 return  false;
    }
}
```

实例化新类型——一个无所操作的锁：

`typedef Lock<SynchroObjectDummy> LockDummy;`

以下函数返回循环缓冲区中的元素数量。如果值无法在构建时计算，编译器将失败：

```cpp
constexpr  size_t calculateCyclicBufferSize() {
 return 10;
}
```

我创建了一个 `CyclicBuffer` 类的对象来处理 8 位无符号整数。我使用了 `uint_fast8_t`，这是另一个针对移植性的 `C++11` 特性。类型 `uint_fast8_t` 允许 `C++`编译器选择至少有 8 位的最佳性能整数。在某些 CPU 上，32 位整数的操作比 8 位操作更快。如果性能比存储分配的内存更重要，选择 32 位整数而不是 8 位是有意义的。最小可能的 8 位无符号整数是 `uint_least8_t`，平台上可用的无符号整数是 `uintmax_t`。

`static CyclicBufferSimple<uint_fast8_t, LockDummy, calculateCyclicBufferSize()> myCyclicBuffer;`

在用法示例中有一个来自 `C++11` 标准范围循环。主函数将打印数字 1, 3, 11：

```cpp
int  main() {
 for (int i : { 1, 3, 11 }) {
        myCyclicBuffer.add(i);
    }
 uint8_t val;
 while (myCyclicBuffer.remove(val)) {
        cout << (int) val << endl;
    }
 return 0;
}
```

让我们查看 `GNU C` 编译器为 Intel CPU 生成的单次 `add()` 方法调用的汇编代码。



# 汇编代码示例

```assembly
xor %esi,%esi
 inline  void add(const ObjectType object) {
mov 0x2009c0(%rip),%rax
 return (index + 1);
mov %rsi,%r8
...............................................
 inline  void add(const ObjectType object) {
mov %rcx,%rdx
cmovbe %rdi,%r8
 if (!isFull()) {
cmp %r8,%rax
...............................................
         data[this->tail] = object;
movb $0x0,0x6011a0
```

# C 代码示例

```cpp
size_t tail = CyclicBufferIncrement(cyclicBuffer->tail, CYCLIC_BUFFRE_SIZE);

 bool res = (cyclicBuffer->head == tail);

return res;

}

static inline void errorOverflow() {

}

static inline void errorUnderflow() {

}

static inline bool CyclicBufferAdd(CyclicBuffer* cyclicBuffer, const CYCLIC_BUFFER_OBJECT_TYPE object) {

 if (!CyclicBufferIsFull(cyclicBuffer)) {
        cyclicBuffer->data[cyclicBuffer->tail] = object;
        cyclicBuffer->tail = CyclicBufferIncrement(cyclicBuffer->tail, CYCLIC_BUFFRE_SIZE);
 return true;
} else {
        errorOverflow();
 return false;
    }
}

static inline bool CyclicBufferRemove(CyclicBuffer* cyclicBuffer, CYCLIC_BUFFER_OBJECT_TYPE* object) {

 if (!CyclicBufferIsEmpty(cyclicBuffer)) {
        *object = cyclicBuffer->data[cyclicBuffer->head];
        cyclicBuffer->head = CyclicBufferIncrement(cyclicBuffer->head, CYCLIC_BUFFRE_SIZE);
 return true;
} else {
        errorUnderflow();
 return false;
    }
}
```

函数`main`输出数字 0,1,2,3

```cpp
int main() {

 for (int i = 0;i < 4;i++) {
        CyclicBufferAdd(&myCyclicBuffer, i);
    }
 uint8_t val;

 while (CyclicBufferRemove(&myCyclicBuffer, &val)) {
        cout << (int) val << endl;
    };
 return 0;
}
```

这段代码具有一些局限性。只有操作相同整数类型的循环缓冲区才能在同一个 C 源文件中使用。添加/删除函数只能在一个 C 文件中定义一次。

对应的汇编代码包含调用`add()` API 的 10 个操作码：

```assembly
 return (index + 1);

 xor %esi,%esi
```

```assembly
static inline void CyclicBufferAdd(CyclicBuffer* cyclicBuffer, const CYCLIC_BUFFER_OBJECT_TYPE object) {

  mov 0x2009be(%rip),%rax        # 0x6011b0 <myCyclicBuffer+16>
 return (index + 1);
  mov %rsi,%r8
```

```assembly
int main() {

  push %rbp
 return (index + 1);
  lea 0x1(%rcx),%rdi
...............................................
```

```assembly
static inline void CyclicBufferAdd(CyclicBuffer* cyclicBuffer, const CYCLIC_BUFFER_OBJECT_TYPE object) {

  mov %rcx,%rdx
  push %rbx
 return (index + 1);
  cmovbe %rdi,%r8
...............................................
```

```assembly
 if (!CyclicBufferIsFull(cyclicBuffer)) {

  cmp %r8,%rax
...............................................
        cyclicBuffer->data[cyclicBuffer->tail] = object;
  movb $0x0,0x6011a0(%rcx)
```

GNUC 针对 ARM 为 C 代码和 C++ 代码产生基本上相同的汇编代码

```assembly
xor    %esi,%esi
mov    0x2009be(%rip),%rax
mov    %rsi,%r8
push    %rbp
lea    0x1(%rdx),%rdi
cmp    $0x9,%rdx
mov    %rdx,%rcx
push    %rbx
cmovbe %rdi,%r8
cmp    %r8,%rax
je 40081c <main+0x3c>
movb  $0x0,0x6011a0(%rdx)
mov    %r8,%rcx
mov    %r8,0x20099c(%rip)
xor    %r12d,%r12d
```

在 Intel 上测量的 C 版本和 C++ 性能是相同的。

# C++ 模板

要理解什么是递归，你必须首先理解递归。

此时，一个耐心的读者会询问由于 C++ 模板和对象代码重复导致的“代码膨胀”。通常情况下，C 语言实现的内存占用应该更小，不是吗？

在循环缓冲区的 C++ 实现中，所有方法都是内联的（inline），并且没有特定的“模板代码”。在一般情况下，对于代码中使用的每一对`ObjectType`/`Size`，C++ 编译器都会实例化一个类并将全套方法添加到应用程序代码中。一个仔细的 C++ 程序员应该将不需要模板参数的方法移动到基类中，并从该新类派生`CyclicBuffer`模板。将类型无关的代码移动到基类中通常被称为“代码提升”（code hoisting）。代码提升并不一定会导致性能损耗。在下面的示例中，我将基类命名为`CyclicBufferBase`。基类的构造函数是保护的（protected）。应用程序只能创建子类的对象。

```cpp
class CyclicBufferBase {
public:
 bool isEmpty() {
 bool res = (this->head == this->tail);
 return res;
    }
 bool isFull() {
 size_t tail = increment(this->tail);
 bool res = (this->head == tail);
 return res;
    }
protected:
 CyclicBufferBase(size_t size) {
 this->size = size;
 this->head = 0;
 this->tail = 0;
    }
 void errorOverflow() {

    }
 void errorUnderflow() {

    }
 size_t increment(size_t index) {
 if (index < this->size) {
return (index + 1);
} else {
 return 0;
    }
    }
 size_t head;
 size_t tail;
 size_t size;
};
```

模板类`CyclicBuffer`包含了依赖模板参数`Size`的数据以及取决于整数类型的添加/删除方法。`CyclicBuffer`类派自`CyclicBufferBase`类，继承了`CyclicBufferBase`的所有方法，并暴露了`CyclicBufferBase`的所有方法。

```cpp
template<typename ObjectType, typename Lock, std::size_t Size>
class CyclicBuffer:public CyclicBufferBase {
public:
 CyclicBuffer() :
        CyclicBufferBase(Size) {
 static_assert(std::numeric_limits<ObjectType>::is_integer, "CyclicBuffer is intended to work only with integer types");
    }
 ~CyclicBuffer() {
}
 bool add(const ObjectType object) {
 Lock lock;
 if (!isFull()) {
data[tail] = object;
tail = increment(tail);
 return true;
} else {
        errorOverflow();
 return false;
    }
}
 bool remove(ObjectType &object) {
 Lock lock;
 if (!isEmpty()) {
object = data[head];
head = increment(head);
 return true;
} else {
        errorUnderflow();
 return false;
    }
}
private:
 ObjectType data[Size + 1];
};
```

我将通过声明一个新类`Stack`来开始关于内存池动态内存分配的讨论。模板类`Stack`与之前使用的`CyclicBuffer`类类似。`Stack`类实现了两个方法：`push`和`pop`。

```cpp
template<typename ObjectType, typename Lock, std::size_t Size>
class Stack: public StackBase {
public:
    Stack() :
    StackBase(Size) {
    }
    ~Stack() {
    }
    inline bool push(ObjectType* object);
    inline bool pop(ObjectType** object);
private:
    ObjectType* data[Size + 1];
};
```

基类`StackBase`包含`top`和`size`字段，以及一些有用的 API。

```cpp
class StackBase {
public:
    bool isEmpty() {
        bool res = (this->top == 0);
        return res;
    }
    bool isFull() {
        bool res = (this->top == size);
        return res;
    }
protected:
    StackBase(size_t size) {
        this->size = size;
        this->top = 0;
    }
    void errorOverflow() {
    }
    void errorUnderflow() {
    }
    size_t top;
    size_t size;
};
```

`push`和`pop`方法实现示例：

```cpp
template<typename ObjectType, typename Lock, std::size_t Size>
inline bool Stack<ObjectType, Lock, Size>::push(ObjectType* object) {
    Lock lock;
    if (!isFull()) {
        data[this->top] = object;
        this->top++;
        return true;
    } else {
        errorOverflow();
        return false;
    }
}

template<typename ObjectType, typename Lock, std::size_t Size>
inline bool Stack<ObjectType, Lock, Size>::pop(ObjectType** object) {
    Lock lock;
    if (!isEmpty()) {
        this->top--;
        *object = (data[this->top]);
        return true;
    } else {
        errorUnderflow();
        return false;
    }
}
```

我的下一步工作是定义一个“原始”数据内存块。一个内存块是一个正确对齐的字节数组，可选情况下，它可以放置在特定的内存地址上。内存块的一个流行应用是 DMA 传输。数据缓冲区可以放在普通 RAM 中，也可以放在专用地址空间中。

我定义了一个内存区域。我使用`new`运算符——定位 new 运算符（placement new）——将数据`place`在指定的地址。我的内存区域为了调试目的有一个名称。区域地址的类型为`uintptr_t`，这是一个能够存储指针的无符号整数。

```cpp
class MemoryRegion {
public:
    MemoryRegion(const char *name, uintptr_t address, size_t size) :
    name(name), address(address), size(size) {
        data = new (reinterpret_cast<void*>(address)) uint8_t[size];
    }
    size_t getSize() const {
        return size;
    }
    const char* getName() const {
        return name;
    }
    uintptr_t getAddress() const {
        return address;
    }
protected:
    const char *name;
    uintptr_t address;
    size_t size;
    uint8_t *data;
};
```

我创建了一个`MemoryRegion`类型的对象，并指向动态数据中的`dmaMemoryData`区域：

```cpp
static uint8_t dmaMemoryDummy[512];
static MemoryRegion dmaMemoryRegion("dmaMem", (uintptr_t)dmaMemoryDummy, sizeof(dmaMemoryDummy));
```

我需要一个分配器。这是一个处理内存块分配的类。分配器处理正确的对齐。我将只使用一次（或很少）分配器代码。例如，当我用数据块填充我的内存池时，我需要一个分配器。在这里性能并不极端重要。`reset`方法将所有分配的块“释放”回分配器。



```cpp
class MemoryAllocatorRaw {
public:
    MemoryAllocatorRaw(MemoryRegion memoryRegion,
    size_t blockSize,
    size_t count, unsigned int alignment);
    uint8_t* getBlock();
    bool blockBelongs(const void* block) const;
    const MemoryRegion& getRegion() const;
    void reset();
    constexpr static size_t predictMemorySize(
    size_t blockSize,
    size_t count, unsigned int alignment);
protected:
    int alignment;
    size_t blockSize;
    const MemoryRegion& memoryRegion;
    size_t count;
    size_t sizeTotalBytes;
    size_t alignedBlockSize;
    uintptr_t firstNotAllocatedAddress;
    static constexpr size_t alignConst(size_t value,
    unsigned int alignment);
    inline static uintptr_t alignAddress(uintptr_t value,
    unsigned int alignment);
};
```

分配器的实现如下。构造函数确保有足够的空间。我在构造函数之后初始化字段：

```cpp
MemoryAllocatorRaw::MemoryAllocatorRaw(MemoryRegion memoryRegion,
size_t blockSize,
size_t count, unsigned int alignment) :
alignment(alignment), blockSize(blockSize), memoryRegion(memoryRegion), count(count) {
    alignedBlockSize = alignConst(blockSize, alignment);
    sizeTotalBytes = alignedBlockSize * count;
    firstNotAllocatedAddress = memoryRegion.getAddress();
}
```

`getBlock` 方法调用 `alignAddress`：

```cpp
uint8_t* MemoryAllocatorRaw::getBlock() {
    uint8_t* block = (uint8_t*)firstNotAllocatedAddress;
    firstNotAllocatedAddress += alignedBlockSize;
    return block;
}
```

`blockBelongs` 需要检查块是否属于该池：

```cpp
bool MemoryAllocatorRaw::blockBelongs(const void* block) const {
    uintptr_t blockPtr = (uintptr_t)block;
    size_t maxAddress = memoryRegion.getAddress() + sizeTotalBytes;
    return blockPtr <= maxAddress;
}
```

剩余的方法：

```cpp
constexpr size_t MemoryAllocatorRaw::alignConst(size_t value,
unsigned int alignment) {
    return (value + (alignment - 1)) & ~(alignment - 1);
}

uintptr_t MemoryAllocatorRaw::alignAddress(uintptr_t value,
unsigned int alignment) {
    return (value + (alignment - 1)) & ~(alignment - 1);
}

const MemoryRegion& MemoryAllocatorRaw::getRegion() const {
    return memoryRegion;
}

void MemoryAllocatorRaw::reset() {
    firstNotAllocatedAddress = memoryRegion.getAddress();
}
```

在声明分配器对象之前，我检查内存区域是否足够。如果内存区域太小，我希望编译失败：

```cpp
static_assert((sizeof(dmaMemoryDummy) >= MemoryAllocatorRaw::predictMemorySize(63, 2, 2)), "DmaMemoryDummy region not enough");
static MemoryAllocatorRaw dmaAllocator;
```

我的内存池是数据块的堆栈。该类包含 `allocate/free` API 以及一些调试统计信息。每个内存池都有一个名称。为对象提供名称对于日志记录和打印调试统计很有用。内存池中的栈由 `Lock` 保护，不是线程安全的。我将在内存池的方法中使用真正的同步器。

签名中带有 `const` 关键字类方法，例如 `resetMaxInUse()`，无法更改类的任何成员。那么 `resetMaxInUse()` 如何能更改 `statistics` 字段呢？`statistics` 字段是 `mutable` 的，这允许 `const` 方法修改它。调试计数是使用 `mutable` 关键字的经典示例。`resetMaxInUse()` 方法不会影响（以有意义的方式）对象的可见状态。

```cpp
template<typename Lock, size_t Size>
class MemoryPoolRaw {
public:
    MemoryPoolRaw(const char* name, MemoryAllocatorRaw* memoryAllocator);
    ~MemoryPoolRaw() {
        memoryAllocator->reset();
    }
    inline void resetMaxInUse() const {
        statistics.maxInUse = 0;
    }
    typedef struct {
        uint32_t inUse;
        uint32_t maxInUse;
        uint32_t errBadBlock;
    } Statistics;
    inline bool allocate(uint8_t** block);
    inline bool free(uint8_t* block);
    inline const Statistics &getStatistics(void) const {return statistics;}
protected:
    mutable Statistics statistics;
};
```

```cpp
mutable Statistics statistics;

const char* name;

Stack<uint8_t, LockDummy, Size> pool;

MemoryAllocatorRaw* memoryAllocator;

};
```

内存池构造函数会调用分配器来填充空闲块栈。构造函数可以例如将新创建的内存池注册到内存池数据库中。应用程序可以内存池的运行时检查提供含义。析构函数将把内存池从数据库中移除：

```cpp
template<typename Lock, size_t Size>
MemoryPoolRaw<Lock, Size>::
MemoryPoolRaw(const char* name, MemoryAllocatorRaw* memoryAllocator) :
name(name), memoryAllocator(memoryAllocator) {
  memset(&this->statistics, 0, sizeof(this->statistics));
  for (size_t i = 0; i < Size;i++) {
    uint8_t *block = memoryAllocator->getBlock();
    pool.push(block);
  }
}
```

如果 `Lock` 类不是空锁（dummy lock），则内存池的分配/释放 API 是重入且线程安全的。所有可以修改栈状态的活动都受到 `lock` 的保护。如果应用程序仅在一个上下文中使用池，则可以为内存池提供 `LockDummy` 模板参数。`LockDummy` 不会向执行文件中添加任何代码。统计计数器的开销相对，但对于调试分配失败等错误非常有帮助。

```cpp
template<typename Lock, size_t Size>
inline bool MemoryPoolRaw<Lock, Size>::
allocate(uint8_t** block) {
  bool res;
  Lock lock;
  res = pool.pop(block);
  if (res) {
    statistics.inUse++;
    if (statistics.inUse > statistics.maxInUse)
      statistics.maxInUse = statistics.inUse;
  }
  return res;
}
```

内存池的“释放”确保指针属于该池。内存分配器知道识别它自己的块。

```cpp
template<typename Lock, size_t Size>
inline bool MemoryPoolRaw<Lock, Size>::
free(uint8_t* block) {
  bool res;
  Lock lock;
  res = memoryAllocator->blockBelongs(block);
  if (res) {
    res = pool.push(block);
    statistics.inUse--;
  } else {
    statistics.errBadBlock++;
  }
  return res;
}
```

防止多次释放同一个块是相当容易的。如果数据块是连续内存的一部分，分配器可以提供一种基于块地址生成唯一索引的方法。内存池可以包含一个数组，其中块被标记为已分配或空闲，`free()` 方法可以根据此数组检查块。如果内存区域不是连续的，分配器可以实现一个哈希函数，将数据块的地址转换为唯一的数据块索引。

## 运算符 new

算法（名词）

程序员当他们不想解释自己做了什么时使用的词。

许多小型微控制器用于动态内存分配的堆空间相对较小。完全不使用动态内存分配的设计选择非常流行。在固件中，使用 C/C++ 库中 `new` 和 `delete` 运算符的标准实现通常没有意义。如果系统耗尽空闲内存，`new` 运算符（其本身是一个动态分配的对象）可能会抛出异常。在运行时对不同对象调用 `new` 和 `delete` 最终会导致内存碎片。后章节中的软件定时器和 STL 容器可以利用采用自定义分配器的用户定义内存分配。自定义的运算符 `new` 可以基于“放置 new（placement new）”。`CyclicBufferDynamic` 类中的构造函数可以这样重定义：

```cpp
template<typename ObjectType, typename Lock>
inline CyclicBufferDynamic
<ObjectType, Lock>::
CyclicBufferDynamic(size_t size, void *address) {
  this->head = 0;
  this->tail = 0;
  this->size = size;
  if (address != nullptr) {
    this->data = new (address) ObjectType[size];
  } else {
    this->data = new ObjectType[size];
  }
  static_assert(sizeof(ObjectType) <= sizeof(uintptr_t), "CyclicBuffer 仅旨在用于整数类型或指针");
}
```

在接下来的示例中，我让编译器静态分配所需的内存，并在调用构造函数时已分配数据的地址：

```cpp
static uint32_t myDynamicCyclicBufferData[calculateCyclicBufferSize()];
CyclicBufferDynamic<uint32_t, LockDummy> myDynamicCyclicBuffer(calculateCyclicBufferSize(), &myDynamicCyclicBufferData);
```

## I/O 访问

需要多少个程序员才能换灯泡？不需要——这是一个硬件问题。

嵌入式软件通过硬件寄存器访问硬件。我假设有三组寄存器：读写寄存器、只读寄存器和只写寄存器。所有寄存器都是内存映射的，每个寄存器都有一个地址。软件访问寄存器的方式与给定变量地址读写变量的方式相同。对于只写寄存器，习惯是保留一个缓存值。缓存是位于数据内存中的一个变量，包含写入只写寄存器的最新值。

以下示例基于 Atmel SAMA5d3 微控制器中的并行输入/输出控制器（PIO）的用户界面。为了节省代码行和文本，我简化了接口。

| 地址 | 名称 | 寄存器 | 权限 |
| :--- | :--- | :--- | :--- |
| `0x0000` | PIO 启用寄存器 | `PIO_PER` | 只写 |
| `0x0004` | PIO 禁用寄存器 | `PIO_PDR` | 只写 |
| `0x0008` | PIO 状态寄存器 | `PIO_PSR` | 只读 |
| `0x000C` | 预留 | | |
| `0x0010` | 输出启用寄存器 | `PIO_OER` | 只写 |
| `0x0014` | 输出禁用寄存器 | `PIO_ODR` | 只写 |
| `0x0018` | 输出状态寄存器 | `PIO_OSR` | 只读 |
| `0x001C` | 预留 | | |
| `0x0020` | 未使用 | | |
| `0x0024` | 未使用 | | |
| `0x0028` | 未使用 | | |
| `0x002C` | 预留 | | |
| `0x0030` | 设置输出数据寄存器 | `PIO_SODR` | 只写 |
| `0x0034` | 清除输出数据寄存器 | `PIO_CODR` | 只写 |
| `0x0038` | 输出状态寄存器 | `PIO_ODSR` | 只读 |

微控制器中有五个如 A、B、C、D、E 的块。寄存器从 `0xFFFFF00` 开始映射。想要修改只写寄存器的用户应向相关位写入 1。例如，用户应向 `PIO_SODR` 写入 `0x04`。

## C 语言中的 I/O 访问

“用 C 或 C++ 编写就像在移除所有安全防护的情况下电锯” —— Bob Gray。

我提供了快速粗糙的 C。宏 `RESER` 展示了一个生成唯一标识符的巧妙技巧。

```c
#define TOKEN_CAT(x, y) x ## y
#define TOKEN_2(x, y) TOKEN_CAT(x, y)
#define RESERVED TOKEN_2(reserved, __COUNTER__)
```

PIO 结构体，一组 32 位。我想确保编译器不进行任何填充并将结构体标记为“紧凑（packed）”。Pragma “pack”可能是不安全的。某些架构如 ARM 或 MIPS 不支持对齐访问。

```c
#pragma pack(push)
#pragma pack(1)
struct PIO {
  volatile uint32_t PIO_PER;
  volatile uint32_t PIO_PDR;
  volatile uint32_t PIO_PSR;
  volatile uint32_t RESERVED;
  volatile uint32_t PIO_OER;
  volatile uint32_t PIO_ODR;
  volatile uint32_t PIO_OSR;
  volatile uint32_t RESERVED;
  volatile uint32_t RESERVED;
  volatile uint32_t RESERVED;
  volatile uint32_t RESERVED;
  volatile uint32_t RESERVED;
  volatile uint32_t PIO_SODR;
  volatile uint32_t PIO_CODR;
  volatile uint32_t PIO_ODSR;
};
#pragma pack(pop)
```

指向内存区域的指针：

```cpp
#ifdef REAL_HARDWARE
static PIO *pios = (PIO*)0xFFFFF200;
#else
static PIO pioDummy[5];
static PIO *pios = pioDummy;
#endif
```

五个 PIO 块：

```c
typedef enum {
  PIO_A,
  PIO_B,
  PIO_C,
  PIO_D,
  PIO_E,
  PIO_F,
} PIO_NAME;
```

## PIO 配置指南

将引脚配置为输出的函数：



```cpp
static void enableOutput(PIO_NAME name, int pin, int value) {
  PIO *pio = &pios[name];
  uint32_t mask = 1 << pin;
  if (value) {
    pio->PIO_SODR = mask;
  }
  else {
    pio->PIO_CODR = mask;
  }
  pio->PIO_PER = mask;
  pio->PIO_OER = mask;
}
```

驱动 `PIO A` 引脚 2 置高函数可能如下所示：

```cpp
static void main() {
  enableOutput(PIO_A, 2, 1);
}
```

## Intel 汇编

这是 Intel 相关的汇编代码——正如预期的，有三个 32 位的移动：

```assembly
PIO *pio = &pios[name];
uint32_t mask = 1 << pin;
if (value) {
  pio->PIO_SODR = mask;
4007e0:             c7 05 e6 19 20 00 04             movl  $0x4,0x2019e6(%rip)
4007e7:             00 00 00
4007ea:31 c0                             xor %eax,%eax
  pio->PIO_SODR = mask;
}
else {
  pio->PIO_CODR = mask;
}
pio->PIO_PER = mask;
4007ec:             c7 05 aa 19 20 00 04             movl  $0x4,0x2019aa(%rip)
4007f3:             00 00 00
pio->PIO_OER = mask;
4007f6:             c7 05 b0 19 20 00 04             movl  $0x4,0x2019b0(%rip)
4007fd:             00 00 00
```

## ARM 汇编

为 ARM 生成的汇编代码稍长。在 ARM 中，存储值之前应将地址加载到寄存器中。

```assembly
PIO *pio = &pios[name];
uint32_t mask = 1 << pin;
if (value) {
  pio->PIO_SODR = mask;
8650:             e59f3014               ldr             r3, [pc, #20]
8654:             e3a02004               mov             r2, #4
8658:             e5832090               str             r2, [r3, #144]
865c:             e3a00000               mov             r0, #0
  pio->PIO_SODR = mask;
}
else {
  pio->PIO_CODR = mask;
}
pio->PIO_PER = mask;
8660:             e5832060               str             r2, [r3, #144]
pio->PIO_OER = mask;
```

# C++ 封装实现

以下结构表示了用于封装 PIO 操作的 C++ 类：

```cpp
class HardwarePIO {
public:
  HardwarePIO(uintptr_t address) : interface((struct Interface*)address) {}
  ~HardwarePIO() {}

  Interface &getInterface(Name name) const {
    return interface[name];
  }

  void enableOutput(Name name, int pin, int value) {
    Interface &interface = getInterface(name);
    uint32_t mask = 1 << pin;
    if (value) {
      interface.PIO_SODR = mask;
    }
    else {
      interface.PIO_CODR = mask;
    }
    interface.PIO_PER = mask;
    interface.PIO_OER = mask;
  }

private:
  enum Name { A, B, C, D, E, F, LAST };
  struct Interface {
    volatile uint32_t PIO_SODR;
    volatile uint32_t PIO_CODR;
    volatile uint32_t PIO_PER;
    volatile uint32_t PIO_OER;
  };
  Interface *interface;
};
```

对 PIO 寄存器的访问被封装在硬件模块类方法中。`HardwarePIO` 类中的方法是修改寄存器的唯一方式。C++ 实现允许在编译时捕获其他错误操作，例如读取或写入预留寄存器。

在硬件模块中缓存所有写入值是非常容易。在硬件模块类中添加一个“影子”（shadow）接口字段，是缓存或记录读写事务的一种方法。

# 间接 I/O 访问

在某些情况下，硬件可以通过串口接口访问。此类接口的一个例子是 `SPI`。为了简洁起见，我使用了直接访问 API。真实 SPI 设备的真实访问接口可以包含系统调用或对串口接口驱动的调用：

```cpp
template<typename IntegerType>
class HardwareDirectAccessAPI {
public:
  inline uint32_t get() const {
    return atomic_load(&value);
  }
  inline void set(uint32_t value) {
    atomic_store(&this->value, value);
  }
protected:
  volatile atomic<IntegerType> value;
  static_assert(numeric_limits<IntegerType>::is_integer, "HardwareDirectAccessAPI works only with integer types");
};
```

我为模板类 `HardwareRegister` 添加了一个参数：

```cpp
template<typename IntegerType, typename AccessAPI>
class HardwareRegister {
protected:
  HardwareRegister() {}
  inline IntegerType get() const {
    return api.get();
  }
  inline void set(IntegerType value) {
    api.set(value);
  }
  AccessAPI api;
};
```

用于 32 位寄存器的 `HardwareRegister` 实例，直接访问看起来如下：

```cpp
class HardwareRegister32: public HardwareRegister<uint32_t, HardwareDirectAccessAPI<uint32_t> > {
protected:
  HardwareRegister32() {}
};
```

其他类保持不变。

# 代码 ROM 和数据 RAM

如果一开始没有成功，就把它称作版本 1.0。

有一些非常流行的硬件平台，ROM 和 RAM 的区别非常重要。此类设备的一个例子是相当流行的 8 位微控制器 `Atmega`。在 `Atmega` MCU 中，代码不能放置在数据内存中，CPU 无法执行位于 RAM 中的代码。对代码内存中数据的任何访问都需要特殊指令。

另一个例子是应用专用集成电路或 `ASICs`。`ASIC` 通常包含集成 ROM 和 RAM。集成的（也称为片上或芯片内）ROM 存储廉价，因为在硅片上需要的空间较小。RAM 相对昂贵，因为每位内存需要更多逻辑，且集成电路（芯片）的平方英寸非常贵。RAM 消耗的功率大得多。

我认为我们周围的大多数电子设备内部都有集成 ROM 和 RAM（通常是 `SRAM`）。通常，片上 RAM 远小于 ROM。

ROM 有两种类型：可擦写和不可擦写。在 `Atmega` MCU 中，ROM 的不同区域可以由固件编程，前提是固件运行另一个区域。在 `ASICs` 中，ROM 通常是不可擦写的。ROM 的编程是 ASIC 生产过程的一部分。芯片离开工厂（`FAB`）后，ROM 无法被修改。

如果没有足够的 RAM 来加载固件，那么部分固件代码应该位于芯片 ROM 中。对于 `ASIC`，这意味着基于 ROM 的固件部分只能在未来的芯片版本中进行更改。现代 ASIC 固件的高复杂度使得在 ASIC 验证过程中很难达到 100% 的代码覆盖。即使基于 ROM 的固件经过了完全验证和测试，仍有可能开发团队误解了某个协议，或者产品需求发生了变化。开发团队准备固件和硬件，是为了应对极可能出现的对 ROM 进行补丁的需求。

本章涵盖了某些与 ROM 有关的问题。

## C++ 初始化数据

至少有一个代码段、启动程序、常量和初始化数据是 ROM 的部分。初始化的非零数据将消耗双倍内存。初始化数据的初始化值是 ROM 的一部分。通常，启动过程会将值从 ROM 复制到 RAM。

如果我检查编译器生成的对象文件，可以很容易找到字符串的初始化数据。有一些工具可以帮助检查对象文件、将不同段转储到单独的文件，并为 ROM 编程准备镜像。此类工具的一个例子是 `GNU objdump`。

让我们来看一些 C++ 初始化数据的实际应用。以下代码产生两行输出：“Hello, world!”，紧接着是“Hello from main()!”。

```cpp
class HelloWorld {
public:
  HelloWorld() {
    cout << "Hello, world!" << endl;
  }
};
static HelloWorld helloWorld;
int main() {
  cout << "Hello from main()!" << endl;
  return 0;
}
```

`main()` 函数只包含一个输出。负责初始化 C++ 对象 `helloWorld` 并打印第一行的实体运行在我操作系统中的对象加载器。在嵌入式系统中，这段代码通常是启动过程的一部分。

`HelloWorld` 类的构造函数是“文本”，在 ROM 中只出现一次。`cout` 的参数（字符串）存在于内存中的两个地方：原始或“主副本”在 ROM 中，由加载器创建的第二个副本在 RAM 中。包含静态分配对象 `helloWorld` 地址的指针 `this` 也有两个副本。ROM 中有一个 `this` 指针的初始化值，RAM 中也有 `this` 指针。

在 32 位 CPU 的 ROM 中，为 `helloWorld` 对象分配的空间至少包含 4 字节的 `this` 和 14 字节的零终止字符串。链接脚本负责代码和数据不同段的正确放置。如果 CPU 无法访问存储在代码内存中的数据，链接脚本应包含相关的分配指令。具体来说，常量数据段将被分配两次：在代码 ROM 地址空间和在 RAM 中。

在通常情况下，链接脚本会添加全局变量，引用未初始化数据段 `bss` 的起始和结束地址、初始化数据，以及一个 `ctor` 函数表。通常，`ctor` 段是一个函数表，启动代码通过调用这些函数来初始化静态 C++ 对象。详细信息请参考你的链接器文档。

## ROM 补丁

编程很像性爱。犯一个错，你就得提供一辈子的支持。

我想为未来的补丁准备构造函数代码。我将检查 RAM 中的某些位置。如果有非零条，我将使用那里的字符串。如果没有，我将打印默认值——即 ROM 中的那一个。

```cpp
static const char *helloWorldStr = 0;
class HelloWorld {
public:
  HelloWorld() {
    if (helloWorldStr == 0)
      cout << "Hello, world!" << endl;
    else
      cout << helloWorldStr << endl;
  }
};
```

加载可以打补丁的 ASIC 有两个阶段。

在第一阶段，外部 CPU（也称为主机处理器）将某些固件加载到 ASIC RAM 中。有一个专用的硬件/启动固件支持将应用固件加载到 RAM 中。另一种方案是 ASIC 中的启动固件从某些外部可编程存储芯片加载应用固件，例如 `EEPROM` 或 `SPI FLASH`。

第二阶段是启动程序跳转到 RAM 中的应用代码。如果主机处理器加载的代码在 `helloWorldStr` 地址处包含非零，则基于 ROM 的应用代码将打印新字符串。我将这种类型的补丁称为 A 类补丁。在 A 类补丁中，我修复函数的一部分。

对于 B 类补丁，我需要硬件支持。当 CPU 从特定地址或地址范围获取指令时——在下面的代码中，这是函数 `printHello()` 的地址——我希望“中断”执行并将控制权切换到位于 RAM 中的中断处理程序。

默认的中断处理程序什么都不做。该处理程序是空的并直接返回，允许 `printHello()` 函数完成它的有用工作。补丁后的中断处理程序可以在允许 `printHello()` 函数打印它之前修改 RAM 中的字符串“Hello, world”。中断处理程序可以执行某些任意代码并将控制权返回给 `printHello()` 的调用者，完全跳过原始的打印代码。

```cpp
class HelloWorld {
public:
 HelloWorld() {
        printHello();
    }
protected:
 void  printHello() {
cout << "Hello, world!" << endl;
    }
};
```

对于 C 类补丁，我需要在链接脚本中获得支持。我想将 `HelloWorld` 的构造函数放在 ROM 中，但 `printHello()` 方法我想在 RAM 中执行。如果 `HelloWorld` 构造函数调用了 RAM 中的函数，我就可以轻松地补丁该函数代码。

# 组合

你是否注意到过 `C` 项目计划与 C++ 项目计划之间的区别？C++ 项目的规划阶段是 C 的三倍。这正是为了确保所有应该继承的都继承了，而不应该继承的没有。尽管如此，他们仍然会出错。

记得平均规模的 `C` 项目的长度吗？大约 6 个月。对于一个有妻有儿的男人来说，这段时间远远不足以维持体面的生活。拿同一个项目，用 C++ 设计，你会得到什么？我告诉你。一到两年。这难道不棒吗？

我将尝试为“创建任务” API 编写一个包装器。类似于 `pthread_create` 或 `FreeRTOS xTaskCreate` 等 API 的典型包装器是基于类（例如 `MyThread`）中的静态方法的。事实上，这是我知道的编写适用于大多数操作系统的可移植 C++ 包装器的唯一方法。

我将适当地展示这种方法的基本示例，不是因为它们迷人，而是因为一本合理的“嵌入式 C++”书籍对此有所期望。你可以自由跳转到下一段，我在那里将展示非可移植的 C++ 创建任务包装器代码。

## 静态（类）成员

C 允许你射自己的脚。C++ 允许你重用子弹。

我将从一个池中分配我的作业线程对象。例如，远程过程调用（Remote Procedure Call）的实现可以使用作业线程池在本地执行过程。从内存池分配线程对象比调用操作系统 API 创建新线程更快。

`MemoryPool` 是一个通用的对象池，它静态地分配对象。这是对之前章节中内存池类的重用。我在这里跳过了一些细节，例如池的名称、调试统计等。

```cpp
template<typename Lock, typename ObjectType, size_t Size>
class MemoryPool {
public:
 MemoryPool();
 ~MemoryPool() {}
 inline bool allocate(ObjectType **obj);
 inline bool free(ObjectType *obj);
protected:
 Stack<ObjectType, LockDummy, Size> pool;
 ObjectType objects[Size];
};
```

栈保留了空闲（未分配）对象的引用。池的构造函数填充对象栈：

```cpp
template<typename Lock, typename ObjectType, size_t Size>
MemoryPool<Lock, ObjectType, Size>::MemoryPool() {
 for (int i = 0;i < Size;i++) {
 pool.push(&objects[i]);
    }
}
```

分配和释放方法调用栈的 `pop` 和 `push` API：



```cpp
template<typename Lock, typename ObjectType, size_t Size>
bool MemoryPool<Lock, ObjectType, Size>::allocate(ObjectType **obj) {
 bool res;
 Lock lock;
res = pool.pop(obj);
 return res;
}

template<typename Lock, typename ObjectType, size_t Size>
bool MemoryPool<Lock, ObjectType, Size>::free(ObjectType *obj) {
 bool res;
 Lock lock;
res = pool.push(obj);
 return res;
}
```

`JobThread` 实现了一个“开始”API 和一个无限循环的静态方法。更现实的实现会添加“等待完成”、某些用于异步调用上下文作业已完成的机制，以及对作业函数参数的支持。

```cpp
template <typename JobType> class JobThread {
public:
 JobThread();
 void start(JobType *job);
protected:
 JobType *job;
 xTaskHandle pxCreatedTask;
 xQueueHandle signal;
 static void mainLoop(JobThread *jobThread);
};
```

`JobThread` 构造函数创建一个二值信号量并产生（spawn）一个新的线程（这个特定动词的选择基于`taskSpawn`，它是 vxWorks 中的一个创建任务 API）。我在示例中假设使用 FreeRTOS API，但任何其他 API 在这里有效：

```cpp
template<typename JobType>
JobThread<JobType>::JobThread() : job(nullptr) {
 static const char *name = "a job";
    vSemaphoreCreateBinary(this->signal);
    portBASE_TYPE res = xTaskCreate((pdTASK_CODE)mainLoop, (const signed char *)name, 300, this, 1, &this->pxCreatedTask);
 if (res != pdPASS) {
cout << "Failed to create a task" << endl;
    }
}
```

线程入口点 `mainLoop` 方法进入 while 循环并等待二值信号量。在实际代码中，我可能会测试一个对象变量 `bool exitFlag` 而不是始终为真的条件：

```cpp
template<typename JobType>
void JobThread<JobType>::mainLoop(JobThread *jobThread) {
 while (true) {
        xSemaphoreTake(jobThread->signal, portMAX_DELAY);
 if (jobThread->job != nullptr) {
            jobThread->job->run();
        }
        jobThread->job = nullptr;
    }
}
```

`start` 方法设置作业指针并唤醒 `mainLoop`：

```cpp
template<typename JobType>
void JobThread<JobType>::start(JobType *job) {
 this->job = job;
xSemaphoreGive(this->signal);
}
```

在下面的示例中，代码打印“Print is running”：

```cpp
struct PrintJob {
 void run(void) {
cout << "Print is running" << endl;
    }
};

MemoryPool<LockDummy, JobThread<PrintJob>, 3> jobThreads;

PrintJob printJob;

int main( void )
{
 JobThread<PrintJob> *jobThread;
 jobThreads.allocate(&jobThread);
 jobThread->start(&printJob);
 vTaskStartScheduler();
 return 1;
}
```

## 非静态成员

“C 让你很容易射中自己的脚；C++ 让它变得更难，但当你这样做时，它会炸掉你的整个腿。”

我只修改了上面代码中的两行。对 `xTaskCreate` 的调用获取了一个成员函数的指针。C++ 编译器对将方法地址转换为通用指针发出警告：

```cpp
void *pMainLoop = (void*)&JobThread<JobType>::mainLoop;
portBASE_TYPE res = xTaskCreate((pdTASK_CODE)pMainLoop, (const signed char *)name, 300, this, 1, &this->pxCreatedTask);
```

主循环方法不再是静态方法，且不需要任何参数：

```cpp
template<typename JobType>
void JobThread<JobType>::mainLoop() {
 while (true) {
        xSemaphoreTake(signal, portMAX_DELAY);
 if (job != nullptr) {
 job->run();
        }
 job = nullptr;
    }
}
```

这个技巧之所以有效，是因为大多数（或所有？）C++ 编译器会将`this`（一个指向对象的指针）首先推入参数栈。如果 C 和 C++ 代码使用栈帧的方式不同，该技巧可能会失效。虚方法指针也可能失效。这总是可以通过暴力破解来解决——反汇编，并弄清楚如何正确调用成员函数。虚函数调用的实现不同编译器之间差异巨大。

本文的读者可能会问，这个成员指针（pointer-to-member）练习的意义何在。我在调试器下运行应用程序时，有时我想使用绝对地址设置断点。我可以打印成员的绝对地址，并查看我的泛型类创建了多少个相同方法的实例。获取函数指针可以确保该函数不是“内联”函数。

## 进程间通信

无论如何，我讨厌多线程。多进程才是正道，应该是消息传递，而不是共享内存。那样无法扩展。我使用多线程是为了利用我所有的 16 个核心，或者说现在机器的平均核心数。大不了什么。我在数据中心有几千台服务器在等我，我该如何用线程来使用它们呢？– Alex Martelli。

经典的进程间通信（IPC）设计模式是邮箱（mailbox）或消息队列。邮箱设计模式在 Windows 3.11 以及第一批真正的实时操作系统（如`RT Kernel`和`vxWorks`）处于技术前沿时变得流行。某些操作系统支持消息队列 API。我将演示一个基于两个原语构建的消息队列：`semaphore`（信号量）和`FIFO`（先进先出队列）。`Mailbox`类是“对象组合”（[4],[5]）的一个示例。我使用了“邮箱拥有一个 FIFO”的关系。或者，我可以使用“邮箱是一个 FIFO”的公式，并从`FIFO`类派生——继承邮箱。不过度使用继承被认为是一种做法。

邮箱 API 有两个方法：发送消息和等待消息 ([6])：

```cpp
template<typename  ObjectType, typename  Lock>

class  Mailbox {

public:

 Mailbox(const  char *name, size_t size);

 const  char *getName() {return  name;}

 inline  bool  send(ObjectType msg);

 enum TIMEOUT {NORMAL, NONE, FOREVER};

 bool  wait(ObjectType *msg,

TIMEOUT waitType, size_t timeout);

protected:

 const  char *name;

 xQueueHandle  semaphore;

 CyclicBufferDynamic<ObjectType, Lock> fifo;

};
```

邮箱构造函数使用了 FreeRTOS 计数信号量：

```cpp
template<typename  ObjectType, typename  Lock>

Mailbox<ObjectType, Lock>::Mailbox(const  char *name, size_t size) :

 fifo(size),

 name(name) {

 semaphore = xSemaphoreCreateCounting(size+1, 0);

}
```

`send`方法向 FIFO 添加消息并递增信号量值：

```cpp
template<typename  ObjectType, typename  Lock>

bool  Mailbox<ObjectType, Lock>::send(ObjectType msg) {

 bool res;

res = fifo.add(msg);

     xSemaphoreGive(semaphore);

 return res;

}
```

接收消息处理不同类型的超时：

```cpp
template<typename  ObjectType, typename  Lock>

bool  Mailbox<ObjectType, Lock>::wait(ObjectType *msg,

TIMEOUT waitType, size_t timeout) {

 bool res = false;

     portBASE_TYPE semaphoreRes = pdFALSE;

 while (semaphoreRes == pdFALSE) {

 if (waitType == TIMEOUT::FOREVER) {

              semaphoreRes = xSemaphoreTake(semaphore, portMAX_DELAY);

          }
 else  if (waitType == TIMEOUT::NORMAL) {

              semaphoreRes = xSemaphoreTake(semaphore, timeout);

 break;

          }
 else {

              semaphoreRes = xSemaphoreTake(semaphore, 0);

 break;

          }

    }

 if ((semaphoreRes == pdTRUE) && !fifo.isEmpty()) {

res = fifo.remove(msg);

     }

 return res;

}
```

在示例应用程序中，中断（生产者）从`UART`设备读取数据，并将收集的数据发送到处理任务（消费者）。我的消息对象包含两个内容：一个消息事件和一些数据。消费者任务预计根据消息事件进行切换：

```cpp
enum EVENT {UART0, UART1};

typedef  struct {

 enum EVENT event;

 size_t  data[32];

 int  dataSize;

} Message;
```

在下面的示例中，我重用了上一个章节中的内存池：

```cpp
MemoryPool<LockDummy, Message, 3> pool;

Mailbox<Message*, LockDummy> myMailbox("mbx", 3);

void  rxTask( void ) {

     myMailbox.wait(&message,

      myMailbox.TIMEOUT::FOREVER, 0);

cout << "data=" <<

         message->data << ", event=" <<

         message->event << endl;

    pool.free(message);

}

int  main( void ) {

     Message *message;

     pool.allocate(&message);

     message->data[0] = 0x30;

     message->dataSize = 1;

     message->event = EVENT::UART0;

     myMailbox.send(message);

}
```

在许多情况下，现代固件开发人员会使用“流水线”（pipeline）。“流水线是一系列串联连接的数据处理元素，其中一个元素的输出是下一个元素的输入”（Wikipedia）。一个处理元素（例如线程）唤醒并检查邮箱——任务队列。如果队列不为空，该线程执行一个阶段的处理，并将处理后的数据转发给流水线中的下一个线程。

流水线任务有两个方法：添加新任务和处理数据。流水线任务——一个阶段——有一个名称并保留对下一个阶段的引用：

```cpp
template<typename  ObjectType, typename  Lock, std::size_t  Size>

class  PipelineTask {

public:

 PipelineTask(const  char *name,

 PipelineTask *nextStage = nullptr) :

 name(name),

 nextStage(nextStage){}

 void  doJob();

 void  addJob(ObjectType &data);

protected:

 const  char *name;

 PipelineTask *nextStage;

 CyclicBuffer<ObjectType, Lock, Size> fifo;

};
```

`addJob` API 向 FIFO 添加数据：

```cpp
template<typename  ObjectType, typename  Lock, std::size_t  Size>

void  PipelineTask<ObjectType, Lock, Size>::addJob(ObjectType &data) {

 fifo.add(data);

}
```

`doJob()` 方法从 FIFO 获取数据，对其进行递增——我假设数据类型支持`operator++()`，并将数据推送到下一个阶段：

```cpp
template<typename  ObjectType, typename  Lock, std::size_t  Size>

void  PipelineTask<ObjectType, Lock, Size>::doJob() {

 while (!fifo.isEmpty()) {

 ObjectType data;

 fifo.remove(data);

         data++;

cout << "Stage:" << name << ", data=" << data << endl;

 nextStage->addJob(data);

    }

}
```

新类型`MyPipelineTask`：

```cpp
typedef PipelineTask<int, LockDummy, 3> MyPipelineTask;
```

流水线的三个阶段——倒数第三个阶段没有“后续”：

```cpp
MyPipelineTask pipelineTask3("3");

MyPipelineTask pipelineTask2("2", &pipelineTask3);

MyPipelineTask pipelineTask1("1", &pipelineTask2);
```

我可以从中断或主循环调用流水线的阶段，例如如下所示：

```cpp
void  testPipeline() {

 int data = 0;

     pipelineTask1.addJob(data);

     pipelineTask1.doJob();

     pipelineTask2.doJob();

     pipelineTask3.doJob();

}
```

上面的代码生成输出：

```
Stage:1, data=1
Stage:2, data=2
Stage:3, data=3
```

流水线范式可以提高 CPU 的利用率，流水线使得更容易利用多核系统。

## 日志（Log）

完美不是已经没有什么可增加的，而是已经没有什么可减少的——安托万·圣埃克佩里

在一个 C 项目中，我看到过以下生成日志条目的代码：



## 日志系统优化

以下是一个基于 C 语言的日志系统实现，以及针对其性能优化的 C++ 方案。

### 原始 C 语言实现

```cpp
enum {
    LOG_LEVEL_INFO,
    LOG_LEVEL_ERROR,
    LOG_LEVEL_LAST,
};

static const char *LOG_LEVEL_NAME[] = {"INFO", "ERROR", "UKNOWN"};

#define LOG_INFO(fmt, ...) log_print(__LINE__, LOG_LEVEL_INFO, fmt, ##__VA_ARGS__)
#define LOG_ERROR(fmt, ...) log_print(__LINE__, LOG_LEVEL_ERROR, fmt, ##__VA_ARGS__)

static void log_print(int line, int level, const char *fmt, ...)
{
    va_list ap;
    printf("%s: line=%d, msg=", LOG_LEVEL_NAME[level], line);
    va_start(ap, fmt);
    vprintf(fmt, ap);
    va_end(ap);
}

void testLog(void) {
    LOG_INFO("This is info %d", 1);
    LOG_ERROR("This is error %d", 2);
}
```

在我的机器上，上面的代码生成输出：

```
INFO: line=402, msg=This is info 1
ERROR: line=403, msg=This is error 2
```

对 `log` API 的调用非常频繁，图像的大小非常重要。调用 `log_print()` 会向栈中推入至少三个参数。我认为我可以节省一次推入操作——日志级别。在 C 语言实现中，我会添加 `log_print_info(...)` 和 `log_print_error(...)` 函数，它们反过来调用 `log_print()`，并相应地修复宏。在 C++ 中，我使用了一个模板。构造函数是原始 `log_print` 函数的精确拷贝，去掉了日志级别：

```cpp
template <int Level> class Log {
public:
    Log(int line, const char *fmt, ...) {
        va_list ap;
        printf("%s: line=%d, msg=", LOG_LEVEL_NAME[Level], line);
        va_start(ap, fmt);
        vprintf(fmt, ap);
        va_end(ap);
    }
};
```

日志宏调用构造函数：

```cpp
#define LOG_INFO(fmt, ...) Log<LOG_LEVEL_INFO>(__LINE__, fmt, ##__VA_ARGS__)
#define LOG_ERROR(fmt, ...) Log<LOG_LEVEL_ERROR>(__LINE__, fmt, ##__VA_ARGS__)
```

C++ 编译器为我生成了两个打印日志函数，并为每次调用 `log` API 节省了一次栈推入操作。`Log` 类是一个“仿函数（functoid）”——它是一个增强版的函数。我可以使用基于普通类的仿函数，而不是像这样的模板：

```cpp
class Log {
public:
    Log(const char *level) : level(level) {}
    void print(int line, const char *fmt, ...) const {
        va_list ap;
        printf("%s: line=%d, msg=", level, line);
        va_start(ap, fmt);
        vprintf(fmt, ap);
        va_end(ap);
    }
protected:
    const char *level;
};

const Log LogInfo("INFO");
const Log LogError("ERROR");

#define LOG_INFO(fmt, ...) LogInfo.print(__LINE__, fmt, ##__VA_ARGS__)
#define LOG_ERROR(fmt, ...) LogError.print(__LINE__, fmt, ##__VA_ARGS__)
```

我舍弃了数组 `LOG_LEVEL_NAME`，现在扩展日志级别枚举变得更简单了。在目标代码中只有一个打印函数实例。代价是数据 RAM 中的几个字，或者两个 `Log` 类型的对象。代码和数据可以放在 ROM 中。

### 二进制日志优化

调用 `vprintf()` 不是固件开发人员经常的操作。事实上，代码会针对同一组格式化字符串反复调用 `vprintf()`。我只需要向控制台发送 `vprintf()` 的参数，以及源代码中的确切位置或目标文件中的偏移。

下方的 `BinaryLog` 类仅处理“int”类型的参数。源代码中的位置由“唯一”的文件标识符和源行号定义：

```cpp
class BinaryLog {
public:
    BinaryLog(int fileId, int line, int count, ...);
};
```

我假设有一个 `sendData` API 可以向控制台发送任意数量的整数：

```cpp
BinaryLog::BinaryLog(int fileId, int line, int count, ...) {
    const int HEADER_SIZE = 3;
    int header[HEADER_SIZE];
    header[0] = fileId;
    header[1] = line;
    header[2] = count;
    sendDataStart();
    sendData(header, HEADER_SIZE);
    va_list ap;
    va_start(ap, count);
    for (int j=0; j < count; j++) {
        int arg = va_arg(ap, int);
        sendData(arg);
    }
    va_end(ap);
    sendDataEnd();
}
```

我仿真中的 `sendData` API 看起来如下：

```cpp
inline void sendData(const int data) {
    cout << dec << data << " ";
}

inline void sendDataStart() {
    cout << endl;
}

inline void sendDataEnd() {
    cout << endl;
}

void sendData(const int *data, int count) {
    for (int i = 0; i < count; i++) {
        cout << hex << data[i] << " ";
    }
}
```

两个宏定义调用构造函数 `BinaryLog`。宏 `ARGUMENTS_COUNT` 具有良好的可移植性，应返回可变宏中的参数数量：

```cpp
#define ARGUMENTS_COUNT(...) (sizeof((int[]){__VA_ARGS__})/sizeof(int))
#define LOG_INFO(fmt, ...) BinaryLog(FILE_ID, __LINE__, ARGUMENTS_COUNT(__VA_ARGS__), __VA_ARGS__)
#define LOG_ERROR(fmt, ...) BinaryLog(FILE_ID, __LINE__, ARGUMENTS_COUNT(__VA_ARGS__), __VA_ARGS__)
```

文件标识符由编译器在构建期间根据文件名生成。我使用了一个简单的哈希函数。真实的、如 MD5 哈希可以在 [7] 中找到。

```cpp
constexpr int hashData(const char* s, int accumulator) {
    return *s ? hashData(s + 1, (accumulator << 1) : accumulator;
}

constexpr int hashMetafunction(const char* s) {
    return hashData(s, 0);
}

constexpr int FILE_ID = hashMetafunction(__FILE__);
```

用法示例：

```cpp
void testBinaryLog(void) {
    LOG_INFO("This is info %d %d", 1, 2);
    LOG_ERROR("This is error %d %d %d", 0, 1, 2);
}
```

在我的系统中，`test` 函数产生输出：

```
26140 511 1 2
26140 512 0 1
```

我现在只需要一个短脚本 ([8]) 来为所有源文件计算文件标识符，根据文件标识符 `26140` 找到正确的文件，解析 c++ 文件中的 `511` 和 `512` 行，并生成两行可读的内容：

```
info 1 2
error 0 1
```

另一个构建脚本可以确保格式字符串正确表示对宏的调用。通过移除昂贵的 `vprintf()` 调用，我节省了大量的 CPU 周期和带宽。二进制日志不使用任何静态数据，且 API 是线程安全的。我的系统生成的日志在处理之前需要额外的处理。

当我在中断中调用系统日志时，我需要禁用中断。对于任务级的系统日志，一个互斥锁（mutex）可能足够了。具有相似性能的 C 语言方案需要一个宏。

## 软件定时器

C++：难以学习，且注生如此。

到目前为止，我演示了一些相当简单的软件组件，例如 `mutex` 或 `cyclic buffer`（环形缓冲区）。在本章中，我将实现一个软件定时器。

现代操作系统提供了定时器 API。通常，应用程序可以启动一个任意过期时间的定时器。当定时器过期时，操作系统会从专用定时器线程或系统中断调用应用程序钩子。如果应用程序启动了许多不同的定时器，此类 API 的性能可能会下降。通常无法控制处理定时器的进程优先级。这里介绍的 API 允许应用程序在单个上下文或具有不同优先级的多个上下文中处理所有与定时器相关的代码。

软件定时器 API 将具有 `O(1)` 复杂度。该 API 将是线程安全的。软件定时器的源代码可以在 `[9]` 中找到。

你已经熟悉面向对象的设计流程了。让我们先声明一个定时器对象。定时器对象保留一个唯一的定时器标识。

唯一的定时器标识可以用于解决 `stopTimer` 和 `timerExpired` 之间可能的竞态条件。考虑以下场景：定时器“a”由上下文 A 启动。定时器“a”被上下文 A 停止，但太晚了——定时器“a”刚刚过期，处理过期的应用程序代码正在运行。根据应用程序回调的实现，事件处理可以异步进行。与此同时，同一个定时器对象被另一个线程 B 分配并修改。如果上下文 A 保留了所有启动定时器的标识，应用程序回调可以检查定时器标识是否在运行中的定时器列表中。如果定时器已停止，回调可以忽略定时器过期。使用定时器对象本身的引用进行此类账目记录不是好的，因为定时器对象池可能是一个共享资源。

在启动定时器时，用户可以提供一个可选的应用程序数据指针，即 cookie。定时器类可以像所示的模板：

```cpp
template<typename CookieType> class Timer {
protected:
    CookieType cookie;
};
```

我想简化接口并避免在定时器对象中使用虚方法——稍后会详细讨论虚方法。定时器对象将保留一个指向应用程序数据的指针，而不是任意类型的对象。

用户只能通过公共方法（getters 和 setters）访问定时器数据。这种方法有助于未来的代码维护。

`Timer` 类实现了一个不带参数的构造函数。我希望能够在不引入太多麻烦的情况下创建定时器的静态数组。`TimerList` 类（尚未声明）是 `Timer` 类的友元类，可以调用 `Timer` 的受保护方法。`start()` 方法是受保护的，因为应用程序应该使用 `TimerList` 方法启动定时器。

```cpp
class Timer {
public:
    Timer();
    inline void stop();
    bool isRunning() const;
    TimerID getId() const;
    inline uintptr_t getApplicationData() const;
    SystemTime getStartTime() const;
protected:
    friend class TimerList;
    TimerID id;
    uintptr_t applicationData;
    bool running;
    SystemTime startTime;
    inline void start();
    inline void setApplicationData(uintptr_t applicationData);
    inline void setId(TimerID id);
    inline void setStartTime(SystemTime systemTime);
};
```

方法的实现非常直观：

```cpp
Timer::Timer() {
    stop();
}

TimerID Timer::getId() const {
    return id;
}

SystemTime Timer::getStartTime() const {
    return startTime;
}

bool Timer::isRunning() const {
    return running;
}

void Timer::stop() {
    running = false;
}

void Timer::start() {
    running = true;
}

void Timer::setApplicationData(uintptr_t applicationData) {
    this->applicationData = applicationData;
}

uintptr_t Timer::getApplicationData() const {
    return applicationData;
}

void Timer::setId(TimerID id) {
    this->id = id;
}

void Timer::setStartTime(SystemTime systemTime) {
    this->startTime = systemTime;
}
```

系统时间通常是由中断增加的 tick 或从硬件读取的。在这个示例中，我使用了 `size_t` 类型。在更高级的设计中，`SystemTime` 类型和 `Timeout` 类型可以是两个类。定时器 API 只需要一个签名为 `bool isTimerExpired(SystemTime, Timeout, SystemTime)` 的函数。在下面的实现中，我处理了 `SystemTime` 溢出，假设定时器的超时时间相对于 `SystemTime` 的最大值是非常小的。

```cpp
typedef size_t SystemTime;
typedef size_t Timeout;

static inline bool isTimerExpired(SystemTime startTime, Timeout timeout,
    SystemTime currentTime) {
    bool timerExpired = false;
    SystemTime timerExpirationTime = startTime + timeout;

    timerExpired = timerExpired
                || ((timerExpirationTime >= currentTime)
                    && (startTime < currentTime));

    timerExpired = timerExpired
                || ((timerExpirationTime >= currentTime)
                    && (startTime > currentTime));

    timerExpired = timerExpired
                || ((timerExpirationTime <= currentTime)
                    && (startTime > currentTime)
                    && (timerExpirationTime < startTime));
    return timerExpired;
}
```

我的 API 拥有一个 C++11 类型的可能返回码枚举。C++11 `enum class` 不是整数，不能转换为整数。一个枚举的成员不能赋值给另一个枚举的成员。

```cpp
enum class TimerError {
    Ok, Stopped, Illegal, FreeTimer, NoRunningTimers
};
```

我需要一个处理定时器过期的应用程序回调。在更高级的设计中，回调可以是模板函数：

```cpp
typedef void (*ExpirationHandler)(const Timer& timer);
```



## 同步 API 与定时器锁

我将通过构造函数的参数提供一个同步 API。在基类 `TimerLock` 中，我将 `get`/`release` 接口设置为零。锁 API 将由派生类实现。虚函数的典型性能开销是 1 或 2 个操作码。

```cpp
class  TimerLock {
public:
    virtual  void  get() = 0;
    virtual  void  release() = 0;
protected:
    virtual  ~TimerLock() {}
};

class  TimerLockDummy : public  TimerLock {
public:
    virtual  void  get() {}
    virtual  void  release() {}
protected:
};
```

## 动态环形缓冲区

我需要一个通过 `operator[]` 使用堆动态分配的环形缓冲区。在之前的章节中，我讨论了 `operator[]` 以及无法从内存堆进行分配的情况。

```cpp
template<typename  ObjectType, typename  Lock>
class  CyclicBufferDynamic {
public:
    inline  CyclicBufferDynamic(size_t size);
    ~CyclicBufferDynamic() {
    }
    inline  bool  isEmpty();
    inline  bool  isFull();
    inline  bool  add(ObjectType object);
    inline  bool  remove(ObjectType *object);
    inline  bool  getHead(ObjectType *object);
private:
    void  errorOverflow() {
    }
    void  errorUnderflow() {
    }
    size_t  increment(size_t index);
    ObjectType *data;
    size_t  head;
    size_t  tail;
    size_t  size;
};
```

构造函数调用 `operator[]` 来配配指针数组。有一个 `static_assert` 确保模板类仅用于指针：

```cpp
template<typename  ObjectType, typename  Lock>
inline  CyclicBufferDynamic<ObjectType, Lock>::
CyclicBufferDynamic(size_t size) {
    this->head = 0;
    this->tail = 0;
    this->size = size;
    this->data = new  ObjectType[size];
    static_assert(sizeof(ObjectType) <= sizeof(uintptr_t), "CyclicBuffer is intended to work only with integer types or pointers");
}
```

其余代码与之前的实现相似：

```cpp
template<typename ObjectType, typename Lock>
inline bool CyclicBufferDynamic<ObjectType, Lock>::isEmpty() {
  bool res = (this->head == this->tail);
  return res;
}

template<typename ObjectType, typename Lock>
inline bool CyclicBufferDynamic<ObjectType, Lock>::isFull() {
  size_t tail = increment(this->tail);
  bool res = (this->head == tail);
  return res;
}

template<typename ObjectType, typename Lock>
inline bool CyclicBufferDynamic<ObjectType, Lock>::add(ObjectType object) {
  Lock lock;
  if (!isFull()) {
    data[this->tail] = object;
    this->tail = increment(this->tail);
    return true;
  } else {
    errorOverflow();
    return false;
  }
}

template<typename ObjectType, typename Lock>
inline bool CyclicBufferDynamic<ObjectType, Lock>::remove(ObjectType *object) {
  Lock lock;
  if (!isEmpty()) {
    *object = data[this->head];
    this->head = this->increment(this->head);
    return true;
  } else {
    errorUnderflow();
    return false;
  }
}

template<typename ObjectType, typename Lock>
inline bool CyclicBufferDynamic<ObjectType, Lock>::getHead(ObjectType *object) {
  Lock lock;
  if (!isEmpty()) {
    *object = data[this->head];
    return true;
  } else {
    errorUnderflow();
    return false;
  }
}

template<typename ObjectType, typename Lock>
size_t CyclicBufferDynamic<ObjectType, Lock>::increment(size_t index) {
  if (index < this->size) {
    return (index + 1);
  } else {
    return 0;
  }
}
```

在这里使用 `LockDummy` 是刻意之为。我不需要环形缓冲区存储指向 `Timer` 类对象的指针是重入的：

`typedef CyclicBufferDynamic<Timer*, LockDummy> TimerCyclicBuffer;`

## 定时器列表

定时器列表保留了具有相同超时时间的定时器。定时器的过期时间取决于开始时间。定时器 API 假设系统中存在有限且数量较少的不同定时器（具有不同超时时间的定时器）。通常在开始编写代码之前，我已经知道系统中需要哪些定时器。`TimerList` 是“对象组合”的一个示例——我将简单对象（如 `FIFOs`）组合成更复杂的对象。与其使用环形缓冲区，可以使用内存池来实现空闲定时器列表 `freeTimers`。

```cpp
class TimerList {
public:
  TimerList(size_t size, Timeout timeout,
    TimerExpirationHandler expirationHandler,
    TimerLock &timerLock,
    bool callExpiredForStoppedTimers=false) :
    timeout(timeout),
    expirationHandler(expirationHandler),
    callExpiredForStoppedTimers(callExpiredForStoppedTimers),
    freeTimers(size),
    runningTimers(size),
    timerLock(timerLock) {
    Timer *timers = new Timer[size];
    for (size_t i = 0; i < size; i++) {
      freeTimers.add(&timers[i]);
    }
  }
  TimerError processExpiredTimers(SystemTime currentTime);
  TimerError startTimer(SystemTime currentTime, SystemTime &nearestExpirationTime, uintptr_t applicationData = 0, const Timer **timer = nullptr);
  inline TimerError stopTimer(Timer &timer) {
    timer.stop();
    return TimerError::Ok;
  }
  SystemTime getNearestExpirationTime() {
    return nearestExpirationTime;
  }
protected:
  inline static TimerID getNextId();
  TimerError _startTimer(SystemTime currentTime, SystemTime &nearestExpirationTime, uintptr_t applicationData = 0, const Timer **timer = nullptr);
  TimerError _processExpiredTimers(SystemTime currentTime);
  Timeout timeout;
  TimerExpirationHandler expirationHandler;
  bool callExpiredForStoppedTimers;
  SystemTime nearestExpirationTime;
  CyclicBufferDynamic<Timer*, LockDummy> freeTimers;
  CyclicBufferDynamic<Timer*, LockDummy> runningTimers;
  TimerLock &timerLock;
};
```

`TimerList` 的保护方法不是线程安全的。例如 `getNextId()` 不是线程安全的。只有子类或公共方法可以访问保护成员并应负责同步：

```cpp
TimerID TimerList::getNextId() {
  static TimerID id = 0;
  id++;
  return id;
}

TimerError TimerList::startTimer(SystemTime currentTime, SystemTime &nearestExpirationTime, uintptr_t applicationData, const Timer **timer) {
  timerLock.get();
  TimerError res = TimerList::_startTimer(currentTime, nearestExpirationTime, applicationData, timer);
  timerLock.release();
  return res;
}
```

保护方法 `_startTimer()` 将定时器从空闲定时器列表移动到运行定时器列表：

```cpp
TimerError TimerList::_startTimer(SystemTime currentTime, SystemTime &nearestExpirationTime, uintptr_t applicationData, const Timer **timer) {
  Timer* newTimer;
  if (freeTimers.isEmpty())
    return TimerError::NoFreeTimer;
  freeTimers.remove(&newTimer);
  newTimer->setStartTime(currentTime);
  newTimer->setApplicationData(applicationData);
  newTimer->setId(getNextId());
  newTimer->start();
  runningTimers.add(newTimer);
  Timer* headTimer;
  runningTimers.getHead(&headTimer);
  nearestExpirationTime = headTimer->getStartTime() + timeout;
  this->nearestExpirationTime = nearestExpirationTime;
  if (timer != nullptr)
    *timer = newTimer;
  return TimerError::Ok;
}
```

方法 `_processExpiredTimers()` 将停止和过期的定时器从运行定时器列表头部移动到空闲定时器列表。定时器列表的用户应调用 `processExpiredTimers()`，这将为过期的定时器调用应用程序回调。用户应调用 `getNearestExpirationTime()` 来获取下一个定时器的过期时间，即再次调用 `processExpiredTimers()` 的时间。`nearestExpirationTime` 和 `currentTime` 之间的差异可以用于例如系统调用 `sleep()`。`runningTimers` 列表上的定时器按过期时间排序。我总是将定时器添加到末尾，且列表上所有定时器的超时时间是相同的。该保护方法是非重入的：

```cpp
TimerError TimerList::_processExpiredTimers(SystemTime currentTime) {
  Timer* timer;
  while (!runningTimers.isEmpty()) {
    if (!runningTimers.getHead(&timer))
      break;
    bool timerExpired = timer->getStartTime() + timeout <= currentTime;
    bool timerRunning = timer->isRunning();
    bool callHandler = timerExpired || (!timerRunning && callExpiredForStoppedTimers);
    if (callHandler) {
      (expirationHandler)(*timer);
    }
    if (timerExpired || !timerRunning) {
      runningTimers.remove(&timer);
      freeTimers.add(timer);
    }
    if (!timerExpired && timerRunning) {
      nearestExpirationTime = timer->getStartTime() + timeout;
      break;
    }
  }
  if (runningTimers.isEmpty())
    return TimerError::Ok;
  else
    return TimerError::NoRunningTimers;
}
```

公共方法是重入的：

```cpp
TimerError TimerList::processExpiredTimers(SystemTime currentTime) {
  timerLock.get();
  TimerError res = TimerList::_processExpiredTimers(currentTime);
  timerLock.release();
  return res;
}
```

## 定时器集合

我将定时器列表分组为“集合”。例如，一组超时时间为 5 秒、20 秒、60 秒的低优先级定时器，以及一组高优先级定时器。不同的集合可以由运行在不同优先级的线程处理。我在编译时知道哪些定时器属于集合。

`TimerSet` 类是“对象熟悉”([4]、[5]) 的示例。`TimerSet` 类与 `TimerList` 类之间存在“感知”关系。可以通过其他对象访问组件对象（定时器列表），而不通过聚合对象 `TimerSet`。组件对象可以比聚合对象生存。

```cpp
class TimerSet {
public:
  TimerSet(const char* name, int size) :
    name(name), listCount(size) {
    this->size = size;
    timerLists = new TimerList*[size];
  }
  const char *getName() {
    return name;
  }
  TimerError processExpiredTimers(SystemTime currentTime, SystemTime& expirationTime);
  bool addList(TimerList* list);
protected:
  const char *name;
  TimerList **timerLists;
  size_t listCount;
  size_t size;
};
```

`addList` API 填充了数组 `timerLists`：



```cpp
bool TimerSet::addList(TimerList* list) {
  if (listCount < size) {
    timerLists[listCount] = list;
    listCount++;
    return true;
  } else {
    return false;
  }
}
```

`processExpiredTimers()` 方法调用所有定时器列表中对应的 API，并方便地返回下次调用该方法的时间。该方法的复杂度为 `O(number of timer lists)`：

```cpp
TimerError TimerSet::processExpiredTimers(
SystemTime currentTime, SystemTime &expirationTime) {
  TimerList* timerList;
  size_t i;
  SystemTime nearestExpirationTime;
  bool res = false;
  for (i = 0; i < listCount; i++) {
    timerList = timerLists[i];
    TimerError timerRes = timerList->processExpiredTimers(currentTime);
    if (timerRes == TimerError::Ok) {
      SystemTime listExpirationTime = timerList->getNearestExpirationTime();
      if (res) {
        if (nearestExpirationTime > listExpirationTime) {
          nearestExpirationTime = listExpirationTime;
        }
      } else {
        nearestExpirationTime = listExpirationTime;
      }
      res = true;
    }
  }
  if (res)
    return TimerError::Ok;
  else
    return TimerError::NoRunningTimers;
}
```

最后是一个用法示例：

```cpp
static void mainExpirationHandler(const Timer& timer) {
  TimerID timerId = timer.getId();
  uintptr_t data = timer.getApplicationData();
  cout << "Expired id=" << timerId << ",appdata=" << data << endl;
}

TimerLockDummy timerLock;
static TimerList timerList(3, 3, mainExpirationHandler, timerLock);

int main() {
  SystemTime currentTime = 0;
  for (int i = 0; i < 3; i++) {
    SystemTime nearestExpirationTime;
    TimerError err = timerList.startTimer(currentTime, nearestExpirationTime, i);
    if (err == TimerError::Ok) {
      cout << "nearestExpirationTime=" << nearestExpirationTime << endl;
    } else {
      cout << "timer start failed for timer " << i << endl;
    }
  }
  timerList.processExpiredTimers(3);
  return 0;
}
```

假设我需要两种不同的 `Timer` 类型——一种带有定时器标识符，另一种没有。我从一个新基类派生出一个更大的定时器类，其中定时器标识符的设置器是一个空方法。转换将不涉及对 `TimerList` 类的任何更改。`TimerList` 类可以与任何实现了 `Timer` 类 API（即 `Timer` 类“契约”）的“接口”（[10]）工作。

在另一个系统中，系统时间是一个包含以下字段的结构：`hours`、`minutes`、`seconds` 和 `milliseconds`。如果定义了两个运算符：`compare` 和 `add`，`TimerList` 类就可以处理这种系统时间。

在另一个系统中，我无法与动态分配的循环缓冲区工作。我将 `TimerList` 类转换为一个模板类，其大小由列表参数决定。`TimerSet` 类可以与任何实现了 `processExpiredTimers()` API 的定时器列表工作。我从一个具有纯虚方法 `processExpiredTimers()` 的抽象基类派生出 `TimerList` 类——现在它是一个模板类。代码的修改将不会影响 `TimerList` 或 `TimerSet` 方法中的逻辑。

在某些应用中，我在同一个线程中启动定时器、停止定时器并处理过期。我不需要重入 API。我可以通过对定时器列表使用虚拟锁（dummy lock）来节省 CPU 周期。

一旦编写并调试完成，`TimerList` 和 `TimerSet` 类可以在许多不同情况下为我提供帮助。我可以在 C 语言中到处使用 `void*` 和一些类型转换来实现同样的事情。C++ 粉丝们会认为，C++ 的替代方案更加优雅且类型安全。

## Lambda

模数转换器（ADC）是一种将连续物理量（例如电压）转换为表示该量幅度的数字的设备（[11]）。在我的应用程序中，我想读取 ADC 设备，在环形缓冲区中收集样本，运行一个简单的环形缓冲区（[12]）。ADC 看起来如下：

```cpp
template<typename ObjectType, size_t Size>
class ADC {
public:
  ADC(ObjectType);
  typedef ObjectType (*Filter)(ObjectType);
  void add(ObjectType, Filter);
  double get();
protected:
  CyclicBuffer<Size> data;
  ObjectType value;
};
```

ADC 构造函数设置了初始值：

```cpp
template<typename ObjectType, size_t Size>
ADC(ObjectType initialValue) {
  value = initialValue;
}
```

`get()` 方法返回计算值：

```cpp
template<typename ObjectType, size_t Size>
double get() {
  return value;
}
```

`add` 方法更新循环缓冲区并调用过滤器：

```cpp
template<typename ObjectType, size_t Size>
void add(ObjectType, Filter) {
  data.add(filter);
}
```

`Filter` 是一个函数指针。大多数人会使用以下示例，我使用了一个 Lambda 函数：

```cpp
static void test() {
  ADC<double, 4> myc(3.0);
  cout << "ADC=" << myc.get() << endl;
  for (int i = 0; i < 10; i++) {
    myc.add([](double current) {
      return current + 0.5;
    });
  }
}
```

在桌面上这产生了：

```text
ADC=3.999
```

`ADC` 类被替换为：

```cpp
class HardwareModule {
public:
  double read();
protected:
};

class ReadADC {
public:
  ReadADC() : myc(3.0) {}
  void run(void) {
    double sample = hardwareModule.read();
    myc.add(sample);
  }
protected:
  ADC<double, 4> myc;
  HardwareModule hardwareModule;
};
```

```cpp
JobThread<ReadADC> jobThread;
```

## 定点算术

很多人对分数有困扰。在需要模数转换器的应用中，我需要定点算术（[13]）。定点算术比标量浮点代码快得多（二三倍）。不幸的是，定点算术不是 C++ 标准的一部分。GCC 编译器提供了支持（[14]）。定点算术的极佳示例请参考 Kurt Gunoth 的实现（[15]）。

以下示例是四种算术操作的简单实现。在代码段中，`lhs` 和 `rhs` 代表算术运算符两侧的参数。带有单个成员 `scale` 的匿名枚举是一种有助于创建模板常量成员的技巧。

```cpp
template<typename IntType, const int FRACTION_BITS>
class FixedPoint {
public:
  typedef FixedPoint<IntType, FRACTION_BITS> T;

  FixedPoint() {}
  FixedPoint(double d) { v = (IntType)(d * scale); }
  FixedPoint(const T &rhs) : v(rhs.v) {}

  T& operator=(const T &rhs) {
    v = rhs.v;
    return *this;
  }

  double toDouble() const {
    return double(v) / scale;
  }

  friend T operator+(T lhs, const T &rhs) {
    T r;
    r.v = lhs.v + rhs.v;
    return r;
  }

  friend T operator-(T lhs, const T &rhs) {
    T r;
    r.v = lhs.v - rhs.v;
    return r;
  }

  friend T operator*(T lhs, const T &rhs) {
    T r;
    r.v = (lhs.v * rhs.v) / scale;
    return r;
  }

private:
  IntType v;
  enum { scale = 1 << FRACTION_BITS };
};
```

```cpp
friend T operator/(T lhs, const T &rhs) {
  T r;
  r.v = (lhs.v * scale) / rhs.v;
  return r;
}

friend bool operator==(const T &lhs, const T &rhs) {
  return lhs.v == rhs.v;
}

protected:
  int v;
  enum { scale = 1 << FRACTION_BITS };
};
```

一个用法示例：

```cpp
static void FixedPointTest() {
  typedef FixedPoint<int_fast16_t, 3> FixedPoint_3;

  FixedPoint_3 value(3.43188);
  value = (2 * (value + FixedPoint_3(1.4) - FixedPoint_3(1.4))) / 2;
  cout << value.toDouble() << endl;
}
```

用法示例的输出：

```text
3.375
```

我可以通过定点算术模板的实例来扩展上一章中的组合 `ReadADC`。Lambda 函数看起来像这样：

```cpp
class ReadADC {
public:
  ReadADC : myAdc(3.0) {}

  typedef FixedPoint<int_fast16_t, 3> FPADC;

  void run(void) {
    FPADC sample = FPADC(hardwareModuleADC.read());

    myAdc.add(
      sample,
      [](FPADC current, FPADC sample) {
        return current + (sample - current) / 2;
      }
    );
  }

protected:
  ADC<FPADC, 4> myAdc;
  HardwareModuleADC hardwareModuleADC;
};
```

# 面试题

智者将继承地球。——《经济学人》，2011 年 1 月 20 日

我知道对于你和我来说，编程并不是为了钱。但尽管如此，我的一些亲爱的读者还是必须考虑家庭。程序员是世界上薪水最高的职业之一。

“随着技术的进步，对聪明人的报酬在增加。计算机极大地增加了信息的可用性，提高了对那些足够敏锐并能理解这些信息的人的需求。1991 年，拥有学士学位的美国男工人平均薪水是中学毕业者的 2.5 倍；而现在这个比例是 3 倍。”（[16]）

一个熟练的软件开发者可以在美国、英国、加拿大、澳大利亚和其他国家获得六位数的薪水或等值报酬。在你和梦想工作之间，只隔着一次职业面试。

如果你经常无法回答脑筋急转弯，也不要担心。在很多公司中，这类面试题是被禁止的。只有极少数人能够实时为一个难题找到解决方案。请相信，这些人已经被各地的 Google 和 Apple 公司聘用了，他们并不会与你竞争这份工作。你的面试官可能并不期望得到正确答案，而是主要想看你是如何处理困难问题的。

在本章中，我尝试收集了一小部分问题，你在申请实时、嵌入式、固件开发人员职位时可能会遇到。我跳过了图表、二叉树、水桶，因为这类问题很少出现在嵌入式系统开发者的技术面试中。

## 通用编程

### 宏和日志函数

Q. 下面代码的局限性是什么？是否存在潜在的问题？

```cpp
#define LOG_CAT(fmt, ...) \
  print_log("%s %d" fmt, __FUNCTION__, __LINE__, ##__VA_ARGS__)

static inline void print_log(const char *fmt, ...) {
  va_list ap;

  va_start(ap, fmt);
  vprintf(fmt, ap);
  va_end(ap);
}
```

A. 宏 `LOG_CAT` 假设 `fmt` 是一个常量字符串。例如，以下代码将无法编译：

```cpp
void testLogCat() {
  char *f = "Test %d";
  LOG_CAT(f, 1);
}
```

对函数 `vprintf()` 的调用在某些平台上不是重入的。在其他平台上，`vprintf()` 使用栈上的一个大缓冲区，如果从中断中调用，可能会产生问题。

### 中断处理程序

Q. 以下中断处理程序有什么问题？尝试尽可能指出所有的潜在问题：

```cpp
uint32_t Tick = 0;

int MyTickIsr() {
  Tick++;
  printf("%s", __FUNCTION__);
  return 0;
}
```

A.

1. 通常情况下中断处理程序不应该返回返回值。返回的结果取决于操作系统。
2. 全局变量的增加是一个“读取-修改-写入”操作。当中断处理程序被调用时，另一个线程可能正处于修改 `tick` 值的过程中。
3. 在许多系统中，`printf()` 不是可重入 API。如果 `printf()` 使用栈分配字符串，调用 `printf()` 可能会导致栈溢出。取决于实现，调用 `printf()` 可能需要大量时间。

### FIFO 实现

Q. 列出在“生产者”和“消费者”之间实现 FIFO（先进先出）的最常用方法。假设生产者产生 1 到 256 字节不同大小的数据块。

A.

1. 指针环形缓冲区，其中每个指针指向一个例如 16 字节数据块的链表。生产者从空闲块链表中分配数据块。
2. 指针环形缓冲区，引用每个 256 字节的数据块。生产者从空闲块链表中分配数据块。
3. 数据环形缓冲区，每个数据块的前面都加上数据块的大小。

请准备好从内存和性能角度讨论每种方法的优缺点，以及 Linux 内核中的 `skb` 缓冲区、DMA 描述符、零拷贝数据处理。

### 判断字节序

Q. 写一个程序来判断机器是大端序还是小端序。

A. 在运行时可以使用此函数：

```cpp
int isLittleEndian() {
  short int data = 0x0001;
  char *byte = (char *)&data;

  return (byte[0] ? 1 : 0);
}
```

在编译时使用此宏：

```cpp
#define IS_LITTLE_ENDIAN (*(uint16_t *)"\0\xff" >= 0x100)
```

在 Linux 中，我们有一个宏 `BYTE_ORDER`。在 GCC 中，我们有宏 `__LITTLE_ENDIAN__`、`__BIG_ENDIAN__`、`__BYTE_ORDER__`。

### 禁止类被继承

Q. 写一个类，使得其他类无法继承它。

A. 解决方案基于单例设计模式——一个具有私有构造函数的类：

```cpp
class YouCanNotInheritMe {
private:



在本章中，我尝试收集了一小部分问题，你在申请实时、嵌入式、固件开发人员职位时可能会遇到。我跳过了图表、二叉树、装水的桶，因为这类问题很少出现在嵌入式系统开发者的技术面试中。

## 通用编程

### 宏和日志函数

**Q.** 下面代码的局限性是什么？是否存在潜在的问题？

```cpp
#define LOG_CAT(fmt, ...) print_log("%s %d" fmt, __FUNCTION__, __LINE__, ##__VA_ARGS__ )

static inline void print_log(const char *fmt, ...)
{
    va_list ap;
    va_start(ap, fmt);
    vprintf(fmt, ap);
    va_end(ap);
}
```

**A.** 宏 `LOG_CAT` 假设 `fmt` 是一个常量字符串。例如，以下代码将无法编译：

```cpp
void testLogCat()
{
    char *f = "Test %d";
    LOG_CAT(f, 1);
}
```

对函数 `vprintf()` 的调用在某些平台上不是可重入的。在其他平台上，`vprintf()` 使用栈上的一个大缓冲区，如果从中断中调用，可能会产生问题。

### 中断处理程序

**Q.** 以下中断处理程序有什么问题？尝试尽可能指出所有的潜在问题：

```cpp
uint32_t Tick = 0;

int MyTickIsr()
{
    Tick++;
    printf("%s", __FUNCTION__);
    return 0;
}
```

**A.**

1. 通常情况下，中断处理程序不应该返回返回值。返回的结果取决于操作系统。
2. 全局变量的增加是一个“读取-修改-写入”操作。当中断处理程序被调用时，另一个线程可能正处于修改 `tick` 值的过程中。
3. 在许多系统中，`printf()` 不是可重入 API。如果 `printf()` 使用栈分配字符串，调用 `printf()` 可能会导致栈溢出。取决于实现，调用 `printf()` 可能需要大量时间。

### 生产者和消费者之间的 FIFO

**Q.** 列出在“生产者”和“消费者”之间实现 FIFO 的最常用方法。假设生产者产生 1 到 256 字节的不同大小的数据块。

**A.**

1. 指针环形缓冲区，其中每个指针指向一个例如 16 字节数据块的链表。生产者从空闲块链表中分配数据块。
2. 指针环形缓冲区，引用每个 256 字节的数据块。生产者从空闲块链表中分配数据块。
3. 数据环形缓冲区，每个数据块的前面都加上数据块的大小。

请准备好从内存和性能角度讨论每种方法的优缺点，以及 Linux 内核中的 `skb` 缓冲区、DMA 描述符、零拷贝数据处理。

### 判断机器的字节序

**Q.** 写一个程序来判断机器是大端序还是小端序。

**A.** 在运行时可以使用此函数：

```cpp
int isLittleEndian()
{
    short int data = 0x0001;
    char *byte = (char *) &data;
    return (byte[0] ? 1 : 0);
}
```

在编译时使用此宏：

```cpp
#define IS_LITTLE_ENDIAN (*(uint16_t *)"\0\xff" >= 0x100)
```

在 Linux 中，我们有一个宏 `BYTE_ORDER`。在 GCC 中，我们有宏 `__LITTLE_ENDIAN__`、`__BIG_ENDIAN__`、`__BYTE_ORDER__`。

### 禁止类被继承

**Q.** 写一个类，使得其他类无法继承该类。

**A.** 解决方案基于单例设计模式——一个具有私有构造函数的类：

```cpp
class YouCanNotInheritMe {
private:
    YouCanNotInheritMe() {}
};
```

### 内存缓存和结构体初始化

在调用第二个 `memset` 时，数据缓存可能已经包含了字段 `a` 以及字段 `b` 的全部或部分。CPU 可能预测到了顺序写入，并提前加载数据缓存行。通常，缓存内存中的单行为 64 或 128 字节。

函数 `initDataArrayC` 写入了字段 `c`，这会导致数据缓存行冲刷，并减慢第二个 `memset()` 的执行速度。

```cpp
memset(dataArray.c, 0, sizeof(dataArray.c));
```

### 优化 `testFastSum`

**Q.** 对下列代码进行何种**单项修改**，可以提高 `testFastSum` 函数的性能？

```cpp
class FastSum {
public:
    FastSum(int delta) : delta(delta) {}
    virtual int sum(int a) { return delta + a; }
    virtual ~FastSum() {}

protected:
    int delta;
};

void testFastSum(int delta, int *result, int count)
{
    FastSum fastSum(delta);

    for (int i = 0; i < count; i++) {
        result[i] = fastSum.sum(i);
    }
}
```

**A.** **去虚化（Devirtualization）**——将虚方法 `sum()` 替换为非虚方法——可以提高性能。将虚函数调用替换为非虚调用，每次迭代可以节省 2～3 条指令。

如果 C++ 编译器的去虚化做得很好（GCC 4.8 则不能），那么下一个选项是确保编译器内联构造函数 `FastSum` 和方法 `sum`。

### 懒加载初始化中的竞态条件

**Q.** 下述代码存在一个竞态条件。它是什么？

```cpp
class LazyInitialization {
    static LazyInitialization *getInstance()
    {
        if (instance == nullptr) {
            MutexAB m;

            if (instance == nullptr) {
                instance = new LazyInitialization();
            }
        }

        return instance;
    }

private:
    LazyInitialization();

    static LazyInitialization *instance;
};

LazyInitialization *LazyInitialization::instance = nullptr;
```

**A.** 线程 A 进入同步区域并初始化静态变量 `instance`。类 `LazyInitialization` 的构造函数可能还没有被调用，但变量 `instance` 可能已经被设置。操作的确切顺序取决于编译器。

此时线程 B 进入 `getInstance()` 方法并返回一个无效指针——指向一个未完全初始化对象的指针。

另一个问题是，地址的赋值（一个 32 位、64 位或其他变量）并不一定是原子操作，并且可能涉及两次内存写入事务。可以通过将变量 `instance` 声明为原子变量来修复代码：

```cpp
atomic<LazyInitialization*> LazyInitialization::instance(nullptr);
```

### 右值和左值

**Q.** 解释右值（rvalue）和左值（lvalue）。`++x` 和 `x++` 有什么区别？

**A.** 右值是临时值，在它们所生存的完整表达式结束时就会消失（“在分号处”）。例如，`1729`、`x + y`、`std::string("meow")` 和 `x++` 都是右值。

左值是命名且持久到单个表达式之外的对象。例如，`obj`、`*ptr`、`ptr[index]` 和 `++x` 都是左值。

表达式 `x++` 是右值。它拷贝持久对象的原始值，修改持久对象，然后返回该拷贝。这个拷贝是临时的。`++x` 和 `x++` 都会增加 `x` 的值，但 `++x` 返回持久对象本身，而 `x++` 返回一个临时拷贝。

### 函数中的局部变量和字符串

**Q.** 解释以下函数中每一行发生了什么：

```cpp
const char *dataTest()
{
    // 1.
    char *a = "123";

    // 2.
    char b[] = "123";

    // 3.
    const char *c = "123";

    // 4.
    static char d[] = "123";

    // 5.
    a[0] = '0';

    // .................
    // 6.
    return a;

    // .................
    // 7.
    return c;

    // ................
    // 8.
    return b;
}
```

**A.**

1. 为局部变量 `a` 分配常量数据 `['1', '2', '3', 0]` 的地址。某些编译器会生成警告：将 `const` 指针赋值给非 `const` 指针。
2. 将数据 `['1', '2', '3', 0]` 在运行时拷贝到局部（栈上）数组。数组 `b` 的初始化在每次调用函数时都会完成。
3. 与第 1 项相同，但修复了编译警告。
4. 将数组 `['1', '2', '3', 0]` 在运行时拷贝到静态变量 `d`。拷贝仅由代码加载器执行一次。
5. 尝试修改常量数据。在某些架构上，常量数据是只读的，此行可能会导致异常。
6. 返回常量数据的指针。该指针是全局的，存在于程序地址空间中。
7. 与第 6 项相同。
8. 返回局部（栈）变量的地址。地址 `b` 处的数据取决于架构。

### 获取当前程序计数器

**Q.** 下面的 x86 汇编代码做什么？

```assembly
call next

next:
pop eax
```

**A.** `call` 操作符将当前程序计数器（PC）推入栈中。随后的 `pop` 将 PC 值设置到寄存器 `eax`。这段代码是获取当前 PC 值的一种方法。

### 高效内存池

**Q.** 实现一个用于分配 4 字节块的高效内存池。

**A.** 使用块本身的数据组织一个空块链表。初始时在第一个块（偏移量 0）中写入 `1`，表示下一个空块的偏移量；在第二个块（偏移量 1）中写入 `2`，以此类推。代码示例如下：

```cpp
static const int POOL_SIZE = 7;
static uint32_t fastPoolData[POOL_SIZE];
static uint32_t fastPoolHead;
static const int ALLOCATED_ENTRY = (POOL_SIZE + 1);

static inline uint32_t fastPoolGetNext(uint32_t node)
{
    return fastPoolData[node];
}

static inline void fastPoolSetNext(uint32_t node, uint32_t next)
{
    fastPoolData[node] = next;
}

void fastPoolInitialize()
{
    fastPoolHead = 0;

    for (int i = 0; i < POOL_SIZE - 1; i++) {
        fastPoolSetNext(i, i + 1);
    }

    fastPoolSetNext(POOL_SIZE - 1, ALLOCATED_ENTRY);
}

uint32_t *fastPoolAllocate()
{
    uint32_t blockOffset = fastPoolHead;

    if (blockOffset != ALLOCATED_ENTRY) {
        fastPoolHead = fastPoolGetNext(blockOffset);
    }

    return &fastPoolData[blockOffset];
}

void fastPoolFree(uint32_t *block)
{
    // 根据上下文简化了逻辑
}
```



```cpp
static const int POOL_SIZE = 7;
static uint32_t fastPoolData[POOL_SIZE];
static uint32_t fastPoolHead;
static const int ALLOCATED_ENTRY = (POOL_SIZE+1);
static inline uint32_t fastPoolGetNext(uint32_t node)
{
    return fastPoolData[node];
}
static inline void fastPoolSetNext(uint32_t node, uint32_t next)
{
    fastPoolData[node] = next;
}
void fastPoolInitialize()
{
    fastPoolHead = 0;
    for (int i = 0; i < POOL_SIZE-1; i++)
    {
        fastPoolSetNext(i, i+1);
    }
    fastPoolSetNext(POOL_SIZE-1, ALLOCATED_ENTRY);
}
uint32_t *fastPoolAllocate()
{
    uint32_t blockOffset = fastPoolHead;
    if (blockOffset != ALLOCATED_ENTRY)
    {
        fastPoolHead = fastPoolGetNext(blockOffset);
    }
    return &fastPoolData[blockOffset];
}
void fastPoolFree(uint32_t *block)
{
    // 源文本中逻辑不完整
}
```

### Q. 实现 `itoa()` —— 将整数转换为字符串

A.

```cpp
int itoa(int value, char *s, int size)
{
    int i = 0;
    int chars = size - 1;
    int digits = 0;
    int v = value;
    while (v)
    {
        if (i >= chars) break;
        s[digits-1] = '0' + value%10;
        i++;
        v = v / 10;
    }
    if (digits-i < 0)
    {
        s[digits-1] = 0;
        return size;
    }
    else
    {
        s[chars] = 0;
        return 0;
    }
}
```

## 位运算技巧

### Q. 你有两个数字 M 和 N，以及两个位置 i 和 j。写一个方法将 M 中 i 到 j 之间的位设置为 N。假设 i < j。

例如，如果输入 M=0x00, N=0x10, i=0, j=5，则输出为 0x10。

A. 你需要清除 N 中从 i 到 j 的位，并对 M 和 N 进行位或操作。使用 `uint32_t` 或类似类型可能是好主意 —— 与面试官讨论。

```cpp
int mask = ((i<< 1)-1) | ((1 << j)-1);
M = M & mask;
M = M | (N << i);
```

### Q. 代码 `((n & (n-1)) == 0)` 表示什么？

如果 `n` 为零或为 2 的幂，该条件为真。

### Q. 如何找到最高置位？

A. GCC 有一个内置函数 `__builtin_clz()`，它返回参数中导零的数量。另一种解决方案：

```cpp
unsigned int v;
unsigned r = 0;
while (v >>= 1) {
    r++;
}
```

### Q. 如何无分支地设置或清除位？为什么需要它？

A. 你可以使用如下代码：

```cpp
bool f;
unsigned int mask;
unsigned int w;
w ^= (-f ^ w) & mask;
```

取决于上下文和 CPU，无分支可以提高 5%-10% 的性能。另见 [17]。

### Q. 查找整数中的第一个置位

#### 位运算

A. 在 GCC 中，我们有一个内置函数 `__builtin_ffs()`。或者，你也可以使用类似下面的软件实现。请讨论涵盖 `x` 等于零情况的可能返回代码。

```cpp
int  findFirst(int x)
{
  if (x == 0)
    return 0;
  int t = 1;
  int r = 1;
  while ((x & t) == 0) {
    t = t << 1;
    r = r + 1;
  }
  return r;
}
```

### Q. 如何清除整数中最低有效位以外的所有位？

例如对于 `0x60`（2 位被设置），结果是 `0x20`（1 位被设置）。

A. 用单行 C 代码即可实现（参见 [18]）：

```c
x &= -x;
```

或者，效果相同：

```c
x &= (~x+1)
```

### Q. 如何检查整数是否为偶数？

A. 偶数的最低有效位为零：

```c
((x & 1) == 0)
```

### Q. 如何清除最右侧设置位？

A. 将整数减 1 并与自身进行按位与运算：

```c
x & (x-1)
```

### Q. 如何设置最右边的零位？

A. 将整数加 1 并与自身进行按位或运算：

```c
x | (x+1)
```

### Q. 统计整数中的非零位。是否存在无分支解决方案？

A. 清除右位并检查结果是否为零（参见 [19]）：

```c
int  countBits(int n)
{
  int count=0;
  while(n) {
    count++;
    n = n&(n-1);
  }
  return count;
}
```

# 热门在线测试

在以下测试中，每个问题后面跟着五个答案。最多三个答案可以是正确的。我不提供正确答案。

### 下列哪些语句描述了用于 C 条件编译的条件？

- 条件必须求值为 0 或 1
- 条件可以取决于任何“const”变量的值
- 条件可以使用 `sizeof` 根据标准数据类型的大小对依赖于编译的操作做出决定
- 条件可以取决于环境变量的值

### 如果将 ANSI C 运算符用于不同类型的操作数，以下哪项正确描述了操作数或结果的类型转换？

- 操作数完全没有发生任何自动转换
- 此操作将由编译器标记为错误
- “窄”操作数被转换为“宽”操作数的类型以避免信息丢失
- 操作数的值被改变以防止“窄”类型中可能的溢出
- 将结果赋值给“窄”类型可能会丢失信息，但不非法

### 下列外围设备允许嵌入式系统使用双线或三线串行接口与其他设备通信？

- 双向三态缓冲器
- 地址译码器
- 通用同步收发器
- 数字模模拟转换器
- 非易失性存储器

### 下列哪些语句正确描述了 ANSI C 语言中的函数在嵌入式系统中的？

- 链接的两个不同文件的全局函数名必须是唯一的
- 函数可以通过值或指针调用
- 函数不能返回多个值
- 函数可以接受的最多参数数量为 12
- 每个函数都必须返回一个值

### 下列哪些语句正确描述了下面的 ANSI C 代码？

```c
typedef  char *pchar;
pchar  funcpchar();
typedef  pchar (*pfuncpchar)();
pfuncpchar  fpfuncpchar();
```

- `pfuncpchar` 是一个返回 char 指针的函数指针
- `fpfuncpchar` 是一个返回函数指针的 char 指针
- `fpfuncpchar` 是一个返回返回 char 指针的函数指针
- `fpfuncpchar` 是一个返回返回 char 指针的函数指针的函数
- `funcpchar` 是一个返回 char 指针的函数

### 下列哪些语句正确描述了 ANSI C 中的按位右移运算符 `>>`？

- 右侧运算符必须大于等于 1
- 它将其左侧操作数的每个位向右移动，移动数为右侧运算符指定的位数
- 它可以用于反转数字的符号
- 对于无符号整数，它会在左侧空出的位填充零
- 它可以用于将整数除以 2 的幂

### 假设 ANSI C 采用补码表示法，以下哪些语句是正确的？

- 表示为带符号整数的负值，如果表示为相同尺寸无符号整数，将表示为大于符号整数最大值的正值
- 同一整数类型的带符号和无符号变范围在大小和数值最大最小值上是等价的
- 整数类型的无符号版本范围是带符号版本的两倍
- 带符号整数的表示多出一个符号位

### 在以下代码中，调用 `print` 函数可能看起来如下所示：

```c
void process (int (*p)(int, int, char*)) {
  int a = 5, b = 4;
  char *c = "aggregate";
  /* 为 b,a,c 调用 print */
  return;
}
int main(void) {
  process(report);
}
```

- `p->report(b,a)`
- `(*p)(b,a)`
- `p(b,a)`
- `(*p)(report, b, a)`
- `report(b,a)`

### 下面代码编译失败的正确修复是：

```c
/* File A */
struct pair a[10];
void initialize(int x, int m, int b) {
  int i;
  a[0].y = (a[0].x = x) * m + b;
  for (i = 1;i < 10;++i)
    a[i].y = (a[i-1].x + 1)*m + b;
}
/*File B*/
struct pair {int x, y;};
struct pair *op(int x) {
  int i;
  for (i = 10; i > 0;--i)
    if (a[i].x == x)
      break;
  return a+1;
}
```

- `extern struct pair a[];`
- 数组 `a` 的声明必须在 `op()` 的定义之前
- 除非数组 `a` 在所有调用 `op()` 的文件中声明为 `extern`，否则返回的指针是的
- 文件 A 中数组 `a` 的定义缺少 `extern` 关键字
- 必须在文件 b 中指定数组的大小
- 两个文件中 `struct pair` 的定义都缺少 `extern` 关键字

### 下列哪些是 ANSI C 中格式正确的 `#define` 指令？

- `#define DIF(X,Y) (X-Y)`
- `#define sqr(x) ((x)*(x))`
- `#define mm_per_meter 1000;`
- `#define SUM(X,Y) ((X)+(Y))`
- `#define INCHES_FEET 12`

### 执行下面的 ANSI 代码的输出是什么？

```c
void f(void **p);
int k =2;
int *pk=&k;
int main() {
  int *p;
  f(&p);
  printf("%d\n", *p);
  return 0;
}
void f(void **pp) {
  (*pk)++;
  *pp = pk;
}
```

- 语法错误
- `pk` 的地址
- 垃圾值
- 3
- 2

### `for` 循环完成后，输出数组的内容是什么？

```c
int encode (char, char);
int main(void) {
  char input [7] = {'M', 'E',':','G',':'}, output [7];
  int i;
  for (i = 0;i < 7;++i) {
    output[i] = encode(input[i], ':');
  }
  return 0;
}
int encode(char c , char t) {
  switch(c) {
    case 'E': c = 'A';break;
    case 'O': c = 'X'; break;
    case 'A': c = 'T'; break;
    case 'U': c = 'M'; break;
  }
  if (c >= 'A' && c <= 'Z' || c >= 'a' && c <= 'z' && (c=t))
    c = '\0';
  return c;
}
```

- `\0`,`0`,`0`,`0`,`0`,`\0`
- `M`,`A`,`\0`,`G`,`O`,`\0`,`\0`
- `M`,`A`,`\0`,`G`,`X`,`\0`,`\0`
- `\0`,`0`,:`,`\0`,`\0`,:`,`\0`
- `:`,`:`,`:`,:::`\0`

### `dump_port()` 函数应该输出

```c
/* I/O 寄存器数量 */
#define PORT_SIZE 7
typedef unsigned int word;
union IO_port {
  word reglist[PORT_SIZE];
  struct {
    word ENABLE ;
    word DIRECTION;
    word OPEN_COLLECTOR;
    word DATA;
  } reg;
};
static union IO_port *GPIO = 0xE0004000; /*端口地址 */
#include <stdio.h>
void dump_port(union IO_port *p) {
  int i;
  for (i = 0;i < PORT_SIZE;++i) {
    printf("%X ", p->reglist[i]);
  }
}
int main(void) {
  GPIO->reg.DATA = 0x000000D0;
  GPIO->reg.OPEN_COLLECTOR = 0x000000F0;
  GPIO->reg.DIRECTION = 0xFFFFFF0F;
  GPIO->reg.ENABLE = 0x000030F0;
  dump_port(GPIO);
 return 0;
}
```

- D0 F0 FFFFFF0F 30F0
- `D000000` `F000000` `FFFFF0F` `F0300000`
- `FFFFFFF` `F0300000` `20000000` `D0000000`
- `FFFFFF0F` `30F0` `2` `D0`

### 以下函数返回什么？

```cpp
unsigned int process(unsigned int x, int p, int n)
{
 return x ^ (~(~0 << n) << p + 1 -n);
}
```

- `x` 从位置 `n` 开始的 `p` 位
- `x` 乘以 `2^(p-n)`
- `x` 的从位置 `p` 开始的 `n` 位置为 1
- `x` 在位置 `p` 的第 `n` 位
- `x` 的从位置 `p` 开始的 `n` 位被取反

### 程序必须在数字输出上产生脉冲宽度调制信号。值 0 由数字输出高电平（HIGH）表示，值 0xFFFF 由数字输出低电平（LOW）表示。哪种脉冲信号代表值 `0x7000`？

- 30ms 周期，13.3ms 脉冲宽度
- 2000Hz，563us 脉冲宽度
- 100KHz，5.63us 脉冲宽度
- 100KHz，4.38us 脉冲宽度
- 20ms，11.25ms 脉冲宽度

### 以下哪个语句正确描述了下方的 C++ 代码段？

```cpp
void foo(long l);
int i =12;
foo(i);
```

- `i` 被提升 `long` 以调用函数 `foo`。
- 函数 `foo` 使用一个值为“12”的 `long` 调用。
- 编译器实例化了一个接受 `int` 而不是 `long` 的新函数。
- 函数 `foo` 使用一个值为“12”的 `int` 调用。
- 函数 `foo` 使用一个未定义值的 `long` 调用。

### 以下代码尝试按组（投诉、表扬、其他）对传入的邮件进行分类。在 `for` 循环中使用什么代码？

```cpp
enum class LetterType {complement, complaint, unknown};
LetterType getMailType(string letter)
{
 pair<string, int> happy = make_pair(happyString, 0);
 pair<string, int> sad = make_pair(sadString, 0);
 string word;
 string fstream ss(letter);
 vector<string> letterWords;
 while (ss >> word) letterWords.push_back(word);
 vector<string>::iterator words;
 for (words=letterWords.begin();words<letterWords.end();words++)
    {
      word = *words;
 //...
    }
 if (happy.second > sad.second) return complement;
 else if (happy.second < sad.second) return complaint;
 else return unknown;
}
```

- `if (happy.find(word)) happy.second++;if (sad.find(word)) sad.second++;`



- `if (happy.find(word) != string::npos) happy.second++;if (sad.find(word) != string::npos) sad.second++;`

- `if (happy.first.find(word)) happy.second++;if (sad.first.find(word)) sad.second++;`

- `if (happy.first.find(word) != string::npos) happy++;if (sad.first::find(word) != string::npos) sad++;`

- `if (happy.first.find(word) != string::npos) happy.second++;if (sad.first.find(word) != string::npos) sad.second++;`

以下哪些是 C++ 声明的不可更改指针，与声明指向某个不可更改内容的指针相区别？

- `extern double *float;`

- `extern const int *const reference_only;`

- `extern const std::vector<int> *global_vector;`

- `extern const void *anything;`

- `extern float *const some_scalar;`

以下哪些操作是由 C++ `catch(...)` 语句执行的？

- 捕获默认异常。

- 忽略异常。

- 捕获异常，将其传递给程序控制的下一层。

- 禁用进一步异常的抛出。

以下哪个语句正确描述了编译器生成的构造函数？

- 编译器生成的构造函数创建一个引用。

- 编译器生成的构造函数调用了赋值操作。

- 编译器生成的构造函数什么都不做。

- 编译器生成的构造函数标记该对象。

- 编译器生成的构造函数是默认的。

- 编译器生成的构造函数执行对象的拷贝。

在重载一元运算符时，以下哪些语句是正确的？

- 当运算符是成员时，没有参数。

- 当运算符不是成员时，有一个参数。

- 当运算符不是成员时，有任意数量的参数。

- 当运算符是成员时，有一个参数。

- 当运算符是成员时，没有参数。

在下方的 C++ 代码段中，以下哪些正确描述了 `assert()` 的行为：

```cpp
int val = 5;
while (true)

{
assert(val);
}
```

- 它将值记录到文件中

- 在调试模式下它确保 `val` 为

- 如果不是，则终止

- 在调试模式下，它记录 `val`

- 如果 `val` 为零，则终止。

## 脑筋急转弯

### 潜艇问题

**Q.** 潜艇位于线上，可以是负数。它每秒以恒速移动。是否有办法确保你击中潜艇？

**A.** 在 `T` 秒后位置为 `v*T` 或 `(-v)`，其中 `v` 是绝对值。如果数字是正数，你可以对数字减 1 并计算你做了多少循环：`v*T` 或 `(-v)`。如果 `v=2`，循环次数为 100。如果数字是负数，循环次数为 100。如果数字为零，循环次数为 100。在位置 `T*(T+1)/2` 和 `(-T/2)` 处命中。

### 鸡蛋掉落问题

**Q.** 有一栋 100 层的楼。如果蛋从第 `N` 层或以上掉落它会破碎。如果从任何以下楼掉落则不会破碎。你有 2 块蛋。找到 `N`，同时最小化掉落次数。

**A.** 无论如何使用第一只蛋，我们对第二只蛋进行线性搜索。一个完美的系统是第一只蛋掉落次数加上第二只蛋掉落次数总是相同的。例如，如果第一只蛋掉落在 20 和 30（破碎），第二只蛋需要 9 步。当我们再次掉落第一只蛋时，我们将第二只蛋的潜在步骤减少到 8。这意味着我们必须在 39 层掉落第一只蛋。因此，第一只蛋从 `X` 开始，然后增加 `X-1`，`X-2`，……`X+(X-1)+(X-2)+1=100`。`X(X+1)/2=100`，`X=14`。[20]。

### 仅使用运算符 `+` 取反数字

**Q.** 如何仅使用运算符 `+` 取反一个数字？

**A.** 如果数字是正数，你可以对数字减 1 并计算你做了多少循环：

```cpp
int negate(int x) {
 int result = 0;
 int sign = x < 0 ? 1 : -1;
 while (x != 0) {
    result += sign;
    x += sign;
    }
 return result;
}
```

### 发现函数中的错误

**Q.** 发现以下函数中的错误（如果有的话）：

```cpp
void mistake()
{
 unsigned int i;
 for (i = 100; i <= 0; --i) {
 printf("%d\n", i);
    }
}
```

**A.** `printf` 永远不会执行。`for` 循环是一个死循环。

### 应用程序随机崩溃

**Q.** 一个应用程序在运行时崩溃。它从不在同一个地方崩溃。应用程序是单线程的，并且只使用标准库。哪些编程错误可能导致这种情况？

**A.** 崩溃由输入引起：用户输入或特定的硬件状态、栈溢出、尝试使用未分配（已释放）的内存。可以记录系统输入。有一些工具（`valgrind`）可以发现内存泄漏和访问未初始化内存。

### 生成随机数 `r7`

**Q.** 给定生成 0 到 4 之间整数的随机数生成器 `r5`，实现一个随机数生成器 `r7`。

两个随机数之和并不是均匀分布的随机数。任何涉及随机生成数字之和的方案都是错误的。在以下代码中，第一次赋值生成了一个五位进制的两位数字——一个在 0 到 24 之间的随机数。下一行从随机数序列中移除了 21、22、23、24。该操作的结果是一系列 0 到 20 之间均匀分布的数字。通过对 7 取模完成了完成任务。

```cpp
int random_7() {
  while (true) {
    int ret = 5 * random_5() + random_5();
    if (ret < 21)
      return (ret % 7);
  }
}
```

# 结论

你已经让我们大开眼足了。让其他的年轻姑娘们也有表现的机会吧——简·奥斯汀，《傲慢与偏见》。

希望你觉得这本书有趣，并且值得投入时间和金钱。这本书经常更新。你可以随时通过 Amazon 网站的“管理您的内容和设备”部分开启“自动更新”来获取更新版本。

请通过在 Amazon 网站上评论或发送电子邮件至 `arkady.miasnikov@gmail.com` 告诉你的想法或提问。

感谢，Arkady。

# 参考文献

[1] RAII [http://en.wikipedia.org/wiki/Resource_Acquisition_Is_Initialization]

[2] 单例模式 [http://en.wikipedia.org/wiki/Singleton_pattern]

[3] 循环缓冲区 [https://github.com/larytet/emcpp/blob/master/src/CyclicBuffer.h]

[4] 对象组合 [http://en.wikipedia.org/wiki/Object_composition]

[5] 《设计模式：可复用面向对象软件元素》，1994, Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides

[6] 邮箱箱 [https://github.com/larytet/emcpp/blob/master/src/Mailbox.h]

[7] Constexpr 哈希值 [https://github.com/mfontanini/Programs-Scripts/tree/master/constexpr_hashes]

[8] Open TI [https://www.assembla.com/code/OpenTI/subversion/nodes/641/scripts]

[9] 定计时 [https://github.com/larytet/emcpp/blob/master/src/Timers.h]

[10] 接口类 [http://en.wikibooks.org/wiki/More_C%2B%2B_Idioms/Interface_Class]

[11] 模模转换器 [http://en.wikipedia.org/wiki/Analog-to-digital_converter]

[12] 低通滤波器 [http://en.wikipedia.org/wiki/Low-pass_filter]

[13] 定点算术 [https://en.wikipedia.org/wiki/Fixed-point_arithmetic]

[14] GCC 中的定点类型 [https://gcc.gnu.org/onlinedocs/gcc-4.9.0/gcc/Fixed-Point.html]

[15] 来自 Kurt Guntheroth 的定点库 [http://www.guntheroth.com/]

[16] 认知精英的兴起 [http://www.economist.com/node/17929013]

[17] 位操作黑客 [http://graphics.stanford.edu/~seander/bithacks.html]

[18] 你必须知道的低级位黑客 [http://www.catonmat.net/blog/low-level-bit-hacks-you-absolutely-must-know/]

[19] 谜题！[http://puddleoriddles.blogspot.co.il/]

[20] Career cup [http://www.careercup.com/]
