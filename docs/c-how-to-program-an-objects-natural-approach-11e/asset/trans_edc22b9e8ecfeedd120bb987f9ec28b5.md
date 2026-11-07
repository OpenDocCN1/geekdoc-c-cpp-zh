
```cpp
6 int main() {
7   std::cout << welcomeStandalone() << '\n'
8             << welcomeFromExportBlock() << '\n'
9             << TestNamespace1::welcomeFromTestNamespace1() << '\n'
10            << TestNamespace2::welcomeFromTestNamespace2() << '\n';
11 }
```

```text
welcomeStandalone function called
welcomeFromExportBlock function called
welcomeFromTestNamespace1 function called
welcomeFromTestNamespace2 function called
```

**图16.3** | 导入模块并使用其导出项。（第2部分，共2部分。）

### 在 Visual C++ 中编译此示例

在 Visual C++ 中，确保 fig16_03.cpp 位于项目的 Source Files 文件夹中。然后运行项目以编译模块和主应用程序。

### 在 g++ 中编译此示例

在 g++ 中，执行以下命令；一旦 C++20 模块在该编译器中最终确定，这些命令可能会发生变化：

- 1. 将 `<string>` 和 `<iostream>` 头文件分别编译为头文件单元，因为它们分别用于我们的模块和主应用程序：
    ```cpp
    g++ -fmodules-ts -x c++-system-header string
    g++ -fmodules-ts -x c++-system-header iostream
    ```
- 2. 编译模块接口单元——这会生成文件 welcome.o：
    ```cpp
    g++ -fmodules-ts -c -x c++ welcome.ixx
    ```
- 3. 编译主应用程序并将其与 welcome.o 链接——该命令生成可执行文件 fig16_03：
    ```cpp
    g++ -fmodules-ts fig16_03.cpp welcome.o -o fig16_03
    ```

在第2步中：

- `-c` 选项表示编译 welcome.ixx 但不链接它，以及
- `-x c++` 选项表示 welcome.ixx 是一个 C++ 文件。

需要 -x c++，因为 .ixx 不是 g++ 的标准文件名扩展名。如果将 welcome.ixx 命名为 welcome.cpp，则不需要 -x c++ 选项。

### 在 clang++ 中编译此示例

在 clang++ 中，执行以下命令；一旦 C++20 模块在该编译器中最终确定，这些命令可能会发生变化：

- 1. 将 `<string>` 和 `<iostream>` 头文件分别编译为头文件单元，因为它们分别用于我们的模块和主应用程序：
    ```cpp
    clang++ -std=c++20 -xc++-system-header --precompile string
            -o string.pcm
    clang++ -std=c++20 -xc++-system-header --precompile iostream
            -o iostream.pcm
    ```
- 2. 将**模块接口单元**编译为**预编译模块**（.pcm）文件，该文件特定于 C++ 编译器：
    ```cpp
    clang++ -std=c++20 -fmodule-file=string.pcm
        -x c++-module welcome.ixx --precompile -o welcome.pcm
    ```
- 3. 编译主应用程序并将其与 welcome.pcm 链接——该命令生成可执行文件 fig16_03：
    ```cpp
    clang++ -std=c++20 -fmodule-file=iostream.pcm fig16_03.cpp
        -fprebuilt-module-path=. welcome.pcm -o fig16_03
    ```

在第2步中：

- `-fmodule-file` 指定我们的 `welcome.ixx` 模块依赖于头文件单元 `string.pcm`，以及
- `-x c++-module` `welcome.ixx` 指定 `welcome.ixx` 表示一个 C++ 模块。

这里需要 `-x c++-module` 选项，因为 `.ixx` 不是 clang++ 的标准文件名扩展名。如果将文件命名为 `welcome.cppm`，则不需要 `-x c++-module`。在第3步中，`-fprebuilt-module-path=...` 指示 clang++ 可以在哪里定位预编译模块（.pcm）文件。点号（`.`）表示当前文件夹，但也可以是系统中另一位置的相对路径或完整路径。

## 16.6.7 示例：尝试访问未导出的模块内容

模块不会隐式导出声明——这被称为强封装。因此，你可以精确控制导出供其他翻译单元使用的声明。图16.4定义了一个名为 `deitel.math` 的主模块接口单元（第3行），其中包含命名空间 `deitel::math`⁴⁵，该命名空间未被导出。在该命名空间中，我们定义了两个函数——`square`（第7–9行）被导出，而 `cube`（第12–14行）未被导出。导出函数 `square` 会隐式导出其所在命名空间的名称，但不会导出该命名空间的其他成员。由于 `cube` 未被导出，其他翻译单元无法调用它，你很快会在图16.5中看到。这是与头文件的一个关键区别——头文件中声明的所有内容都可以在 `#include` 它的任何地方使用。⁴⁶

