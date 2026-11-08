It takes some figuring out in which order these actions should be performed. If you’re not careful, you may even run into crashes. Here is a working solution, though:

```
```cpp
template <typename T>
{
    Stack<T>::pop()
    {
        if (isEmpty())                  // If it's empty, pop() is not valid so throw exception
            throw std::logic_error {"Stack empty"};

        auto* next {m_head->m_next};    // Save pointer to the next node
        T item {m_head->m_item};        // Save the T value to return later
        delete m_head;                  // Delete the current head
        m_head = next;                  // Make head point to the next node
        return item;                    // Return the top object
    }
}
```
```

The key is that you mustn’t delete the old `m_head` without first extracting all information from it that you still need—in this case both its `m_next` pointer (which is to become the new `m_head`) and its `T item` (the value that you have to return from the `pop()` function). Once you realize this, the rest writes itself.

In the destructor you face a similar problem (remember this for later!). Clearly, it needs to release all dynamically allocated Node objects belonging to the current Stack object. From the `pop()` template you know not to delete any Nodes without first copying what you still need from it:

```
```cpp
template <typename T>
Stack<T>::~Stack()
{
    while (m_head)
    {
        auto* next = m_head->m_next;    // while current pointer is not null
        delete m_head;                  // Delete the current node
        m_head = next;                  // Make m_head point to the next node
    }
}
```
```

Without the temporary pointer `next` to hold the address stored in `m_head->m_next`, you couldn’t move `m_head` along anymore to the next Node in the list. At the end of the while loop, all Node objects belonging to the current Stack object will have been deleted and `m_head` will be nullptr.

That’s all the templates you need to define the stack. If you gather all the templates into a module interface file, Stack.cpp you can try it with the following code:

```
```cpp
// Ex17_04.cpp
// Using a stack defined by nested class templates
import stack;
import <iostream>;
import <string>;

int main()
{
    std::string words[] {"The", "quick", "brown", "fox", "jumps"};
    Stack<std::string> wordStack;       // A stack of strings
```
```