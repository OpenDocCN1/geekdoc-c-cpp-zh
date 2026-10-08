
D 为基于锁的同步提供了有限的机制。这些限制非常完善，并且具有强保证的优势。在 `BankAccount` 的特殊情况下，D 版本非常简单：

```d
// 使用 synchronized 类的 D 原子银行账户
synchronized class BankAccount {
    private double balance;
    void deposit(double amount) {
        balance += amount;
    }
    void withdraw(double amount) {
        enforce(balance >= amount);
        _balance -= amount;
    }
    double balance() { }
}
```

---

**注意：**

- 7. 一个潜在的混淆来源是 Windows 使用临界区（critical section）作为保护临界区域的轻量级互斥对象，而使用互斥锁（mutex）作为帮助进程间通信的重量级互斥锁。

```d
return balance;
}
```

`synchronized` 会向上提升一级，应用于整个类。这使得 D 的 `BankAccount` 提供了更强的保证：即使你想想错错，也没有办法为 `balance` 提供后门式的非同步访问。如果允许在同一个类中混合使用 `synchronized` 和非同步方法，那么一切规则都将失效。事实上，对方法级 `synchronized` 的经验表明，最好的做法是将所有方法定义为同步，或者全部不定义；双用途类带来的麻烦远大于其收益。

`synchronized` 类级属性影响共享类型的对象（`BankAccount`），并自动对该类方法的调用进行序列化。此外，对于 `synchronized` 类，保护变得更加严格。回想第 37 页的第 11.1 节，普通的保护检查通常允许模块内的所有代码访问非公共成员。但对于 `synchronized` 类则不然，它们遵循以下规则：

- 完全不允许存在公共数据。
- 对受保护成员的访问仅限于该类及其后类的方法。
- 对私有成员的访问仅限于该类的方法。

## 13.14 同步类中的字段类型

共享对象的传递性规则规定，共享类对象会将 `shared` 修饰符向下传递给它。显然，`synchronized` 引入了一些额外的秩序，这反映在对 `synchronized` 类方法内部字段类型检查的放宽上。为了提供强有力的保证，`synchronized` 以一种略微独特的方式影响字段的语义检查，这种方式契合了 `synchronized` 独特的语义。

`synchronized` 方法对竞态条件的防护是临时的且局部的。“临时性”是因为当方法返回时，字段不再受到对竞态条件的保护。“局部性”涉及 `synchronized` 确保了直接嵌入在对象内部的数据受到保护，但并不保护对象间接引用的数据（例如，通过类引用、指针或数组）。让我们逐一查看。

### 13.14.1 临时保护 == 不可逃逸

这可能并不非常直观，但 `synchronized` 的临时性质意味着一条规则：任何字段的地址都不能逃离 `synchronized` 的地址范围。如果发生这种情况，代码的其他部分就可以访问超出方法级同步所提供的临时保护范围之外的数据。

编译器将拒绝任何试图从方法返回字段的引用（ref）或指针，或者试图通过引用或指针将字段传递给某些函数的尝试。为了说明为什么这条规则是合理的，请考虑以下示例：

```d
double * nyukNyuk; // 注意：非共享
```

```d
void sneaky(ref double r) { nyukNyuk = &r; }
```

```d
synchronized class BankAccount {
    private double _balance;
    void fun() {
        nyukNyuk = // 错误！（如其应当）
        sneaky(_balance); // 错误！（如其应当）
    }
}
```

第一行代码尝试获取 `_balance` 的地址并将其赋值给全局变量。如果该操作成功，系统的保证就会失效——从此以后，程序将通过非共享值获得数据的共享访问。该赋值无法通过类型检查。第二个操作稍微微妙一点，因为它试图通过一个接受 `ref` 参数的函数来实现别名。它也失败了；在实践中，通过引用传递值意味着在调用之前获取地址。由于获取地址是被禁止的，因此调用失败。

### 13.14.2 局部保护 == 尾部共享

`synchronized` 提供的保护也是局部的，这意味着它并不一定保护对象直接字段之外的数据。一旦引入间接层，只有“只有一个线程可以访问数据”的保证就消失了。如果你将数据看作由一个“头部”（位于 `BankAccount` 对象占据的物理内存中的部分）和一个可能的“尾部”（间接访问的内存）组成，那么 `synchronized` 类能够保护数据的“头部”，而“尾部”仍然保持共享。根据实际情况，在方法内部对 `synchronized` 类的字段进行类型划分如下：

- 所有数值类型都不是共享的（没有“尾部”），因此可以很正常地进行操作。
- 声明为类型 `T[]` 的数组字段接收 `shared` 类型（即 `T[]`），也就是说，“头部”（切片限制/长度限制）不是共享的，而“尾部”（数组的内容）保持共享。
- 声明为类型 `T*` 的指针字段接收 `shared` 类型（即 `T *`），也就是说，“头部”（指针本身）不是共享的，而“尾部”（所指向的数据）保持共享。
- 声明为类型 `T` 的类字段接收 `shared (T)`。类自动是按引用传递的，因此它们是“全尾部”。

