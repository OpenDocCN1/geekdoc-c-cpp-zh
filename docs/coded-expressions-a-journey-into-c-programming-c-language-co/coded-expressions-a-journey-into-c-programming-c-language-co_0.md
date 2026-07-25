# C语言表达式：C语言编程之旅：C 语言课程学习书籍



![](img/image_rsrc1T9.jpg)








在整个课程中，应该定期进行测验、作业和项目，以评估学生的理解情况。此外，鼓励学生经常练习编程以增强他们的编程技能。

# 第 1 天：C 语言简介、历史与重要性

**C 语言简介**：C 是一种通用的过程化编程语言，由 Dennis Ritchie 在 20 世纪 70 年代初在贝尔实验室开发。它为系统编程而设计，但广泛应用于各个领域的应用程序开发。

**历史**：C 出现于早期的编程语言 `B`，`B` 是 Ken Thompson 在贝尔实验室开发的。C 的创建是为了提供对计算机内存的低级访问，同时提供高级结构支持。

**重要性**：C 被认为是最影响力的编程语言之一，是许多其他编程语言的基础。它用于操作系统、嵌入式系统、设备驱动、游戏以及对性能和效率至关重要的应用程序。

# 第 2 天：配置开发环境（IDE, 编译器）

**IDE（集成开发环境）**：IDE 为编写、编译、调试和执行程序提供了一个全面的环境。流行的 C 语言 IDE 包括 Visual Studio、Code::Blocks 以及带有 C/C++ 插件的 Eclipse。

**编译器**：编译器将 C 源代码翻译成计算机处理器可以执行的机器读二进制代码。常见的 C 编译器包括 `GCC`（GNU 编译器集）、`Clang` 和 Microsoft Visual C++ 编译器。

# 第 3 天：C 程序结构、变量与数据类型

**C 程序结构**：一个典型的 C 程序由一组函数组成。每个 C 程序都必须包含一个 `main()` 函数，该函数作为程序的入口。

**变量**：变量用于存储可以在程序内进行操作的数据值。在 C 中，变量在使用之前必须进行声明，并指定其数据类型。

**数据类型**：C 提供了几种基本数据类型，包括 `int`（整数）、`float`（浮点数）、`double`（双精度浮点数）、`char`（字符）和 `void`（空数据类型）。此外，C 允许使用结构体和枚举创建自定义数据类型。

# 第 4 天：输入输出函数 (`printf`, `scanf`)

`printf()`：`printf()` 是一个标准库函数，用于向标准输出设备（通常是控制台）显示格式化输出。它允许使用格式说明符打印变量、字符串和特殊字符。

`scanf()`：`scanf()` 是一个标准库函数，用于从标准输入设备（通常是键盘）读取格式化输入。它将数据读入提供的格式说明符指定的变量中。

# 第 5 天：运算符与表达式

**运算符**：运算符是代表在操作数上执行的操作的符号。C 提供了各种运算符，包括算术运算符（`+`, `-`, `*`, `/`）、关系运算符（`==`, `!=`, `<`, `>`）、逻辑运算符（`&&`, `||`, `!`）、赋值运算符（`=`, `+=`, `-=`）和位运算符（`&`, `|`, `^`）。

**表达式**：表达式是变量、常量和运算符的组合，评估为一个单个值。C 支持多种类型的表达式，包括算术表达式、关系表达式、逻辑表达式和位表达式。

理解这些基础概念对于为 C 编程打下坚实基础至关重要。它们为开始编写 C 程序提供了必要的知识和技能。

## 第二周：控制流与函数

### 第 6 天：决策语句 (`if`, `if-else`, 嵌套 `if`)

**if 语句**：`if` 语句用于在条件为真时执行代码块。如果条件为假，则跳过代码块。

```c
if (condition) {
    // 条件为真时执行的代码块
}
```

**if-else 语句**：`if-else` 语句允许在条件为真时执行一个代码块，在条件为假时执行另一个。

```c
if (condition) {
    // 条件为真时执行的代码块
} else {
    // 条件为假时执行的代码块
}
```

**嵌套 if 语句**：嵌套 if 是另一个 `if` 语句中的 `if` 语句。它允许顺序检查多个条件。

```c
if (condition1) {
    if (condition2) {
        // 当 condition1 和 condition2 都为真时执行的代码块
    }
}
```

### 第 7 天：循环 (`while`, `for`, `do-while`)

**while 循环**：`while` 循环在指定的条件为真时重复执行代码块。

```c
while (condition) {
    // 条件为真时重复执行的代码块
}
```

**for 循环**：`for` 循环提供了一种遍历值范围的简洁方式。它包含三部分：初始化、条件和递增/递减。

```c
for (initialization; condition; increment/decrement) {
    // 重复执行代码块直到条件为假
}
```

**do-while 循环**：`do-while` 循环与 `while` 循环相似，但它保证在检查条件之前至少执行一次代码块。

```c
do {
    // 执行的代码块
} while (condition);
```

### 第 8 天：Switch-case 语句




`switch-case` 语句用于在多个条件中执行一条语句。它评估一个表达式并与 case 值进行比较。如果找到匹配项，则执行对应的代码块。

```c
switch (expression) {
    case value1:
        // 如果 expression 等于 value1，执行此代码块
        break;
    case value2:
        // 如果 expression 等于 value2，执行此代码块
        break;
    default:
        // 如果没有 case 匹配 expression，执行此代码块
}
```

### 第 9 天：Break 和 Continue 语句

**Break 语句**：`break` 语句用于在立即退出循环或 `switch-case` 语句。它通常用于提前终止循环。

**Continue 语句**：`continue` 语句用于跳过循环的当前迭代并继续下一次迭代。它通常用于避免在特定条件下执行特定的代码。

### 第 10 天：函数介绍、函数声明、定义与调用

**函数**：函数是执行特定任务的自包含代码块。它们允许代码重用、模块化和更易于调试。

**函数声明**：函数声明指定了函数的名称、返回类型和参数（如果有）。它通知编译器该函数的存在。

```c
return_type function_name(parameter1_type parameter1, parameter2_type parameter2, ...) {
    // 函数体
}
```

**函数定义**：函数定义包含了函数的实际实现。它包括函数头（返回类型和名称）和函数体（要执行的代码）。

**函数调用**：函数调用涉及调用一个函数来执行其定义的任务。它包括函数名，后面跟上包含在括号内的参数（如果有）。

