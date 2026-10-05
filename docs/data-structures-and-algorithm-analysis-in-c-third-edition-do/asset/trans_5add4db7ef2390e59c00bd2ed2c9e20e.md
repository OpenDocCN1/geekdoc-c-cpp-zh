

```cpp
// 支持空闲表的双向链表节点
template <typename E> class Link {
private:
    static Link<E>* freelist; // 指向空闲表头的引用

public:
    E element;      // 节点的值
    Link* next; // 指向链表中下一个节点的指针
    Link* prev; // 指向上一个节点的指针

    // 构造函数
    Link(const E& it, Link* next, Link* prev) {
        element = it;
        prev = prev;
        next = next;
    }
    Link(Link* prev=NULL, Link* next=NULL) {
        prev = prev;
        next = next;
    }

    void* operator new(size_t) { // 重载 new 运算符
        if (freelist == NULL) return ::operator new(size); // 创建空间
        Link<E>* temp = freelist; // 可以从空闲表中获取
        freelist = freelist->next;
        return temp;
    }

    void operator delete(void* ptr) {
        ((Link<E>*)ptr)->next = freelist; // 放入空闲表
        freelist = (Link<E>*)ptr;
    }
};

// 空闲表头指针实际上在此创建
template <typename E>
Link<E>* Link<E>::freelist = NULL;
```

图 4.13 带有空闲表的双向链表节点实现。

```cpp
// 在当前位置插入 "it"
void insert(const E& it) {
    curr->next = curr->next->prev =
    new Link<E>(it, curr, curr->next);
    cnt++;
}
```

```cpp
// 将 "it" 追加到链表末尾。
void append(const E& it) {
    tail->prev = tail->prev->next =
    new Link<E>(it, tail->prev, tail);
    cnt++;
}
```

```cpp
// 并返回当前元素
E remove() {
    if (curr->next == tail) // 无可删除内容
        return NULL;
    E it = curr->next->element; // 记住值
    Link<E> ltemp = curr->next->prev; // 记住链接节点
    curr->next->next->prev = curr;
    curr->next = curr->next->next; // 从链表中移除
    delete ltemp; // 释放空间
    cnt--; // 递减 cnt
    return it;
}
```

```cpp
// 边界向左移动一步；如果左侧为空则不改变
void prev() {
    if (curr != head) // 无法从头部列表回退
        curr = curr->prev;
}
```

图 4.14 双向链表插入、追加、删除和上 prev 方法的实现。

```cpp
Link<E> ltemp = curr->next; // 记住链接节点
curr->next->next->prev = curr;
curr->next = curr->next->next; // 从链表中移除
delete ltemp; // 释放空间
```

第一行设置一个指向被删除节点的指针。第二行让下一个节点的 `prev` 指向被删除节点的左侧。最后，调整被删除节点的 `next` 字段。`remove` 方法的最后步骤是更新长度、将删除的节点返回存储，并返回被删除元素的值。

双向链表与单向链表相比的唯一缺点是额外的空间。双向链表每个节点需要两个指针，因此在所展示的实现中，开销是单向链表的两倍。

第 4.1 节 列表

119

![](img/0ae21f56d72533acf0527c86ba21e1e6_137_0.png)

图 4.15 双向链表的插入。标签 1、2、3 对应链表节点构造函数完成的赋值。4 标记对 `curr->next` 的赋值。5 标记对新插入节点之后节点的 `prev` 指针的赋值。

![](img/0ae21f56d72533acf0527c86ba21e1e6_137_1.png)

图 4.16 双向链表的删除。元素 `it` 存储被删除节点的元素。然后调整其两侧节点的指针。

# 示例 4.1 有一种节省空间的技术可以用来消除额外的空间需求，尽管它会使实现变得复杂且速度较慢。因此，这是一个空间/时间权衡的示例。它基于一种观察：如果我们存储两个值的和，就可以通过减去另一个值来获取其中一个值。也就是说，如果我们将 $a+b$ 存储在变量 $c$ 中，那么 $b=c-a$ 且 $a=c-b$。当然，为了从存储的和中恢复其中一个值，必须提供另一个值。指向链中第一个节点的指针，带有其两个链接字段之一的值，将允许访问链中剩余的所有节点。这是因为该指针必须是节点的 `next` 指针。利用节点 `prev` 指针的值，可以沿着链表向下移动，拆分相加的链接字段，就像拉开拉链一样。关于实现这种变体的细节被留作课后练习。

这种技术背后的原理值得记住，因为它有很多应用。下面的代码片段将交换两个变量的内容：

```cpp
a = a + b;
b = a - b;
a = a - b;
```

这种技术也可以用于交换数组中的元素，而不需要临时变量。然而，这种方法在实际应用中并不常见，因为存在溢出的风险。

# 4.2 栈

栈是一种只能从一端插入或删除元素的结构。这种限制使得栈比列表不灵活，但也使其操作更高效且容易实现。栈开发了一种特殊的术语：LIFO（后进先出）。

数组栈实现本质上是数组列表的简化版本。唯一重要的设计决策是确定数组的哪一端代表栈的顶部。一种选择是让顶部位于数组的位置 0。对于列表函数来说，插入和删除操作在这里。这种实现是低效的，因为每次 `push` 或 `pop` 操作都会将栈中所有元素移动一个位置，当有 $n$ 个元素时开销为 $\Theta(n)$。另一种选择是当栈中有 $n$ 个元素时，让顶部元素位于位置 $n-1$。换句话说，当元素推入栈时，它们被追加到链表的末尾。`pop` 方法移除末尾元素。

```cpp
// 栈抽象类
template <typename E> class Stack {
private:
    int maxSize;                // 栈的最大容量
    int top;                    // 顶部索引
    E *listArray;               // 存储元素的数组

public:
    Stack(int size = 100) { // 构造函数
        maxSize = size; top = 0; listArray = new E[size];
    }
    ~Stack() { delete [] listArray; } // 析构函数
    void clear() { top = 0; } // 初始化
    void push(const E& it) { // 将 "it" 入栈
        Assert(top != maxSize, "栈溢");
        listArray[top++] = it;
    }
    E pop() { // 返回顶部元素
        Assert(top != 0, "栈空");
        return listArray[--top];
    }
    const E& top() const { // 返回顶部
        Assert(top != 0, "栈空");
        return listArray[top-1];
    }
    int length() const { return top; } // 返回长度
};
```

图 4.18 数组栈。

对于图 4.18 的实现，`top` 被定义为栈中第一个空闲位置的数组索引。因此，空栈的 `top` 设置为 0，即数组中第一个可空位置。（或者，`top` 可以被定义为