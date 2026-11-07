
栈容器是 STL 的基本组成部分，模拟后进先出（LIFO）行为。在本示例中，创建并操作了一个整数栈。push 操作将元素添加到栈顶，pop 操作从栈顶移除元素。栈的简单性和高效性使其成为在各种场景中管理数据的宝贵工具。

```cpp
// Example: Using STL queue for managing a queue of strings
#include <iostream>
#include <queue>

int main() {
    // Creating a queue of strings
    std::queue<std::string> stringQueue;

    // Enqueuing elements into the queue
    stringQueue.push("apple");
    stringQueue.push("banana");
    stringQueue.push("orange");

    // Dequeuing elements from the queue
    while (!stringQueue.empty()) {
        std::cout << stringQueue.front() << " ";
        stringQueue.pop();
    }

    return 0;
}
```

## STL 队列：精通先进先出（FIFO）

队列容器体现了先进先出（FIFO）原则，在必须按顺序处理数据的场景中非常有用。本代码片段演示了如何使用 STL 队列管理字符串集合。push 操作将元素添加到队列尾部，pop 操作从队列前端移除元素。

```cpp
// Example: Using STL priority_queue for managing priorities of tasks
#include <iostream>
#include <queue>

int main() {
    // Creating a priority queue of integers
    std::priority_queue<int> priorityQueue;

    // Enqueuing elements into the priority queue
    priorityQueue.push(30);
    priorityQueue.push(10);
    priorityQueue.push(20);

    // Dequeuing elements from the priority queue
    while (!priorityQueue.empty()) {
        std::cout << priorityQueue.top() << " ";
        priorityQueue.pop();
    }

    return 0;
}
```

## STL 优先队列：轻松实现优先级

优先队列是队列概念的扩展，具有根据特定条件对元素进行优先级排序的内在能力。在本示例中，管理了一个整数优先队列。最高优先级的元素始终位于前端，这使其成为需要按优先级级别执行任务场景的理想选择。

理解这些 STL 容器——栈、队列和优先队列——为 C++ 开发者提供了用于管理各种数据结构和场景的丰富工具包。利用这些容器，程序员能够编写更简洁、更高效、更具表现力的代码，这与现代 C++ 编程实践的理念相一致。

## STL 映射与集合

标准模板库（STL）模块的第 2 部分将深入探索关联容器的多用途世界，即映射和集合；它们分别提供了高效且灵活的机制来管理键值对和唯一元素。本节探讨它们的应用、优势以及实现细节，突出它们为 C++ 编程带来的优雅。

```cpp
// Example: Using STL map for associating names with ages
#include <iostream>
#include <map>

int main() {
    // Creating a map to associate names with ages
    std::map<std::string, int> ageMap;

    // Adding entries to the map
    ageMap["Alice"] = 25;
    ageMap["Bob"] = 30;
    ageMap["Charlie"] = 22;

    // Accessing and displaying values from the map
    std::cout << "Age of Alice: " << ageMap["Alice"] << std::endl;
    std::cout << "Age of Bob: " << ageMap["Bob"] << std::endl;

    return 0;
}
```

### STL 映射：揭开键值对的魔力

STL 中的映射容器体现了关联性的强大之处，允许开发者将键与对应的值关联起来。本示例展示了一个将姓名与年龄关联起来的映射。下标（[]）运算符便于使用键来访问和操作值，为需要高效查找的场景提供了一种优雅的解决方案。

```cpp
// Example: Using STL set for managing unique elements
#include <iostream>
#include <set>

int main() {
    // Creating a set of integers
    std::set<int> uniqueNumbers;

    // Inserting unique elements into the set
    uniqueNumbers.insert(10);
    uniqueNumbers.insert(20);
    uniqueNumbers.insert(10);  // Ignored, as 10 is already in the set

    // Displaying unique elements from the set
    for (const auto& number : uniqueNumbers) {
        std::cout << number << " ";
    }

    return 0;
}
```

### STL 集合：构建不重复集合

STL 中的集合容器印证了对包含唯一元素的集合的需求。本代码片段演示了创建一个整数集合，确保只存储不同的值。重复值的插入会被妥善处理，凸显了集合在高效维护不同元素方面的作用。