```c
return_type result = function_name(argument1, argument2, ...);
```

理解控制流语句和函数对于开发更复杂、结构化的 C 程序至关重要。它们提供了决策、重复操作以及将代码组织成可重用单元的能力。

## 第 3 周：数组与字符串

### 第 11 天：数组介绍、声明、初始化与元素访问

**数组介绍**：数组是存储在连续内存中的相同数据类型元素的集合。它允许在单个名称下存储和操作多个值。

**声明数组**：在 C 中声明数组时，您需要指定元素的数据类型以及在方括号 `[]` 内指定数组的大小。

```c
data_type array_name[size];
```

**初始化数组**：可以在声明时初始化数组，也可以稍后使用赋值语句。

```c
int numbers[5] = {1, 2, 3, 4, 5}; // 声明时初始化
char vowels[] = {'a', 'e', 'i', 'o', 'u'}; // 大小从初始化推断
```

**访问元素**：使用从零开始的索引访问数组元素。在数组名后的方括号 `[]` 中指定索引。

```c
int value = numbers[2]; // 访问 numbers 数组的第三元素
```

### 第 12 天：多维数组

**多维数组**：多维数组是数组的数组。它们允许以多个维度（如行和列）表示表格数据。

```c
data_type array_name[rows][columns];
```

**初始化多维数组**：可以使用嵌套的大括号初始化多维数组。

```c
int matrix[2][3] = {{1, 2, 3}, {4, 5, 6}};
```

**访问多维数组中的元素**：使用多组方括号 `[]` 访问多维数组中的元素。

```c
int value = matrix[1][2]; // 访问第二行第三列的元素
```

### 第 13 天：字符串介绍、字符串函数

**字符串介绍**：C 中的字符串是以空字符（`'\0'`）终止的字符序列。字符串以字符数组的形式存储。

**字符串函数**：C 提供了几个用于处理字符串的内置函数，如 `strlen()`、`strcpy()`、`strcat()`、`strcmp()` 等。

```c
#include <string.h>
```

### 第 14 天：字符串操作函数

- `strlen()`：计算字符串的长度。
- `strcpy()`：将一个字符串复制到另一个字符串。
- `strcat()`：将一个字符串拼接（追加）到另一个字符串的末尾。
- `strcmp()`：按字典顺序比较两个字符串。
- 更多：C 提供了许多其他字符串操作函数，用于搜索、分词和大小转换等任务。

### 第 15 天：字符数组对比 字符串字面量

**字符数组**：字符数组是用于在 C 中存储字符串的字符数组。它们允许操作字符串，但需要小心处理空终止符。

**字符串字面量**：字符串字面量是用双引号的字符序列。它们在结尾自动包含一个空终止符。

```c
char str[] = "Hello"; // 字符数组
char* str_literal = "Hello"; // 字符串字面量
```

理解数组和字符串对于处理 C 中的数据集合至关重要。数组提供了高效存储和访问多个值的方法，而字符串有助于文本处理任务。掌握这些概念使开发者能够有效处理复杂的数据结构和算法。

## 第 4 周：指针与内存管理

### 第 16 天：指针介绍、指针运算

**指针介绍**：指针存储另一个变量内存地址的变量。它允许直接操作内存位置，实现高效内存管理。

**声明指针**：通过指定指向的变量类型来声明指针，后跟星号 (`*`) 和指针名。

```c
int *ptr; // 指向整数的指针
```

**给指针赋值**：使用地址运算符 (`&`) 将变量的地址赋给指针。

```c
int num = 10;
int *ptr = &num; // 指针现在持有 num 的地址
```

**指针运算**：指针运算涉及对指针进行算术运算（加减）。这允许遍历内存位置。

```c
ptr++; // 指针指向下一个内存位置
ptr--; // 指针指向上一个内存位置
```

### 第 17 天：指针与数组

**指针与数组的关系**：在 C 中，数组和指针密切相关。数组名可以作为指向第一个元素的指针。

```c
int arr[5] = {1, 2, 3, 4, 5};
int *ptr = arr; // 指针 ptr 指向数组 arr 的第一个元素
```

**数组指针运算**：可以使用指针运算高效地遍历数组。

```c
for (int i = 0; i < 5; i++) {
    printf("%d ", *(ptr + i)); // 使用指针运算访问数组元素
}
```

### 第 18 天：指针与函数

**作为函数参数的指针**：可以将指针作为参数传递给函数，允许函数修改调用者作用域内变量的值。

**向函数传递指针**：向函数传递指针可以高效地传递大型数据结构，无需复制整个数据。

```c
void modifyValue(int *ptr) {
    *ptr = 20; // 修改 ptr 指向的值
}
```

### 第 19 天：动态内存分配 (malloc, calloc, realloc, free)

**动态内存分配**：动态内存分配允许程序在运行时动态分配内存。这使得创建编译时未知大小的数据结构成为。

`malloc()`：分配指定字节数的内存块，并返回指向所分配内存第一个字节的指针。

```c
int *ptr = (int *)malloc(5 * sizeof(int)); // 为 5 个整数分配内存
```

`calloc()`：为元素数组分配一块内存，将其初始化为零，并返回指向分配内存的指针。





```c
int *ptr = (int *)calloc(5, sizeof(int)); // 为 5 个整数分配内存并初始化为零
```

`realloc()`: 更改之前分配的内存块的大小，可能会将其移动到内存的新位置，并返回指向新内存块的指针。

```c
int *new_ptr = (int *)realloc(ptr, 10 * sizeof(int)); // 调整内存块大小以容纳 10 个整数
```

`free()`: 释放由 `malloc()`、`calloc()` 或 `realloc()` 之前分配的内存块，释放内存以便用。

```c
free(ptr); // 释放 ptr 指向的内存块
```

## 第 20 天：函数指针、传递函数指针

函数指针：像变量一样，函数拥有内存地址，这些地址可以存储在指针中。函数指针允许在运行时动态调用函数。

```c
int add(int a, int b) {
return a + b;
}

int (*ptr)(int, int) = &add; // 函数 add 的指针
```

将函数指针作为参数传递：函数指针可以作为参数传递给其他函数，实现回调和函数间接。

```c
void process(int (*func_ptr)(int, int)) {
// 调用 func_ptr 指向的函数
int result = (*func_ptr)(5, 3);
printf("Result: %d\n", result);
}
```

