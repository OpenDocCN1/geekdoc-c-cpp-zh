
# 20.4.4 实现 `removeFirst()`

`removeFirst<T>` 函数可以如下实现：

```cpp
template<typename T>
LinkedList<T>::removeFirst() throw (runtime_error)
{
    if (size == 0)
        throw runtime_error("No elements in the list");
    else
    {
        Node<T> *temp = head;
        head = head->next;
        size--;
        if (head == NULL) tail = NULL;
        T element = temp->element;
        delete temp;
        return element;
    }
}
```

考虑三种情况：

1. 如果链表为空，抛出一个异常（第5行）；
2. 否则，通过将 `head` 指向第二个节点从列表中移除第一个节点，如图 20.9 所示。删除后 `size` 减少 1（第10行）；
3. 如果链表只有一个节点，在移除它后，`tail` 应该设置为 `NULL`（第11行）。

![](img/3b8bc24ba08ad32ac1a370eb095746a9_653_0.png)
(a) 在删除节点之前。

![](img/3b8bc24ba08ad32ac1a370eb095746a9_653_1.png)
(b) 在删除节点之后。

**图 20.9** 从链表中删除第一个节点。

## 20.4.5 实现 `removeLast()`

`removeLast<T>` 函数可以如下实现：

```cpp
template<typename T>
LinkedList<T>::removeLast() throw (runtime_error)
{
    if (size == 0)
        throw runtime_error("No elements in the list");
    else if (size == 1)
    {
        Node<T> *temp = head;
        head = tail = NULL;
        size = 0;
        T element = temp->element;
        delete temp;
        return element;
    }
    else
    {
        Node<T> *current = head;
        for (int i = 0; i < size - 2; i++)
            current = current->next;
        Node<T> *temp = tail;
        tail = current;
        tail->next = NULL;
        size--;
        T element = temp->element;
        delete temp;
        return element;
    }
}
```

考虑三种情况：

1. 如果链表为空，抛出一个异常（第5行）；
2. 如果链表只包含一个节点，该节点被销毁；`head` 和 `tail` 变为 `NULL`（第9行）；
3. 否则，最后一个节点被销毁，`tail` 重新定位指向倒数第二个节点，如图 20.10 所示。对于后两种情况，删除后 `size` 减少 1（第10行、25行），并返回被删除节点的值（第13行、28行）。

![](img/3b8bc24ba08ad32ac1a370eb095746a9_654_0.png)

**图 20.10** 从链表中删除最后一个节点。

## 20.4.6 实现 `removeAt(int index)`

`removeAt(int index)` 函数找到指定索引处的节点并将其移除。它可以如下实现：

```cpp
template<typename T>
Linkedlist<T>::removeAt(int index) throws (runtime_error)
{
    if (index < 0 || index >= size)
        throw runtime_error("Index out of range");
    else if (index == 0)
        return removeFirst();
    else if (index == size - 1)
        return removeLast();
    else
    {
        // 定位前一个节点
        Node<T> *previous = head;
        for (int i = 1; i < index; i++)
        {
            previous = previous->next;
        }
        // 定位当前节点
        Node<T> *current = previous->next;
        // 从列表中删除
        previous->next = current->next;
        size--;
        T element = current->element;
        delete current;
        return element;
    }
}
```

考虑以下四种情况：

- 1. 如果 `index` 超出了链表的范围（即 `index < 0 || index >= size`），抛出异常（第 5 行）；
- 2. 如果 `index` 为 0，调用 `removeFirst()` 删除第一个节点（第 7 行）；
- 3. 如果 `index` 为 `size - 1`，调用 `removeLast()` 删除最后一个节点（第 9 行）；
- 4. 否则，定位指定索引处的节点。让 `current` 表示该节点，`previous` 表示其前一个节点，如图 20.11(a)所示。将 `current->next` 赋值给 `previous->next` 以消除 `current` 节点，如图 20.11(b)所示。

![](img/3b8bc24ba08ad32ac1a370eb095746a9_655_0.png)

**图 20.11** 从链表中删除一个节点。

## 20.4.7 `LinkedList` 的源代码

列表 20.2 给出了 `LinkedList` 的实现。

### 列表 20.2 `LinkedList.h`

```cpp
#ifndef LINKEDLIST_H
#define LINKEDLIST_H

#include <stdexcept>
using namespace std;
```

`runtime_error` 头文件

