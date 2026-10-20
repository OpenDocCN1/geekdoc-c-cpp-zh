
## Bubble Sort:-

```
#include <iostream>

void bubbleSort(int arr[], int size) {
    for (int i = 0; i < size - 1; ++i) {
        for (int j = 0; j < size - i - 1; ++j) {
            if (arr[j] > arr[j + 1]) {
                // Swap elements if they are in the wrong order
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

int main() {
    int numbers[] = {5, 2, 8, 1, 3};
    int size = 5;

    // Sorting the array using bubble sort
    bubbleSort(numbers, size);

    // Printing the sorted array
    for (int i = 0; i < size; ++i) {
        std::cout << numbers[i] << " ";
    }
    // Outputs: 1 2 3 5 8

    return 0;
}
```

## Conclusion:

Arrays serve as a powerful data structure for sequential storage, offering efficient random access and supporting various manipulation techniques and algorithms. As we delve deeper into this chapter, we will explore linked lists, another dynamic data structure that provides flexibility in memory allocation and manipulation.

## Singly Linked Lists: Unveiling Dynamic Linked Structures

Singly Linked Lists are dynamic data structures that provide an efficient way to store and manage collections of elements. Unlike arrays, linked lists offer dynamic memory allocation, allowing for easy insertion and removal of elements at any position.

## Basic Structure of a Singly Linked List:

A Singly Linked List consists of nodes, where each node contains two parts: the data and a reference (or pointer) to the next node in the sequence.

```
#include <iostream>

// Node structure for a Singly Linked List
template <typename T>
struct Node {
    T data;
    Node* next;

    Node(const T& value) : data(value), next(nullptr) {}
};

int main() {
    // Creating nodes for a Singly Linked List
    Node<int>* node1 = new Node<int>(1);
    Node<int>* node2 = new Node<int>(2);
    Node<int>* node3 = new Node<int>(3);

    // Linking nodes to form a Singly Linked List
    node1->next = node2;
    node2->next = node3;

    // Traversing and printing the linked list
    Node<int>* current = node1;
    while (current != nullptr) {
        std::cout << current->data << " ";
        current = current->next;
    }
    // Outputs: 1 2 3

    return 0;
}
```

## Insertion and Deletion in Singly Linked Lists:

One of the key advantages of linked lists is the ease of insertion and deletion. Adding a new node or removing an existing one involves adjusting the pointers, without the need for contiguous memory.

## Insertion at the Beginning:-

```
#include <iostream>

template <typename T>
void insertAtBeginning(Node<T>*& head, const T& value) {
    Node<T>* newNode = new Node<T>(value);
    newNode->next = head;
    head = newNode;
}

int main() {
    Node<int>* head = nullptr;

    // Inserting nodes at the beginning
    insertAtBeginning(head, 3);
    insertAtBeginning(head, 2);
    insertAtBeginning(head, 1);

    // Traversing and printing the modified linked list
    Node<int>* current = head;
    while (current != nullptr) {
        std::cout << current->data << " ";
        current = current->next;
    }
    // Outputs: 1 2 3

    return 0;
}
```

## Deletion at a Given Position:-

```
#include <iostream>

template <typename T>
void deleteAtPosition(Node<T>*& head, int position) {
    if (head == nullptr) {
        return;  // No nodes to delete
    }
}

if (position == 0) {
    Node<T>* temp = head;
    head = head->next;
    delete temp;
    return;
}

Node<T>* current = head;
for (int i = 0; i < position - 1 && current->next != nullptr; ++i)
{
    current = current->next;
}

if (current->next == nullptr || position < 0) {
    return; // Invalid position
}

Node<T>* temp = current->next;
current->next = current->next->next;
delete temp;
}

int main() {
    Node<int>* head = nullptr;
    // Inserting nodes
    insertAtBeginning(head, 3);
    insertAtBeginning(head, 2);
    insertAtBeginning(head, 1);

    // Deleting a node at position 1
    deleteAtPosition(head, 1);

    // Traversing and printing the modified linked list
    Node<int>* current = head;
    while (current != nullptr) {
        std::cout << current->data << " ";
        current = current->next;
    }
    // Outputs: 1 3

    return 0;
}
```

## Searching and Traversing in Singly Linked Lists:

Searching in a singly linked list involves traversing the list until the target element is found or the end of the list is reached.

```
```cpp
#include <iostream>

template <typename T>
bool searchElement(const Node<T>* head, const T& target) {
    const Node<T>* current = head;
    while (current != nullptr) {
        if (current->data == target) {
            return true; // Element found
        }
        current = current->next;
    }
    return false; // Element not found
}

int main() {
    Node<int>* head = nullptr;
    // Inserting nodes
    insertAtBeginning(head, 3);
    insertAtBeginning(head, 2);
    insertAtBeginning(head, 1);
    // Searching for an element
    int target = 2;
    if (searchElement(head, target)) {
        std::cout << "Element " << target << " found in the linked list." << std::endl;
    } else {
        std::cout << "Element " << target << " not found in the linked list." << std::endl;
    }
    return 0;
}
```
```

## Conclusion:

Singly Linked Lists provide a flexible and dynamic data structure for managing collections of elements. Their simplicity allows for efficient insertion and deletion operations, making them suitable for scenarios where dynamic memory allocation and modification are common requirements.

## Doubly Linked Lists: Embracing Bidirectional Linking

Doubly Linked Lists extend the capabilities of singly linked lists by providing bidirectional links between nodes. In addition to a reference to the next node, each node in a doubly linked list also contains a reference to the previous node. This bidirectional linking simplifies certain operations, such as traversing the list in both directions.

## Basic Structure of a Doubly Linked List:

A Doubly Linked List node contains three parts: the data, a reference to the next node, and a reference to the previous node.

```
#include <iostream>

// Node structure for a Doubly Linked List
template <typename T>
struct Node {
    T data;
    Node* next;
    Node* prev;

    Node(const T& value) : data(value), next(nullptr), prev(nullptr) {}
};

int main() {
    // Creating nodes for a Doubly Linked List
    Node<int>* node1 = new Node<int>(1);
    Node<int>* node2 = new Node<int>(2);
    Node<int>* node3 = new Node<int>(3);

    // Linking nodes to form a Doubly Linked List
    node1->next = node2;
    node2->prev = node1;
    node2->next = node3;
    node3->prev = node2;

    // Traversing and printing the linked list in both directions
    Node<int>* forward = node1;
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

## Insertion and Deletion in Doubly Linked Lists:

Doubly Linked Lists allow for efficient insertion and deletion operations, especially when working with both forward and backward traversal.

## Insertion at the Beginning:-

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
    while (forward != nullptr) {
        std::cout << forward->data << " ";
        forward = forward->next;
    }
    // Outputs: 1 2 3

    return 0;
}
```

## Deletion at a Given Position:-

```
#include <iostream>

template <typename T>
void deleteAtPosition(Node<T>*& head, int position) {
    if (head == nullptr) {
        return; // No nodes to delete
    }

    Node<T>* current = head;
    for (int i = 0; i < position && current != nullptr; ++i) {
        current = current->next;
    }

    if (current == nullptr) {
        return; // Invalid position
    }

    if (current->prev != nullptr) {
        current->prev->next = current->next;
    } else {
        head = current->next;
    }

    if (current->next != nullptr) {
        current->next->prev = current->prev;
    }

    delete current;
}

int main() {
    Node<int>* head = nullptr;

    // Inserting nodes
    insertAtBeginning(head, 3);
```