理解指针和内存管理对于 C 语言中高效资源利用和高级数据处理至关重要。掌握这些概念使开发者能够处理复杂的数据结构、优化内存使用并编写更高效、更灵活的代码。

## 第 5 周：结构体、文件处理与高级主题

### 第 21 天：结构体简介、定义和访问结构体成员

结构体简介：C 语言中的结构体（`structs`）允许将不同数据类型的变量组合到一个名称下。它们提供了一种表示复杂数据结构的方法。

定义结构体：使用 `struct` 关键字定义结构体，后跟结构体名称和包含在大括号 `{}` 中的成员变量列表。

```c
struct Person {
char name[50];
int age;
float salary;
};
```

访问结构体成员：使用点（`.`）运算符访问结构体成员，后跟成员名。

```c
struct Person p1;
strcpy(p1.name, "John");
p1.age = 30;
p1.salary = 50000.0;
```

### 第 22 天：嵌套结构体、结构体数组

嵌套结构体：结构体可以嵌套在其他结构体内部以表示分级数据结构。

```c
struct Date {
int day;
int month;
int year;
};

struct Employee {
char name[50];
struct Date dob;
float salary;
};
```

结构体数组：结构体数组允许创建结构化数据的集合。

```c
struct Employee employees[100]; // 100 个 Employee 结构体的数组
employees[0].salary = 50000.0; // 访问第一个员工的工资
```

### 第 23 天：C 语言文件处理（打开、读取、写入、关闭文件）

文件处理基础：C 语言的文件处理涉及打开文件、从文件中读取数据、向文件写入数据以及关闭文件等操作。

打开文件：使用 `fopen()` 函数打开文件，该函数返回一个文件指针。

```c
FILE *file_ptr = fopen("file.txt", "r"); // 以读取模式打开 file.txt
```

从文件读取：可以使用 `fscanf()` 和 `fgets()` 等函数从文件中读取数据。

写入文件：可以使用 `fprintf()` 和 `fputs()` 函数向文件写入数据。

关闭文件：在对文件进行读取或写入后，应使用 `fclose()` 函数关闭。

```c
fclose(file_ptr); // 关闭文件
```

### 第 24 天：文件操作 (fseek, ftell, rewind)

文件定位：文件定位函数允许你将文件指针移动到文件内的特定位置。

`fseek()`：将文件指针移动到距离参考点指定的字节偏移量。

`ftell()`：返回文件指针相对于文件开头的当前位置（以字节为单位）。

`rewind()`：将文件指针移动到文件开头。

### 第 25 天：错误处理与文件操作

错误处理：文件操作中的错误处理涉及执行文件相关操作后检查错误并进行适当处理。

文件操作：文件操作涉及各种操作，如复制文件、重命名文件、删除文件和检查文件是否存在。

理解 C 语言中的结构体和文件处理对于处理复杂数据结构以及对文件执行输入输出操作至关重要。掌握这些概念使开发者能够有效地处理数据，并构建与文件等外部数据源交互的应用程序。

## 第 6 周：高级概念

### 第 26 天：枚举与 typedef

枚举：枚举（`enums`）允许你定义一组命名的常量（称为枚举常量），它们表示一组整数值。

```c
enum Weekday {Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday};
enum Weekday today = Wednesday;
```

typedef：`typedef` 允许你为现有数据类型创建别名或新名称，使代码更具可读且易于管理。

```c
typedef int Age; // 定义 Age 为 int 的别名
Age my_age = 30; // 使用 Age 别名
```

### 第 27 天：预处理器指令 (#define, #include, #ifdef)

#define：`#define` 指令用于定义宏，宏是定义符号常量或简单函数的预处理器指令。

```c
#define PI 3.14159
```

#include：`#include` 指令用于将另一个文件（头文件）包含到源文件中。

```c
#include <stdio.h>
```

#ifdef：`#ifdef` 指令检查宏是否已定义。如果定义了，则编译代码块。

```c
#ifdef DEBUG
printf("Debug mode enabled\n");
#endif
```

### 第 28 天：位运算符

位运算符：位运算符对操作数的二进制位进行操作。

`&` (AND)：执行按位与操作。

`|` (OR)：执行按位或操作。

`^` (XOR)：执行按位异或操作。

`~` (NOT)：执行按位取反操作。

`<<` (左移)：位向左移动。

`>>` (右移)：位向右移动。

### 第 29 天：递归简介

递归：递归是一种编程技术，函数直接或间接地自调用自己来解决问题。

```c
int factorial(int n) {
if (n == 0 || n == 1)
return 1;
else
return n * factorial(n - 1);
}
```

基例：递归涉及将问题分解为更小的实例，直到达到基例，基例是不需要进一步递归的条件。

### 第 30 天：数据结构简介（链表）

链表：链表是由节点组成的线性数据结构，每个节点包含数据以及指向序列中下一个节点的指针。

链表的类型：

单向链表：每个节点包含数据和一个指向下一个节点的指针。

双向链表：每个节点包含数据、一个指向下一个节点的指针以及一个指向上一个节点的指针。

循环链表：最后一个节点指向第一个节点，形成环形结构。

链表的优点：

动态大小。

高效的插入和删除操作。

链表的缺点：

需要额外的内存来存储指针。

与数组相比，遍历可能较慢。

理解枚举、typedef、预处理器指令、位运算符、递归以及链表等数据结构等高级概念对于编写高效且复杂的 C 程序至关重要。这些概念为解决广泛的编程问题和优化代码性能提供了强大的工具。

## 第 7 周：高级数据结构与项目工作

### 第 31 天：栈与队列





## 概述

### 栈 (Stacks)
栈是一种遵循后进先出（LIFO）原则的线性数据结构。它支持两个主要操作：`push`（向栈顶添加元素）和 `pop`（从栈顶移除元素）。

### 队列 (Queues)
队列是一种遵循先入出（FIFO）原则的线性数据结构。它支持两个主要操作：`enqueue`（向队尾元素）和 `dequeue`（从队移除元素）。

## 第 32 天：树（二叉树、二叉搜索树）

### 二叉树 (Binary Trees)
二叉树是一种层次化数据结构，由节点组成，每个节点最多有两个子节点：左孩子和右孩子。

### 二叉搜索树 (BST)
二叉搜索树是一种二叉树，其中每个节点的左孩子的值小于该节点的值，而右孩子的值大于该节点的值。它支持高效的搜索、插入和删除操作。

