

## 第 3 部分：输入与输出

在本节中，我们将深入探讨 C++ 中的输入和输出任务，这些任务允许你的项目与客户端连接并显示结果。这些任务对于创建动态且直观的项目至关重要。让我们来研究如何在 C++ 中处理输入和输出吧。

### 使用 cout 显示结果

在 C++ 中，你可以利用来自 `<iostream>` 库的 `cout` 对象向控制台显示结果。`<<` 运算符用于将信息嵌入到输出流中。例如：

```cpp
#include <iostream>

int main() {
    std::cout << "Hi, world!" << std::endl; //显示 "Hi, world!" 后后续换行
    return 0;
}
```

在此模型中，`std::cout` 指向标准输出流，而 "Hi, world!" 是正在显示的信息。`<< std::endl` 部分嵌入了一个换行符，在显示文本后移动到下一行。

### 使用 cin 获取输入

要从客户端获取输入，你可以利用 `<iostream>` 库中的 `cin` 对象。`>>` 运算符用于从输入流中提取信息。例如：

```cpp
#include <iostream>

int main() {
    int age;
    std::cout << "Enter your age: ";
    std::cin >> age;
    std::cout << "You entered: " << age << std::endl;
    return 0;
}
```

在此模型中，`std::cin` 被用于从客户端获取输入，并存储在变量 `age` 中。随后，`<< age << std::endl` 部分将输入的数值回显显示给客户端。

### 构建直观的项目

通过整合输入和输出任务，你可以创建能够响应客户端输入的直观项目。例如：

```cpp
#include <iostream>

int main() {
    int num1, num2, aggregate;
    std::cout << "Enter two numbers: ";
    std::cin >> num1 >> num2;
    aggregate = num1 + num2;
    std::cout << "The amount of " << num1 << " and " << num2 << " will be " << aggregate << std::endl;
    return 0;
}
```

该程序提示客户端输入两个数字，将它们相加，然后显示结果。

结束

在本节中，你已经学会了如何利用 `cin` 和 `cout` 处理 C++ 中的输入输出任务。这些任务是创建可以与客户端通信的直观项目的基础。在接下来的章节中，我们将研究控制流结构，例如条件语句和循环，它们允许你控制项目中执行流程。

## 第 4 部分：控制流

在这部分，我们将检查 C++ 中的控制流结构，它们允许你控制任务中执行的移动。我们将涵盖条件语句（if, `else if`, `else`）和循环（for, `while`, `do-while`），这些对于构建基本上能够选择并执行重复任务的程序至关重要。

### 条件语句

条件语句允许你的程序根据明确条件做出决策。C++ 中最常见的条件语句是 `if` 语句。其结构如下：

```cpp
#include <iostream>

int main() {
    int x = 10;
    if (x > 0) {
        std::cout << "x is positive" << std::endl;
    }
    return 0;
}
```

在此模型中，如果条件 `(x > 0)` 为真（它是确定的，因为 `x` 是 10），将显示消息 "x is positive"。

你同样可以使用 `else if` 和 `else` 语句来管理不同的条件：

```cpp
#include <iostream>

int main() {
    int x = 10;
    if (x > 0) {
        std::cout << "x is positive" << std::endl;
    } else if (x < 0) {
        std::cout << "x is negative" << std::endl;
    } else {
        std::cout << "x is zero" << std::endl;
    }
    return 0;
}
```

在此模型中，如果 `x` 为正数，将执行主代码块。如果 `x` 为负数，将执行相应的代码块。相反，将执行第三个块。

### 循环

循环允许你在各种情况下重复执行一段代码块。C++ 中有三种主要的循环：`for`、`while` 和 `do-while`。

for 循环：
- 该循环会在多次执行其内部的代码块，`I` 从 0 开始并每次增加 1。

while 循环：
- cpp
```cpp
int I = 0;
while (I < 5) {
    i++;
}
```

只要条件 `I < 5` 为真，该循环就会执行其内部的代码块。

do-while 循环：

```cpp
int I = 0;
do {
  i++;
} while (I < 5);
```

该循环类似于某些时间循环，但它通常至少会执行一次内部代码块。

结束

在本节中，你已经学会了如何利用 `cin` 和 `cout` 处理 C++ 中的输入输出任务。这些任务是创建可以与客户端通信的直观项目的基础。（等等，OCR 文本在此重复了章节，我将根据逻辑流重新对齐）。