这些规则适用于上一节描述的“不可逃逸”规则之上。一个直接结果是，如果对对象直接字段的操作被临时挂了共享，那么这些操作在方法内部可以自由地进行重排序和优化——这正是 `synchronized` 的作用。

在某些情况下，一个对象完全拥有另一个对象。例如，`BankAccount` 将所有的交易都存储在一个 `double` 类型的列表中：

```d
// 非同步的且通常与线程无关
class List(T) {
    void append(T value) {
        ...
    }
}

// 保留一个交易列表
synchronized class BankAccount {
    private double balance;
    private List<double> transactions;
    void deposit(double amount) {
        balance += amount;
        transactions.append(amount);
    }
    void withdraw(double amount) {
        enforce(balance >= amount);
        balance -= amount;
        transactions.append(amount);
    }
    double balance() {
        return balance;
    }
}
```

`List` 机制并没有为了跨线程共享而设计，因此它是完全与线程无关的。

## 13.14. 同步类中的字段类型

```
}
}
// 保持一个事务列表
synchronized class BankAccount {
    private double _balance;
    private List<double> _transactions;
```

```cpp
this() {
    // 账户拥有该列表
    setSameMutex(_transactions, this);
}
```

该方案的运行方式要求 `List`（拥有的对象）是同步的。对 `_transactions` 的后续操作将根据普通规则锁定 `_transactions` 字段，但实际上它们会直接进入并获取 `BankAccount` 对象的互斥锁。这样，编译器就满意的，因为每个对象都是独立锁定的。同时，程序也是满意的，因为实际上有一个互斥锁控制了 `BankAccount` 以及 `List` 子对象。获取 `_transactions` 的互斥锁实际上是获取了已经锁定的 `this` 的互斥锁。幸运的是，对已拥有且未竞争的锁进行递归获取是非常廉价的，因此代码是正确的，且不会过于密集锁。

## 13.14.4 不可思议：强制类型转换

接上一个示例，如果你完全确定事务列表对于 `BankAccount` 对象是私有的，你可以像这样强制丢弃 `shared` 并使用它，而不考虑任何线程：

```
// 不是同步的，且通常与线程无关
class List(T) {
```

```
...
void append(T value) {
}
}
```

```
synchronized class BankAccount {
    private double _balance;
    private List<double> _transactions;
```

```cpp
void deposit(double amount) {
    balance += amount;
    (cast(List<double>).transactions).append(amount);
}
void withdraw(double amount) {
    enforce(balance >= amount);
    balance -= amount;
    (cast(List<double>).transactions).append(-amount);
}
double balance() {
    return balance;
}
```

现在代码可以编译并运行了。唯一的需要忌是，现在程序中基于锁的规范的正确性是由你来保证的，而不是语言的类型系统，你并没有比使用默认共享的语言好到哪里。你仍然享有的优势是，类型转换是局部的，可以被搜索并仔细审查。

## 13.15 死锁与 `synchronized` 语句

银行账户示例是线程化程序的“Hello, world!”，而账户转账示例必须是相应的（尽管更阴暗）关于线程死锁的介绍。该示例如下：假设你有两个 `BankAccount` 对象，检查账户和储蓄账户。挑战在于定义一个从一个账户到另一个账户的资金原子转账。

Implementation简单的方法如下：

```
// 转账版本 1：非原子性
void transfer(shared BankAccount source, shared BankAccount target) {
    double amount =
    source.withdraw(amount);
    target.deposit(amount);
}
```

然而，这个版本不是原子的；在两次调用之间，有一段时间资金从两个账户中都消失了。如果就在那个时候一个线程执行了 `inspectForAuditing` 函数，情况可能会变得有点紧张。

为了使转账具有原子性，你需要在转账开始时在方法外部获取两个对象的隐藏互斥锁。你可以通过 `synchronized` 语句来实现：

```
// 转账版本 2：有问题的
void transfer(shared BankAccount source, shared BankAccount target,
    double amount) {
    synchronized (source) {
        synchronized (target) {
            source.withdraw(amount);
            target.deposit(amount);
        }
    }
}
```

`synchronized` 语句通过执行语句体来获取对象的隐藏互斥锁。对该对象的任何方法调用都受益于已获取的锁。

第二个版本转账的问题在于它很容易导致死锁：如果两个线程尝试在相同的账户之间以相反的方向执行转账，线程可能会永久阻塞。一个线程尝试从 A 转到 B，另一个尝试从 B 转到 A。为了解决这个问题，你需要使用多参数 `synchronized`：