## 第 33 天：图（基础概念）

### 图 (Graphs)
图是一种非线性数据结构，由有限的顶点（节点）和这些顶点之间的边（连接）组成。图广泛用于建模对象之间的关系。

### 基础概念
图可以是有向或无向的，加权或无权的。常见的表示方法包括邻接矩阵和邻接列表。

## 第 34 天：排序算法（选择排序、冒泡排序）

### 选择排序
选择排序是一种简单的排序算法，它重复地从数组未排序的部分选择最小元素并将其放在开头。

### 冒泡排序
冒泡排序是一种基础排序算法，它重复遍历列表，比较相邻元素，如果它们的顺序错误则进行交换。

## 第 35 天：项目工作：使用 C 实现小型应用程序或项目

学生的任务是使用整个课程中学到的概念和技术来实现小型应用程序或项目。这可能包括创建一个简单的游戏、实用工具或其他任何软件应用程序，展示他们对 C 语言编程基础和高级主题的理解。

实现项目允许学生在实际背景中应用知识，强化学习，并获得解决现实问题的实践经验。它还为创造力和创新提供了机会，培养对该语言及其能力的深层理解。

## 第 8 周：复习与练习

### 第 36-40 天：概念复习、习题解答与练习题

### 概念复习
学生重新复习课程涵盖的关键概念，包括基础语法、控制结构、函数、数组、指针、文件处理、数据结构和算法。

### 习题解答
为学生提供涵盖 C 语言编程不同方面的各种练习题和问题。这些习题从从简单到复杂不等，旨在强化理解和解决问题的能力。

### 练习题
练习题侧重于应用所学概念来解决现实世界的编程挑战。它们鼓励学生进行批判性思考，编写高效代码并调试任何错误。

### 第 41-45 天：微型项目、作业与评估以强化学习

### 微型项目
学生开展微型项目，要求他们应用整个课程中学到的多个概念。这些项目可能涉及实现算法、构建数据结构或创建小型应用程序。

### 作业
给学生布置作业以评估他们对特定主题的理解。作业可能涉及编写代码、回答理论问题或解决编程问题。

### 评估
通过评估来评价学生对 C 编程的整体理解。评估可能包括涵盖课程大纲各个方面的测验、测试或实践考试。

### 复习与练习的好处
- **巩固学习**：复习概念和解答练习有助于巩固对基本原理的理解。
- **强化解决问题的能力**：练习题和微型项目挑战学生应用知识解决现实世界的问题。
- **识别弱点**：通过评估和作业，学生可以识别需要进一步改进领域。
- **鼓励创造力**：微型项目允许学生探索创造力并以创新的方式应用知识。
- **建立信心**：成功完成习题、作业和项目将增强学生对自己编程能力的信心。

总的来说，第 8 周是课程的总结，为学生在进入更高级的主题或项目之前提供了一个复习、练习和评估他们对 C 编程概念理解的机会。

## C 程序的基本结构

```c
#include <stdio.h>

// 函数原型（如果有的话）

int main() {
    // 变量声明
    // 语句
    return 0;
}

// 函数定义（如果有的话）
```

### 让我们分解每个部分：

- `#include <stdio.h>`：这一行在程序中包含了标准输入输出库，允许你使用 `printf()` 和 `scanf()` 等函数。
- **函数原型**：这些是程序使用的函数声明，放置在 `main()` 函数之前。它们指定了函数的名称、返回类型和参数列表（如果有的话）。
- `main()` 函数：每个 C 程序必须有一个 `main()` 函数，它作为程序的入口。程序的执行从该函数开始。
- **变量声明**：这是你声明将在程序使用的变量的地方。变量应该在程序中使用之前进行声明。
- **语句**：这些是程序执行的实际指令或操作。它们可以包括赋值、函数调用、控制流语句等。
- `return 0;`：这一行表示 `main()` 函数的结束和程序的成功终止。值 `0` 表示程序执行成功。可以返回其他非零值来表示不同类型的错误。
- **函数定义**：这些是之前声明的函数的实现。它们包含了定义每个函数的实际代码。

## C 语言变量和数据类型概述

### 变量
- **命名规范**：C 中的变量名必须以字母（A-Z, a-z）或下划线（`_`）开头，跟着字母、数字（0-9）或下划线。
- **声明**：变量在使用之前必须声明。声明指定了变量的名称和数据类型。
- **初始化**：变量可以在声明时或程序后期进行初始化（分配初始值）。
- **作用域**：变量的作用域决定了它们在程序的范围内可以被访问。变量可以是局部作用域（定义在块或函数内部）或全局作用域（定义在函数外部）。

### 数据类型
C 支持多种数据类型，分为四类：

### 基础数据类型
- `int`：整数类型，用于存储整数。
- `char`：字符类型，用于存储单个字符。
- `float`：浮点类型，用于存储单精度小数。
- `double`：双精度浮点类型，用于存储双精度小数。

### 衍生数据类型
- `array`：相同类型元素的集合，存储在连续的内存中。
- `pointer`：存储另一个变量内存地址的变量。
- `structure`：用户定义的数据类型，将不同类型的变量组合在一个名称下。

### 枚举数据类型
- `enum`：用户定义的数据类型，用于定义一组命名常量（枚举值）。

### 空类型
- `void`：表示类型的缺失。





`void`: 表示数据类型的缺失。它通常用于指示函数不返回任何值，或者指针不指向任何特定的数据类型。

### 示例：

```c
#include <stdio.h>

int main() {
    // 变量声明与初始化
    int age = 25;
    char gender = 'M';
    float height = 5.9;
    double weight = 68.5;

    // 打印变量值
    printf("Age: %d\n", age);
    printf("Gender: %c\n", gender);
    printf("Height: %.2f\n", height);
    printf("Weight: %.1f\n", weight);

    return 0;
}
```

在这个示例中，我们声明并初始化了不同数据类型的变量（`int`、`char`、`float`、`double`）。然后我们使用 `printf()` 函数打印了它们的值。

当然！`printf()` 和 `scanf()` 是 C 语言中用于输入输出的两个常用函数。以下是你在 C 程序中使用它们的方法：

### `printf()` 函数：

`printf()` 函数用于将格式化输出打印到标准输出（通常是控制台）。它接受一个格式字符串作为第一个参数，随后是任何表示要格式化并打印的值的额外参数。