理解 STL 映射和集合的复杂细节，为 C++ 开发者提供了管理关联关系和唯一集合的强大工具。这些容器的表现力与现代 C++ 编程原则无缝契合，有助于编写更简洁、更可读、更高效的代码。利用这些特性，程序员能够娴熟地驾驭复杂数据结构，释放 C++ 语言的全部潜力。

## 函数对象（仿函数）简介

标准模板库（STL）的第 2 部分深入探讨函数对象（通常称为仿函数）领域，提供了一种多用途且富有表现力的方法来增强算法功能。本节对仿函数进行了深入探索，阐明其定义、用例，以及它们如何促进 C++ 编程的灵活性和可扩展性。

```cpp
// Example: Creating a Functor for Multiplication
#include <iostream>

// Functor class for multiplication
class Multiplier {
public:
    // Overloaded function call operator
    int operator()(int x, int y) const {
        return x * y;
    }
};

int main() {
    // Creating an instance of the Multiplier functor
    Multiplier multiply;

    // Using the functor to perform multiplication
    int result = multiply(5, 3);

    // Displaying the result
    std::cout << "Multiplication result: " << result << std::endl;

    return 0;
}
```

### 仿函数揭秘：一个乘法示例

从本质上讲，仿函数是行为类似函数的对象。本示例展示了创建一个名为 Multiplier 的仿函数，它能够将两个整数相乘。其魔力在于重载函数调用运算符（operator()），将仿函数的实例转变为可调用实体。这为 C++ 带来了更浓厚的面向对象色彩，使函数能够封装在类中。

```cpp
// Example: Using Functor with STL Algorithm
#include <iostream>
#include <vector>
#include <algorithm>

// Functor class for checking if a number is even
class IsEven {
public:
    // Overloaded function call operator
    bool operator()(int number) const {
        return number % 2 == 0;
    }
};

int main() {
    // Creating a vector of integers
    std::vector<int> numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

    // Creating an instance of the IsEven functor
    IsEven isEven;

    // Using the functor with STL count_if algorithm
    int evenCount = std::count_if(numbers.begin(), numbers.end(), isEven);

    // Displaying the count of even numbers
    std::cout << "Count of even numbers: " << evenCount << std::endl;

    return 0;
}
```

### 仿函数实战：增强 STL 算法

仿函数可与 STL 算法无缝集成，提升其功能。本代码片段展示了创建一个 IsEven 仿函数来检查数字是否为偶数。随后将该仿函数与 std::count_if 算法一起使用，演示如何利用仿函数自定义算法行为，为 C++ 开发者提供强大工具。

理解仿函数为 C++ 中更具表现力和面向对象的编程风格打开了大门。无论是将特定行为封装在类中，还是增强 STL 算法的能力，仿函数都能让开发者编写简洁、可复用且可扩展的代码。

## 在实际应用中使用 STL

在标准模板库（STL）的第二部分中，重点转向 STL 组件在真实场景中的实际应用。本节探讨 STL 如何凭借其丰富的算法、容器和实用工具集合，显著简化健壮且高效的 C++ 程序开发。

```cpp
// Example: Applying STL Algorithms to a Real-world Problem
#include <iostream>
#include <vector>
#include <algorithm>

// Data structure representing a book
struct Book {
    std::string title;
    std::string author;
    int year;
};

int main() {
    // Creating a vector of Book objects
    std::vector<Book> library = {
        {"The Catcher in the Rye", "J.D. Salinger", 1951},
        {"To Kill a Mockingbird", "Harper Lee", 1960},
        {"1984", "George Orwell", 1949},
        // ... additional books
    };

    // Sorting the library by publication year using STL sort algorithm
    std::sort(library.begin(), library.end(), [](const Book& a, const Book& b) {
        return a.year < b.year;
    });

    // Displaying the sorted library
    std::cout << "Sorted Library by Publication Year:" << std::endl;
    for (const auto& book : library) {
        std::cout << book.title << " by " << book.author << " (" << book.year << ")" <<
            std::endl;
    }

    return 0;
}
```

