
**导入头单元的源文件 `head.cpp`**

```cpp
// head.cpp

import "head.h";

void hello() {

    std::cout << '\n';

    std::cout << "Hello World: header unit\n";

    std::cout << '\n';

}
```

**使用该模块的主程序 `helloWorld13.cpp`**

```cpp
// helloWorld13.cpp

import "head.h";

int main() {

    hello();

}
```

我将为 Microsoft Visual C++ 编译器和 GCC 编译器创建并使用来自头文件 `head.h` 的头单元。与官方文档[标准 C++ 模块](https://clang.llvm.org/docs/StandardCPlusPlusModules.html#header-units)不同，我无法在 Clang 编译器上掌握头单元。

## Microsoft Visual C++ 编译器

以下是使用头单元的必要步骤。

### 创建模块 `head.h.ifc` 并使用它

```bat
cl.exe /std:c++latest /EHsc /exportHeader head.h
cl.exe /std:c++latest /EHsc /headerUnit head.h=head.h.ifc head.cpp
cl.exe /std:c++latest /EHsc /headerUnit head.h=head.h.ifc helloWorld13.cpp head.obj
```

-   第 1 行中的标志 `/exportHeader` 会根据头文件 `head.h` 创建 ifc 文件 `head.h.ifc`。
-   实现文件 `head.cpp`（第 2 行）和客户端文件 `helloWorld13.cpp`（第 3 行）使用该头单元。标志 `/headerUnit head.h=head.h.ifc` 导入该头文件，并告诉编译器/链接器指定头文件对应的 ifc 文件名。

![](img/c60a87adb7f61e2e82071d081bbb389a_149_0.png)

使用模块 `head.h.ifc`

## GCC 编译器

创建和使用该模块包括三个步骤。

### 创建模块 `head.h.gcm` 并使用它

```text
g++ -fmodules-ts -fmodule-header head.h -std=c++20
g++ -fmodules-ts -c -std=c++20 head.cpp
g++ -fmodules-ts -std=c++20 head.h.gcm helloWorld13.cpp -o helloWorld13
```

-   第 1 行创建模块 `head.h.gcm`。标志 `-fmodule-header` 指定 `head.h` 是一个头单元。
-   下一行创建对象文件 `head.o`。
-   最后，第 3 行创建可执行文件，它隐式引用模块 `head.h.gcm`。

## 一个缺点

头单元有一个缺点。并非所有头文件都是可导入的。哪些头文件可导入由实现定义[^5]，但 C++ 标准保证所有标准库头文件都是可导入的头文件。可导入的范围不包括 C 头文件。它们被包装在 `std` 命名空间中。例如，`<cstring>` 是 `<string.h>` 的 C++ 包装器。你可以快速识别被包装的 C 头文件，因为模式是：`xxx.h` 变成 `cxxx`。

[^5]: https://en.cppreference.com/w/cpp/language/ub

## 其他方面

### 宏

头单元支持宏，但模块会忽略它们。以下程序由模块 `macro`、用作头单元的头文件 `macro.h` 以及主程序 `macroMain.cpp` 组成。

**主程序 `macroMain.cpp`**

```cpp
// macroMain.cpp

#include <iostream>

import macro;
import "macro.h";

int main() {

    std::cout << '\n';

    std::cout << MACRO_HEADER_UNIT << '\n';
    std::cout << MACRO_MODULE << '\n';

    std::cout << '\n';
}
```

程序 `macroMain.cpp` 使用两个宏 `MACRO_HEADER_UNIT`（第 12 行）和 `MACRO_MODULE`（第 13 行）。`MACRO_HEADER_UNIT` 定义在头单元 `macro.h` 中，而 `MACRO_MODULE` 定义在模块 `macro` 中。

**头单元 `macro.h`**

```cpp
// macro.h

#define MACRO_HEADER_UNIT "macro header unit"
```

**模块 `macro.ixx`**

```cpp
// macro.ixx

module;

#define MACRO_MODULE "macro module"

export module macro;
```

该程序的编译包括以下三个步骤：

### 导入头单元和宏

```bat
cl.exe /std:c++latest /EHsc /exportHeader macro.h
cl.exe /std:c++latest /EHsc /c macro.ixx
cl.exe /std:c++latest /EHsc /headerUnit macro.h=macro.h.ifc macroMain.cpp macro.obj
```

第 1 行创建头单元，第 2 行编译模块，最后一行同时使用两者。正如预期的那样，最终编译步骤失败，因为宏 `MACRO_MODULE`（`macroMain.cpp` 中的第 13 行）在主程序中不可见。

![](img/c60a87adb7f61e2e82071d081bbb389a_151_0.png)

宏 `MACRO_MODULE` 不可见

你不能从模块中导出宏，但可以将头文件包含到模块中。这个头文件可以含有宏。全局模块片段是插入头文件并因此插入宏的正确位置。

```cpp
// macro.ixx

module;

#include "macro.h"

export module macro;
```

### 模块中的模板

我经常听到这样的问题：模块如何导出模板？当你实例化一个模板时，其定义必须可用。因此，模板定义存放在头文件中。从概念上讲，模板的使用具有以下结构。

### 不使用模块

**`templateSum.h`**

**函数模板 `sum` 的定义**

```cpp
// templateSum.h

template <typename T, typename T2>
auto sum(T fir, T2 sec) {
    return fir + sec;
}
```

**`sumMain.cpp`**

**模板 `sum` 的使用**

```cpp
// sumMain.cpp

#include "templateSum.h"

int main() {

    sum(1, 1.5);

}
```

主程序包含头文件 `templateSum.h`。调用 `sum(1, 1.5)` 会触发模板实例化。在这种情况下，编译器会根据函数模板 `sum` 生成具体的函数 `sum`，它接受一个 `int` 和一个 `double` 作为参数。如果你想可视化这个过程，请使用 [C++ Insights](https://cppinsights.io/) 上的示例。

[https://cppinsights.io/](https://cppinsights.io/)

编译该程序的命令行与前面的命令行没有不同。因此，我跳过它，直接展示程序的输出：

![](img/c60a87adb7f61e2e82071d081bbb389a_154_0.png)

函数模板 `sum` 的使用

使用模块后，我们得到一种新的链接方式。

### 从头文件迁移到模块

广义上讲，从头文件迁移到模块时有两种选择。你可以使用头单元代替头文件，或者在一个模块或一个模块分区中重新实现你的头文件。从实现者和使用者的角度来看，这两种选择都非常方便。

为方便起见，在本节剩余部分，我将模块和模块分区统称为模块。

头单元对实现者来说无需多虑。头文件是模块的良好起点，因为它们已经提供了系统所需的模块化。头单元的用户必须将 `#include` 指令替换为新的 `import` 语句，并添加一个分号（`;`）。

**用头单元替换头文件**

```text
#include <vector> => import <vector>;
#include "math.h" => import "math.h";
```

使用模块对用户来说没有显著区别。导入模块与包含头文件非常相似。

**用模块替换头文件**

```text
#include <vector> => import vector;
#include "math.h" => import math;
```

模块的负担落在实现者身上，但借助头单元，实现者可以成功完成这种迁移。因此，一个合理的迁移策略是从头单元开始迁移。只有不可导入的头文件才必须实现为模块。此外，新功能应实现为具名模块。

## 提炼信息

-   模块克服了头文件和宏的缺陷。导入它们确实没有额外成本，而且与宏不同，导入顺序无关紧要。此外，它们还克服了名称冲突。
-   一个模块由一个模块接口单元和任意多个模块实现单元组成。模块接口必须具有导出模块声明，模块实现单元必须具有非导出模块声明。模块接口中未导出的名称具有模块链接，不能在模块外部使用。
-   模块可以包含头文件，也可以导入并重新导出其他模块。
-   C++20 中的标准库尚未模块化。在 C++20 中，构建你的模块是一项具有挑战性的任务。
-   为了组织大型软件系统，模块提供了两种方式：子模块和分区。与分区不同，子模块可以独立存在。
-   借助头单元，你可以将 include 语句替换为 import 语句，编译器会自动生成一个模块。
-   头单元确实支持宏，但模块不支持。
-   从头文件迁移到模块或模块分区的一个合理策略是从头单元开始迁移。只有不可导入的头文件才必须实现为模块。此外，新功能应实现为具名模块。

