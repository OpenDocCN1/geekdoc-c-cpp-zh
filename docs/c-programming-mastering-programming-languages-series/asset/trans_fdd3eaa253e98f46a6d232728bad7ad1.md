
```cpp
#include <iostream>

int main() {
    // Declaration and initialization of a 2D integer array
    int matrix[3][4] = {
        {1, 2, 3, 4},
        {5, 6, 7, 8},
        {9, 10, 11, 12}
    };

    // Accessing and displaying individual elements
    std::cout << "Element at row 2, column 3: " << matrix[1][2] << std::endl;

    return 0;
}
```

在此示例中，声明并初始化了一个名为 matrix 的二维整型数组，包含三行四列。使用行索引和列索引访问各个元素。

## 遍历多维数组：嵌套循环

为了高效地遍历和操作多维数组的元素，通常会使用嵌套循环。外层循环遍历行，内层循环遍历列。示例如下：

```cpp
#include <iostream>

int main() {
    // Declaration and initialization of a 2D integer array
    int matrix[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    // Iterating through the 2D array and displaying elements
    for (int i = 0; i < 3; ++i) {
        for (int j = 0; j < 3; ++j) {
            std::cout << "Element at row " << i << ", column " << j << ": " << matrix[i][j]
                      << std::endl;
        }
    }

    return 0;
}
```

在此场景中，嵌套循环遍历一个 3x3 矩阵，显示每个元素及其行索引和列索引。

## 在矩阵中的应用：数学运算

多维数组，尤其是二维数组，在表示和操作矩阵方面有着广泛的应用。矩阵在矩阵乘法和变换等数学运算中起着至关重要的作用，这使其在诸如线性代数和计算机图形学等领域中不可或缺。

理解 C++ 中多维数组的语法和应用可以扩展开发者的工具箱，使其能够高效处理表格或矩阵形式的结构化数据。无论是表示游戏棋盘、图像还是数学矩阵，多维数组都为在 C++ 程序中组织和操作复杂数据结构提供了一种通用解决方案。

## 向量与动态数组简介

在 C++ 编程领域，向量作为动态且多功能的容器脱颖而出，为传统数组提供了一种现代替代方案。本节介绍向量和动态数组的概念，探讨它们的语法、优势以及在管理具有动态大小需求的数据集合方面的应用。

## 向量声明与初始化的语法

C++ 中的向量是标准模板库（STL）的一部分，并提供动态调整大小的能力，这使得它们在数据集合大小事先未知时特别有用。其语法包括包含 `<vector>` 头文件，并声明一个具有指定数据类型的向量。以下是一个基本示例：

```cpp
#include <iostream>
#include <vector>

int main() {
    // Declaration and initialization of an integer vector
    std::vector<int> dynamicVector = {1, 2, 3, 4, 5};

    // Accessing and displaying individual elements
    std::cout << "Element at index 2: " << dynamicVector[2] << std::endl;

    return 0;
}
```

在此示例中，程序声明并初始化了一个名为 dynamicVector 的整型向量，展示了向量的动态特性。

## 动态调整大小：适应运行时需求

向量的关键优势之一是其能够在运行时动态调整大小，以适应不同的数据集合需求。与静态数组不同，向量可以随着元素的添加或删除而增大或缩小。示例如下：

```cpp
#include <iostream>
#include <vector>

int main() {
    // Declaration and initialization of an integer vector
    std::vector<int> dynamicVector = {1, 2, 3};

    // Dynamically adding elements to the vector
    dynamicVector.push_back(4);
    dynamicVector.push_back(5);

    // Displaying the modified vector
    for (int i = 0; i < dynamicVector.size(); ++i) {
        std::cout << "Element " << i << ": " << dynamicVector[i] << std::endl;
    }

    return 0;
}
```

在此场景中，使用 push_back 方法向向量动态添加元素，展示了向量对不断变化的数据需求的适应能力。

