

IntList5& IntList5::operator=(IntList5&& temp) {
    // Exchange the head and tail pointers and len from this list
    // with those of the new, temporary list
    std::swap(head, temp.head);
    std::swap(tail, temp.tail);
    std::swap(len, temp.len);
    // The temporary list now points to this list's original contents,
    // and this list now points to the temporary's list
    // The temporary list will be destroyed since it is a temporary
    return *this;
}

移动构造函数总是将其空列表与临时对象的列表进行交换，但移动赋值运算符用临时对象的列表替换被赋值对象的列表。被赋值对象的列表可能为空，但通常情况下不会为空。当移动赋值运算符返回时，传递给它的临时对象将不复存在。随后，临时对象的析构函数将正确释放被赋值对象原先的节点列表。

与移动构造函数一样，移动赋值运算符的右值引用参数不得声明为 const，否则临时对象将无法接收被赋值对象的数据。同样与移动构造函数一样，移动赋值运算符对临时对象进行的修改必须使其处于良好定义的状态，以便其析构函数能够成功销毁它。

清单 18.19 (intlist5.cpp) 包含了 IntList5 类的完整实现。

```
Listing 18.19: intlist5.cpp

// intlist5.cpp

#include "intlist5.h"
#include <iostream>
#include <utility>

// Private IntList5 operations

// Node constructor
IntList5::Node::Node(int n): data(n), next(nullptr) {
    std::cout << "Creating node " << data
              << " (" << reinterpret_cast<uintptr_t>(this) << ")\n";
}

IntList5::Node::~Node() {
    std::cout << "Destroying node " << data
              << " (" << reinterpret_cast<uintptr_t>(this) << ")\n";
}

// The constructor makes an initially empty list.
// The list is empty when head and tail are null.
// The list's size initially is zero.
IntList5::IntList5(): head(nullptr), tail(nullptr), len(0) {}

// Copy constructor makes a copy of the other object's list
IntList5::IntList5(const IntList5& other): IntList5() {
    // Walk through other's list inserting each of its elements
    // into this list
```

```
for (auto cursor = other.head; cursor; cursor = cursor->next)
    insert(cursor->data);
}
```

```
// Move constructor takes possession of the temporary's list
IntList5::IntList5(IntList5&& temp): IntList5() {
    // Swap contents with the temporary
    std::swap(head, temp.head);
    std::swap(tail, temp.tail);
    std::swap(len, temp.len);
}
```

```
// Assignment operator
IntList5& IntList5::operator=(const IntList5& other) {
    // Make a local, temporary copy of other
    IntList5 temp(other);
    // Exchange the head and tail pointers and len from this list
    // with those of the new, temporary list
    std::swap(head, temp.head);
    std::swap(tail, temp.tail);
    std::swap(len, temp.len);
    // The temporary list now points to this list's original contents,
    // and this list now points to the copy of other's list
    // The temporary list will be destroyed since it is a temporary
    return *this;
}
```

```
// Move assignment operator
IntList5& IntList5::operator=(IntList5&& temp) {
    // Exchange the head and tail pointers and len from this list
    // with those of the new, temporary list
    std::swap(head, temp.head);
    std::swap(tail, temp.tail);
    std::swap(len, temp.len);
    // The temporary list now points to this list's original contents,
    // and this list now points to the temporary's list
    // The temporary list will be destroyed since it is a temporary
    return *this;
}
```

```
// The destructor deallocates the memory held by the list
IntList5::~IntList5() { clear(); }
```

```
// Inserts n onto the back of the list.
// n is the element to insert.
void IntList5::insert(int n) {
    // Make a node for the new element n
    IntList5::Node *new_node = new Node(n);
    if (tail) { // Is tail non-null?
        tail->next = new_node; // Link the new node onto the back
        tail = new_node; // The new node is the new tail of the list
    }
    else // List is empty, so make head and tail point to new node
        head = tail = new_node;
    len++; // List now contains one more element
}
```

