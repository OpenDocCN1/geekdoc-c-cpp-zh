

using std::literals::string_literals::operator""s" 使得字符串仅可以使用后缀 "s"，而不能使用其他后缀，特别是来自 <chrono> 的秒数后缀 "s"。这适用于所有其他 `operator""`。

| 后缀 | 类型 | 头文件 |
|---|---|---|
| "s" | std::string | <string> |
| "sv" | std::string_view | <string_view> |
| "i" | std::complex<double> | <complex> |
| "if" | std::complex<float> | |
| "il" | std::complex<long double> | |
| "h" | std::chrono::hours | <chrono> |
| "min" | std::chrono::minutes | |
| "s" | std::chrono::seconds | |
| "ms" | std::chrono::milliseconds | |
| "us" | std::chrono::microseconds | |
| "ns" | std::chrono::nanoseconds | |
| "d" | std::chrono::day (since C++20) | |
| "y" | std::chrono::year (since C++20) | |

**表 28.10** 情况下的预定义字面量。特别是如果你需要，来自 <string> 的字符串 "s" 和来自 <chrono> 的秒数 "s" 可以清晰地分开。

你可以找到许多示例，例如第 4 章的列表 4.17 (<string>)、第 4 章的列表 4.39 (<complex>) 以及列表 28.24 (<chrono>)。以下是包含几个不同字面量的总结：

```
// http://godbolt.org/z/o359THMJ
#include <iostream>
#include <string>
#include <chrono>
#include <complex>

using std::cout;
```

int main() {
    using namespace std;
    cout << "string" << "\n";    // string
    cout << (1.2+3.4i) << "\n";     // complex
    using namespace std::chrono;
    cout << (35s).count() << "\n"; // chrono
    using namespace std::literals;
    cout << (41s).count() << "\n";    // chrono seconds
    cout << "texts" << "\n";         // string
    using namespace std::chrono;
    cout << (4h).count() << "\n";      // chrono hours
    using namespace::literals::chrono_literals;
    cout << (16min).count() << "\n";  // chrono minutes
    using std::literals::string_literals::operator""s;
    cout << "letters" << "\n";        // string
}
```

注意，尽管字符串和秒数都存在 "s"，但你可以同时使用它们，因为 `operator""` 的重载不会产生冲突。文本字面量如 "texts" string 和数值字面量如 41s 会变成秒数。

# GCC 和 "complex" 后缀

对于 GCC，复数字面量的 "i"、"if" 和 "il" 后缀目前只有在编译时指定 `-fno-ext-numeric-literals` 的情况下才能按预期工作。否则，来自 <complex.h> C 头文件的定义以及长期存在的 GCC 扩展会混淆编译器。

## 28.5 使用 "system_error" 进行系统错误处理

由操作系统或类似的低级引起并到达程序的错误通常以*数值值*的形式返回给调用者。例如，在 POSIX 系统上，“拒绝访问”（Permission denied）错误是通过错误代码 `1`（常量 EPERM）报告的。

为了编写可移植的代码，你需要将这些代码转换为通用的（可移植的）表示。在此过程中，你必须处理许多可能的系统。为了做到这一点，你还需要能够再次访问系统特定的代码。一方面，你想要一种可移植的翻译；另一方面，你又想要系统特定的底层访问。

`<system>` 头文件试图弥补这一差距。它包含了轻级的 `error_code` 对象，这些对象一方面包含了系统特定的 `int` 错误代码，另一方面引用了更抽象且可移植的 `error_condition` 对象。

这些错误对象也可以在不使用异常类的情况下使用，在环境中不使用异常的开发者更倾向于这种方式。

`<system>` 头文件提供了以下组件：

- `error_code`: 表示系统特定的错误值。
- `error_condition`: 更具可移植性的错误表示。
- `error_category`: 将错误分类为组。
- `system_error`: 一个包含 `error_code` 和消息的异常类。
- `generic_category()`: 返回通用错误的范畴。
- `system_category()`: 返回系统错误的范畴。

### 28.5.1 概述

`error_code` 和 `error_condition` 类看起来几乎完全相同，但它们有不同的角色。`error_code` 传输依赖于系统的错误，而 `error_condition` 用于可移植的分类。

### 28.5.2 原则

尽管 `system_error` 是异常，但它并不总是处理错误的正确方法。在某些环境（例如嵌入式系统或实时应用）中，异常是不受欢迎的。因此，你必须使用错误代码。

