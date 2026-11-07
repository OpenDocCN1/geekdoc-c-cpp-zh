
```text
fig16_05.cpp:12:47: error: declaration of 'cube' must be imported from module 'deitel.math' before it is required
   std::cout << "cube(3) = " << deitel::math::cube(3) << '\n';
                               ^
/usr/src/lesson16/fig16_04-05/deitel.math.ixx:12:8: note: declaration here is not visible
   int cube(int x) {
   ^
1 error generated.
```

## 16.7 全局模块片段

正如我们提到的，某些头文件无法作为**头文件单元**编译，因为它们需要**预处理状态**，例如在翻译单元或其他头文件中定义的宏。通过将这些头文件放入**全局模块片段**<sup>48</sup>，可以在**模块单元**中 `#included` 它们以供使用

```cpp
module;
```

你应将其放在模块单元开头的 `module` 声明之前。**全局模块片段**只能包含预处理指令。**模块接口单元**可以导出在**全局模块片段**中 `#included` 的声明，因此 `import` 该模块的其他**实现单元**可以使用该声明。<sup>49</sup> 来自所有模块单元的**全局模块片段**都会被放入**全局模块**，该全局模块还包含非模块翻译单元中的非模块化代码，例如包含 `main` 的翻译单元。

## 16.8 将接口与实现分离

在第 9 章和第 10 章中，我们使用 `.h` 头文件和 `.cpp` 源代码文件定义类，以将类的接口与其实现分离。模块也支持将接口与实现分离：

- 你可以将接口和实现拆分到不同文件中（如第 16.8.1—16.8.2 节所示）。
- 你可以在一个源文件中定义接口和实现（在第 16.8.3 节讨论）。

### 16.8.1 示例：模块实现单元

有时将大型模块拆分为更小、更易管理的部分会很有帮助——例如，当一个开发团队正在处理同一模块的不同方面时。你可以将模块定义拆分到多个源文件中。让我们使用**主模块接口单元**来表示模块的接口，并使用单独的源代码文件表示**模块的实现细节**。

- 48. “C++ 标准：10 模块——10.4 全局模块片段。”访问于 2023 年 4 月 18 日。https://timsong-cpp.github.io/cppwp/n4861/module.global.frag。
- 49. Dos Reis，《使用 C++ 模块编程：面向实际软件开发者的指南》。

**主模块接口单元**

`deitel.math` 模块的主模块接口单元（图 16.6）导出 `deitel::math` 命名空间（第 7—10 行），其中包含函数 `average` 的函数原型，该函数计算 `vector<int>` 元素的平均值。

```cpp
// Fig. 16.6 deitel.math.ixx
// Primary module interface for a module named deitel.math.
export module deitel.math; // introduces the module name

import <vector>;

export namespace deitel::math {
   // calculate the average of a vector<int>'s elements
   double average(const std::vector<int>& values);
}
```

**图 16.6**  |  名为 `deitel.math` 的模块的主模块接口。

**模块实现单元**

所有包含模块声明但不含 `export` 关键字（图 16.7 第 3 行）的文件都是模块实现单元（通常定义在 `.cpp` 文件中）。<sup>50</sup> 这些文件可以将较大的模块拆分为多个源文件，使其更易管理。第 3 行表明该文件是 `deitel.math` 模块的模块实现单元。模块实现单元会隐式导入其模块的接口。编译器将主模块接口单元及其对应的模块实现单元合并为一个单一命名模块，其他翻译单元可以导入该模块。<sup>51</sup> 第 10—13 行在命名空间中实现 average 函数，该命名空间必须与主模块接口单元（图 16.6）中包含 average 原型的命名空间同名。

```cpp
// Fig. 16.7 deitel.math-impl.cpp
// Module implementation unit for the module deitel.math.
module deitel.math; // this file's contents belong to module deitel.math

import <numeric>;
import <vector>;

namespace deitel::math {
   // average function's implementation
   double average(const std::vector<int>& values) {
      double total{std::accumulate(values.begin(), values.end(), 0.0)};
      return total / values.size();
   }
}
```

**图 16.7**  |  模块 `deitel.math` 的模块实现单元。

- 50. “C++20 标准：10 模块——10.1 模块单元与范围。”访问于 2023 年 4 月 18 日。https://timsong-cpp.github.io/cppwp/n4861/moduleunit。
- 51. “C++20 标准：10 模块。”访问于 2023 年 4 月 18 日。https://timsong-cpp.github.io/cppwp/n4861/module。

**使用该模块**