```
// 转账版本 3：正确的
void transfer(shared BankAccount source, shared BankAccount target,
    double amount) {
    synchronized (source) {
        synchronized (target) {
            source.withdraw(amount);
            target.deposit(amount);
        }
    }
}
```

同步多个对象与在同一个语句中按顺序同步是不同的。这取决于对象的全局顺序。这样，死锁被避免了。多参数 `synchronized` 是有帮助的，但遗憾的是并不是万灵药。死锁可能非局部发生——在一个函数中同步一个，在另一个函数中同步另一个，直到死锁循环。

## 13.16 使用共享类无锁编程

基于锁的同步理论建立于 20 世纪 60 年。早在 1972 年 [23]，研究人员就开始尝试避免缓慢的互斥锁。用通俗的话说，`cas` 原子地比较内存位置和给定的值，如果该位置等于该值，则存储新值；否则什么都不做。操作的结果告诉我们存储是否发生。整个操作是原子的并且必须作为原语提供。可能的类型集合限于主机的原生字大小（例如 32 或 64 位）。越来越多的机器提供双重比较交换，有时被称为 `cas2`。该操作在 32 位机器上处理 64 位数据，在 64 位机器上处理 128 位数据。鉴于机器对 `cas2` 支持的增加，Dofers 以相同的名称 `cas` 作为重载函数提供双重比较交换。因此你可以对 `int`、`long`、`float`、`double`、数组以及所有指针和类引用进行 `cas`。

### 13.16.1 共享类

遵循 Herlihy 的通用性证明，许多数据结构和算法在早期“基于 cas 的编程”中兴起。现在，虽然理论上基于 cas 的实现可以解决同步问题，但没有人说这很容易。定义基于 cas 的数据结构和算法，特别是证明它们的有效性，是一项巨大的工程。幸运的是，这样的实体被定义并封装，或者它可以被重用于基于 cas 的无锁特性，对类或结构体使用 `shared` 属性 [57]。

为了利用基于 cas 的无锁特性，请对类或结构体使用 `shared` 属性：

```
shared struct LockFreeStruct {
  ...
}

shared class LockFreeClass {
...
}
```

通常的传递规则适用：`shared` 传播到结构体类的字段，且方法不提供特殊保护。如果一切都可以依靠原子赋值 `cas`，保证编译器和机器不会对操作进行任何重排序，或者你那无忌的信心。但请注意——如果编程是走路，而消息传递是慢跑，那么无锁编程将不亚于奥运会。

### 13.16.2 几个无锁结构

作为一个热身练习，让我们实现一个无锁栈类型。基本思想非常简单：栈被维护为一个单链表，插入和删除都在列表前端进行：

```cpp
shared struct Stack(T) {
    private shared struct Node {
        T *payload;
        Node *next;
    }
    private Node *root;
}

void push(T value) {
    auto n = new Node(value);
    shared(Node)* oldRoot = root;
    do {
        oldRoot = root;
        n.next = oldRoot;
    } while (!cas(&root, oldRoot, n));
}

shared(T)* pop() {
    typeof(return) result;
    shared(Node)* oldRoot = root;
    do {
        oldRoot = root;
        if (!oldRoot) return null;
        result = &oldRoot->payload;
    } while (!cas(&root, oldRoot, oldRoot->next));
    return result;
}
```

`Stack` 是一个共享结构体（shared struct），因此其内部几乎所有内容都是共享的。内部类型 `Node` 具有经典的有效负载-指针结构，而 `Stack` 本身存储列表的根节点。

两个原子操作中的 `do/while` 循环看起来可能有点奇怪，但它们非常常见；它们会缓慢而坚定地在每一位未来的 CAS 编程专家的皮层中挖掘出深沟。`push` 的工作原理是创建一个存储新值的新 `Node`。在循环中，`root` 被赋值给新节点，但前提是只有在此期间没有其他线程更改过它！另一个线程可能也执行了栈操作，因此 `push` 需要确保在 `oldRoot` 中假设的 `root` 在新节点被准备就绪期间没有发生变化。

`pop` 方法不是按值返回，而是通过指针返回。这是因为 `pop` 可能会发现队列为空，这并不是一个异常状态（在单线程栈中会是）。对于共享栈，检查元素、移除元素并返回元素是一个有机的整体操作。

## 13.16. 使用 shared 类进行无锁编码

除了返回方面外，`pop` 在实现上与 `push` 相似：小心地替换 `root`，以确保在获取负载时没有其他线程对其进行更改。在循环结束时，提取出的栈值可以安全地返回给其调用者。

如果 `Stack` 看起来并没有那么复杂，让我们来看看如何实际上暴露一个更丰富的单链接口；毕竟，大多数基础设施都是在 `Stack` 内部构建的。
