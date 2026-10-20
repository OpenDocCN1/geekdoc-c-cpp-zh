

```
template <typename T>
struct Node {
    T data;
    Node* next;

    Node(const T& value) : data(value), next(nullptr) {}
};

// Queue implemented with a linked list
template <typename T>
class Queue {
private:
    Node<T>* front;
    Node<T>* rear;

public:
    Queue() : front(nullptr), rear(nullptr) {}

    // Enqueue operation
    void enqueue(const T& value) {
        Node<T>* newNode = new Node<T>(value);
        if (rear == nullptr) {
            front = rear = newNode;
        } else {
            rear->next = newNode;
            rear = newNode;
        }
    }

    // Dequeue operation
    void dequeue() {
        if (front != nullptr) {
            Node<T>* temp = front;
            front = front->next;
            if (front == nullptr) {
                rear = nullptr;  // Queue is empty after dequeue
            }
            delete temp;
        }
    }

    // Display the queue
    void display() const {
        Node<T>* current = front;
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }
};

int main() {

    // Using a queue implemented with a linked list
    Queue<int> myQueue;

    myQueue.enqueue(3);
    myQueue.enqueue(7);
    myQueue.enqueue(1);

    myQueue.display();  // Outputs: 3 7 1

    myQueue.dequeue();

    myQueue.display();  // Outputs: 7 1

    return 0;
}
```

## 结论

实现队列和双端队列提供了对其机制和灵活性的实践理解。无论是队列中遵循 FIFO 原则，还是探索双端队列的增强功能，这些数据结构在算法设计、问题解决和实际应用中都发挥着关键作用。随着我们继续本章，我们将深入探讨使用栈和队列解决问题的过程，并探索诸如优先队列等高级主题。

```
    std::cout << "Expression 1 is "
              << (isValidParentheses(expression1) ? "valid." : "not valid.")
              << std::endl;
    std::cout << "Expression 2 is "
              << (isValidParentheses(expression2) ? "valid." : "not valid.")
              << std::endl;
    return 0;
}
```

## 使用队列解决问题

现在我们将使用队列解决一个问题。

### 问题：实现 BFS 算法

队列在广度优先搜索 BFS 算法中起着至关重要的作用。在 BFS 中，节点按层级顺序探索，队列用于维护探索顺序。

```
#include <iostream>
#include <queue>
#include <vector>

// Adjacency list representation of a graph
std::vector<std::vector<int>> graph = {
    {1, 2},
    {0, 3, 4},
    {0, 4},
    {1},
    {1, 2}
};

void bfs(int startNode) {
    std::vector<bool> visited(graph.size(), false);
    std::queue<int> nodeQueue;

    visited[startNode] = true;
    nodeQueue.push(startNode);

    while (!nodeQueue.empty()) {
        int currentNode = nodeQueue.front();
        nodeQueue.pop();

        std::cout << currentNode << " ";

        for (int neighbor : graph[currentNode]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                nodeQueue.push(neighbor);
            }
        }
    }
}

int main() {
    // Performing BFS starting from node 0
    std::cout << "BFS starting from node 0: ";
    bfs(0);
    std::cout << std::endl;

    return 0;
}
```

## 结合栈和队列解决复杂问题

现在我们将结合栈和队列一起解决一个问题。

### 问题：求值后缀表达式

结合栈和队列可以有效地解决更复杂的问题。例如，在求值后缀表达式时，可以使用栈来跟踪操作数，队列可以帮助管理操作序列。

```
#include <iostream>
#include <stack>
#include <queue>
#include <sstream>

int evaluatePostfix(const std::string& expression) {
    std::stack<int> operandStack;
    std::istringstream iss(expression);
    std::string token;

    while (iss >> token) {
        if (isdigit(token[0])) {
            operandStack.push(std::stoi(token));
        } else {
            int operand2 = operandStack.top();
            operandStack.pop();

            int operand1 = operandStack.top();
            operandStack.pop();

            switch (token[0]) {
                case '+':
                    operandStack.push(operand1 + operand2);
                    break;
                case '-':
                    operandStack.push(operand1 - operand2);
                    break;
                case '*':
                    operandStack.push(operand1 * operand2);
                    break;
                case '/':
                    operandStack.push(operand1 / operand2);
                    break;
                default:
                    std::cerr << "Invalid operator: " << token << std::endl;
                    return -1;  // Error
            }
        }
    }

    return operandStack.top();
}

int main() {
    // Evaluating a postfix expression
    std::string postfixExpression = "3 4 + 2 *";
    std::cout << "Result: " << evaluatePostfix(postfixExpression) << std::endl;

    return 0;
}
```

## 结论

使用栈和队列解决问题展示了这些数据结构在算法设计中的多功能性。无论是确保括号匹配、实现图算法，还是处理复杂的算术表达式，栈和队列都提供了优雅而高效的解决方案。随着我们继续本章，我们将探索高级主题，包括优先队列和双端队列，以进一步增强我们的解决问题工具箱。

## 高级主题：优先队列和双端队列

在本节中，我们探索栈和队列领域内的高级主题，特别关注优先队列和双端队列 deque。

优先队列是一种队列，其中元素被分配优先级，并且具有最高或最低优先级的元素会在其他元素之前被服务。这种排序在需要根据重要性处理任务或事件的场景中至关重要。

优先队列的常见实现是使用堆，特别是二叉堆。二叉堆提供高效的最高或最低优先级元素的插入和提取。

```
#include <iostream>
#include <vector>
#include <algorithm>

template <typename T>
class MaxHeap {
private:
    std::vector<T> heap;

    void heapifyUp(int index) {
        while (index > 0) {
            int parentIndex = (index - 1) / 2;
            if (heap[index] > heap[parentIndex]) {
                std::swap(heap[index], heap[parentIndex]);
                index = parentIndex;
            } else {
                break;
            }
        }
    }

    void heapifyDown(int index) {
        int leftChild = 2 * index + 1;
        int rightChild = 2 * index + 2;
        int largest = index;

        if (leftChild < heap.size() && heap[leftChild] > heap[largest]) {
            largest = leftChild;
        }

        if (rightChild < heap.size() && heap[rightChild] > heap[largest]) {
            largest = rightChild;
        }

        if (largest != index) {
            std::swap(heap[index], heap[largest]);
            heapifyDown(largest);
        }
    }

public:
    void insert(T value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    T extractMax() {
        if (heap.empty()) {
            throw std::out_of_range("Heap is empty");
        }

        T max = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);

        return max;
    }

    bool isEmpty() const {
        return heap.empty();
    }
};

int main() {
    // Using a max heap as a priority queue
    MaxHeap<int> priorityQueue;
    priorityQueue.insert(20);
    priorityQueue.insert(10);
    priorityQueue.insert(30);

    while (!priorityQueue.isEmpty()) {
        std::cout << priorityQueue.extractMax() << " ";
    }

    return 0;
}
```

### 双端队列 Deques：具有两端的通用队列

双端队列，或 deque，是允许从前端和后端插入和删除元素的队列。这种灵活性使 deque 适用于各种场景，包括算法中滑动窗口的管理。

deque 可以使用数组或链表实现，具体取决于问题的特定要求。

### 示例：使用链表的 Deque 实现

```
#include <iostream>

template <typename T>
struct Node {
    T data;
    Node* next;
    Node* prev;
    Node(const T& value) : data(value), next(nullptr), prev(nullptr) {};
};

template <typename T>
class Deque {
private:
    Node<T>* front;
    Node<T>* rear;

public:
    Deque() : front(nullptr), rear(nullptr) {}
};
```
