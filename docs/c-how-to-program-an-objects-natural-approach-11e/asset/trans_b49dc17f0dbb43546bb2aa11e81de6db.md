
然而，C++ 核心准则建议将“小型且时间关键”的函数声明为**内联**。[18,19] 图 5.7 使用内联函数 `cube`（第 9–11 行）计算立方体的体积。

```cpp
// fig05_07.cpp
// inline function that calculates the volume of a cube.
#include <iostream>
using namespace std;

// Definition of inline function cube. Definition of function appears
// before function is called, so a function prototype is not required.
// First line of function definition also acts as the prototype.
inline double cube(double side) {
    return side * side * side; // calculate cube
}

int main() {
    double sideValue; // stores value entered by user
    cout << "Enter the side length of your cube: ";
    cin >> sideValue; // read value from user

    // calculate cube of sideValue and display result
    cout << "Volume of cube with side "
         << sideValue << " is " << cube(sideValue) << '\n';
}
```

```text
Enter the side length of your cube: 3.5
Volume of cube with side 3.5 is 42.875
```

**图 5.7** | *计算立方体体积的内联函数。*

### 检查点

- 1. **(判断正误)** 在函数定义中将 `inline` 放在函数返回类型之前，会强制编译器在函数被调用的每个位置（在适当情况下）生成函数体代码的副本，以避免函数调用。
  **答案：** 错误。实际上，编译器可以忽略 `inline` 限定符。
- 2. **(填空)** 可重用的内联函数通常放在 ______ 中，以便其定义可以在使用它们的每个源文件中内联。
  **答案：** 头文件。
- 3. **(判断正误)** 如果更改内联函数的定义，任何调用该函数的代码都会自动重新编译。
  **答案：** 错误。实际上，如果更改内联函数的定义，必须重新编译任何调用该函数的代码。

18. C++ 核心准则。访问日期：2023 年 4 月 14 日。https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rf-inline。

19. 关于内联函数细微之处的详尽常见问题解答，请访问 https://isocpp.org/wiki/faq/inline-functions。

```cpp
int squareByValue(int number);  // prototype (for value pass)
void squareByReference(int& numberRef);  // prototype (for reference pass)

int main() {
    int x{2};  // value to square using squareByValue
    int z{4};  // value to square using squareByReference

    // demonstrate squareByValue
    cout << "x = " << x << " before squareByValue\n";
    cout << "Value returned by squareByValue: "
         << squareByValue(x) << '\n';
    cout << "x = " << x << " after squareByValue\n";

    // demonstrate squareByReference
    cout << "z = " << z << " before squareByReference\n";
    squareByReference(z);
    cout << "z = " << z << " after squareByReference\n";
}

// squareByValue multiplies number by itself, stores the
// result in number and returns the new value of number
int squareByValue(int number) {
    return number *= number;  // caller's argument not modified
}

// squareByReference multiplies numberRef by itself and stores the result
// in the variable to which numberRef refers in function main
void squareByReference(int& numberRef) {
    numberRef *= numberRef;  // caller's argument modified
}
```

```text
x = 2 before squareByValue
Value returned by squareByValue: 4
x = 2 after squareByValue

z = 4 before squareByReference
z = 16 after squareByReference
```

图 5.8 | 按值传递实参和按引用传递实参。（第 2 部分，共 2 部分。）

### 函数内作为别名的引用

引用也可以在函数内用作其他变量的别名（不过它们通常与函数一起使用，如图 5.8 所示）。例如，以下代码

```cpp
int count{1};  // declare integer variable count
int& cRef{count};  // create cRef as an alias for count
++cRef;  // increment count (using its alias cRef)
```

通过别名 cRef 递增 count。引用变量必须在其声明中初始化，并且不能重新赋值为其他变量的别名。在这个意义上，引用是常量。对别名（即引用）执行的所有操作实际上都是对原始变量执行的。别名只是原始变量的另一个名称。除非它是对常量的引用（下面讨论），否则引用的初始化器必须是左值——即可以出现在赋值左侧的内容，例如变量名。引用不能用常量或*值*表达式初始化——也就是只能出现在赋值右侧的内容，例如计算结果。

