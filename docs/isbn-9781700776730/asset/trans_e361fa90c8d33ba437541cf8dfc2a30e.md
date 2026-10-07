

这些程序中的每一个将按照如下方式输出：

( 2.667)
(3.000)

注意，如果要输出的值小于字段宽度，将插入填充字符作为填充。然而，如果一个值大于指定的宽度，它不会被截断。它将占据其所需的空间。宽度设置仅适用于下一次插入或提取，之后宽度将隐式地设置为零。

我们之前提到过，`employ1.cpp` 程序产生的输出并不十分理想。请使用格式操纵符将程序重写为 `employ2.cpp`，以更易接受的格式显示结果。忘记包含 `omanip`。

## 基本数据类型

编写一个程序 `size.cpp`，打印基本数据类型（`char`、`int`、`short int`、`long int`、`float`、`double`、`long double`）的大小。还要打印指向这些数据类型的指针的大小。使用 `sizeof` 运算符查找大小，并使用 `cout` 对象打印。

## Capture程序输出

当你提交计算机实验作业时，需要包含一个包含程序生成的输出的文件。虽然你可能想简单地将屏幕上显示的输出复制并粘贴到文件中，但通常程序生成的输出无法完全显示在屏幕上，并且通常会滚出屏幕。请遵循下面的说明将程序的输出捕获到名为 `csis.txt` 的文件中：

- 在所有生成输出到文件的 `.cpp` 源代码中包含 `fstream` 库的头文件：

```
#include <fstream>
```

- 在包含 `main()` 函数的 `.cpp` 源代码中包含以下全局声明（在 `using namespace std;` 之后）：

```
ofstream csis;
```

- 在除包含 `main()` 的文件外的所有生成输出的 `.cpp` 源代码中包含以下全局声明（在 `using namespace std;` 之后）：

```
extern ofstream csis;
```

- 在 main() 的变量声明之后以下语句。它将打开 `csis.txt` 文件以捕获你的输出。

```
csis.open("csis.txt");
```

对于程序中的每个输出语句，你都应该包含一条相应的语句将相同的数据输出到 `csis.txt` 文件：

```
cout << "Hello" << endl;
csis << "Hello" << endl;
```

最后，main() 中 `return` 语句之前的最后语句应该是：

```
csis.close();
```

这会在程序结束执行前刷新输出缓冲区并关闭 `csis.txt` 文件。

这是一个将其输出捕获到 `csis.txt` 文件的 C++ 程序的示例：

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
ostream csis;

void main() {
    int a = 3, b = 4, c = 5;

    csis.open("csis.txt");

    cout << "All you need is love." << endl;
    csis << "All you need is love." << endl;

    cout << "a" << " " << a << " b = " << b
         << " c = " << c << endl;
    csis << "a" << a << " b = " << b
         << " c = " << c << endl;

    cout << "A";
    csis << "A";

    cout << endl;
    csis << endl;

    cout << "Samantha" << endl;
    csis << "Samantha" << endl;

    csis.close();
}
```

```
// output from csis.txt file

All you need is love.
a = 3 b = 4 c = 5
^
Haley
Samantha
```

## 如果你正在使用 Xcode，请遵循这些说明：

我们现在必须告诉 Xcode 将我们的 `csis.txt` 输出文件放在项目文件夹中。

选择 Product | Scheme | Edit Scheme

选择 Options 标签并在 Working Directory 旁边打勾。

在 Use Custom Working Directory 下，导航到你的项目文件夹并点击 OK。

程序执行后，程序的输出文件 `csis.txt` 现在将出现在项目文件夹中。

## 第 3 章 数据类型与数据保护

数据类型与数据保护
数据类型与数据保护作业
数据类型与数据保护作业源代码

## 数据类型与数据保护

类型 = 结构体 + 函数
我们将查看 C++ 如何实现新数据类型并利用数据保护。

### C 结构体
假设我们想要构建一个包含几部电梯的系统。在 C 中，通常通过创建一个结构体来存储关于每部电梯的数据来解决问题：

```
struct elevator {
    int floorSelected;
    int floorNumber;
}
```

创建了一个结构体，包含了我们想要关于每个电梯的所有信息。要创建一个变量，我们使用 `struct` 关键字配合结构体名：

```
struct elevator e;
```

或者，我们可以使用 `typedef` 标识符并说：

```
typedef struct elevator Elevator;
Elevator e;
```

第二个例子更像是一个内置数据类型。

#### 作为函数参数的 C 结构体指针
当我们创建一个用于处理结构体的函数时，我们必须将指向结构体的指针作为参数传递给函数。

下面的函数初始化结构体的字段：

```
void initialize (Elevator *e) {
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

我们可以看到，在我们任何想要使用 `Elevator` 结构体的地方，都必须对指针解引用。我们被迫使用指针而不是按值传递 `Elevator` 结构体，是因为我们正在修改函数作用域之外的变量。按值传递 `Elevator` 结构体只会创建一个局部变量！

### C++ 结构体
让我们看看可能如何在 C++ 中解决相同的问题。

我们知道一个类型具有特征和行为。这些特征统称为：

- 函数成员
- 数据成员

数据成员代表状态（特征），函数成员代表可以对变量执行的操作（行为）。

```cpp
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

#### 成员函数声明
在 C++ 中，在调用函数之前必须声明成员函数。

- 函数定义在结构体内部。
- 这些函数的作用域是结构体。
- 这些不是全局名称。

#### 作用域运算符
在定义成员函数时，我们使用作用域运算符 `::` 告诉编译器该函数与特定类型关联。

```
Elevator::initialize() {
    floorSelected = 0;
    floorNumber = 0;
}
```

成员函数位于结构体的范围内，它可以访问结构体的其他成员。因此，访问数据成员不需要指针。

```cpp
int main() {
  Elevator e;

  e.initialize();
  e.selectFloor();
  e.go();
}
```

定义自定义类型的变量与定义内置类型的变量一样。然而，我们不需要像在 C 中那样创建 `typedef`。

### 数据保护
所以我们已经看到在 C++ 中如何通过扩展结构体以包含函数来表示一个类型。如果程序仍然直接访问结构体的所有成员，数据就是未受保护的，程序员可以进入并搞乱它。

保护数据有三个原因：

1. 有时修改一个数据元素可能需要修改另一个以维护对象的完整性。如果你拒绝程序员对某些数据元素的访问，这将迫使他们使用你设计来维护完整性的成员函数。
2. 在结构体中，所有成员都可能被修改，程序员很难知道应该使用哪个接口。通过拒绝对结构体内部某些成员的访问，他们只能使用公共接口允许的成员。
3. 它有助于你隔离错误。假设程序员对数据成员进行了错误的修改，突然你的系统某处出现了错误。如果所有成员都是公开的，该错误可能来自任何地方。但如果其中某些成员是私有的，你就知道问题一定来自有权限访问数据的函数。

