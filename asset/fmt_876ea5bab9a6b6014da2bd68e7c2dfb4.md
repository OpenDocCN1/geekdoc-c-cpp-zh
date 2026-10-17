
```cpp
1 string L[K];
2 int lines = 0;
3 while (file.good()) {
4 getline(file, L[lines % K]); // 按行读取文件
5 ++lines;
6 }
7 // 如果读取的行少于 K 行，打印所有它们
8 int start, count;
9 if (lines < K) {
10 start = 0;
11 } else {
12 start = lines % K;
13 count = K;
14 }
15 for (int i = 0; i < count; ++i) {
16 cout << L[(start + i) % K] << endl;
17 }
```

# 观察与建议

注意，如果执行 `%s` 发生，会发生坏事。

# 第 13 章题解答 | C++

## 13.2 对比哈希表和 STL 映射。哈希表是如何实现的？如果输入量很小，可以用什么数据结构代替哈希表？

### 答案

#### 对比哈希表与 STL 映射

在哈希表中，值通过对键应用哈希函数来存储，因此值在哈希表中不是按顺序存储的。此外，由于哈希表使用键查找存储值的索引，插入/查询可以在摊均 `O(1)` 时间内完成（假设冲突很少）。必须处理哈希表的潜在冲突。

在 `STL` `map` 中，键值对的插入是按键排序的。它使用树来存储值，这就是为什么需要 `O(log n)` 的插入/查询。也不需要处理冲突。`STL` `map` 适用于此类情况：

- 找到最小元素
- 找到最大元素
- 按顺序打印元素
- 找到精确元素，如果未找到元素，则找到下一个最小元素

#### 哈希表是如何实现的？

1. 需要一个良好的哈希函数（例如：操作 `%` 质数），以哈希值分布均匀。
2. 需要一种冲突解决方法：链法（适用于密集表项）、探测法（适用于稀疏表项）等。
3. 实现根据给定标准动态增加或减少哈希表大小。例如，当 `[元素数量]` 与 `[表大小]` 的比例超过固定阈值时，通过创建新哈希表并使用新哈希函数计算索引，将旧表中的项传输到新表中来增加哈希表的大小。

# 第 13 章解决方案 | C++

## 13.3 C++ 中的虚函数是如何运作的？

### 解决方案

虚函数依赖于一个 `vtable` 或 `虚函数表`。如果类中的任何函数被声明为 `virtual`（虚函数），就会构造一个 `v-table`，用于存储该类虚函数的地址。编译器在所有类中都添加了一个隐藏的 `vptr` 变量，它指向该类的 `vtable`。如果虚函数在派生类中没有被重写，则派生类的 `vtable` 将存储其父类中该函数的地址。在调用虚函数时，通过 `v-table` 解析函数的地址。C++ 中的动态绑定是通过虚函数表机制实现的。

因此，当我们将派生类对象赋值给基类指针时，`vptr` 指向派生类的 `vtable`。这种赋值确保了调用的是最派生类的虚函数。

```cpp
class Shape {
public:
    int edge_length;
    virtual int circumference() {
        cout << "Circumference of Base Class\n";
        return 0;
    }
};
class Triangle: public Shape {
public:
    int circumference() {
        cout << "Circumference of Triangle Class\n";
        return 3 * edge_length;
    }
};
void main() {
    Shape *x = new Shape();
    x->circumference(); // 输出 "Circumference of Base Class"
    Shape *y = new Triangle();
    y->circumference(); // 输出 "Circumference of Triangle Class"
}
```

在上面的示例中，`circumference` 是 `shape` 类中的虚函数，因此它在每个派生类（`triangle`、`rectangle`）中都成为虚函数。C++ 的非虚函数调用在编译时通过静态绑定解析，而虚函数调用则在运行时通过动态绑定解析。

![](img/50974dc108b2978cf2cacf9397df9934_223_0.png)

## 13.4 深拷贝和浅拷贝之间的区别是什么？解释你将如何使用它们。

第 76 页

### 解决方案

```cpp
struct Test {
  char *ptr;
};
void shallow_copy(Test &src, Test &dest) {
  dest.ptr = src.ptr;
}
void deep_copy(Test &src, Test &dest) {
  dest.ptr = malloc(strlen(src.ptr) + 1);
  memcpy(dest.ptr, src.ptr);
}
```

注意，浅拷贝（`shallow_copy`）可能会导致许多运行时错误，特别是在对象的创建和删除时。使用浅拷贝必须非常小心，只有当程序员真正理解自己想要做什么时才使用。在大多数情况下，当需要在不实际复制数据的情况下传递复杂结构的信息时（例如通过引用传递），会使用浅拷贝。处理浅拷贝的析构也必须小心。

