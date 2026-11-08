This copies the stack represented by the stack input argument to the current Stack object, which is assumed to be empty (the m_head member variable starts out initialized to nullptr). It does this by replicating the m_head of the argument object, then walking through the sequence of Node objects, copying them one by one. The process ends when the Node object with a null m_next member has been copied. The isEmpty() functions simply check whether the m_head member points to an actual Node or is nullptr:

```
```cpp
template <typename T>
bool Stack<T>::isEmpty() const { return m_head == nullptr; }
```
```

The template for the swap() function is implemented as follows:

```
```cpp
template <typename T>
void Stack<T>::swap(Stack& other) noexcept
{
    std::swap(m_head, other.m_head);
}
```
```

(For completeness, you could add the conventional template for nonmember swap(Stack<T>&, Stack<T>&) functions as well. We do not show it here, but it is part of Ex17_04.)

The template for the assignment operator then uses the corresponding swap() function to implement the copy-and-swap idiom we introduced earlier in this chapter:

```
```cpp
template <typename T>
Stack<T>& Stack<T>::operator=(const Stack& stack)
{
    auto copy{rhs}; // Copy this             (could go wrong and throw an exception)
    swap(copy);     // ... and swap!         (noexcept)
    return *this;
}
```
```

The template for the push() operation is fairly easy as well:

```
```cpp
template <typename T>
void Stack<T>::push(const T& item)
{
    Node* node{new Node(item)}; // Create the new node
    node->m_next = m_head;      // Point to the old top node
    m_head = node;              // Make the new node the top
}
```
```

The Node object encapsulating m_item is created by passing the reference to the Node constructor. The m_next member of the new node needs to point to the node that was previously at the top. The new Node object then becomes the top of the stack, so its address is stored in m_head.

The pop() operation is slightly more involved, though. The first question you need to answer is, what should happen if pop() is invoked on an empty stack? Because the function returns a T object by value, you can’t easily signal an error through the return value. One obvious solution is to throw an exception in this case, so let’s do that. Once that corner case is taken care of, you know that the function has to perform at least the following three actions:

+   1. Return the T item stored in the current m_head.
+   2. Make m_head point to the next Node in the linked list.
+   3. Delete the old m_head Node that is no longer required now.