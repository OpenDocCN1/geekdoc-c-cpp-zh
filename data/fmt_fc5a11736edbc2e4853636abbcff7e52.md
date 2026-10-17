
图 15.14 | 展示 C++ 标准库类模板 `vector`。（第 1/4 部分）

# 第 15 章 更好的 C++：引入对象技术

```cpp
// 打印 integers1 的大小和内容
cout << "Size of vector integers1 is " << integers1.size();
cout << "\nvector after initialization:" << endl;
outputVector(integers1);
```

```cpp
// 打印 integers2 的大小和内容
cout << "\nsize of vector integers2 is " << integers2.size();
cout << "\nvector after initialization:" << endl;
outputVector(integers2);
```

```cpp
// 输入并打印 integers1 和 integers2
cout << "\nEnter 17 integers:" << endl;
inputVector(integers1);
inputVector(integers2);
```

```cpp
cout << "\nafter print, the vectors contain:\n"
cout << "integers1:" << endl;
outputVector(integers1);
cout << "integers2:" << endl;
outputVector(integers2);
```

```cpp
// 在 vector 对象上使用不等运算符 (!=)
cout << "\nintegers1 != integers2" << endl;
```

```cpp
if (integers1 != integers2)
    cout << "\nintegers1 and integers2 are not equal" << endl;
```

```cpp
// 使用 integers1 作为初始化器创建 vector integers3；
// 打印大小和内容
vector<int> integers3(integers1); // 拷贝构造函数
```

```cpp
cout << "\nSize of vector integers3 is " << integers3.size();
cout << "\nvector after initialization:" << endl;
outputVector(integers3);
```

```cpp
// 使用重载赋值运算符 (=)
cout << "\nassigning integers2 to integers1:" << endl;
integers1 = integers2; // 将 integers2 赋值给 integers1
```

```cpp
cout << "integers1:" << endl;
outputVector(integers1);
cout << "integers2:" << endl;
outputVector(integers2);
```

```cpp
// 在 vector 对象上使用相等运算符 (=)
cout << "\nevaluating: integers1 == integers2" << endl;
```

```cpp
if (integers1 == integers2)
    cout << "\nintegers1 and integers2 are equal" << endl;
```

```cpp
// 使用方括号创建右值
cout << "\nintegers1[5] is " << integers1[5];
```

图 15.14 | 演示 C++ 标准库类模板 `vector`。（4 部分中的 2 部分）

## 15.15 C++ 标准库类模板 vector 简介

```cpp
68 // 使用方括号创建左值
69 cout << "\n\nAssigning 1000 to integers1[5]" << endl;
70 integers1[5] = 1000;
71 cout << "integers1: " << endl;
72 outputVector(integers1);
73
74
75 // 尝试使用越界索引
76 try
77 {
78 cout << "\nAttempt to display integers1.at( 5 )" << endl;
79 integers1.at(5) << endl; // 错误：越界
80 }
81
82 catch (const out_of_range &ex)
83 {
84 cout << "\n exception occurred: " << ex.what() << endl;
85 }
```

```cpp
87 // 输出 vector 内容
88 void outputVector(const vector<int> &array)
89 {
90 size_t i; // 声明控制变量
91
92 for (i = 0; i < array.size(); ++i)
93 {
94 cout << setw(12) << array[i];
95
96 if ((i + 1) % 4 == 0) // 每行输出 4 个数
97 cout << endl;
98 }
99
100 if (i % 4 == 0)
101 cout << endl;
102 }
103
104 // inputVector(vector<int> &array)
105 void inputVector(vector<int> &array)
106 {
107 for (size_t i = 0; i < array.size(); ++i)
108 cin >> array[i];
109 }
```

| Size of vector integers1 is 7 | vector after initialization: |

| :--- | :--- |

| 0 | 0 |

| 0 | 0 |

| Size of vector integers2 is 10 | vector after initialization: |

| 0 | 0 |

| 0 | 0 |

![](img/fa81e3d0bce03c9026ba997d7b_611_0.png)

integers 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17

输入后vector包含：

| integers1: | 2 | 4 |

| :--- | :--- |

| 5 | 6 | 7 |

| integers2: | 8 | 9 | 10 |

| :--- | :--- |

| 12 | 13 | 14 | 15 | 16 | 17 |

评估：integers1 != integers2

integers1 和 integers2 不相等

vector integers3 的大小为 7

初始化后：

| 1 | 3 | 4 |

| :--- | :--- | :--- |

| 5 | 6 | 7 |

将 integers2 赋值给 integers1：

| integers1: | 8 | 9 | 10 | 11 |

| :--- | :--- | :--- | :--- | :--- |

| 12 | 13 | 14 | 15 | 16 | 17 |

| integers2: | 8 | 9 | 10 | 11 |

| :--- | :--- | :--- | :--- | :--- |

| 12 | 13 | 14 | 15 | 16 | 17 |

评估：integers1 == integers2

integers1 和 integers2 相等

integers1[5] 为 13

将 1000 赋值给 integers1[5]

| integers1: | 8 | 9 | 10 | 11 |

