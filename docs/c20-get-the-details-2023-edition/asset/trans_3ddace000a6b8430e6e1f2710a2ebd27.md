
### 导出组

```cpp
export module math;

export {

    int mul(int fir, int sec);
    void doTheMath();

}
```

## 4.2.3.6 导出命名空间

除了使用导出组，你还可以使用导出命名空间。

### 导出命名空间

```cpp
export module math;

export namespace math {

    int mul(int fir, int sec);
    void doTheMath();

}
```

当客户端使用来自导出命名空间的名称时，必须对它们进行限定。

![](img/c60a87adb7f61e2e82071d081bbb389a_131_0.png)

### 选择性导出命名空间

你还可以在命名空间内使用导出说明符、导出组和导出命名空间。在这种情况下，只有导出的名称对模块使用者可见。以下示例使用了在命名空间内导出名称的三种方式。

### 在命名空间内选择性导出

```cpp
export module math;

namespace math {

    export int mult(int fir, int sec); // use with math::mult
    export {
        void doTheMath();            // use with math::doTheMath
    }
    export namespace mathDetails {   // use with math::mathDetails::add
        int add(int fir, int sec);
    }
    int div(int fir, int sec);       // no use outside the module

}
```

函数 div 不能在模块 math 外部使用，并且必须完全限定：math::div(6, 2)。

只有不具有内部链接的名称才能被导出。

## 4.2.3.7 导入

借助 import，你可以导入模块、模块分区或头文件单元。

上下文关键字 import

```cpp
export module math;

import math.sin;
import math::cos;
import <vector>;
```

import 是上下文关键字。这意味着 import 是一个标识符，只在某些上下文中才是关键字。在导入一个可导入实体之前，你应该先编译它。否则，你可能会导入该可导入实体的旧版本。

## 4.2.3.8 模块结构指南

让我们考察一下如何组织模块的指南。

### 模块结构的指南

```cpp
module;                        // starts the global module fragment

#include <headers for libraries not modularized so far>

export module math;            // exporting module declaration; starts the module preamble

import <importing of other modules>

<non-exported declarations>    // names only visible inside the module

export namespace math {

    <exported declarations>    // exported names

}

module :private;               // not part of the interface

// part of the module implementation that does not cause a recompilation
```

本指南只有一个目的：为你提供一个模块结构，并让你了解我接下来要写的内容。那么，这个模块结构有什么新意呢？

- 以关键字 `module` 开头的*全局模块片段*是可选的。在它之后、模块声明之前，这里是包含头文件的正确位置。这里只允许出现预处理指令。
- 必需的导出模块声明 `export module math` 会启动所谓的*模块前导*，随后是*模块范围*，其结束于翻译单元的末尾。模块前导由导入声明组成，而模块范围主要由导出声明组成。
- 模块范围可以包含 `private module fragment`。私有模块片段是模块实现的一部分，并且只能在主模块接口单元中使用。对私有模块片段的修改不需要重新编译该模块。
- 你可以在模块范围的开头导入模块。被导入的模块具有模块链接，并且在模块外部不可见。这一观察同样适用于未导出的声明。
- 我将导出的名称放在命名空间 `math` 中，它与模块同名。
- 该模块只声明了名称。下面我们来讨论模块接口与实现的分离。

本质上，模块结构可归结为三个部分。

![](img/c60a87adb7f61e2e82071d081bbb389a_133_0.png)

## 4.2.3.9 模块接口单元与模块实现单元

当模块变大时，你应该将其组织为一个模块接口单元和一个或多个模块实现单元。遵循前面提到的模块结构指南，我将重构 math 模块的前一版本。

### 4.2.3.9.1 模块接口单元

### 模块接口单元

```cpp
// mathInterfaceUnit.ixx

module;

#include <vector>

export module math;

export namespace math {

    int add(int fir, int sec);

    int getProduct(const std::vector<int>& vec);

}
```

- 模块接口单元包含导出模块声明：`export module math`（第 7 行）。
- 名称 `add` 和 `getProduct` 被导出（第 11 行和第 13 行）。
- 一个模块只能有一个模块接口单元。

### 4.2.3.9.2 模块实现单元

### 模块实现单元

```cpp
// mathImplementationUnit.cpp

module math;

#include <numeric>

namespace math {

    int add(int fir, int sec) {
        return fir + sec;
    }

    int getProduct(const std::vector<int>& vec) {
        return std::accumulate(vec.begin(), vec.end(), 1, std::multiplies<int>());
    }

}
```

- 模块实现单元包含非导出模块声明：`module math;`（第 3 行）。
- 一个模块可以有多个模块实现单元。

### 4.2.3.9.3 主程序

客户端使用模块 math

```cpp
// client3.cpp

#include <iostream>
#include <vector>

import math;

int main() {

    std::cout << '\n';

    std::cout << "math::add(2000, 20): " << math::add(2000, 20) << '\n';

    std::vector<int> myVec{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

    std::cout << "math::getProduct(myVec): " << math::getProduct(myVec) << '\n';

    std::cout << '\n';

}
```

从用户的角度看，包含了模块 math（第 6 行），并添加了命名空间 math。

当我的解释变得依赖于编译器时，我会将它们放在单独的提示框中。如果你决定尝试，这些信息通常很宝贵。

### 带有私有模块片段的模块声明文件

```cpp
// mathInterfaceUnit2.ixx

module;

#include <numeric>
#include <vector>

export module math;

export namespace math {

    int add(int fir, int sec);

    int getProduct(const std::vector<int>& vec);

}

module :private;

int add(int fir, int sec) {
    return fir + sec;
}

int getProduct(const std::vector<int>& vec) {
    return std::accumulate(vec.begin(), vec.end(), 1, std::multiplies<int>());
}
```

第 18 行中的 `module :private;` 表示私有模块片段的开始。修改模块声明文件的这个可选最后部分不会导致该模块的导入者重新编译。

## 4.2.3.11 子模块与模块分区

当你的模块增长时，你会希望将其功能划分为可管理的组件。C++20 模块提供了两种方法：子模块和分区。

### 4.2.3.11.1 子模块

一个模块可以导入模块，然后重新导出它们。在以下示例中，模块 math 导入了子模块 math.math1 和 math.math2。

### 模块 math

```cpp
// mathModule.ixx

export module math;

export import math.math1;
export import math.math2;
```

表达式 `export import math.math1` 导入模块 `math.math1`，并将其作为模块 `math` 的一部分重新导出。

为完整起见，下面给出模块 `math.math1` 和 `math.math2`。我使用句点将模块 `math` 与其子模块分隔开。这个句点不是必需的。

### 子模块 math.math1

```cpp
// mathModule1.ixx

export module math.math1;

export int add(int fir, int sec) {
    return fir + sec;
}
```

### 子模块 math.math2

```cpp
// mathModule2.ixx

export module math.math2;

export {
    int mul(int fir, int sec) {
        return fir * sec;
    }
}
```

如果仔细看，你会注意到模块 `math` 中的导出语句有一个细微差别。`math.math1` 使用导出说明符，而 `math.math2` 使用导出组或导出块。

从客户端的角度看，使用 `math` 模块很直接。

