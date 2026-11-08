
> GCC 与“complex”后缀
> 对于 GCC，复数文本的 `i`、`if` 和 `il` 后缀目前只有在编译期间指定 `-fno-ext-numeric-literals` 时才会按预期工作。否则，来自 C 头文件 `<complex.h>` 的定义以及长期存在的 GCC 扩展会使编译器混淆。

## 28.5 使用“system_error”的系统错误处理

由操作系统或类似低层级原因导致并到达程序的错误，通常会以*数值*形式返回给调用者。例如，在 POSIX 系统上，“Permission denied”错误会通过错误码 1（常量 `EPERM`）报告。

要编写可移植代码，你需要将这些错误码转换为通用的——可移植的——表示形式。在此过程中，你必须处理许多可能的系统。而为了做到这一点，你还需要能够再次访问系统特定的错误码。一方面，你想要可移植的转换；另一方面，你想要系统特定的低层访问。

`<system_error>` 头文件试图弥合这一差距。它包含轻量级的 `error_code` 对象，这些对象一方面包含系统特定的 `int` 错误码，另一方面引用更抽象、更可移植的 `error_condition` 对象。

这些错误对象也可以在不使用异常类的情况下使用，在不使用异常的环境中工作的开发者会对此表示赞赏。如果你使用异常，可以触发一个 `error_code`，并附带一条文本消息作为 `system_error`。

可扩展性通过以下事实得到处理：这两个字段各自都与一个 `error_category` 关联。在这里，用户可以添加自己的错误组，或识别由系统定义的错误组。

### 28.5.1 概述

`<system_error>` 头文件主要定义以下组件：

- **类 error_code**  
  表示可由操作（例如系统函数调用）返回的*系统特定*错误值。
- **类 error_condition**  
  一种*通用*错误条件，人们在*可移植*代码中针对它进行检查。
- `class error_category`  
  将错误分类为*组/族*，也是用于转换为可读文本的抽象基类。
- `class system_error`  
  是一个异常类，当错误通过异常传播时，它包含一个 `error_code`。
- `enum class errc`  
  是由 POSIX 标准派生的通用值枚举，其类型为 `error_condition`。
- **is_error_code_enum<>**、`is_error_condition_enum<>`、`make_error_code`、`make_error_condition`  
  实现将 `enum class` 值转换为 `error_code` 或 `error_condition` 值的机制。
- `generic_category()`  
  返回一个 `error_category` 实例，该实例可以解释基于 `errc` 的代码和*条件*。
- `system_category()`  
  返回一个实例，用于解释来自操作系统的错误。

### 28.5.2 原理

尽管 `system_error` 定义了自己的异常类，但抛出异常并不总是处理错误的正确方式。有时，函数的附加返回值只是提供你希望纳入程序控制流的信息。与网络服务器的连接中断可能会作为异常传播，但如果你在连接设置期间尝试多个服务器，就不一定应该用异常循环来实现这一点。而且不要忘记，在某些领域，异常是完全不可取的：在*实时系统*中，对确定性时序行为的要求如此之高，以至于实现者有时完全避免异常。而在*嵌入式系统*中，某些异常实现带来的额外内存消耗不可忽视。因此，C++ 务实性地支持两种错误处理方式——带错误码的返回值和异常——并弥合这两个世界。

发生错误时，`errno` 变量通常会存储有关错误性质的更详细信息。来自 `<stdio>` 和 `<math>` 的许多函数在失败时会把错误码存储在这里。在符合 POSIX 的平台上，许多系统函数在函数调用失败时会在 `errno` 中提供详细信息。在 Windows 上，通常还会额外使用或改用 `GetLastError`。你使用的库越多，可确定错误码的来源就越多。C++ 考虑到可能需要评估来自不同来源的错误码，并支持库对这些错误码进行扩展。发生这种情况时，现有函数的接口不得改变。

