
保存源文件，并使用你的 C++ 编译器编译它。如果使用命令行，请进入包含源文件的目录并运行以下命令：

```
g++ -o basic_calculator basic_calculator.cpp
```

然后运行编译后的可执行文件：

```
./basic_calculator
```

### 第 10 步：输入和输出

在提示时输入两个数字，观察程序显示这两个数字的和、差、积和商。

恭喜！你已成功创建了一个基础 C++ 程序，它可对用户输入的数字执行算术运算。

```
#include <iostream>
#include "student.h" // Include the header file

void Student::SetDetails(std::string n, int a, char g) {
    name = n;
    age = a;
    grade = g;
}

void Student::DisplayDetails() {
    std::cout << "Name: " << name << std::endl;
    std::cout << "Age: " << age << std::endl;
    std::cout << "Grade: " << grade << std::endl;
}
```

### 第 5 步：创建主程序

在另一个源文件（例如 `main.cpp`）中，包含 `Student` 类的头文件，并创建一个 `main` 函数来测试该类：

```
#include <iostream>
#include "student.h" // Include the header file

int main() {
    Student student1; // Create an instance of Student

    // Set details using the SetDetails method
    student1.SetDetails("Alice", 18, 'A');

    // Display the details using the DisplayDetails method
    std::cout << "Student Details:" << std::endl;
    student1.DisplayDetails();

    return 0;
}
```

### 第 6 步：编译并运行

你应该会看到程序输出学生的详细信息：

```
Student Details:
Name: Alice
Age: 18
Grade: A
```

恭喜！你已成功使用 C++ 中的面向对象编程实现了 `Student` 类，该类包含用于设置和显示学生详细信息的方法。

## 练习 3：文件处理

编写一个程序，从包含数字列表的文本文件中读取数据，并计算它们的平均值。

### 第 1 步：设置你的开发环境

确保你的计算机上已安装 C++ 编译器，以及文本编辑器或集成开发环境（IDE）。

### 第 2 步：创建新的 C++ 源文件

打开你首选的文本编辑器或 IDE，并创建一个新的 C++ 源文件。
将文件保存为 `.cpp` 扩展名，例如 `average_calculator.cpp`。

### 第 3 步：包含必要的头文件

包含用于输入和输出操作的必要头文件：

```
#include <iostream>
#include <fstream> // For file handling
```

### 第 4 步：创建主程序

编写 `main` 函数，从文本文件读取数据并计算平均值：

```
int main() {
    std::ifstream inputFile("numbers.txt"); // Open the file
    double sum = 0.0;
    int count = 0;
    double number;

    if (!inputFile) {
        std::cerr << "Error opening file." << std::endl;
        return 1;
    }

    while (inputFile >> number) {
        sum += number;
        count++;
    }

    inputFile.close(); // Close the file

    if (count > 0) {
        double average = sum / count;
        std::cout << "Average: " << average << std::endl;
    } else {
        std::cout << "No numbers found in the file." << std::endl;
    }

    return 0;
}
```

### 第 5 步：准备输入文件

在与源文件相同的目录中创建一个名为 `numbers.txt` 的文本文件。用数字列表填充该文件，每行一个数字。

例如：

```
10.5
20.7
15.0
```

### 第 6 步：编译并运行

使用 C++ 编译器编译你的源文件。如果使用命令行，请进入包含源文件的目录并运行以下命令：

```
g++ -o average_calculator average_calculator.cpp
```

然后运行编译后的可执行文件：

```
./average_calculator
```

### 第 7 步：观察输出

你应该会看到程序根据 `numbers.txt` 文件中的数字输出计算出的平均值。

恭喜！你已成功创建了一个 C++ 程序，它从文本文件读取数据并计算这些数字的平均值。

## 练习 4：模板与函数

实现一个泛型函数模板，用于查找任意数据类型数组中的最大元素。

### 第 1 步：设置你的开发环境

确保你的计算机上已安装 C++ 编译器，以及文本编辑器或集成开发环境（IDE）。

### 第 2 步：创建新的 C++ 源文件

打开你首选的文本编辑器或 IDE，并创建一个新的 C++ 源文件。
将文件保存为 `.cpp` 扩展名，例如 `max_finder.cpp`。