```c
#include <stdio.h>

int main() {
    int num = 10;
    float pi = 3.14159;

    // 打印整数和浮点数
    printf("The value of num is: %d\n", num);
    printf("The value of pi is: %.2f\n", pi);

    // 打印字符串
    printf("Hello, world!\n");

    return 0;
}
```

### `scanf()` 函数：

`scanf()` 函数用于从标准输入（通常是键盘）读取格式化输入。它接受一个格式字符串作为第一个参数，随后是指向存储输入值的变量的指针。

```c
#include <stdio.h>

int main() {
    int num;
    float pi;

    // 读取一个整数和一个浮点数
    printf("Enter an integer: ");
    scanf("%d", &num);
    printf("Enter a float: ");
    scanf("%f", &pi);

    // 打印用户输入的值
    printf("You entered: %d\n", num);
    printf("You entered: %.2f\n", pi);

    return 0;
}
```

#### 注意：

- `%d`、`%f`、`%c` 等是格式说明符，用于指定读取或打印的数据类型。
- 在 `scanf()` 中，变量名名前使用 `&` 运算符来传递其地址，指示输入值应该存储的位置。
- 使用 `scanf()` 时始终确保进行适当的错误处理，以处理用户输入意外内容的情况。

运算符和表达式是 C 编程的基础组件，允许你对数据执行各种操作。以下是 C 语言中运算符和表达式的概述：

#### 算术运算符：

算术运算符用于对操作数执行数学运算。

```c
int a = 10, b = 5;
int sum = a + b;    // 加法
int difference = a - b; // 减法
int product = a * b; // 乘法
float division = a / (float)b; // 除法（强制类型转换为 float 以获得准确结果）
int remainder = a % b; // 取模（除法的余数）
```

#### 关系运算符：

关系运算符用于比较两个操作数的值。

```c
int a = 10, b = 5;
if (a > b) {
    printf("a is greater than b\n");
}
if (a == b) {
    printf("a is equal to b\n");
}
if (a != b) {
    printf("a is not equal to b\n");
}
```

#### 逻辑运算符：

逻辑运算符用于组合多个条件。

```c
int x = 5, y = 10;
if (x > 0 && y > 0) {
    printf("Both x and y are positive\n");
}
if (x > 0 || y > 0) {
    printf("At least one of x or y is positive\n");
}
if (!(x > 0)) {
    printf("x is not positive\n");
}
```

#### 赋值运算符：

赋值运算符用于向变量赋值。

```c
int a = 10;
a += 5; // 等于 a = a + 5
```

#### 增减运算符：

递增（`++`）和递减（--`）运算符用于增加或减少变量的值。

```c
int x = 5;
x++; // x 加 1
```

#### 位运算符：

位运算符用于在位层级上执行操作。

```c
int x = 5, y = 3;
int bitwise_and = x & y; // 按位与
int bitwise_or = x | y; // 按位或
int bitwise_xor = x ^ y; // 按位异异
int bitwise_not = ~x; // 按位非
int left_shift = x << 1; // 左移
int right_shift = x >> 1; // 右移
```

#### 条件运算符（三元运算符）：

条件运算符（`? :)）用于决策。

```c
int a = 10, b = 5;
int max = (a > b) ? a : b; // max 将存储 a 和 b 之间的最大值
```




## 控制流

`switch` 关键字表示 `switch-case` 块的开始。

选择变量（表达式）被求值，其值决定了执行哪个 `case` 块。

每个 `case` 标签指定表达式的一个可能值。

如果 `choice` 的值与 `case` 标签匹配，则执行相应的代码块。

`break` 语句用于在执行相应的 `case` 块后退出 `switch` 块。

`default` 情况是可选的，当没有 `case` 的值与表达式的值匹配时执行。

`switch-case` 语句提供了一种根据表达式的值处理多种替代方案的方便方法。

当然！`break` 和 `continue` 语句用于循环（如 `for`、`while` 和 `do-while`）中，以改变执行流。

### break 语句
`break` 语句用于提前退出循环，而不执行剩余的迭代。

```c
#include <stdio.h>

int main() {
    // 打印 1 到 10，但当达到 5 时退出循环
    for (int i = 1; i <= 10; i++) {
        if (i == 5) {
            break; // i 为 5 时退出循环
        }
        printf("%d ", i);
    }
    return 0;
}
```

### continue 语句
`continue` 语句用于跳过当前迭代并进入下一次迭代。

```c
#include <stdio.h>

int main() {
    // 打印 1 到 10，跳过偶数
    for (int i = 1; i <= 10; i++) {
        if (i % 2 == 0) {
            continue; // 跳过偶数
        }
        printf("%d ", i);
    }
    return 0;
}
```

#### 比较
在两个示例中：
- `break` 和 `continue` 语句用于 `for` 循环以控制执行流。
- 当遇到 `break` 语句时，循环终止，程序继续执行代码。
- 当遇到 `continue` 语句时，当前迭代终止，循环进入下一次迭代。

## 数组和字符串

### 数组
数组是存储在连续内存位置上的相同类型元素的集合。你可以这样声明、初始化和访问数组元素：

```c
#include <stdio.h>

int main() {
    // 数组的声明和初始化
    int numbers[5] = {10, 20, 30, 40, 50};
    // 访问数组元素
    printf("Element 0: %d\n", numbers[0]);
    printf("Element 1: %d\n", numbers[1]);
    // 修改数组元素
    numbers[2] = 35;
    printf("Element 2: %d\n", numbers[2]);
    return 0;
}
```

### 字符串
在 C 中，字符串是以空字符 (`0`) 结尾的字符数组。你可以这样声明、初始化和操作字符串：

```c
#include <stdio.h>

int main() {
    // 字符串的声明和初始化
    char greeting[] = "Hello, world!";
    // 访问字符串的字符
    printf("First character: %c\n", greeting[0]);
    printf("Second character: %c\n", greeting[1]);
    // 修改字符串的字符
    greeting[7] = 'W'; // 将 'w' 改为 'W'
    printf("Modified string: %s\n", greeting);
    // 遍历字符串
    for (int i = 0; greeting[i] != '\0'; i++) {
        printf("%c", greeting[i]);
    }
    printf("\n");
    return 0;
}
```

