
在这个例子中，首先定义了 `constexpr MAX = 20;`，然后对 `char *createName();` 进行了原型，表示该函数返回一个指向一个或多个字符的指针。

在 `main()` 函数中，定义了一个局部变量 `char *name;`，但没有初始化。接着，调用了 `createName()` 并将其返回值赋值给 `name`。注意，`name` 和函数的返回类型都是 `char *` 类型。

在调用 `createName()` 时，注意局部变量 `char *temp = new char[MAX];` 既被定义了，又通过运算符 `new()` 分配了内存以指向堆上固定数量的内存。用户被提示输入名称，该名称存储在 `temp` 中。然后，局部变量 `temp` 从 `createName()` 返回。

在 `createName()` 中，重要的是 `temp` 的内存必须由堆内存组成，这样它才能在该函数的作用域之外持续存在。在这里，存储在 `temp` 中的地址的副本将被复制到栈上为为函数返回值预留的区域。幸运的是，该地址指向堆内存。`main()` 中的赋值语句 `name = createName();` 将捕获此地址并将其复制到 `name` 变量中，而 `name` 是 `main()` 的局部变量。由于在 `createName()` 中分配的内存在堆上，这部分内存在函数完成后仍然存在。

同样重要的是，如果在 `createName()` 中将 `temp` 定义为 `char temp[MAX];`，那么组成 `temp` 的内将存在栈上，并且对于 `createName()` 是局部的。一旦 `createName()` 返回到 `main()`，该变量的内存将从栈中弹出且无法正常使用——即使该地址在 `main()` 内的指针变量中被捕获。这是 C++ 中另一个潜在的指针陷阱。从函数返回指针时，务必确保指针所指向的内存在范围超出函数的范围。

此示例的输出为：

```
Enter name: Gabrielle

Name: Gabrielle
```

现在我们已经理解了指针如何作为函数的参数和函数的返回值使用，让我们继续前进，检查进一步的指针的细微差别。

### 在指针中使用 const 修饰符

`const` 修饰符可以用几种不同的方式来修饰指针。`const` 关键字可以应用于被指向的数据、指针本身，或两者兼有。通过以这些方式使用 `const` 修饰符，C++ 允许保护程序中可能被初始化但永远不再被修改的值。让我们检查这些不同的场景。我们还将带有 `const` 修饰符的指针与函数的返回值结合，以理解这些不同场景中哪些是合理的。

## 指向常量对象的指针

可以指定指向常量对象的指针，以便所指向的对象不能被直接修改。指向此对象的解引用指针不能在任何赋值中用作左值（l-value）。左值意味着可以被修改的值，它出现在赋值的左侧。

让我们引入一个简单的例子来理解这种情况：

```cpp
// const 修饰的 str;，被指向的数据将是 const
char *const constData = "constant";
const char *moreConstData = nullptr;
// 定义了普通字符串。其中一个使用 strcpy 加载
char *regularString = nullptr;
char *anotherRegularString = new char[8]; // 大小刚好适应
                                // 此字符串
strcpy(anotherRegularString, "regular");
// 尝试修改标记为 const 的数据将无效
// strcpy(constData, "Can I do this?"); // 不行
```

### 将指针作为函数的返回值

函数可以通过其 `return` 语句返回数据的指针。通过函数的 `return` 语句返回指针时，请确保所指向的内存在函数调用完成后仍然存在。不要返回指向函数局部栈内存的指针。也就是说，不要返回指向函数内栈定义的局部变量的指针。然而，返回函数内部使用 `new()` 分配的内存指针是可以接受的。因为所分配的位于堆上，它在函数调用结束后仍会存在。

让我们来看一个例子来解释这些概念：

https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/blob/main/Chapter03/Chp3-Ex7.cpp

```cpp
#include <iostream>
#include <iomanip>
using std::cin;
using std::cout;
using std::endl;
using std::setw;
constexpr int MAX = 20;
```

```cpp
[[nodiscard] char *createName(); // 函数原型
int main()
{
    char *name = nullptr; // 指针的声明与初始化
    // 函数将分配内存
    name = createName();
    cout << "Name: " << name << endl;
    delete [] name; // 删除分配的内存（在不同的作用域中）
    return 0; // 这可能会出错
}

[[nodiscard] char *createName()
{
    char *temp = new char[MAX];
    cout << "Enter name: " << flush;
    cin >> setw(MAX) >> temp; // 确保 temp 不溢出
    return temp;
}
```

