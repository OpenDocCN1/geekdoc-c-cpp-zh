

在某个系统上，程序打印

```
Creating widget 5
Entering main
Creating widget 10
10
5
Destroying widget 10
Destroying widget 5
```

请注意，在这个特定系统上，程序没有运行到完成，因为它没有打印 Leaving main。程序在尝试释放未在堆上动态分配的全局内存后崩溃。在某些系统的某些执行过程中，程序会运行到完成且没有明显问题，但这是因为该程序非常简单，在错误删除之后做的事情很少。无论程序表现如何，它都涉及被识别为未定义行为的代码，因此包含必须修复的错误。

虽然我们可以在清单 18.1 (howdelete.cpp) 的源代码中看到 get_widget1 和 get_widget2 的实现，但如果这些函数是我们没有源代码的预编译库的一部分，问题将更具挑战性。阅读库文档中返回指针的函数非常重要，以了解调用者预期如何管理这些指针所引用的内存。

## 18.3 链表

C++ 中的对象可以保存几乎任何类型的数据，但存在一些限制。考虑以下结构体定义：

结构体定义：

```
struct Node {
    int data;
    Node next; // Error, illegal self reference
};
```

（这里我们使用结构体而不是类，因为我们将把 Node 对象视为不需要客户端特殊保护的原始数据类型。）编译器应该为 Node 对象预留多少空间？Node 包含一个整数和一个 Node，但这个包含的 Node 字段本身又包含一个整数和一个 Node，嵌套包含将永远持续下去。这样的结构在 C++ 中是非法的，这可以理解，编译器会发出错误。在定义的类或结构体中，不允许拥有相同类型的字段。

另一个对象定义看起来相似，但它是合法的结构：

```
struct Node {
    int data;
    Node *next; // Self reference via pointer is legal
};
```

第二个版本之所以合法，是因为编译器现在可以计算 Node 对象的大小。指针本质上只是一个内存地址，因此所有指针变量的大小都相同，无论其声明类型如何。指针解决了无限嵌套包含的问题。

对象引用自身类型对象的能力不仅仅是一个有趣的奇观；它具有实际应用。假设我们希望实现类似 vector 的序列结构。我们可以使用

### Figure 18.2 以空终止的链表

![](img/e84ad11adb18201d71595b31ce6c9eff_561_0.png)

上面定义的自引用结构来构建一个通过指针链接在一起的 Node 对象列表。清单 18.2 (manualinkedlist.cpp) 手动构建一个小链表。

```
#include <iostream>

using namespace std;

struct Node {
  int data;    // The element of interest
  Node *next;  // Link to successor node in the link
             // Constructor
  Node(int data, Node *next): data(data), next(next) {}
};

int main() {
  // Node objects
  Node n4(3, nullptr),   // Make the last node
       n3(0, &n4),       // Make the next to last node and link to last node
       n2(10, &n3),      // Make the second node and link to third node
       n1(23, &n2);      // Make the first node and link to second node

  // Print the linked list built from the Node objects
  for (Node *cursor = &n1; cursor != nullptr; cursor = cursor->next)
    std::cout << cursor->data << ' ';
  std::cout << '\n';
}
```

清单 18.2 (manualinkedlist.cpp) 创建了图 18.2 中所示的以空终止的链表。程序打印

```
23 10 0 3
```

在图 18.2 中，节点 n4 的 next 字段中的线表示空指针。

清单 18.2 (manualinkedlist.cpp) 通过添加构造函数来扩展简单的 Node 结构体。程序不使用动态内存（没有调用 new）；这只有在我们事先知道列表中包含哪些节点时才可能。for 循环使用名为 cursor 的指针来访问列表中的每个节点。cursor 变量首先指向节点 n1。语句 cursor = cursor->next 将 cursor 重新赋值为指向当前节点之后的节点。这使得 cursor 可以访问节点 n1、n2、n3，最后 cursor 将指向列表中的最后一个节点 n4。n4 的 next 字段是 nullptr，因此当循环将 cursor 重新赋值为 n4 的 next 字段时，cursor 将为 nullptr，循环将终止。