### 第 3 步：定义泛型函数模板

定义一个泛型函数模板，它接受数组及其大小作为参数，并返回最大元素：

```cpp
template <typename T>
T FindMax(const T arr[], int size) {
    T maxElement = arr[0];
    for (int i = 1; i < size; ++i) {
        if (arr[i] > maxElement) {
            maxElement = arr[i];
        }
    }
    return maxElement;
}
```

### 第 4 步：创建主程序

编写 `main` 函数来测试 `FindMax` 函数模板：

```
int main() {
    int intArray[] = {10, 3, 27, 5, 14};
    double doubleArray[] = {3.14, 1.618, 2.718, 0.577};

    int intMax = FindMax(intArray, 5);
    double doubleMax = FindMax(doubleArray, 4);

    std::cout << "Max integer: " << intMax << std::endl;
    std::cout << "Max double: " << doubleMax << std::endl;

    return 0;
}
```

### 第 5 步：编译并运行

使用 C++ 编译器编译你的源文件。如果使用命令行，请进入包含源文件的目录并运行以下命令：

```
g++ -o max_finder max_finder.cpp
```

然后运行编译后的可执行文件：

```
./max_finder
```

### 第 6 步：观察输出

你应该会看到程序输出数组中的最大整数值和最大双精度浮点值。

恭喜！你已成功创建了一个 C++ 程序，它实现了泛型函数模板，用于查找任意数据类型数组中的最大元素。

## 练习 5：异常处理

编写一个程序，接受用户输入以进行两个数字的除法，并处理除零和无效输入的异常。

### 第 1 步：设置你的开发环境

确保你的计算机上已安装 C++ 编译器，以及文本编辑器或集成开发环境（IDE）。

### 第 2 步：创建新的 C++ 源文件

打开你首选的文本编辑器或 IDE，并创建一个新的 C++ 源文件。
将文件保存为 `.cpp` 扩展名，例如 `divide_numbers.cpp`。

### 第 3 步：包含必要的头文件

包含用于输入和输出操作的必要头文件：

```cpp
#include <iostream>
```

### 第 4 步：创建主程序

编写 `main` 函数，接受用户输入以进行两个数字的除法并处理异常：

```cpp
int main() {
    double numerator, denominator;
    try {
        std::cout << "Enter numerator: ";
        std::cin >> numerator;
        std::cout << "Enter denominator: ";
        std::cin >> denominator;
        if (denominator == 0) {
            throw std::runtime_error("Division by zero is not allowed.");
        }
        double result = numerator / denominator;
        std::cout << "Result: " << result << std::endl;
    } catch (const std::exception& e) {
        std::cerr << "Exception: " << e.what() << std::endl;
    }
    return 0;
}
```

### 第 5 步：编译并运行

使用 C++ 编译器编译你的源文件。如果使用命令行，请进入包含源文件的目录并运行以下命令：

```
g++ -o divide_numbers divide_numbers.cpp
```

然后运行编译后的可执行文件：

```
./divide_numbers
```

### 第 6 步：测试异常处理

为分子和分母输入各种值，包括分母为零的情况。观察程序如何处理除零和无效输入的异常。

恭喜！你已成功创建了一个 C++ 程序，它接受用户输入以进行两个数字的除法，并处理各种场景下的异常。

## 练习 6：链表实现

在 C++ 中实现一个单链表数据结构。创建用于插入、删除和显示链表中元素的方法。

以下是创建 C++ 程序的分步指南，该程序实现一个单链表数据结构，并包含插入、删除和显示元素的方法：

### 第 1 步：设置你的开发环境

确保你的计算机上已安装 C++ 编译器，以及文本编辑器或集成开发环境（IDE）。

### 第 2 步：创建新的 C++ 源文件

打开你首选的文本编辑器或 IDE，并创建一个新的 C++ 源文件。
将文件保存为 `.cpp` 扩展名，例如 `linked_list.cpp`。

### 第 3 步：定义节点结构

定义链表节点的结构：

```cpp
struct Node {
    int data;
    Node* next;
};
```

### 第 4 步：创建 LinkedList 类

创建链表类，包含插入、删除和显示元素的方法：