```cpp
template<typename T>
class Node
{
public:
    T element; // 节点包含的元素
    Node<T>* next; // 指向下一个节点的指针
    Node() // 无参数构造函数
    {
        next = NULL;
    }
    Node(T element) // 构造函数
    {
        this->element = element;
        next = NULL;
    }
};

template<typename T>
class Iterator : public std::iterator<std::forward_iterator_tag, T> {
public:
    Iterator(Node<T>* p)
    {
        current = p;
    }
    Iterator operator++()
    {
        current = current -> next;
        return *this;
    }
    T& operator*()
    {
        return current -> element;
    }
    bool operator==(const Iterator<T>& iterator)
    {
        return current == iterator.current;
    }
    bool operator!=(const Iterator<T>& iterator)
    {
        return current != iterator.current;
    }
private:
    Node<T>* current;
};

template<typename T>
class LinkedList
{
public:
    LinkedList();
    LinkedList(LinkedList<T>& list);
    ~LinkedList();
    void addFirst(T element);
    void addLast(T element);
    T getFirst() const;
    T getLast() const;
    T removeFirst() throw (runtime_error);
    T removeLast();
    void add(T element);
    void add(int index, T element);
    void clear();
    bool contains(T element) const;
    T get(int index) const;
    int indexOf(T element) const;
    bool isEmpty() const;
    int lastIndexOf(T element) const;
    void remove(T element);
    int getSize() const;
    T removeAt(int index);
    T set(int index, T element);
    Iterator<T> begin()
    {
        return Iterator<T>(head);
    }
    Iterator<T> end()
    {
        return Iterator<T>(tail->next);
    }
private:
    Node<T> *head, *tail;
    int size;
};

template<typename T>
LinkedList<T>::LinkedList()
{
    head = tail = NULL;
    size = 0;
}

template<typename T>
LinkedList<T>::LinkedList(const LinkedList<T> &list)
{
    head = tail = NULL;
    size = 0;
    Node<T> *current = list.head;
    while (current != NULL) {
        this->add(current->element);
        current = current->next;
    }
}

template<typename T>
LinkedList<T>::~LinkedList()
{
    clear();
}
```

```cpp
template<typename T>
void LinkedList<T>::addFirst(T element)
{
    // 与 §20.4.1 相同，此处省略
}
```

```cpp
template<typename T>
void LinkedList<T>::addLast(T element)
{
    // 与 §20.4.2 相同，此处省略
}
```

```cpp
template<typename T>
T LinkedList<T>::getFirst() const
{
    if (size == 0)
        throw runtime_error("Index out of range");
    else
        return head->element;
}
```

```cpp
template<typename T>
T LinkedList<T>::removeFirst() throw (runtime_error)
{
    // 与 §20.4.4 相同，此处省略
}
```

```cpp
template<typename T>
T LinkedList<T>::removeLast()
{
    // 与 §20.4.5 相同，此处省略
}
```

```cpp
template<typename T>
void LinkedList<T>::add(int index, T element)
{
    // 与 §20.4.3 相同，此处省略
}
```

```cpp
template<typename T>
void LinkedList<T>::clear()
{
    while (head != NULL)
    {
        Node<T> *temp = head;
        head = head->next;
        delete temp;
    }
    tail = NULL;
}
```

```cpp
template<typename T>
T LinkedList<T>::get(int index) const
{
    if (index < 0 || index >= size)
        throw runtime_error("Index out of range");
    Node<T>* current = head;
    for (int i = 0; i < index; i++)
        current = current->next;
    return current->element;
}
```

```cpp
template<typename T>
int LinkedList<T>::indexOf(T element) const
{
    Node<T>* current = head;
    for (int i = 0; i < size; i++)
    {
        if (current->element == element)
            return i;
        current = current->next;
    }
    return -1;
}
```

```cpp
template<typename T>
bool LinkedList<T>::isEmpty() const
{
    return head == NULL;
}
```

```cpp
template<typename T>
int LinkedList<T>::getSize() const
{
    return size;
}
```

```cpp
template<typename T>
T LinkedList<T>::removeAt(int index)
{
    if (index < 0 || index >= size)
        throw runtime_error("Index out of range");
    Node<T>* current = head;
    for (int i = 0; i < index; i++)
        current = current->next;
    T element = current->element;
    if (index == 0)
        removeFirst();
    return element;
}
```

```cpp
template<typename T>
T LinkedList<T>::set(int index, T element)
{
    if (index < 0 || index >= size)
        throw runtime_error("Index out of range");
    Node<T>* current = head;
    for (int i = 0; i < index; i++)
        current = current->next;
    current->element = element;
    return element;
}
```