在这个例子中，`constexpr MAX = 20;` 被定义了，然后对 `char *createName();` 进行了原型，表示该函数返回一个指向一个或多个字符的指针。

在 `main()` 函数中，定义了一个局部变量 `char *name;`，但没有初始化。接着，调用了 `createName()` 并将其返回值赋值给 `name`。注意，`name` 和函数的返回类型都是 `char *` 类型。

在调用 `createName()` 时，注意局部变量 `char *temp = new char[MAX];` 既被定义了，又通过运算符 `new()` 分配了内存以指向堆上固定数量的内存。用户被提示输入名称，该名称存储在 `temp` 中。然后，局部变量 `temp` 从 `createName()` 返回。

在 `createName()` 中，重要的是 `temp` 的内存必须由堆内存组成，这样它才能在函数的作用域之外持续存在。在这里，存储在 `temp` 中的地址的副本将被复制到栈上为为函数返回值预留的区域。幸运的是，该地址指向堆内存。`main()` 中的赋值语句 `name = createName();` 将捕获此地址并将其复制到 `name` 变量中，而 `name` 是 `main()` 的局部变量。由于在 `createName()` 中分配的内存在堆上，这部分内存在函数完成后仍然存在。

同样重要的是，如果在 `createName()` 中将 `temp` 定义为 `char temp[MAX];`，那么组成 `temp` 的内将存在栈上，并且对于 `createName()` 是局部的。一旦 `createName()` 返回到 `main()`，该变量的内存将从栈中弹出且无法正常使用——即使该地址在 `main()` 内的指针变量中被捕获。这是 C++ 中另一个潜在的指针陷阱。从函数返回指针时，务必确保指针所指向的内存在范围超出函数的范围。

此示例的输出为：

```
Enter name: Gabrielle

Name: Gabrielle
```

## 使用指向常量对象的常量指针

指向常量对象的常量指针是指指向特定对象且不可修改数据的指针。指针本身必须初始化为一个给定的对象，而该对象（理想情况下）已使用适当的值进行了初始化。该对象或指针都不得被修改，也不能在赋值中用左值（l-values）。

这里是一个示例：

```cpp
// 定义两个普通字符串并使用 strcpy() 加载
char *regularString = new char[36]; // 为下方的字符串留空间
strcpy(regularString, "I am a modifiable string");
char *anotherRegularString = new char[21]; // 为下面的
// 字符串留空间
strcpy(anotherRegularString, "I am also modifiable");
// 定义指向常量对象的常量指针；必须初始化
const char *const constStringAndPtr = regularString; // 正确
// 尝试更改指针或数据是非法的
constStringAndPtr = anotherRegularString; // 不行！不能
// 修改地址
strcpy(constStringAndPtr, "Nope"); // 不行！不能修改数据
```

在这个示例中，声明了两个 `char *` 变量，`regularString` 和 `anotherRegularString`。每一个都用一个字符串字面量初始化。接下来，我们引入了 `const char *const constStringAndPtr = regularString;`，这是一个指向数据的常量指针，且该数据也被视为常量。注意，这个变量不能被初始化，因为指针本身在随后的赋值中不能作为左值。你可能还希望确保此指针初始化为一个有意义的值，因为所指向的数据也无法更改（如 `strcpy` 语句所示，它将产生编译器错误）。在指针和所指向的数据上同时使用 `const` 是保护数据的一种严谨方法。

# 提示 – 解密指针声明

在阅读复杂的指针声明时，从后往前（从右到左）读声明通常很有帮助。例如，指针声明 `const char *p1 = "hi!";` 被解释为 `p1` 是一个指向（一个或多个）常量字符的指针。声明 `const char *const p2 = p1;` 则被读为 `p2` 是一个指向（一个或多个）常量字符的常量指针。

最后，让我们继续了解对指针进行 `const` 修饰的影响，这些指针可以作为函数参数或函数的返回值。

# 将指向常量对象的指针用函数参数和返回类型

在栈上拷贝用户定义类型的参数可能非常耗时。将指针作为函数参数传递速度更快，但它允许被引用的对象在函数作用域内被修改。将指向常量对象的指针作为函数参数传递，可以为该参数同时提供速度和安全性。在相关的函数作用域内，被引用的指针简单地不能作为左值。这一原则同样适用于函数的返回值。对所指向的数据进行 `const` 修饰，强制要求函数的调用者也必须将返回值存储在指向常量对象的指针中，从而确保对象的长期不可变性。

让我们来看一个示例来检查这些概念：

https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/blob/main/Chapter03/Chp3-Ex8.cpp