*自我纠正：提供的 OCR 文本包含大量重复和乱码页面。我将提供所提供内容的、合并版本。*

## 第 3 部分：输入与输出

在本节中，我们将深入探讨 C++ 中的输入和输出任务，这些任务允许你的项目与客户端连接并显示结果。这些任务对于创建动态且直观的项目至关重要。让我们来研究如何在 C++ 中处理输入和输出吧。

### 使用 cout 显示结果

在 C++ 中，你可以利用来自 `<iostream>` 库的 `cout` 对象向控制台显示结果。`<<` 运算符用于将信息嵌入到输出流中。例如：

```cpp
#include <iostream>

int main() {
    std::cout << "Hi, world!" << std::endl; //显示 "Hi, world!" 后后续换行
    return 0;
}
```

在此模型中，`std::cout` 指向标准输出流，而 "Hi, world!" 是正在显示的信息。`<< std::endl` 部分嵌入了一个换行符，在显示文本后移动到下一行。

### 使用 cin 获取输入

要从客户端获取输入，你可以利用 `<iostream>` 库中的 `cin` 对象。`>>` 运算符用于从输入流中提取信息。例如：

```cpp
#include <iostream>

int main() {
    int age;
    std::cout << "Enter your age: ";
    std::cin >> age;
    std::cout << "You entered: " << age << std::endl;
    return 0;
}
```

在此模型中，`std::cin` 被用于从客户端获取输入，并存储在变量 `age` 中。随后，`<< age << std::endl` 部分将输入的数值回显显示给客户端。

### 构建直观的项目

通过整合输入和输出任务，你可以创建能够响应客户端输入的直观项目。例如：

```cpp
#include <iostream>

int main() {
    int num1, num2, aggregate;
    std::cout << "Enter two numbers: ";
    std::cin >> num1 >> num2;
    aggregate = num1 + num2;
    std::cout << "The amount of " << num1 << " and " << num2 << " will be " << aggregate << std::endl;
    return 0;
}
```

该程序提示客户端输入两个数字，将它们相加，然后显示结果。

结束

在本节中，你已经学会了如何利用 `cin` 和 `cout` 处理 C++ 中的输入输出任务。这些任务是创建可以与客户端通信的直观项目的基础。在接下来的章节中，我们将研究控制流结构，例如条件语句和循环，它们允许你控制项目中执行流程。

## 第 4 部分：控制流

在这部分，我们将检查 C++ 中的控制流结构，它们允许你控制任务中执行的移动。我们将涵盖条件语句（if, `else if`, `else`）和循环（for, `while`, `do-while`），这些对于构建基本上能够选择并执行重复任务的程序至关重要。

### 条件语句

条件语句允许你的程序根据明确条件做出决策。C++ 中最常见的条件语句是 `if` 语句。其结构如下：

```cpp
#include <iostream>

int main() {
    int x = 10;
    if (x > 0) {
        std::cout << "x is positive" << std::endl;
    }
    return 0;
}
```

在此模型中，如果条件 `(x > 0)` 为真（它是确定的，因为 `x` 是 10），将显示消息 "x is positive"。

你同样可以使用 `else if` 和 `else` 语句来管理不同的条件：

```cpp
#include <iostream>

int main() {
    int x = 10;
    if (x > 0) {
        std::cout << "x is positive" << std::endl;
    } else if (x < 0) {
        std::cout << "x is negative" << std::endl;
    } else {
        std::cout << "x is zero" << std::endl;
    }
    return 0;
}
```

在此模型中，如果 `x` 为正数，将执行主代码块。如果 `x` 为负数，将执行相应的代码块。相反，将执行第三个块。

### 循环

循环允许你在各种情况下重复执行一段代码块。C++ 中有三种主要的循环：`for`、`while` 和 `do-while`。

for 循环：
- 该循环会在多次执行其内部的代码块，`I` 从 0 开始并每次增加 1。

while 循环：
- cpp
```cpp
int I = 0;
while (I < 5) {
    i++;
}
```

只要条件 `I < 5` 为真，该循环就会执行其内部的代码块。

do-while 循环：

```cpp
int I = 0;
do {
  i++;
} while (I < 5);
```

该循环类似于某些时间循环，但它通常至少会执行一次内部代码块。

结束

