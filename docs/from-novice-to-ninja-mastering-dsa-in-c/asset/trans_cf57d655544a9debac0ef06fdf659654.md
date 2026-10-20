
```cpp
insertAtBeginning(head, 2);
insertAtBeginning(head, 1);

// Deleting a node at position 1
deleteAtPosition(head, 1);

// Traversing and printing the modified linked list
Node<int>* forward = head;
while (forward != nullptr) {
    std::cout << forward->data << " ";
    forward = forward->next;
}
// Outputs: 1 3

return 0;
}
```

## 在双向链表中搜索和遍历：

在双向链表中搜索可以在正向和反向两个方向进行，提供遍历的灵活性。

### 搜索元素

```cpp
#include <iostream>

template <typename T>
bool searchElement(const Node<T>* head, const T& target) {
    const Node<T>* forward = head;
    while (forward != nullptr) {
        if (forward->data == target) {
            return true;  // Element found
        }
        forward = forward->next;
    }
    return false;  // Element not found
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

### 结论

双向链表通过在节点之间提供双向链接增强了链表的功能，允许在两个方向上高效遍历。它们在插入、删除和搜索方面的灵活性使其适用于需要双向导航和修改的场景。随着我们继续本章，我们将探索循环链表，并了解它们如何在链表结构中引入循环关系。

## 循环链表：拥抱无限循环

循环链表通过允许最后一个节点指向第一个节点来扩展链表的概念，形成循环结构。这种循环排列在某些场景下提供优势，并在遍历和操作中引入独特的挑战。

### 循环链表的基本结构

在循环链表中，最后一个节点指向第一个节点，形成一个环。

```cpp
#include <iostream>

// Node structure for a Circular Linked List
template <typename T>
struct Node {
    T data;
    Node* next;

    Node(const T& value) : data(value), next(nullptr) {}
};
```

```cpp
Node<int>* head = nullptr;

// Inserting nodes at the beginning
insertAtBeginning(head, 3);
insertAtBeginning(head, 2);
insertAtBeginning(head, 1);

// Traversing and printing the modified circular linked list
Node<int>* current = head;
for (int i = 0; i < 5; ++i) {
    std::cout << current->data << " ";
    current = current->next;
}
// Outputs: 1 2 3 1 2

return 0;
}
```

### 在给定位置删除

```cpp
#include <iostream>

template <typename T>
void deleteAtPosition(Node<T>*& head, int position) {
    if (head == nullptr) {
        return; // No nodes to delete
    }

    Node<T>* current = head;
    for (int i = 0; i < position - 1 && current->next != head; ++i) {
        current = current->next;
    }

    if (current->next == head || position < 0) {
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

    // Traversing and printing the modified circular linked list
    Node<int>* current = head;
    for (int i = 0; i < 4; ++i) {
        std::cout << current->data << " ";
        current = current->next;
    }
    // Outputs: 1 3 1 2

    return 0;
}
```

### 📚 **算法中的循环链表：**

循环链表在循环关系有益的算法中找到应用，例如在调度和循环缓冲区中。

### 📚 **结论：**

循环链表引入循环结构，允许最后一个节点指向第一个节点。这种循环排列在特定场景下提供优势，并且在插入和删除操作中需要仔细处理指针。随着我们继续本章，我们将探索数组和链表在算法中的集成，结合两种数据结构的优势来解决各种计算挑战。

## 在算法中结合数组和链表：实现最优解

在算法中结合数组和链表提供了一种强大的问题解决方法，利用两种数据结构的优势。这种协同作用允许高效处理动态数据、内存分配的灵活性以及对各种计算挑战的最优解决方案。

### 动态数据管理

数组和链表在管理动态数据时互为补充。数组提供常数时间随机访问，而链表则促进动态内存分配以及轻松的插入和删除。

### 示例：使用链表实现栈

```cpp
#include <iostream>

// Node structure for a linked list
template <typename T>
struct Node {
    T data;
    Node* next;

    Node(const T& value) : data(value), next(nullptr) {}
};

// Stack implemented with a linked list
template <typename T>
class Stack {
private:
    Node<T>* top;

public:
    Stack() : top(nullptr) {}

    // Push operation
    void push(const T& value) {
        Node<T>* newNode = new Node<T>(value);
        newNode->next = top;
        top = newNode;
    }

    // Pop operation
    void pop() {
        if (top != nullptr) {
            Node<T>* temp = top;
            top = top->next;
            delete temp;
        }
    }

    // Display the stack
    void display() const {
        Node<T>* current = top;
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    // Using a stack implemented with a linked list
    Stack<int> stack;

    stack.push(3);
    stack.push(7);
    stack.push(1);

    stack.display();  // Outputs: 1 7 3

    stack.pop();

    stack.display();  // Outputs: 7 3

    return 0;
}
```

### 算法效率

算法通常受益于数组和链表的结合以实现最优效率。数组提供对元素的常数时间访问，使其适合搜索和排序等任务。另一方面，链表在动态场景中表现出色，允许轻松插入和删除。

### 示例：使用数组的归并排序

```cpp
#include <iostream>
#include <vector>

// Merge function for merging two sorted arrays
template <typename T>
void merge(std::vector<T>& arr, int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;

    // Create temporary arrays
    std::vector<T> L(n1), R(n2);

    // Copy data to temporary arrays L[] and R[]
    for (int i = 0; i < n1; i++) {
        L[i] = arr[left + i];
    }

    // Merge the temporary arrays back into arr[left..right]
    int i = 0, j = 0, k = left;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k++] = L[i++];
        } else {
            arr[k++] = R[j++];
        }
    }

    // Copy the remaining elements of L[], if there are any
    while (i < n1) {
        arr[k++] = L[i++];
    }

    // Copy the remaining elements of R[], if there are any
    while (j < n2) {
        arr[k++] = R[j++];
    }
}

// Recursive function to perform merge sort on the array
template <typename T>
void mergeSort(std::vector<T>& arr, int left, int right) {
    if (left < right) {
        // Same as (left+right)/2, but avoids overflow
        int mid = left + (right - left) / 2;
        // Recursive calls to split the array into halves
    }
}
```