```
// Prints the contents of the linked list of integers.
void IntList5::print() const {
    for (auto cursor = head; cursor; cursor = cursor->next)
        std::cout << cursor->data << ' ';
    std::cout << '\n';
}

// Returns the length of the linked list.
int IntList5::Length() const {
    return len;
}

// Removes all the elements in the linked list.
void IntList5::clear() {
    auto cursor = head;
    while (cursor) {
        auto temp = cursor;
        cursor = cursor->next;
        delete temp;
    }
    head = tail = nullptr; // Null head signifies list is empty
    len = 0;
}
```

清单 18.20 (templist2.cpp) 与清单 18.16 (templist.cpp) 的代码相同，只是它使用了我们迭代器链表类的最新迭代版本。

## 清单 18.20: templist2.cpp

```
#include <iostream>
#include "intlist5.h"

IntList5 make_list(int n) {
    IntList5 result;
    for (int i = 0; i < n; i++)
        result.insert(i);
    return result;
}

int main() {
    auto my_list = make_list(5);
    my_list.print();
}
```

清单 18.20 (templist2.cpp) 的输出证实，我们添加的移动构造函数避免了仅为了传递临时对象而创建额外链表对象。

```
Creating node 0 (21169512)
Creating node 1 (21214272)
Creating node 2 (21214512)
Creating node 3 (21214304)
Creating node 4 (21214208)
0 1 2 3 4
Destroying node 4 (21214208)
Destroying node 3 (21214304)
Destroying node 2 (21214512)
Destroying node 1 (21214272)
Destroying node 0 (21169512)
```

make_list 函数创建临时对象；这解释了所有以 "Creating node..." 开头的语句。移动构造函数交换了临时对象的节点列表与新创建的 my_list 对象中发现的空列表。此时，my_list 包含临时对象的原始列表，而临时对象包含空列表。临时对象的析构函数执行，但找不到可销毁的节点（head 为 null）。在 main 函数结束时，my_list 的析构函数删除 my_list 中的所有节点。

顺便指出，编译器可以检测到 make_list 函数创建了一个局部对象 (result) 但仅将其返回给调用者。编译器可以使用返回值优化（参见第 11.1.4 节）来避免在函数内创建额外对象以返回给调用者。相反，编译器生成代码，使 make_list 函数能够直接在调用者的环境中创建链表对象。

移动构造和移动赋值的加入将我们带到了 C++ 的“五法则”。五法则涉及拷贝构造、移动构造、析构、拷贝赋值和移动赋值。如果程序员为类没有定义这些特殊方法中的任何一个，编译器将自动为每个方法提供自己的版本，这些版本适用于支持值语义的类；例如，第 16 章中的所有类都支持值语义。使用值语义的类避免了我们在链表类中遇到的内存管理和别名问题。

如果程序员定义了拷贝构造函数、析构函数或拷贝赋值运算符中的一个或多个，编译器不会自动提供移动构造函数或移动赋值运算符。就程序正确性而言，这不是问题；移动构造和移动赋值仅提供一种优化，用于在从右值（临时对象）构造或赋值时避免不必要地创建额外对象。缺少移动构造函数意味着临时对象将由拷贝构造函数拷贝，缺少移动赋值运算符意味着临时对象将由拷贝赋值运算符拷贝。

程序员可以通过显式地用 default 或 delete 标记这些方法，精确控制编译器提供哪些特殊方法。我们不会在此深入细节，而仅提供几个示例。

考虑类 X1：

```
class X1 {
public:
   int data;
};
```

类 X1 没有显式构造函数；因此，编译器将提供一个允许调用者创建 X1 对象的构造函数。

```
X1 my_x1; // Okay; default constructed
std::cout << my_x1.data << '\n'; // Prints some random integer value
```

在这种情况下，客户端需要重新赋值 my_x1.data，该对象才算是有点用处。

接下来，考虑类 X2：

