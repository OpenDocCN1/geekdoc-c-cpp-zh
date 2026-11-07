

```cpp
std::string sentence = "C++ programming is powerful.";
size_t position = sentence.find("programming");

// Displaying the results
std::cout << "Substring found at position: " << position << std::endl;

return 0;
}
```

在这里，`compare` 函数用于比较两个字符串，而 `find` 成员函数用于定位子字符串在另一个字符串中的位置。

“字符串操作与函数”模块为开发者提供了对 C++ 中可用于操作字符串的众多函数的透彻理解。这些操作使程序员能够有效地处理字符串，无论是基本的拼接，还是比较和搜索等更复杂的任务。掌握这些函数能够增强开发者在不同编程场景中处理文本数据的能力。

## 字符串格式化与操作

“字符串与字符串操作”模块中的“字符串格式化与操作”部分深入探讨了 C++ 中格式化和操作字符串的细微之处。该模块为开发者提供了构建结构良好且视觉美观的文本输出的基本技能，这在从用户界面到数据表示的各种应用中至关重要。

### 使用 printf 风格格式化字符串

C++ 支持继承自 C 语言的 printf 风格格式化，为构造格式化字符串提供了一种简洁而强大的机制。

```cpp
#include <iostream>
#include <iomanip>

int main() {
    // Using printf-style formatting
    int integerValue = 42;
    double doubleValue = 3.14159;

    std::cout << "Integer value: " << std::setw(5) << integerValue << std::endl;
    std::cout << "Double value: " << std::setprecision(3) << doubleValue << std::endl;

    return 0;
}
```

在此示例中，`setw` 操纵符确保整数值具有最小宽度，而 `setprecision` 控制双精度浮点值的精度。

### 使用 stringstream 格式化字符串

`<sstream>` 头文件提供了 `std::stringstream` 类，使得能够通过流接口进行字符串格式化。

```cpp
#include <iostream>
#include <sstream>

int main() {
    // Using stringstream for string formatting
    int day = 15;
    int month = 7;
    int year = 2023;

    std::stringstream formattedDate;
    formattedDate << "Date: " << std::setw(2) << std::setfill('0') << day << "/"
                  << std::setw(2) << month << "/" << year;

    // Displaying the formatted date
    std::cout << formattedDate.str() << std::endl;

    return 0;
}
```

在这里，`std::setfill` 确保前导零，格式化后的日期在显示之前存储在一个 `std::stringstream` 中。

### 使用 substr、append 和 erase 进行字符串操作

`substr`、`append` 和 `erase` 函数使开发者能够高效地操作字符串。这些函数在提取子字符串、追加额外内容以及删除字符串的某些部分方面提供了灵活性。

```cpp
#include <iostream>
#include <string>

int main() {
```

理解 C++ 字符串（`std::string`）和 C 风格字符串之间的差异至关重要。C++ 字符串提供了动态调整大小和大量成员函数，而 C 风格字符串则需要手动进行内存管理。

```cpp
#include <iostream>
#include <string>
#include <cstring>

int main() {
    // Comparison of C++ Strings and C-Style Strings
    std::string cppString = "C++ is modern.";
    const char cString[] = "C is classic.";

    // C++ String to C-Style String
    const char* convertedCString = cppString.c_str();

    // Displaying the results
    std::cout << "C++ String: " << cppString << std::endl;
    std::cout << "C-Style String: " << convertedCString << std::endl;

    return 0;
}
```

在这里，`c_str()` 成员函数将 C++ 字符串转换为 C 风格字符串，以便实现互操作性。

“使用 C 风格字符串”部分提供了关于 C++ 中 C 风格字符串处理细节的全面见解。开发者能够获得处理底层字符串操作、与 C 库交互以及确保在 C 风格字符串普遍存在的场景中实现兼容性的关键技能。理解 C 风格字符串的优势和局限性对于掌握 C++ 编程的多样化领域至关重要。

## 模块 17：结构体和联合体

《C++ 编程》一书中的“结构体和联合体”模块是一个基石性的章节，读者将在此深入探讨组织复杂数据结构的艺术。该模块经过精心设计，旨在让学习者掌握利用结构体和联合体（C++ 中用于创建聚合不同元素的自定义数据类型的关键构造）的能力。在探索本模块的过程中，读者将揭示这些构造在编写高效且富有表现力的程序方面的潜力和多样性。

### 理解结构体：揭示复合数据类型的威力

该模块首先解释结构体这一复合数据类型，它允许开发者将相关变量组合在同一个名称下。读者将探索结构体的语法和功能，理解它们如何有助于创建更有组织性、更易读的代码。通过实际示例，学习者将掌握结构体在从表示现实世界实体到组织数据以进行高效处理等各种场景中的多样性。

### 结构体成员与初始化：构建自定义数据表示

随着探索的深入，重点转向结构体成员与初始化——这些基本方面塑造了自定义数据类型的结构和行为。本节指导读者定义和访问结构体中的成员，理解如何有效地初始化和操作这些组件。实际示例将说明结构体如何支持创建针对特定程序需求定制的自定义数据表示。

### 结构体数组：精确扩展数据组织

接着，重点转向结构体数组，释放精确扩展数据组织的潜力。读者将探索数组如何由结构体构成，从而创建相关数据实体的集合。本节深入探讨使用结构体数组的优势，演示它们如何简化大型数据集的管理，并促进模块化和可扩展的程序设计。

### 联合体：数据存储的灵活性

该模块自然地过渡到联合体的概念，联合体通过允许多个成员共享同一内存位置来提供数据存储的灵活性。读者将理解联合体的语法和应用，探索能够以多种方式表示数据的优势场景。实际示例将展示联合体如何有助于高效的内存使用，并在程序内容纳多样的数据表示。

### 应用数据结构：真实项目与挑战

为了巩固模块中引入的概念，读者将参与需要应用结构体和联合体原则的实际项目和挑战。从设计表示复杂实体的数据结构，到实现通过联合体优化内存使用的解决方案，这些动手活动弥合了理论与实践应用之间的差距。通过应对这些挑战，读者不仅能巩固对 C++ 中结构体和联合体的理解，还能培养编写高效且富有表现力的软件解决方案所必需的问题解决技能。

“结构体和联合体”模块是掌握 C++ 编程中构建复杂数据结构的门户。通过全面涵盖结构体、结构体成员、结构体数组、联合体以及应用数据结构，该模块使读者能够以精确性和灵活性掌握组织和表示数据的艺术。作为许多编程任务中的基本组成部分，从本模块获得的知识将使学习者能够创建高效、可扩展且富有表现力的软件解决方案，从而熟练地处理复杂的数据排列。

### 定义和使用结构体