| :--- | :--- | :--- | :--- | :--- |

| 12 | 1000 | 14 | 15 | 16 | 17 |

尝试显示 integers1.at(5)

发生异常：无效的 vector<T>下标

图 15.14 | 演示 C++ 标准库类模板 `vector`。（4 部分中的 4 部分）

## 创建 vector 对象

第13-14 行创建了两个存储 `int` 类型值的 `vector` 对象——`integers1`包含七个元素，而`integers2`包含十个元素。默认情况下，每个 `vector` 对象的所有元素都设置为0。注意，`vector` 可以定义为存储任何数据类型，只需将其放在相应类型的 `vector<int>` 中。这种指定 `vector` 中存储类型的表示法与15.3 节中随函数模板引入的模板表示相似。

## vector 成员函数 size；函数 outputVector

第 17 行使用 `vector` 成员函数 `size` 获取 `integers1` 的大小（即元素个数）。要调用成员函数，你使用点运算符（`.`）来访问它，就像访问 `struct` 和 `union` 成员一样。第 19 行将 `integers1` 传递给函数 `outputvector`（88–102 行），使用方括号 `[]`（第 94 行）来获取 `vector` 中每个元素的值用于输出。这种表示法与访问数组元素值的方法相似。第 22 行和第 24 行对 `integers2` 执行相同任务。

类模板 `vector` 的成员 `size` 返回 `vector` 中元素的个数，其值为 `size_t`（在许多系统中表示为无符号 `int`）。结果如下

## 函数 inputVector

第 28–39 行将 `integers1` 和 `integers2` 传递给函数 `inputVector`（105–109 行），以便从源读取每个 `vector` 元素的值。该函数使用方括号 `[]` 构建左值，用于存储每个 `vector` 元素中的输入值。

## 比较 vector 对象的不等性

第 40 行演示了 `vector` 对象可以使用 `!=` 运算符相互比较。如果两个 `vector` 的内容不相等，运算符返回 `true`；否则返回 `false`。

## 用另一个 vector的内容初始化 vector

C++ 标准库类模板 `vector` 允许你创建一个新的 `vector` 对象，该对象用现有 `vector` 的内容初始化。第 45 行创建了一个 `vector` 对象 `integers3` 并用 `integers1` 的拷贝对其初始化。这调用了 `vector` 的拷贝构造函数来执行对象拷贝。你将在第 18 章学习拷贝构造函数是如何工作的。第 47–49 行使用 `integers3` 的大小和内容证明了它的初始化正确。

## 赋值并比较 vector 的相等性

第 53 行赋值 `integers2`，证明了赋值运算符 (`=`) 可以用于 `vector` 对象。

# 15.16 总结 583

本节总结

在本节中，我们演示了 C++ 标准库类模板 `vector`，这是一个健壮且可重用的类，可以替代 C 风格的指针数组。在第 18 章中，你将看到 `vector` 如何通过“重载”C++ 内置运算符来实现许多功能，并且你将学习如何以类似的方式为自己的类自定义操作符。例如，我们创建了一个 `Array` 类，它像模板 `vector` 一样改进了基本数组的功能。我们的 `Array` 类还提供了额外功能，例如通过运算符 `>>` 和 `<<` 输入和输出数组流。

# 15.16 总结

在本章中，你学习了 C++ 对 C 的增强。我们展示了使用 `cin` 和 `cout` 的基础 C 风格输入输出，并探索了 C++ 标准库文件。我们讨论了通过消除函数调用开销来提高性能的内联函数。你学习了如何使用 C++ 引用参数进行按引用传递，这允许你为现有变量创建别名。你学习了通过提供具有相同名称但不同签名的函数来实现多个函数的重载；此类函数可以使用可以使用不同类型或数量的参数来执行相同或相似的任务。然后，我们演示了使用函数模板进行重载的更简单的方法，其中定义的一个函数可以用于不同的类型。在第 16 章中，你将学习如何实现自己的类并在应用程序中使用这些类的对象。

## 总结

## 第 15.2 节 C++

- C++ 改进了 C 的功能，并提供了面向对象编程（OOP；p550）能力，这提高了软件的生产力、质量和易用性。
- C++ 由 Bjarne Stroustrup 在贝尔实验室开发，最初是“带有类的 C”。

## 第 15.3 节 简单程序：两个整数相加

- C++ 文件名具有几种扩展名中的一种，例如 `.cpp`、`.cxx` 或 `.C`（大写）。
- C++ 允许你用 `//` 开头开始注释，并将行的剩余部分作为注释文本。C++ 程序员也可以使用由 `/*` 和 `*/` 分隔的注释。
- 在任何向屏幕输出内容或使用 C++ 风格输入输出从键盘输入的程序中，必须包含输入/输出头文件 `<iostream>` (p. 552)。
- 与 C 一样，每个 C++ 程序都从 `main` 函数开始。main 左侧的关键字表示“返回”整数值。
- 在 C 中，你不需要为函数指定返回类型。然而，C++ 要求为所有函数指定返回类型（可能是 `void`），否则将发生语法错误。
- 声明可以放置在 C++ 程序的任何位置，但它们必须在程序中使用变量之前出现。
- 输出流对象（`std::cout`；p. 552）和流插入运算符（`<<`；p. 552）用于在屏幕上显示文本。
- 标准输入流对象（`std::cin`；p. 552）和流提取运算符（`>>`；p. 552）用于从键盘获取值。
- 流操纵符 `std::endl` (p. 553) 输出换行符并“刷新输出缓冲区”。
- 符号 `std::cout` 指定 `cout` 属于“命名空间” `std`。
- 在单个语句中使用多个流插入运算符（`<<`）被称为连接、级联流插入操作（p. 553）。

