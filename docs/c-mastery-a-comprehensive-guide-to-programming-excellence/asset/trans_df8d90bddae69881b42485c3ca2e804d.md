

```cpp
// 计算区域的技巧（虚拟能力）

virtual double calculateArea() = 0; // 纯粹的虚拟能力

};
```

```cpp
// 派生类
class Circle : public Shape {
private:
    double radius;

public:
    // 构造函数
    Circle(double r) : radius(r) {}

    // 计算区域的方法（执行）
    double calculateArea() override {
        return 3.14 * radius * radius;
    }
};
```

在这个模型中，Shape 是基类，Circle 是继承自 Shape 的派生类。`calculateArea()` 技巧在基类中被声明为一种纯粹的虚拟能力，并在派生类中被重写。

# 多态

多态允许将各种类的对象被视为典型基类的对象。这赋予了你编写可以处理不同类型对象代码的能力，而无需了解它们的具体类类型。

# cpp

```cpp
// 确定形状绝对面积的能力
double totalArea(Shape shapes[], int count) {
    double aggregate = 0.0;
    for (int i = 0; i < count; ++i) {
        aggregate += shapes[i]->calculateArea();
    }
    return aggregate;
}
```

在这个模型中，`totalArea()` 能力接收各种 Shape 指针并计算总面积，无论它们的具体类型是什么，一切都是等等的。

# 构造函数与析构函数

构造函数是在对象创建时被调用的特殊成员函数。它们用于实例化对象的状态。而析构函数在对象销毁时被调用，用于释放资源或执行清理任务。

```cpp
class MyClass {
public:
    // 构造函数
    MyClass() {
        std::cout << "Constructor called" << std::endl;
    }

    // 析构函数
    ~MyClass() {
        std::cout << "Destructor called" << std::endl;
    }
};
```

在这个模型中，当创建 MyClass 对象时，构造函数会打印一条消息；当项被销毁时，析构函数会打印一条消息。

# 结束

在本节中，你了解了 C++ 面对象编程 (OOP) 中的高级思想，包括继承、多态、构造函数和析构函数。这些元素赋予了你编写更严谨、可扩展且可行代码的能力。在后续部分，我们将研究 C++ 中处理记录的操作，允许你从外部文档读取并与其进行交互。

# 第 10 节：处理记录

在本节中，我们将研究如何在 C++ 中处理记录。文件输入/输出任务允许你从外部文档读取信息并向其写入信息，使你的项目能够与持久化存储进行通信。

# 从记录读取

要在 C++ 中从记录中读取信息，你需要执行以下步骤：

- 使用输入文件流 (ifstream) 打开记录。
- 从文档中读取信息。
- 关闭文档。

这是一个从文本文档中读取信息的实例：

```cpp
#include <iostream>
#include <fstream>
#include <string>

int main() {
    std::ifstream inputFile("input.txt"); // 打开文档

    if (inputFile.is_open()) { // 检查假设记录已打开
        std::string line;

        while (std::getline(inputFile, line)) { // 从文档读取每行
            std::cout << line << std::endl; // 打印该行
        }
        inputFile.close(); // 关闭记录
    } else {
        std::cerr << "Unable to open document!" << std::endl; // 如果记录无法打开则打印错误消息
    }

    return 0;
}
```

在这个模型中，我们利用输入记录流打开了一个名为 "input.txt" 的文档。然后，我们利用 `std::getline()` 从记录中读取每行，并将其打印到控制中心。最后，我们利用 `close()` 技巧关闭记录。

# 向文档写入

要在 C++ 中向记录中写入信息，你确实需要执行以下步骤：

- 使用结果记录流 (ofstream) 打开文档。
- 向文档中写入信息。
- 关闭记录。

这是一个向文本记录中组合信息的实例：

```cpp
#include <iostream>
#include <fstream>

int main() {
  std::ofstream outputFile("output.txt"); // 打开文档

  if (outputFile.is_open()) { // 检查假设记录已打开
    outputFile << "Hi, world!" << std::endl; // 向文档写入信息
    outputFile.close(); // 关闭文档

    std::cout << "Information written to record effectively." << std::endl;
  } else {
    std::cerr << "Unable to open document!" << std::endl; // 如果记录无法打开则打印错误消息
  }

  return 0;
}
```

在这个模型中，我们利用结果记录流打开了一个名为 "output.txt" 的文档。然后，我们在此处利用插入运算符 << 向文档写入 "Hi, world!"。最后，我们利用 `close()` 技巧关闭记录。

# 结束

在本节中，你学会了如何在 C++ 中处理记录，包括从外部文档读取和向其写入信息。文件输入/输出任务对于处理确定数据和外部交互至关重要。在接下来的章节，我们将研究 C++ 中的排查和调试方法，帮助你修复代码错误。

# 第 11 节：排查与调试

在本节中，我们将深入研究 C++ 中的排查和调试策略。排查是识别和修复代码错误（bug）的最常见方法，而调试包含了诊断并解决可能出现的问题。

# 错误及其修复方法

理解 C++ 中的常见错误可以帮助你更有效地分析和修复错误。一些常见错误包括：

- 语法错误：当代码违反 C++ 规则时发生。示例包括缺少分号、括号不匹配和拼写错误。编译器通常会指出这些符号错误并提供错误消息。

- 逻辑错误：当代码由于逻辑缺陷产生错误结果时发生。排查逻辑错误通常包括使用打印语句、调试设备以及逐行检查代码以识别逻辑缺陷。

- 运行时错误：当程序在执行期间遇到错误时发生，例如除以零或访问越界数组元素。运行时错误可能难以排查，因为它们并不总是发生。利用调试工具或添加错误检查代码可以帮助修复运行时错误。

# 排查策略

以下是你有效排查 C++ 程序的一些策略：

- 打印语句：在代码中嵌入打印语句以显示因子值或执行过程，可以帮你了解程序各个位置的情况。

- 排查工具：集成开发环境 (IDE) 如 Visual Studio、Code::Blocks 或 CLion 提供了内置调查工具，允许你设置断点、评估因子并逐行执行代码。

- 编译器警告：关注编译器警告，因为它们经常会显示代码中可能导致运行时错误的预期问题。

- 代码审查：让他人审核你的代码可以提供新的视角，并协助识别你可能忽略的错误或改进区域。

# 结束