```cpp
// Fig. 16.4: deitel.math.ixx
// Primary module interface for a module named deitel.math.
export module deitel.math;  // introduces the module name

namespace deitel::math {
    // exported function square; namespace deitel::math implicitly exported
    export int square(int x) {
        return x * x;
    }

    // non-exported function cube is not implicitly exported
    int cube(int x) {
        return x * x * x;
    }
};
```

**图16.4** | 名为 `deitel.math` 的模块的主模块接口。（第1部分和第2部分，共2部分。）

45. 命名空间 `deitel::math` 定义了一个 `deitel` 命名空间，其中嵌套了命名空间 `math`。这里使用的表示法是在 C++17 中引入的。我们在第20章讨论嵌套命名空间。

46. Dos Reis，《C++ 模块编程：面向实际软件开发者的指南》。

在模块中，**将导出的标识符放在命名空间中，以帮助避免名称冲突**是一种良好做法，尤其是当多个模块导出同一标识符时。我们在研究中发现，命名空间名称通常模仿其模块名⁴⁷——因此对于 `deitel.math` 模块，我们指定了命名空间 `deitel::math`（第5行）。

在图16.5中，第4行导入 `deitel.math` 模块。第9行调用该模块导出的 `deitel::math::square` 函数，并用其所在命名空间的名字限定函数名。这可以编译，因为 `square` 是由 `deitel.math` 模块导出的。然而，第12行会导致编译错误——`deitel.math` 模块没有导出 `cube`。图16.5中的编译错误来自 Visual C++。我们用粗体突出了关键错误消息，并为便于阅读增加了垂直间距。

```cpp
// fig16_05.cpp
// Showing that a module's non-exported identifiers are inaccessible.
import <iostream>;
import deitel.math; // import the deitel.math module

int main() {
    // can call square because it's exported from namespace deitel::math,
    // which implicitly exports the namespace
    std::cout << "square(3) = " << deitel::math::square(3) << '\n';

    // cannot call cube because it's not exported
    std::cout << "cube(3) = " << deitel::math::cube(3) << '\n';
}
```

**图16.5** | 展示模块中未导出的标识符不可访问。（第1部分，共2部分。）

```text
Build started...
1>------ Build started: Project: modules_demo, Configuration: Debug Win32 ----
1>Scanning sources for module dependencies...
1>deitel.math.ixx
1>fig16_05.cpp
1>Compiling...
1>deitel.math.ixx
1>fig16_05.cpp

1>C:\Users\pauldeitel\Documents\examples\ch16\fig16_04-05\fig16_05.cpp(12,47): error C2039: 'cube': is not a member of 'deitel::math'

1>C:\Users\pauldeitel\Documents\examples\ch16\fig16_04-05\fig16_05.cpp(12,49): message : see declaration of 'deitel::math'

1>C:\Users\pauldeitel\Documents\examples\ch16\fig16_04-05\fig16_05.cpp(12,51): error C3861: 'cube': identifier not found
```

**图16.5** | 展示模块中未导出的标识符不可访问。（第2部分，共2部分。）

### g++ 错误消息

要查看 g++ 错误消息，请执行以下命令，我们已在第16.6.6节解释过其中的每条命令：

- 1. `g++ -fmodules-ts -x c++-system-header iostream`
- 2. `g++ -fmodules-ts -c -x c++ deitel.math.ixx`
- 3. `g++ -fmodules-ts fig16_05.cpp deitel.math.o`

我们用粗体突出了关键错误消息：

```text
fig16_05.cpp: In function 'int main()':
fig16_05.cpp:12:49: error: 'cube' is not a member of 'deitel::math'
   12 |   std::cout << "cube(3) = " << deitel::math::cube(3) << '\n';
      |                                      ^~~~
```

### clang++ 错误消息

要查看 clang++ 错误消息，请执行以下命令，我们已在第16.6.6节解释过其中的每条命令：

- 1. `clang++ -std=c++20 -xc++-system-header --precompile iostream -o iostream.pcm`
- 2. `clang++ -std=c++20 -x c++ deitel.math.ixx --precompile -o deitel.math.pcm`
- 3. `clang++ -std=c++20 -fmodule-file=deitel.math.pcm -fmodule-file=iostream.pcm fig16_05.cpp -o fig16_05`

我们用粗体突出了关键错误消息：