在上面的示例中：
- 我们使用字符数组声明并初始化字符串 `greeting`。
- 我们使用数组索引访问并修改字符串的单个字符。
- 我们使用 `for` 循环遍历字符串，直到遇到字符串结束的空字符 `'\0'`。
- 确保字符串以空字符结尾以避免操作或打印时出现未定义行为。

多维数组是数组的数组，允许你以多个维度表示数据，例如矩阵中的行和列。你可以这样在 C 中声明、初始化和访问多维数组元素：

```c
#include <stdio.h>

int main() {
    // 2D 数组 (3x3) 的声明和初始化
    int matrix[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };
    // 访问 2D 数组元素
    printf("Element at row 1, column 1: %d\n", matrix[0][0]);
    printf("Element at row 2, column 3: %d\n", matrix[1][2]);
    // 修改 2D 数组元素
    matrix[1][1] = 10;
    printf("Modified element at row 2, column 2: %d\n", matrix[1][1]);
    // 遍历 2D 数组
    printf("Elements of the 2D array:\n");
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            printf("%d ", matrix[i][j]);
        }
        printf("\n");
    }
    return 0;
}
```




```c
#include <stdio.h>
#include <string.h>

int main() {
    char str[] = "Hello, world!";
    char *substr = strstr(str, "world");
    if (substr != NULL) {
        printf("找到子字符串，位置：%ld\n", substr - str);
    } else {
        printf("未找到子字符串\n");
    }
    return 0;
}
```

### `strtok()`
该函数用于根据分隔符将字符串分割更小的字符串（标记）。

```c
#include <stdio.h>
#include <string.h>

int main() {
    char str[] = "Hello, world! How are you?";
    char *token = strtok(str, " ,!?"); // 使用空格、逗号或感叹号进行分词
    while (token != NULL) {
        printf("%s\n", token);
        token = strtok(NULL, " ,!?"); // 获取下一个标记
    }
    return 0;
}
```

这些只是 C 语言中字符串处理函数的几个示例。`<string.h>` 库提供了许多其他处理字符串的有用函数，如 `strcpy()`、`strcat()`、`strcmp()`、`strlen()` 等。

在 C 语言中，字符数组和字符串字量都用于表示字符串，但它们在声明、初始化和使用上存在一些区别。

#### 字符数组
- 字符数组是固定大小的字符数组，用于存储和操作字符串。
- 你可以修改字符数组的内容。
- 你必须显式地为字符数组添加空终止以指示字符串的结束。
- 字符数组提供了更大的活性，但你需要手动管理内存。

**示例：**
```c
#include <stdio.h>
int main() {
    char str[20]; // 声明一个字符数组
    str[0] = 'H';
    str[1] = 'e';
    str[2] = 'l';
    str[3] = 'l';
    str[4] = 'o';
    str[5] = '\0'; // 字符串空终止
    printf("字符数组：%s\n", str);
    return 0;
}
```

#### 字符串字面量
- 字符串字面量是用双引号括的字符序列。
- 字符串字面量存储在只读内存中，你无法修改其内容。
- 编译器会自动对字面量进行空终止。
- 字面量提供了一种处理字符串的方便方法，无需手动管理内存。

**示例：**
```c
#include <stdio.h>
int main() {
    char *str = "Hello"; // 声明一个字符串字面量
    printf("字符串字面量：%s\n", str);
    return 0;
}
```

#### 比较
- 字符数组和字符串字面量都可以表示字符串。
- 字符数组更灵活且可以修改，而字符串字面量是只读的。
- 字面量会自动空终止，而你需要显式地为字符数组添加空终止。
- 字面量对于简单的字符串操作更方便，而字符数组对于需要动态内存管理的更复杂场景非常有用。

理解字符数组和字符串字面量之间的区别有助于根据程序需求选择合适的方法。

### 指针与内存
在 C 语言中，指针是存储内存地址的变量。它们是处理内存和数据结构的强大工具。以下是 C 语言指针和内存的概述：

#### 指针
- 指针是一个存储另一个变量内存地址的变量。
- 你可以使用星号 `*` 符号跟随变量名来声明指针。
- 你可以使用取地址运算符 `&` 获取变量的内存地址。
- 你可以使用解引用运算符 `*` 访问指针指向的内存地址存储的值。

```c
#include <stdio.h>
int main() {
    int num = 10;
    int *ptr; // 指针声明
    ptr = &num; // 将 num 的地址赋值给 ptr
    printf("num 的值：%d\n", *ptr); // 解引用 ptr 以访问 num 的值
    return 0;
}
```

#### 内存管理
C 语言提供了 `malloc()`、`calloc()`、`realloc()` 和 `free()` 等函数用于动态内存分配和释放。
- `malloc()` 分配指定大小的内存块，并返回指向该块第一个字节的指针。
- `calloc()` 为元素数组分配内存块并将所有字节初始化为零。
- `realloc()` 更改之前分配的内存块的大小。
- `free()` 释放之前由 `malloc()`、`calloc()` 或 `realloc()` 分配的内存。

```c
#include <stdio.h>
#include <stdlib.h>
int main() {
    int *ptr;
    ptr = (int *)malloc(5 * sizeof(int)); // 为 5 个整数分配内存
    if (ptr == NULL) {
        printf("内存分配失败\n");
        return 1;
    }
    // 使用 ptr 访问分配的内存
    ptr[0] = 10;
    ptr[1] = 20;
    ptr[2] = 30;
    // 释放分配的内存
    free(ptr);
    return 0;
}
```

#### 指针与数组
在 C 语言中，数组和指针密切相关。
- 数组名可以视为指向第一个元素的指针。
- 数组可以通过指针算术来访问元素。

```c
#include <stdio.h>
int main() {
    int arr[] = {10, 20, 30};
    int *ptr = arr; // 指针指向数组首
    printf("第一个元素：%d\n", *ptr);
    printf("第二个元素：%d\n", *(ptr + 1)); // 使用指针算术
    return 0;
}
```




要向文件写入数据，你可以使用 `fprintf()` 或 `fputc()` 等函数。

```c
#include <stdio.h>

int main() {
    FILE *file;
    file = fopen("example.txt", "w"); // Open file in write mode
    if (file == NULL) {
        printf("File open failed\n");
        return 1;
    }
    fprintf(file, "Hello, world!\n"); // Write data to the file
    fclose(file); // Close the file
    return 0;
}
```

### 从文件中读取

