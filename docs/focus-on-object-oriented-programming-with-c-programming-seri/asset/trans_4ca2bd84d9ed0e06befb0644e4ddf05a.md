

每个程序将按以下方式更改输出：

```
(   2.667)
(3.000)
```

请注意，如果要输出的值小于字段宽度，则会插入填充字符作为填充。但是，宽度大于指定宽度的值不会被截断。它将获取所需的内容。宽度设置仅适用于下一次插入或提取，之后宽度会隐式设置为零。

我们之前提到，employ1.cpp 程序生成的输出并不十分理想。请使用格式操纵符将程序重写为 employ2.cpp，以更可接受的格式显示结果。别忘了包含 iomanip。

## 基本数据类型

编写一个名为 size.cpp 的程序，打印基本数据类型（char、int、short int、long int、float、double、long double）的大小。同时打印每种数据类型指针的大小。使用 sizeof 运算符查找大小，并使用 cout 对象打印它们。

## 捕获程序输出

提交计算机实验室作业时，需要包含一个包含程序生成的输出的文件。您可能很想直接将屏幕上显示的输出复制粘贴到文件中，但程序生成的输出通常无法全部显示在屏幕上，并且通常会被滚出屏幕。请按照以下说明将程序的输出捕获到名为 `csis.txt` 的文件中：

- 在所有生成输出到文件的 `.cpp` 源代码中包含 `fstream` 库的头文件：

```
#include <fstream>
```

- 在包含 `main()` 函数的 `.cpp` 源代码中包含以下全局声明（在 `using namespace std;` 之后）：

```
ofstream csis;
```

- 在所有生成输出的 `.cpp` 源代码中（不包括包含 `main()` 的文件），包含以下全局声明（在 `using namespace std;` 之后）：

```
extern ofstream csis;
```

- 在 `main()` 的变量声明之后添加以下语句。它将打开 `csis.txt` 文件以捕获输出。

```
csis.open("csis.txt");
```

- 对于程序中的每个输出语句，都应包含适当的语句将相同的数据输出到 `csis.txt` 文件：

```
cout << "Hello" << endl;
csis << "Hello" << endl;
```

- 最后，`main()` 中 `return` 语句之前的最后一条语句应该是：

```
csis.close();
```

这将刷新输出缓冲区并在程序结束执行前关闭 `csis.txt` 文件。

- 以下是一个将其输出捕获到 `csis.txt` 文件的 C++ 程序示例：

```
// testB.h
void foo();
// testB.cpp
#include <iostream>
#include <fstream>
#include "testB.h"
using namespace std;
extern ofstream csis;
void foo() {
    cout << "Haley" << endl;
    csis << "Haley" << endl;
}
```

```
// testA.h
#include "testB.h"
void main();

// testA.cpp
#include <iostream>
#include <fstream>
#include "testA.h"
using namespace std;
ofstream csis;
void main() {
    int a = 3, b = 4, c = 5;
    csis.open("csis.txt");
    cout << "All you need is love." << endl;
    csis << "All you need is love." << endl;
    cout << "a = " << a << " b = " << b
         << " c = " << c << endl;
    csis << "a = " << a << " b = " << b
         << " c = " << c << endl;
    cout << 'A';
    csis << 'A';
    cout << endl;
    csis << endl;
    foo();
    cout << "Samantha" << endl;
    csis << "Samantha" << endl;
    csis.close();
}
```

```
// output from csis.txt file

All you need is love.

a = 3 b = 4 c = 5

A

Haley

Samantha
```

## 如果您使用 Xcode，请遵循以下说明：

我们现在必须告诉 Xcode 将 csis.txt 输出文件放在项目文件夹中。

选择 Product | Scheme | Edit Scheme

选择 Options 选项卡，并在 Working Directory 旁边打勾。

在 Use Custom Working Directory 下，导航到您的项目文件夹并单击 OK。

程序执行后，程序的输出文件 csis.txt 将出现在项目文件夹中。

- 数据类型与数据保护
- 数据类型与数据保护作业
- 数据类型与数据保护作业源代码

## 数据类型与数据保护

### 类型 = 结构体 + 函数