## 遍历向量：增强操作

与数组类似，可以使用循环高效地遍历向量以进行各种操作。以下示例演示了遍历一个向量并将其元素翻倍：

```cpp
#include <iostream>
#include <vector>

int main() {
    // Declaration and initialization of an integer vector
    std::vector<int> dynamicVector = {1, 2, 3, 4, 5};

    // Modifying vector elements using a for loop
    for (int i = 0; i < dynamicVector.size(); ++i) {
        dynamicVector[i] = dynamicVector[i] * 2; // Doubling each element
    }

    // Displaying the modified vector
    for (int i = 0; i < dynamicVector.size(); ++i) {
        std::cout << "Modified Element " << i << ": " << dynamicVector[i] << std::endl;
    }

    return 0;
}
```

此示例说明了如何使用 for 循环将向量中的值翻倍，然后显示修改后的元素。

理解 C++ 中向量的语法和优势，为管理具有不同大小需求的数据集合开辟了动态可能性。无论是动态添加元素、调整大小，还是执行迭代操作，向量都为现代 C++ 编程提供了灵活而强大的解决方案。

C++ 的一个显著特性是 do-while 循环，这种结构保证在评估循环条件之前，代码块至少执行一次。本模块探讨 do-while 循环的机制，演示其在必须在评估循环条件之前执行某个操作的场景中的实用性。通过动手练习，读者将理解 do-while 循环如何有助于构建健壮且具有韧性的代码结构。

## 嵌套循环：优雅地编排复杂性

本模块延伸至嵌套循环领域，在这里多个循环的协同作用可以编排复杂的模式和结构。读者将探索嵌套 for、while 和 do-while 循环的细节，揭示分层迭代的优雅之处。实际示例将展示嵌套循环在从矩阵操作到图案打印等场景中的应用，使读者能够应对并掌握复杂的编码挑战。

## 应用迭代：真实项目与挑战

为了巩固本模块介绍的概念，读者将参与需要应用迭代编程原则的实践项目和挑战。从实现需要循环的算法到为现实问题设计解决方案，这些动手活动弥合了理论与实际应用之间的差距。通过应对这些挑战，读者不仅能巩固对 C++ 循环的理解，还能培养解决各种编程场景所必需的问题解决能力。

“循环与重复结构”模块是掌握 C++ 编程中迭代艺术的门户。通过全面涵盖 for 循环、while 循环、do-while 循环和嵌套循环，本模块使读者能够创建通过重复过程高效且优雅执行的代码。作为算法设计中不可或缺的一方面，从本模块获得的知识使学习者能够以精确和创造力应对复杂挑战。

## 循环简介

在 C++ 编程领域中，while 和 do-while 循环提供了动态且多功能的构造，用于基于指定条件重复执行代码。本节深入探讨 while 和 do-while 循环的语法、功能和用例，提供关于它们独特特性以及在创建高效且可适应的重复结构中的应用的见解。

### while 循环的语法与功能

C++ 中的 while 循环在指定条件为真时执行代码块。其语法包括关键字 while，后跟括号中的条件以及要执行的代码块。以下是一个基本示例，说明如何使用 while 循环计算一个数的阶乘：

```cpp
#include <iostream>

int main() {
    // Calculating the factorial of 5 using a while loop
    int number = 5;
    long long factorial = 1;

    while (number > 0) {
        factorial *= number;
        --number;
    }

    // Displaying the calculated factorial
    std::cout << "Factorial of 5: " << factorial << std::endl;

    return 0;
}
```

在此示例中，只要 number 变量大于零，while 循环就会迭代，并在每次迭代中将 factorial 变量相乘。

### do-while 循环：确保至少执行一次

do-while 循环是 while 循环的一种变体，它确保代码块至少执行一次，即使条件最初为假。其语法包括 do 关键字、代码块，以及后跟括号中条件的 while 关键字。以下是一个示例，其中提示用户输入一个正数：