要从文件中读取数据，你可以使用 `fscanf()` 或 `fgetc()` 等函数。

```c
#include <stdio.h>

int main() {
    FILE *file;
    char str[100];
    file = fopen("example.txt", "r"); // Open file in read mode
    if (file == NULL) {
        printf("File open failed\n");
        return 1;
    }
    fscanf(file, "%s", str); // Read data from the file
    printf("Data read from file: %s\n", str);
    fclose(file); // Close the file
    return 0;
}
```

### 向文件中追加

要向文件中追加数据，你可以在打开文件时使用模式 `"a"`。

```c
#include <stdio.h>

int main() {
    FILE *file;
    file = fopen("example.txt", "a"); // Open file in append mode
    if (file == NULL) {
        printf("File open failed\n");
        return 1;
    }
    fprintf(file, "This text is appended.\n"); // Append data to the file
    fclose(file); // Close the file
    return 0;
}
```

### 错误处理

在执行任何文件操作之前，请务必检查文件是否成功打开。此外，还要适当处理错误。

```c
#include <stdio.h>

int main() {
    FILE *file;
    file = fopen("example.txt", "r");
    if (file == NULL) {
        printf("File open failed\n");
        return 1;
    }
    // File operations...
    fclose(file);
    return 0;
}
```

文件处理是 C 语言编程的一个重要方面，允许你与外部文件交互以进行输入输出操作。C 语言的高级概念涵盖了基础之外的广泛主题，包括枚举、`typedef`、预处理器指令、位运算符、递归和数据结构。以下是每个概念的概述及示例：

### 枚举

枚举允许你定义一组具有固定可能值的命命名常量。

```c
#include <stdio.h>

enum Day {Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday};
int main() {
    enum Day today = Wednesday;
    printf("Today is day number: %d\n", today);
    return 0;
}
```

### typedef

`typedef` 允许你为现有数据类型创建别名，这可以使你的代码更易读且更于维护。

```c
#include <stdio.h>

typedef unsigned long long ULL;
int main() {
    ULL x = 123456789012345;
    printf("Value of x: %llu\n", x);
    return 0;
}
```

### 预处理器指令

预处理器指令是在编译过程之前由预处理器执行的命令。

```c
#include <stdio.h>

#define PI 3.14159
#define SQUARE(x) ((x) * (x))
int main() {
    printf("Value of PI: %f\n", PI);
    printf("Square of 5: %d\n", SQUARE(5));
    return 0;
}
```

### 位运算符

位运算符用于操作操作数的单个二进制位。

```c
#include <stdio.h>

int main() {
    unsigned int x = 5; // Binary representation: 0000 0101
    unsigned int y = 3; // Binary representation: 0000 0011
    printf("Bitwise AND: %u\n", x & y); // Binary AND: 0000 0001
    printf("Bitwise OR: %u\n", x | y);  // Binary OR: 0000 0111
    printf("Bitwise XOR: %u\n", x ^ y); // Binary XOR: 0000 0110
    printf("Bitwise NOT of x: %u\n", ~x); // Binary NOT: 1111 1010
    return 0;
}
```

### 递归

递归是一种函数直接或间接调用自己的技术。

```c
#include <stdio.h>

int factorial(int n) {
    if (n == 0 || n == 1)
        return 1;
    else
        return n * factorial(n - 1);
}
int main() {
    int num = 5;
    printf("Factorial of %d is: %d\n", num, factorial(num));
    return 0;
}
```

### 数据结构

数组、链表、栈、队列、树和图等数据结构用于高效地存储和组织数据。

```c
#include <stdio.h>

struct Node {
    int data;
    struct Node* next;
};
int main() {
    // Example of a linked list
    struct Node* head = NULL;
    // ... implementation ...
    return 0;
}
```




```
addEdge(graph, 1, 2);
addEdge(graph, 2, 3);
printGraph(graph);
return 0;
}
```

这些仅仅是 C 语言中高级数据结构的例子。根据你的应用程序需求，你可能会遇到其他结构，如堆、哈希表或字典树（tries）。理解并实现这些结构将使你能够高效地解决广泛的问题。

## 项目

### 简单银行项目

好的，这是一个用 C 语言实现的简单银行项目。该项目包含了创建账户、存款、取款、余额查询和销户等功能。它使用文件处理将账户信息存储在文本文件中。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// 表示银行账户的结构体
struct Account {
int accountNumber;
char name[50];
float balance;
};

// 创建新账户的函数
void createAccount() {
FILE *file = fopen("accounts.txt", "a");
if (file == NULL) {
printf("Error: Cannot open file.\n");
return;
}

struct Account newAccount;
printf("Enter account number: ");
scanf("%d", &newAccount.accountNumber);
printf("Enter name: ");
scanf("%s", &newAccount.name);
printf("Enter initial balance: ");
scanf("%f", &newAccount.balance);
fprintf(file, "%d %s %.2f\n", newAccount.accountNumber, newAccount.name, newAccount.balance);
fclose(file);
printf("Account created successfully.\n");
}

// 向账户存款的函数
void deposit() {
int accountNumber;
float amount;
printf("Enter account number: ");
scanf("%d", &accountNumber);
printf("Enter amount to deposit: ");
scanf("%f", &amount);

FILE *file = fopen("accounts.txt", "r+");
if (file == NULL) {
printf("Error: Cannot open file.\n");
return;
}

struct Account currentAccount;
while (fscanf(file, "%d %s %f", &currentAccount.accountNumber, currentAccount.name, &currentAccount.balance) != EOF) {
if (currentAccount.accountNumber == accountNumber) {
currentAccount.balance += amount;
fseek(file, -sizeof(struct Account), SEEK_CUR);
fprintf(file, "%d %s %.2f\n", currentAccount.accountNumber, currentAccount.name, currentAccount.balance);
fclose(file);
printf("Deposit successful. Current balance: %.2f\n", currentAccount.balance);
return;
}
}
fclose(file);
printf("Account not found.\n");
}