当用户和第三方提供者获得扩展错误码系统的手段时，低层错误码（可能因系统而异）需要在某处进行映射，同时需要向用户提供可移植的解释。例如，实现 HTTP 服务器的人希望以每个人都能理解的方式传递 RFC 标准中定义的错误码，但为此必须依赖操作系统特定的错误码。我们将在下一节用一个示例来演示这一点。最初，库（标准库以及第三方提供者的库）原本只打算向用户提供已经解释过的错误码。然而，原始信息对于问题分析也很重要，因此它必须以某种方式出现在*错误报告*或*日志记录*中。因此，错误码处理必须同时提供两者：低层错误码和解释后的/可移植的值。

### 28.5.3 “error_code”与“error_condition”

`error_code` 和 `error_condition` 类看起来几乎相同，但它们有不同的作用。`error_code` 传输依赖于系统的错误，而 `error_condition` 用于更可移植的分类。

因此，这取决于你想要实现什么。考虑以下示例。

```cpp
// https://godbolt.org/z/1XnY8vd8Y
#include <system_error> // error_code
#include <string>

void create_dir(const std::string& pathname, std::error_code& ec);

void run() {
    std::error_code ec;
    create_dir("/some/path", ec);
    if(!ec) {  // Success ...
    } else {   // Failure ...
    }
}
```

**清单 28.34** 一个非常简单的示例，说明如何检查操作是否成功。

这里我们只关心成功或失败，这就是为什么可以使用 `if(!ec)` 轻松地将 `error_code` 转换为 `bool`。这种行为源自检查函数返回值以查看是否发生错误——不幸的是，这因函数而异，例如 `FILE *f=fopen("f.txt", "r"); if(f==NULL)...`。

发生错误时，你也可以使用 `error_code` 获取更多信息：是缺少权限，文件名已经存在，路径名太长，还是父目录不存在？诸如此类。无论如何，`ec` 都包含一个系统特定的值——类似于传统代码中的 `errno` 变量（但仅在发生错误时）。

假设你更关心具有该名称的文件或目录是否已经存在。那么你可以用 `if(ec.value() == EEXIST)` 来判断——但这是错误的方式！它在 POSIX 平台上可行，但在 Windows 上，你必须比较 `if(ec.value() == ERROR_ALREADY_EXISTS)`。

根据经验法则：*如果你调用 value()，你很可能做错了。*

但是，你该如何改为针对“已经存在”事件测试系统特定的错误码（EEXIST 或 ERROR_ALREADY_EXISTS）呢？这是通过 error_condition 完成的。

你可以使用 == 或 != 将返回的 error_code ec 直接与 error_condition 实例进行比较。在这种情况下，比较不是为了精确相同，而是为了等价——意思是它“表示相同含义”。

因此，要进行比较，你必须将 error_code ec 与表示“已经存在”的 error_condition 对象进行比较——即 errc::file_exists。目前，请将 errc::file_exists 以及 enum class errc 的其他元素视为类型为 error_condition 的常量的占位符。随着我们继续，确切的机制会变得清晰。

```cpp
// https://godbolt.org/z/TPWc5nexq
#include <system_error> // error_code, errc
#include <string>
void create_dir(const std::string& pathname, std::error_code& ec);

void run() {
    std::error_code ec;
    create_dir("/some/path", ec);
    if(ec == std::errc::file_exists) {    // specifically ...
    } else if(!ec) {                      // Success ...
    } else {                              // Failure ...
    }
}
```

**清单 28.35** `error_code` 与 `error_condition` 的比较。

为了启用比较，重载了 `operator==` 自由函数。

```cpp
bool operator==
    (const error_code&       lhs, const error_code&       rhs) noexcept;
    (const error_code&       lhs, const error_condition&  rhs) noexcept;
    (const error_condition& lhs, const error_code&       rhs) noexcept;
    (const error_condition& lhs, const error_condition&  rhs) noexcept;
```

**清单 28.36** “operator==()”的重载（简写）。

这些重载间接确保 `error_code` EEXIST 和 ERROR_ALREADY_EXISTS 都可以作为等价于 error_condition::file_exists 的值进行比较。

实现负责将系统特定的 error_codes 映射到通用的 error_condition 错误类别。