值 `nullptr` 在布尔上下文中被视为 `false`，因此我们可以将布尔表达式 `cursor != nullptr` 简化为仅 `cursor`；这使我们可以稍微简化循环，如下所示：

```
// Print the linked list built from the Node objects
for (Node *cursor = &n1; cursor = cursor->next)
    std::cout << cursor->data << ' ';
```

由于我们将四个列表节点硬编码到程序源代码中，循环实际上并不必要。以下语句：

```
std::cout << n1.data << ' ' << n2.data << ' ' << n3.data
     << n4.data << '\n';
```

更简单，但何止于此？由于我们事先知道节点及其值，以下语句更简单：

```
std::cout << "23 10 0 3\n";
```

图 18.2 和清单 18.2 (manualinkedlist.cpp) 中的硬编码列表并未展示链表动态特性所能带来的实用性。只有在元素事先未知时，使用链表才有意义。然后我们可以在元素可用时动态分配空间。

凭借我们对 C++ 类、封装和方法的了解，我们可以构建一个对客户端友好的动态链表类型。清单 18.3 (intlist1.h)、清单 18.4 (intlist1.cpp) 和清单 18.5 (listmain.cpp) 中的代码展示了链表的强大功能。清单 18.3 (intlist1.h) 是简单整数链表类的头文件。

### Listing 18.3: intlist1.h

```
class IntList1 {
    /*
     * An object that holds an element in a linked list.
     * This type is local to the IntList1 class and inaccessible
     * to outside this class.
     */
    struct Node {
        int data;      // A data element of the list
        Node *next;    // The node that follows this one in the list
        Node(int d);   // Constructor
    };

    Node *head;   // Points to the first item in the list
    Node *tail;   // Points to the last item in the list

    /*
     * Returns the length of the linked list pointed to by p.
     */
    int length(Node *p) const;

    /*
     * dispose(p)
     * Deallocate the memory held by the list pointed to by p.
     */
    void dispose(Node *p);
```

```
public:
    /*
     * The constructor makes an initially empty list
     */
    IntList();

    /*
     * insert(n)
     *  Inserts n onto the back of the list.
     *  n is the element to insert.
     */
    void insert(int n);

    /*
     * print()
     *  Prints the contents of the linked list of integers.
     */
    void print() const;

    /*
     * Returns the length of the linked list.
     */
    int length() const;

    /*
     * clear()
     *  Removes all the elements in the linked list.
     */
    void clear();
};
```

Node 结构体在 IntList 类中声明。我们说 Node 是一个嵌套结构体。由于 Node 的声明出现在 IntList 的私有部分，Node 是仅 IntList 类中的代码所知的类型。由于其声明嵌套在 IntList 类中，Node 类型的完整名称是 IntList::Node。请回顾，结构体相当于类，只是其成员的默认访问权限是 public。我们可以以定义嵌套结构体的相同方式定义嵌套结构体。

请注意，IntList 类除了公有方法外还有几个私有方法。类外部的代码不能直接执行这些私有方法。这些私有方法是辅助方法，多个公有方法会调用它们来完成任务。我们说公有方法将工作委托给其私有辅助方法。为什么在这里需要这种委托？私有方法使用递归，需要 IntList1::Node 类型的参数，而该类型在 IntList1 类之外未知。因此，客户端无法直接使用私有方法，即使它们被设为公有。公有方法不会向客户端暴露类的任何实现细节；具体来说，它们将 IntList1::Node 类型以及 head 和 tail 实例变量对客户端隐藏起来。

请注意，IntList1 类的重载 length 方法（私有和公有）以及 print 方法都声明为 const。既不打印列表也不请求其长度应该修改 IntList1 对象。因此，客户端可以在常量 IntList1 对象上使用 print 和 length 方法。尝试在常量 IntList1 对象上使用 insert 或 clear 会导致编译器错误。这个错误是有道理的，因为 insert 肯定会修改列表对象，而 clear 可能会修改列表对象（我们说可能是因为 clear 不会修改一个