在现实生活中，浅拷贝很少使用。有一个重要的编程概念叫做 `智能指针`，它在某种意义上是浅拷贝概念的增强。

在大多数情况下应该使用深拷贝，特别是当复制的结构体较较小时。

## 13.5 C 语言中关键字 "volatile" 的意义是什么？第 76 页

### 解决方案

`volatile` 告诉编译器变量的值可能会从外部发生变化，而无需通过代码进行任何更新。

声明一个简单的 `volatile` 变量：

```cpp
volatile int x;
int volatile x;
```

声明指向 `volatile` 内存的指针变量（仅指针地址是 `volatile`）：

```cpp
volatile int * x;
int volatile * x;
```

指向非 `volatile` 内存的 `volatile` 指针变量（仅包含的内容是 `volatile`）：

```cpp
int * volatile x;
```

指向 `volatile` 内存的 `volatile` 变量指针（指针地址和包含的内容都是 `volatile`）：

```cpp
volatile int * volatile x;
int volatile * volatile x;
```

`volatile` 变量不会被优化，但这实际上是有用的。想象一下这个函数：

```cpp
1 int opt = 1;
2 void Fn(void) {
3 start:
4 if (opt == 1) goto start;
5 else break;
6 }
```

乍看，我们的代码似乎在无限循环。编译器尝试将其优化为：

```cpp
1 void Fn(void) {
2 start:
3 int opt = 1;
4 if (true)
5 goto start;
6 }
```

这变成了一个死循环。然而，外部程序可能会向变量 `opt` 的位置写入 '0'。当多线程程序具有全局变量且任何线程都可以修改这些共享变量时，`volatile` 变量也有用。当然，我们不对它们进行优化。

## 13.6 C++ 中的名称隐藏（name hiding）是什么？第 76 页

### 解决方案

让我们通过一个例子来解释。在 C++ 中，当 `true` 有一个带有重载方法的类时，如果你派生并重写了该方法，你必须重写所有方法。例如：

```cpp
class FirstClass {
public:
    virtual void MethodA(int);
    virtual void MethodA(double);
};

class SecondClass : public FirstClass {
public:
    void MethodA(int);
};
```

在这种情况下，如果你调用 `SecondClass::MethodA(double)`，编译器会报错，因为 `FirstClass` 中的 `MethodA(double)` 被隐藏了。这就是名称隐藏。

```cpp
class Base {
public:
    virtual void MethodA(int);
    virtual void MethodA(double);
};

class Derived : public Base {
public:
    void MethodA(int);
};
```

如果你想让基类的方法也变为可见，可以使用 `using` 关键字：

```cpp
class Derived : public Base {
public:
    using Base::MethodA;
    void MethodA(int);
};
```

## 13.7 为什么基类的析构函数需要声明为虚函数？第 76

### 解决方案

使用指针调用方法总是会调用：

- 派生类的析构函数，如果它是虚的。
- 基类的析构函数，如果它不是虚的。

例如：

```cpp
class Base {
public:
  Base() { cout << "Base Constructor\n"; }
  ~Base() { cout << "Base Destructor\n"; }
};
class Derived: Base {
public:
  Derived() { cout << "Derived Constructor\n"; }
  ~Derived() { cout << "Derived Destructor\n"; }
};
void main() {
  Base *p = new Derived();
  delete p;
}
```

输出：

Base Constructor

Derived Constructor

Base Destructor

我们将基类的析构函数声明为虚的，这使得所有的派生类析构函数都是虚的。

```cpp
class Base {
public:
  Base() { cout << "Base Constructor\n"; }
  virtual ~Base() { cout << "Base Destructor\n"; }
};
```

那么输出变为：

```
Base Constructor
Derived Constructor
Derived Destructor
Base Destructor
```

所以当我们删除指向派生类的基类指针时，应该使用虚析构函数。

## 13.8 编写一个方法，接受 Node 结构的指针作为参数并返回传入结构的完整拷贝。Node 结构包含指向其他 Node 的指针。

### 解决方案

算法将维护从原始节点地址到新结构对应节点的映射。这种映射允许我们在深度优先遍历结构时发现已复制的节点。遍历通常会标记访问过的节点——标记可以有多种形式，而不一定存储在节点中。因此，我们有一个简单的递归算法：

```cpp
typedef map<Node*, Node*> NodeMap;
Node* copy_recursive(Node* cur, NodeMap& nodeMap) {
    if(cur == NULL) {
        return NULL;
    }
    NodeMap::iterator i = nodeMap.find(cur);
    if (i != nodeMap.end()) {
        return i->second;
    }
    // 我们以前来过这里，返回拷贝
    Node* node = new Node;
    nodeMap[cur] = node; // 在遍历链接之前映射当前节点
    node->ptr1 = copy_recursive(cur->ptr1, nodeMap);
    node->ptr2 = copy_recursive(cur->ptr2, nodeMap);
    return node;
}
Node* copy_structure(Node* root) {
    NodeMap nodeMap; // 我们一个空的 map
    return copy_recursive(root, nodeMap);
}
```

