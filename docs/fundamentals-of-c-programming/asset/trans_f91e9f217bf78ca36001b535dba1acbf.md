

```cpp
// Move assignment operator
IntList6& IntList6::operator=(IntList6& temp) {
    // Exchange the head and tail pointers and len from this list
    // with those of the new, temporary list
    std::swap(head, temp.head);
    std::swap(tail, temp.tail);
    std::swap(len, temp.len);
    // The temporary now points to this list's original contents,
    // and this list now points to the temporary's list
    // The temporary list will be destroyed since it is a temporary
    return *this;
}
```

```cpp
// The destructor deallocates the memory held by the list
IntList6::~IntList6() { clear(); }
```

```cpp
// Inserts n onto the back of the list.
// n is the element to insert.
void IntList6::insert(int n) {
    // Make a node for the new element
    auto new_node = std::make_shared<Node>(n);
    if (tail) { // Is tail non-null?
        tail->next = new_node; // Link the new node onto the back
        tail = new_node; // The new node is the new tail of the list
    }
    else // List is empty, so make head and tail point to new node
        head = tail = new_node;
    len++;
}
```

```cpp
// Prints the contents of the linked list of integers.
void IntList6::print() const {
    for (auto cursor = head; cursor; cursor = cursor->next)
        std::cout << cursor->data << ' ';
    std::cout << '\n';
}
```

```cpp
// Returns the length of the linked list.
int IntList6::length() const {
    return len;
}
```

```cpp
// Removes all the elements in the linked list.
void IntList6::clear() {
    auto cursor = head;
    while (cursor) {
        auto temp = cursor; // Remember where we are
        cursor = cursor->next; // Move next node
        temp->next = nullptr; // Sever link from previous node
    }
    head = tail = nullptr; // Null head signifies list is empty
    len = 0;
}
```

在 IntList6 类中，我们看不到 new 或 delete 运算符。std::make_shared 函数和 std::shared_ptr 类为我们隐藏了这些细节。

我们本可以将 clear 方法中的代码表述得像下面这样简单：

```cpp
void IntList6::clear() {
    head = tail = nullptr; // Null head signifies list is empty
    len = 0;
}
```

请注意，它不使用循环来遍历列表中的节点。当我们将指向列表第一个元素的 head 设置为 nullptr 时，智能指针的重新赋值会自动销毁列表中的第一个节点。这是因为当前没有其他智能指针指向该节点。将 tail 指针设置为 null 可确保列表中的最后一个元素仅由倒数第二个元素的 next 指针指向。列表中第一个节点的销毁将销毁指向列表中第二个节点的第一个节点的 next 指针。这导致第二个节点被销毁。第二个节点的销毁会销毁其 next 指针，进而导致第三个节点、第四个节点等被销毁。这种级联过程最终会销毁 head 所指向列表中的所有节点。

如果 clear 的这种简单实现能与使用循环的清单 18.25（intlist6.cpp）中更复杂的 clear 方法达到相同的结果，为什么还要考虑更复杂的代码呢？事实证明，简单的方法在处理非常长的列表时存在问题。要了解原因，假设我们有一个很长的链表。当 clear 方法将 std::shared_ptr head 设置为 null 时，没有其他智能指针会指向第一个节点。在这种情况下，智能指针的重新赋值会在幕后调用一个方法来销毁它所指向的对象（即 head 所指向的对象，也就是列表中的第一个节点）。这个清理方法在过程完成之前不会返回，而对于很长的列表，这个过程可能非常耗时。第一个节点的销毁需要销毁其 next 指针 head->next。这个 head->next 指针指向列表中的第二个节点。销毁这个 head->next 指针会触发第二个节点的销毁，因为没有其他 std::shared_ptr 对象指向它。这意味着在 head 的清理方法返回之前，它触发的一系列事件必须调用 head->next 的清理方法，从而导致第二个节点被销毁。第二个节点的销毁必然要销毁第二个节点的下一个智能指针（head->next->next）。这反过来又会导致 head->next->next 所指向的对象（即列表中的第三个节点）被销毁。通过同样的过程，列表中第三个节点的销毁会导致第四个节点、第五个节点等被销毁。这种方法调用的级联过程会一直持续到到达列表中的最后一个节点。有两个智能指针指向最后一个节点：列表中倒数第二个节点的 next 指针以及 LinkedList 对象本身的 tail 指针。销毁倒数第二个节点会移除其中一个智能指针，但不会移除另一个。这意味着倒数第二个节点的清理方法无法销毁最后一个节点。然而，这会导致内存泄漏，因为 clear 方法也将 tail 设置为 nullptr，因此最后一个节点最终会被正确销毁。

一切看起来都运行完美——自动资源管理正如广告所宣称的那样——那么对于非常长的列表，问题出在哪里呢？我们之前描述 LinkedList::clear 方法的活动时，停留在倒数第三个智能指针的清理方法正在销毁倒数第二个节点的地方。问题在于：列表中第一个节点的销毁要等到第二个节点的销毁完成才算结束。第二个节点的销毁要等到第三个节点的销毁完成才算结束，以此类推。这意味着销毁第一个节点的清理方法不会完成自己的工作、返回，然后再清理该节点的 next 指针；它要等到第二个节点完成清理才返回，而第二个节点又要等到第三个节点的清理完成，以此类推。理论上，这条函数调用链最终会返回到发起它的操作——即将 head 重新赋值为 nullptr，对于不太长的列表，情况确实如此。每个方法调用都会消耗一些栈空间，对于非常长的列表，这条调用链可能会很深，以至于导致栈溢出，从而使程序崩溃。这种情况类似于递归层数过深的递归函数。在一个系统上，程序在尝试销毁包含 10,000 个节点的链表时崩溃了。

清单 18.25（intlist6.cpp）中 clear 方法的版本会遍历列表，将其最近访问过的节点的 next 指针设置为 nullptr。在下一次迭代中，临时指针 temp 在从 cursor 重新赋值期间销毁节点。这意味着它必须销毁 temp 的下一个智能指针，但上一次迭代已将其设置为 null。这消除了链式问题，并允许前一个节点通过单个立即返回的函数调用来销毁。这个版本通过一系列独立、隔离的立即返回的函数调用来释放列表，而不是一条可能导致栈溢出的函数调用链。

## 清单 18.26：smartlist.cpp

```cpp
// smartlist.cpp

#include <iostream>
#include "intlist6.h"

void test() {
  IntList6 list;
  for (int i = 0; i < 10; i++)
    list.insert(i);
  list.print();
}

int main() {
  for (int i = 0; i < 10; i++)
    test();
}
```

运行清单 18.26（smartlist.cpp）时，你会看到所有 Node 对象的创建都有对应的销毁。std::shared_ptr 对象负责处理所有堆内存管理。

我们的链表类有一个 insert 方法，允许客户端向列表中添加元素，但没有方法可以让客户端删除单个元素。在我们最近的非智能指针类 IntList5 中，我们可以添加以下方法：

```cpp
// Removes the first occurrence of n from the list.
// Returns true if successful (found n and removed it).
// Returns false if n is not originally present in the list.
bool IntList5::remove(int n) {
  Node *cursor = head, // Start at head of list
       *prev = head;   // Keep track of previous node seen
  // Loop until we run off the end of the list or
  // whichever comes first
  while (cursor && cursor->data != n) {
    prev = cursor;     // Remember previous node
    cursor = cursor->next; // Move to next node
  }
  if (!cursor)         // Did we run off the end of the list?
    return false;      // Indicate we did not find n
```

