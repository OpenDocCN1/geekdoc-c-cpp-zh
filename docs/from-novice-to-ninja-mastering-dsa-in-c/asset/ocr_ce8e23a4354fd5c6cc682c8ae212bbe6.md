```
while (forward != nullptr) {
    std::cout << forward->data << " ";
    forward = forward->next;
}
// Outputs: 1 2 3

std::cout << std::endl;

Node<int>* backward = node3;
while (backward != nullptr) {
    std::cout << backward->data << " ";
    backward = backward->prev;
}
// Outputs: 3 2 1

return 0;
}
```

# Insertion and Deletion in Doubly Linked Lists:

Doubly Linked Lists allow for efficient insertion and deletion operations, especially when working with both forward and backward traversal.

# Insertion at the Beginning:-

```
#include <iostream>

template <typename T>
void insertAtBeginning(Node<T>*& head, const T& value) {
    Node<T>* newNode = new Node<T>(value);
    newNode->next = head;
    if (head != nullptr) {
        head->prev = newNode;
    }
    head = newNode;
}

int main() {
    Node<int>* head = nullptr;

    // Inserting nodes at the beginning
    insertAtBeginning(head, 3);
    insertAtBeginning(head, 2);
    insertAtBeginning(head, 1);

    // Traversing and printing the modified linked list
    Node<int>* forward = head;
```