我们将了解 C++ 如何实现新数据类型并利用数据保护。

### C 结构体

假设我们想构建一个由多部电梯组成的系统。在 C 中，我们通常通过创建一个 `struct` 来存储每部电梯的数据来解决这个问题：

```
struct elevator {
    int floorSelected;
    int floorNumber;
};
```

创建了一个结构体，用于保存我们想要记住的每部电梯的所有信息。要创建变量，我们使用 `struct` 关键字和结构体名称：

```
struct elevator e;
```

或者，我们可以使用 `typedef` 标识符并说：

```
typedef struct elevator Elevator;
Elevator e;
```

第二个示例的行为更像内置数据类型。

### 作为函数参数的 C 结构体指针

当我们创建一个作用于 `struct` 的函数时，必须将指向 `struct` 的指针作为参数传递给函数。

以下函数初始化 `struct` 的字段：

```
void initialize(Elevator *e) {
  e->floorSelected = 0;
  e->floorNumber = 0;
}
```

我们创建另一个函数来选择楼层：

```
void selectFloor(Elevator *e, int floor) {
  e->floorSelected = floor;
}
```

我们可以看到，每当我们想要使用 `Elevator` 结构体时，都必须解引用指针。我们被迫使用指针而不是按值传递 `Elevator` 结构体，因为我们正在修改函数作用域之外的变量。按值传递 `Elevator` 结构体只会创建一个局部变量！

### C++ 结构体

让我们看看如何在 C++ 中解决同样的问题。

我们知道，一个类型具有特征和行为。C++ 将类型实现为扩展的 `struct`，其中包含函数声明和数据声明。统称为成员：

- 函数成员
- 数据成员

数据成员表示变量的状态（特征），函数成员表示可以对数据成员执行的操作（行为）。

```
#include <iostream>
using namespace std;
#define FLOORS 10
struct Elevator {
    int floorSelected;
    int floorNumber;
    void initialize();
    void selectFloor(int floor);
    void go();
};
```

### 成员函数声明

在 C++ 中，所有成员函数都必须声明完整的原型，即在函数被调用之前必须声明所有参数类型。

- 函数在 `struct` 内部声明。
- 这些成员函数的作用域是 `struct` 的作用域。
- 这些不是全局名称。

### 作用域解析运算符

在定义成员函数时，我们必须使用作用域解析运算符 (::) 告诉编译器该函数与特定类型相关联。

```
void Elevator::initialize() {
    floorSelected = 0;
    floorNumber = 0;
};
```

由于成员函数在 `struct` 的作用域内，它可以访问 `struct` 的其他成员。因此，无需指针即可访问和修改 `struct` 的数据成员！

```
int main() {
    Elevator e;
    e.initialize();
    e.selectFloor();
    e.go();
}
```

定义用户定义类型的变量就像定义内置类型的变量一样。但是，我们不必像在 C 中那样创建 typedef。

调用成员函数时，必须指定一个对象。调用成员函数或向对象发送消息就像选择结构体的数据成员一样。由于用户不必将变量的地址传递给函数，因此成员函数调用更易于使用且更清晰。

### 数据保护

我们已经看到，在 C++ 中，类型是通过扩展结构体来包含函数和数据来表示的。但是，如果程序仍然可以直接访问结构体中的所有成员，数据就不受保护，程序员可以进入其中并搞乱一切。

我们需要保护数据的原因有三个：

- 1. 有时修改一个数据元素可能需要修改另一个数据元素以保持对象的完整性。如果你可以拒绝程序员访问某些数据元素，这将迫使他们使用成员函数，你可以设计这些成员函数以保持对象的完整性。
- 2. 在 `struct` 中，所有成员都可能被修改，程序员可能难以知道应该使用哪个接口。通过拒绝访问 `struct` 中的某些成员，他们只能使用属于公共接口的成员。
- 3. 这有助于你隔离错误。假设程序员对数据成员进行了错误的修改，突然系统中某个地方出现了错误。如果所有成员都是公共的，该错误可能来自任何地方。但是，如果某些成员是私有的，你知道问题一定来自有权访问数据的函数。