## 第 15.4 节 C++ 标准库

- C++ 程序由组合的类和函数组成。你可以编写形成 C++ 程序所可能需要的每个部分。然而，大多数 C++ 程序员都利用了现有类和函数的丰富性，这些位于 C++ 标准库（p. 554）。

## 第 15.5 节 头文件

- C++ 标准库分为许多部分，每个部分都有其所有的头文件。头文件包含了库中每个部分相关函数的原型。头文件还包含各种类和函数的定义，以及这些函数所需的常量。
- `.h` 中的头文件名称是“旧式”头文件，它们已由 C++ 标准库文件取代。

## 第 15.6 节 内联函数

- C++ 提供了内联函数 (p. 556) 来帮助减少函数开销。在定义中函数的返回类型之前放置 `inline` 修饰符 (p. 556) 是“建议”编译器在原地生成函数代码的副本，以避免函数调用。

## 第 15.8 节 引用和引用参数

- 许多编程语言向函数传递参数的两种方法是按值传递和按引用传递。
- 当按值传递参数时，会创建其值的副本并将其（在函数栈上）传递给被调用函数。对副本的修改不影响者中的原始值。
- 按引用传递，引用让被调用函数能够直接访问调用者的数据，并在被调用函数选择时对其进行修改。
- 引用参数 (p. 559) 是函数调用中其对应参数的别名。
- 类型安全链接确保调用了正确的重载函数，并且参数的类型与参数的类型一致。
- 要指示函数参数是按引用传递，只需在原型中参数的类型后跟一个取地址符 `&`；在函数头中列出参数类型时使用相同的符号。
- 一旦引用声明为任何变量的别名，所有认为在别名上执行的操作（即引用）实际上都是在原始变量上执行的。别名仅仅是原始变量的另一个名称。

## 第 15.9 节 空参数列表

- 在 C++ 中，通过在括号中写 `void` 或留空来指定空参数列表。

## 第 15.10 节 默认参数

- 重复使用特定参数的相同参数值调用函数并不罕见。在这种情况下，程序员可以指定此类参数有一个默认参数 (p. 564)，即传递给该参数的默认值。
- 当程序省略默认参数的参数时，编译器会插入该参数的默认值以作为参数传递给函数调用。
- 默认参数必须是函数列表中最右侧（尾）的参数。
- 默认参数应与函数原型一起指定。

## 第 15.11 节 一元作用域解析符

- C++ 提供了一元作用域运算符（`::`；p. 566），当局部变量在作用范围内时访问全局变量。

## 第 15.12 节 函数重载

- C++ 允许定义具有相同名称的函数，只要它们具有不同的参数集。这种能力是函数重载 (p. 667)。
- 当调用重载函数时，C++ 编译器通过检查数量、类型和顺序来选择函数。
- 重载函数通过其签名 (p. 568) 进行区分。

## 第 15.13 节 函数模板

- 重载函数用于执行涉及不同类型的相似操作。如果每个类型的程序逻辑相同，可以使用函数模板 (p. 570) 执行得更加紧凑方便。
- 程序员编写单个函数模板。根据调用时提供的参数，C++ 自动生成函数模板特化 (p. 570) 来处理每个类型。
- 所有函数模板都以关键字开头，后面跟着在角括号内的模板参数列表 (p. 571)。
- 类型参数 (p. 571) 是基本类型或用户定义类型的占位符。它们用于指定函数的参数类型、函数的返回类型以及在函数体内声明变量。

## 第 15.14 节 对象技术简介和 UML

- 统一建模语言（UML；p. 573）是一种图形化语言，允许构建自己的面向对象设计的人使用通用符号。
- 面向对象设计（OOD；p. 573）用真实世界对象建模软件。它利用了类关系，特定类的对象（p. 573）具有相同的特征。它还利用了继承关系，新创建的对象类是通过吸收现有类的特征并添加自身的独特特征得出的。OOD 将数据（属性；p. 573）和函数（行为；p. 573）封装到对象中——数据和函数是紧密结合的。
- 对象具有信息隐藏（p. 574）属性——对象不允许知道其他对象的实现方式。
- 面向对象编程（OOP）允许程序员将面向对象设计实现为工作的系统。

# 第 15 章 更好的更好的 C++：引入对象技术

- 标准输入流对象（`std::cin`；p. 552）和流提取运算符（`>>`；p. 552）用于从键盘获取值。
