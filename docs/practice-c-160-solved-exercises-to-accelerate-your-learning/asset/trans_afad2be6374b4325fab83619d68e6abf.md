

# 练习 C++
160 道已解练习，加速你的学习
RUHAN CONCEIÇÃO

# 练习 C++
160 道已解练习，加速你的学习

Ruhan Avila da Conceição

## 前言

欢迎阅读本书，书中介绍了许多附带答案和注释的 C++ 练习题。在本书中，你将找到超过 160 道练习题，旨在帮助你提高在这门强大语言中的编程技能。

学习编程不仅涉及理解理论概念，还涉及将这些概念应用于现实场景中。这正是你将在书中发现的内容：从基础性知识到更复杂的挑战的各种问题。

随着练习的进行，你将面临涉及数学公式操作、字符串、条件判断、循环、向量操作、矩阵等更多任务的挑战。

本书的主要目标是为寻求进步的程序员提供一份实用且全面的资源。无论你是一个想要巩固知识的 C++ 初学者，还是希望加深专业知识的经验丰富的程序员，这些练习都将作为极佳的学习指南和参考。这本书也适用于那些希望拥有丰富的编程逻辑练习题集，以便为学生创建题目的老师们。

享受这段学习旅程，深入探索这些带答案和注释的 C++ 练习吧。准备好迎接刺激的挑战、创造性的解决方案，以及提升编程技能的独特机会。

本书的内容创作过程中使用了人工智能工具，但所有材料都经过了作者的审核和编辑，以交付最终的高质量产品。

阅读愉快，学习进步，并在探索 C++ 编程奇妙世界中获得乐趣。

Ruhan Avila da Conceição.

## 目录

- 引言
- 基础练习
- 数学公式
- 条件判断
- 重复循环
- 数组
- 字符串
- 矩阵
- 递归函数
- 正则表达式
- 排序算法
- 练习完整列表
- 额外内容
- 关于作者

## 引言

如果你购买了这本书，说明你想尽快开始编程并接受逻辑挑战，而不想听布教山上的大篇大论。但在开始之前，强调几点是非常重要的。

尽管许多练习可能被认为是简单的，但如果你是这段编程旅程的新手，那么在看答案之前，首先尝试自己解决问题是非常关重要的。同一个问题可能有多种解决方案，你只需要思考并开发出自己的方案。然后，你就可以将其与书中提出的方案进行比较，识别各自的优点，并尝试多学一点。

如果练习太难且你无法解决，请跳到下一个，并在第二天再次尝试。即使无法解决，也不要立即跳到答案，更不要在没有尝试解决的情况下直接看答案。

学习编程逻辑不在于得到答案，而在于你通往答案所经历的历程。

话如此，本书的其余章节将根据建议练习中涵盖的编程主题进行划分。

从现在起，这一切取决于你！

## 基础练习

1. 编写一个程序在屏幕上打印 "Hello World!"。

```cpp
#include <iostream>
```

int main() {
    std::cout << "Hello World!" << std::endl;
    return 0;
}
```

2. 编写一个程序，使用两个不同的命令在一行打印 "Hello"，在底部打印 "World!"。

```cpp
#include <iostream>
```

int main() {
    std::cout << "Hello" << std::endl;
    std::cout << "World!" << std::endl;
    return 0;
}
```

# 3. 编写一个程序，仅使用一个打印命令在一行打印 "Hello"，在底部打印 "World!"。

```cpp
#include <iostream>

int main() {
    std::cout << "Hello" << std::endl << "World!" << std::endl;
    return 0;
}
```

# 4. 编写一个程序在一行打印 "Hello"，在底部打印 "World!" 并留出一个空行。

```cpp
#include <iostream>

int main() {
    std::cout << "Hello" << std::endl << std::endl << "World!" << std::endl;
    return 0;
}
```

# 5. 编写一个程序在一行打印 "Hello"，并在最后打印 "World!"。

```cpp
#include <iostream>

int main() {
    std::cout << "Hello" << "\nWorld!" << std::endl;
    return 0;
}
```

# 6. 编写一个程序在屏幕上打印 "HellonWorld!"。

```cpp
#include <iostream>

int main() {
    std::cout << "Hello" << std::endl << "World!" << std::endl;
    return 0;
}
```

# 7. 编写一个程序要求用户输入姓名。

```cpp
#include <iostream>
#include <string>

int main() {
    std::string name;
    std::cout << "Enter your name: ";
    std::cin >> name;
    std::cout << "Hello " << name << "!" << std::endl;
    return 0;
}
```

# 8. 编写一个程序顺序读取三个人的姓名，然后是相应的年龄，并以表格格式输出。

```cpp
#include <iostream>
#include <iomanip>
#include <string>

int main() {
    std::string name1, name2, name3;
    int age1, age2, age3;

    // 第一个人的
    std::cout << "Enter the name of the first person: ";
    std::getline(std::cin, name1);
    std::cout << "Enter the age of " << name1 << ": ";
    std::cin >> age1;
    std::cin.ignore(); // 清除换行符

    // 第二个人的人的
    std::cout << "Enter the name of the second person: ";
    std::getline(std::cin, name2);
    std::cout << "Enter the age of " << name2 << ": ";
    std::cin >> age2;
    std::cin.ignore(); // 清除换行符

    // 第三个人的
    std::cout << "Enter the name of the third person: ";
    std::getline(std::cin, name3);
    std::cout << "Enter the age of " << name3 << ": ";
    std::cin >> age3;
    std::cin.ignore(); // 清除换行符

    // 以表格格式输出
    std::cout << std::endl;
    std::cout << std::left << std::setw(20) << "Name" << std::setw(5) << "Age" << std::endl;
    std::cout << "--------------------------------" << std::endl;
    std::cout << std::left << std::setw(20) << name1 << std::setw(5) << age1 << std::endl;
    std::cout << std::left << std::setw(20) << name2 << std::setw(5) << age2 << std::endl;
    std::cout << std::left << std::setw(20) << name3 << std::setw(5) << age3 << std::endl;

    return 0;
}
```