# 第 13 章解答 | C++

## 13.9 编写一个智能指针（smart_ptr）类。

### 答案

`Smart_ptr` 与普通指针相同，但它通过自动内存提供安全性。它避免了悬空指针、内存泄漏、分配失败等问题。智能指针必须为所有实例维护单一的引用计数。

```cpp
template <class T> class SmartPointer {
public:
    SmartPointer(T * ptr) {
        ref = ptr;
        ref_count = (unsigned*)malloc(sizeof(unsigned));
        ref_count = 1;
    }
    SmartPointer(SmartPointer<T> sptr) {
        ref = sptr.ref;
        ref_count = sptr.ref_count;
        ++ref_count;
    }
    SmartPointer<T> &operator=(SmartPointer<T> &sptr) {
        if (this != &sptr) {
            ref = sptr.ref;
            ref_count = sptr.ref_count;
            ++ref_count;
        }
        return *this;
    }
    ~SmartPointer() {
        --ref_count;
        if (*ref_count == 0) {
            delete ref;
            free(ref_count);
        }
        ref = NULL;
        ref_count = NULL;
    }
    T getValue() { return *ref; }
protected:
    T * ref;
    unsigned *ref_count;
};
```

![](img/50974dc108b2978cf2cacf9397df9934_230_0.png)

## 14.1 从继承的角度来看，将构造函数私有有什么影响？

### 答案

将构造函数声明为私有将确保类外部的人无法直接实例化类。在这种情况下，创建类实例唯一方法是提供一个静态公共方法，就像在使用工厂方法模式时那样。

此外，由于构造函数是私有的，该类也无法被继承。

# 第 14 章解答 | Java

在 Java 中，如果我们在 `try-catch-finally` 的 `try` 块内部插入 `return` 语句，`finally` 块还会执行吗？

第 78 页

### 答案

是的，它会被执行。

当 `try` 块存在时，`finally` 块会被执行。即使我们尝试在 `try` 块中退出（正常退出、`return`、`continue`、`break` 或任何异常），`finally` 块仍然会被执行。

> 注意：在某些情况下 `finally` 块不会执行：如果虚拟机在 `try-catch` 块执行期间退出，或者执行 `try/catch` 块的线程被杀死。

# 第 14 章解答 | Java

## 14.3 final、finally 和 finalize 之间有什么区别？

### 答案

### Final

- 应用于变量（基本数据类型）时：变量的值不能改变。
- 应用于变量（引用类型）时：引用变量不能指向堆上的任何其他对象。
- 应用于方法时：该方法不能被重写。
- 应用于类时：该类不能被子化。

### Finally

在 `try` 块之后或 `catch` 块之后有一个可选的 `finally` 块。`finally` 块中的语句始终会被执行（JVM 从 `try` 块退出的除外）。`finally` 块用于编写清理代码。

### Finalize

这是 JVM 在运行垃圾回收之前运行的方法。

# 第 14 章解答 | Java

## 14.4 解释 C++ 模板（templates）与 Java 泛型（generics）之间的区别。第 78 页

### 答案

| C++ 模板 | Java 泛型 |
| :--- | :--- |
| 类和函数可以是模板。 | 类和方法可以是泛型的。 |
| 参数可以是任何类型或整数值。 | 参数只能是引用类型（不是基本数据类型）。 |
| 编译时可能会为每个类型参数生成类或函数的独立副本。 | 只编译一个类或函数版本，适用于所有类型参数。 |
| 不同类型参数的类对象在运行时是不同的类型。 | 类型参数在编译时被擦除；具有不同参数的类对象在运行时是相同类型。 |
| 必须包含模板类或函数的实现源码（仅有声明是不够的）。 | 来自编译类文件中的类或方法签名即可使用。 |
| 模板可以特化 - 可以为特定的模板参数提供单独的实现。 | 泛型不能特化。 |
| 不支持通配符。相反，返回类型通常作为嵌套类型定义可用。 | 如果类型参数只使用一次，则支持通配符作为类型参数。 |
| 不直接支持类型参数的边界，但元编程提供了这一点。 | 通过 "extends" 和 "super" 分别支持上界和下界边界；允许强制类型参数之间的关系。 |
| 允许实例化类型参数的类。 | 不允许实例化类型参数的类。 |
| 模板类的类型参数用于静态方法和变量。 | 模板类的类型参数不能用于静态方法和变量。 |
| 静态变量不在不同类型参数的类之间共享。 | 静态变量在不同类型参数类的实例之间共享。 |