// 从账户取款的函数
void withdraw() {
int accountNumber;
float amount;
printf("Enter account number: ");
scanf("%d", &accountNumber);
printf("Enter amount to withdraw: ");
scanf("%f", &amount);

FILE *file = fopen("accounts.txt", "r+");
if (file == NULL) {
printf("Error: Cannot open file.\n");
return;
}

struct Account currentAccount;
while (fscanf(file, "%d %s %f", &currentAccount.accountNumber, currentAccount.name, &currentAccount.balance) != EOF) {
if (currentAccount.accountNumber == accountNumber) {
if (currentAccount.balance >= amount) {
currentAccount.balance -= amount;
fseek(file, -sizeof(struct Account), SEEK_CUR);
fprintf(file, "%d %s %.2f\n", currentAccount.accountNumber, currentAccount.name, currentAccount.balance);
fclose(file);
printf("Withdrawal successful. Current balance: %.2f\n", currentAccount.balance);
return;
} else {
fclose(file);
printf("Insufficient balance.\n");
return;
}
}
}
fclose(file);
printf("Account not found.\n");
}

// 查询账户余额的函数
void balanceInquiry() {
int accountNumber;
printf("Enter account number: ");
scanf("%d", &accountNumber);

FILE *file = fopen("accounts.txt", "r");
if (file == NULL) {
printf("Error: Cannot open file.\n");
return;
}

struct Account currentAccount;
while (fscanf(file, "%d %s %f", &currentAccount.accountNumber, currentAccount.name, &currentAccount.balance) != EOF) {
if (currentAccount.accountNumber == accountNumber) {
fclose(file);
printf("Account balance: %.2f\n", currentAccount.balance);
return;
}
}
fclose(file);
printf("Account not found.\n");
}

// 销户的函数
void closeAccount() {
int accountNumber;
printf("Enter account number to close: ");
scanf("%d", &accountNumber);

FILE *file = fopen("accounts.txt", "r");
if (file == NULL) {
printf("Error: Cannot open file.\n");
return;
}

FILE *tempFile = fopen("temp.txt", "w");
if (tempFile == NULL) {
printf("Error: Cannot create file.\n");
fclose(file);
return;
}

struct Account currentAccount;
int found = 0;
while (fscanf(file, "%d %s %f", &currentAccount.accountNumber, currentAccount.name, &currentAccount.balance) != EOF) {
if (currentAccount.accountNumber != accountNumber) {
fprintf(tempFile, "%d %s %.2f\n", currentAccount.accountNumber, currentAccount.name, currentAccount.balance);
} else {
found = 1;
}
}
fclose(file);
fclose(tempFile);
rename("temp.txt", "accounts.txt");

if (found) {
printf("Account closed successfully.\n");
} else {
printf("Account not found.\n");
}
}
```




```c
printf("Welcome to Kaun Banega Crorepati!\n");

for (int i = 0; i < NUM_QUESTIONS; i++) {
    printf("\nQuestion %d\n", i + 1);
    displayQuestion(questions[i]);

    if (lifelines[0]) {
        printf("Lifelines: 1\. 50-50 ");
    }

    if (lifelines[1]) {
        printf("2\. Phone a Friend ");
    }

    if (lifelines[2]) {
        printf("3\. Audience Poll ");
    }
    printf("\n");

    int answer;
    printf("Enter your answer (1-4): ");
    scanf("%d", &answer);

    if (answer == 0) {
        printf("You have chosen to quit the game.\n");
        break;
    }

    if (answer == 1 && lifelines[0]) { // 50-50 lifeline
        lifelines[0] = 0;
        int correctOption = questions[i].correctOption;
        int option1 = correctOption;
        int option2;
        do {
            option2 = rand() % 4;
        } while (option2 == correctOption);
        printf("Options %d and %d eliminated.\n", option1 + 1, option2 + 1);
        printf("Enter your answer (1-4): ");
        scanf("%d", &answer);
    }

    if (answer == 2 && lifelines[1]) { // Phone a friend lifeline
        lifelines[1] = 0;
        int friendAnswer = rand() % 4 + 1;
        printf("Your friend says option %d.\n", friendAnswer);
        printf("Enter your answer (1-4): ");
        scanf("%d", &answer);
    }

    if (answer == 3 && lifelines[2]) { // Audience poll lifeline
        lifelines[2] = 0;
        int correctOption = questions[i].correctOption;
        int audiencePoll[4] = {0};
        audiencePoll[correctOption]++;
        for (int j = 0; j < 100; j++) {
            int randomOption;
            do {
                randomOption = rand() % 4;
            } while (randomOption == correctOption);
            audiencePoll[randomOption]++;
        }
        printf("Audience poll results:\n");
        for (int j = 0; j < 4; j++) {
            printf("Option %d: %d%%\n", j + 1, (audiencePoll[j] * 100) / 101);
        }
        printf("Enter your answer (1-4): ");
        scanf("%d", &answer);
    }

    if (checkAnswer(questions[i], answer)) {
        printf("Correct answer! You win Rs.%d\n", PRIZE_MONEY[i]);
        currentPrize = PRIZE_MONEY[i];
    } else {
        printf("Wrong answer! Game over. You win Rs.%d\n", currentPrize);
        break;
    }
}
return 0;
}
```

该项目通过从文本加载问题来模拟“Kaun Banega Crorepati”游戏，允许玩家回答问题并提供救救手段来协助他们。玩家每个正确答案可获得虚拟货币，回答错误则游戏结束。

## 计算机班录取报名表

以下是用 C 语言实现的计算机班录取报名表的基础版本。该程序提示用户输入姓名、年龄、性别和课程偏好等详情以申请计算机班。

```c
#include <stdio.h>

struct Student {
    char name[50];
    int age;
    char gender;
    char course[50];
};

int main() {
    struct Student student;
    printf("Computer Class Admission Form\n");
    printf("----------------------------\n");
    // 输入详情
    printf("Enter your name: ");
    scanf("%s", student.name);
    printf("Enter your age: ");
    scanf("%d", &student.age);
    printf("Enter your gender (M/F): ");
    scanf(" %c", &student.gender);
    printf("Enter your course preference: ");
    scanf("%s", student.course);
    // 显示输入的详情
    printf("\nEntered Details\n");
    printf("Name: %s\n", student.name);
    printf("Age: %d\n", student.age);
    printf("Gender: %c\n", student.gender);
    printf("Course Preference: %s\n", student.course);
    // 录取确认
    printf("\nAdmission form submitted successfully! Thank you.\n");
    return 0;
}
```

此代码允许学生输入其计算机班的录取详情，然后显示所输入的信息。你可以通过添加对用户输入的验证检查、将输入的详情保存到文件中，或根据需要实现额外功能来扩展此程序。

作者：Hambirrao Sarnobat