图 16.8 中的主程序导入模块 `deitel.math`（第 7 行），并调用其 average 函数（第 17 行）来计算整数 vector 元素的平均值。

```cpp
// fig16_08.cpp
// Using the deitel.math module’s average function.
import <algorithm>;
import <iostream>;
import <iterator>;
import <vector>;
import deitel.math; // import the deitel.math module

int main() {
    std::ostream_iterator<int> output(std::cout, " ");
    std::vector<int> integers{1, 2, 3, 4};

    std::cout << "vector integers: ";
    std::copy(integers.begin(), integers.end(), output);

    std::cout << "\naverage of integers' elements: "
              << deitel.math::average(integers) << '\n';
}
```

```text
vector integers: 1 2 3 4
average of integers' elements: 2.5
```

**图 16.8** | 使用 `deitel.math` 模块的 average 函数

**在 Visual C++ 中编译此示例**

将 `deitel.math.ixx` 文件添加到你的 Visual C++ 项目中，就像你在第 16.6.1 节中所做的那样。确保你的项目在其源文件文件夹中包含：

- `deitel.math.ixx`——主模块接口单元，
- `deitel.math-impl.cpp`——模块实现单元，以及
- `fig16_08.cpp`——主应用程序。

然后，只需运行你的项目即可编译该模块和主应用程序。

**在 g++ 中编译此示例**

在 g++ 中，使用第 16.6.6 节介绍的命令，将标准库头文件 `<algorithm>`、`<iostream>`、`<iterator>`、`<numeric>` 和 `<vector>` 编译为头文件单元。接下来，编译主模块接口单元：

```bash
g++ -fmodules-ts -c -x c++ deitel.math.ixx
```

然后，编译模块实现单元：

```bash
g++ -fmodules-ts -c deitel.math-impl.cpp
```

现在我们有目标文件 `deitel.math.o` 和 `deitel.math-impl.o`，它们分别表示模块的接口和实现。最后，编译主应用程序并将其与 `deitel.math.o` 和 `deitel.math-impl.o` 链接：

```bash
g++ -fmodules-ts fig16_08.cpp deitel.math.o deitel.math-impl.o
             -o fig16_08
```

**在 clang++ 中编译此示例**

在 clang++ 中，使用第 16.6.6 节中的命令，将标准库头文件 `<algorithm>`、`<iostream>`、`<iterator>`、`<numeric>` 和 `<vector>` 编译为头文件单元。接下来，将主模块接口单元编译为预编译模块（`.pcm`）文件：

```bash
clang++ -std=c++20 -fmodule-file=vector.pcm
        -x c++-module deitel.math.ixx --precompile -o deitel.math.pcm
```

接下来，将模块实现单元编译为目标文件：

```bash
clang++ -std=c++20 -fmodule-file=deitel.math.pcm
        -fmodule-file=vector.pcm -fmodule-file=numeric.pcm
        -c deitel.math-impl.cpp -o deitel.math-impl.o
```

选项 `-fmodule-file=deitel.math.pcm` 指定模块的主模块接口单元的名称。最后，编译主应用程序并将其与文件 `deitel.math-impl.o` 和 `deitel.math.pcm` 链接：

```bash
clang++ -std=c++20 -fmodule-file=algorithm.pcm
        -fmodule-file=iostream.pcm -fmodule-file=iterator.pcm
        -fmodule-file=vector.pcm fig16_08.cpp deitel.math-impl.o
        -fprebuilt-module-path=. deitel.math.pcm -o fig16_08
```

### 16.8.2 示例：将类模块化

让我们定义第 9 章 `Time` 类的简化版本，将其接口放在**主模块接口单元**中，将其实现放在**模块实现单元**中。我们将模块命名为 `deitel.time`，并将该类放入 `deitel::time` 命名空间。

**deitel.time 主模块接口单元**

`deitel.time` 模块的主模块接口单元（图 16.9）定义并导出命名空间 `deitel::time`（第 7—19 行），其中包含 `Time` 类定义（第 8—18 行）。

```cpp
1   // Fig. 16.9: deitel.time.ixx
2   // Primary module interface for a simple Time class.
3   export module deitel.time; // declare the primary module interface
4
5   import <string>; // rather than #include <string>
6
7   export namespace deitel::time {
8       class Time {
9       public:
10          // default constructor because it can be called with no arguments
11          explicit Time(int hour = 0, int minute = 0, int second = 0);
12
13          std::string toString() const;
```

![](img/7b5e2088e71c7f78681d4ddbcf104c06_1012_0.png)