### const 引用

若要指定不允许引用形参修改调用方中的对应实参，请在形参声明中把 const 限定符放在类型名之前。例如，考虑一个 displayName 函数：

```cpp
void displayName(std::string name) {
    std::cout << name << '\n';
}
```

调用时，它接收其 string 实参的一个*副本*。由于 string 对象可能很大，这种复制操作可能会降低应用程序的性能。因此，string 对象（以及一般对象）应通过引用传递给函数。

此外，displayName 函数不需要修改其实参。因此，遵循最小权限原则，我们会将形参声明为

```cpp
const std::string& name
```

从右向左读，name 形参是一个对常量 string 的引用。我们获得了按引用传递 string 的性能。此外，displayName 将实参视为常量，因此 displayName 不能修改调用方中的值。

### 返回局部变量的引用是危险的

当返回对局部非静态变量的引用时，该引用指向一个在函数返回时被丢弃的变量。试图访问这样的变量会产生未定义行为，常常导致程序崩溃或数据损坏。²² 对未定义变量的引用称为悬空引用。这是一种逻辑错误，编译器通常会发出警告。软件工程团队通常有策略要求代码在部署前必须无警告地编译。你可以通过使用编译器的选项让编译器将警告视为错误，从而在你的团队中强制执行这一点。

### 检查点

- 1. **(判断正误)** 无论你通过按值传递，还是通过带引用形参的按引用传递来传递变量，在函数调用中都只是按名称提及这些变量。编译器会检查函数原型和定义，以确定你采用的是按值传递还是按引用传递。
  **答案：** 正确。
- 2. **(判断正误)** 引用变量可以重新赋值为其他变量的别名。
  **答案：** 错误。引用变量必须在其声明中初始化，并且不能重新赋值为其他变量的别名。在这个意义上，引用是常量。
- 3. **(填空)** 若要指定不允许引用形参修改调用方中的对应实参，请在形参声明中把 ________ 限定符放在类型名之前。
  **答案：** const。

22. C++ 核心准则。访问日期：2023 年 4 月 14 日。https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rf-dangle。

## 5.13 默认实参

程序经常从多个位置以相同的实参值调用某个特定形参对应的函数。在这种情况下，可以为相应形参指定默认实参。当程序在函数调用中省略具有默认实参的形参对应的实参时，编译器会重写该函数调用，插入该实参的默认值。

### 带默认实参的 boxVolume 函数

图 5.9 演示了使用默认实参计算盒子体积。boxVolume 的函数原型（第 7 行）通过在每个形参右侧放置 = 1，指定所有三个形参的默认值均为 1。

```cpp
// fig05_09.cpp
// Using default arguments.
#include <iostream>
using namespace std;

// function prototype that specifies default arguments
int boxVolume(int length = 1, int width = 1, int height = 1);

int main() {
   // no arguments--use default values for all dimensions
   cout << "The default box volume is: " << boxVolume();

   // specify length; default width and height
   cout << "\nThe volume of a box with length 10,\n"
        << "width 1 and height 1 is: " << boxVolume(10);

   // specify length and width; default height
   cout << "\nThe volume of a box with length 10,\n"
        << "width 5 and height 1 is: " << boxVolume(10, 5);

   // specify all arguments
   cout << "\nThe volume of a box with length 10,\n"
        << "width 5 and height 2 is: " << boxVolume(10, 5, 2)
        << '\n';
}

// function boxVolume calculates the volume of a box
int boxVolume(int length, int width, int height) {
   return length * width * height;
}
```

```text
The default box volume is: 1

The volume of a box with length 10,
width 1 and height 1 is: 10
```

**图 5.9** | 使用默认实参。（第 1 部分，共 2 部分。）
