
# 2 - C++ 编程语言（参考）

搜索：`[ ]`　登录：`[登录]`

记住我 `[ ]`　[注册]

## 不喜欢 .NET？获取 Real Studio

跨平台、开箱即用的开发！`www.realsoftware.com/realstudio`

C++ 语言库的参考文档，包含了对其元素的详细描述以及如何使用这些函数的示例。

C++ 标准库是一系列函数、常量、类、对象和模板的集合，它们为 C++ 语言提供了执行各种任务的基本功能、与操作系统交互的类、数据容器、用于操作的操纵符以及常用的算法。

这些元素的声明由头文件提供。您需要在代码的头文件中包含这些头文件，以访问它们：

| 头文件 | 头文件 | 头文件 | 头文件 | 头文件 |
| :--- | :--- | :--- | :--- | :--- |
| `algorithm` | `complex` | `exception` | `list` | `stack` |
| `bitset` | `csetjmp` | `fstream` | `locale` | `stexception` |
| `cassert` | `csignal` | `functional` | `map` | `strstream` |
| `ctype` | `cname` | `memory` | `streambuf` |  |
| `cerrno` | `cstddef` | `ios` | `new` | `typeinfo` |
| `cfloat` | `cstdio` | `iosfwd` | `numeric` | `string` |
| `ciso646` | `cldblib` | `istream` | `ostream` | `utility` |
| `climits` | `string` | `queue` | `valarray` |  |
| `ctime` | `iterator` | `set` | `vector` |  |
| `cmath` | `deque` | `limits` | `stream` |  |

它可以被分为：

## C 语言库

C 语言库的元素作为 C++ 标准库的子集包含在其中。它们涵盖了许多方面，从通用实用函数到映射、输入输出函数以及内存管理函数：

- `assert`（`assert.h`）：C 诊断库（头文件）
- `ctype`（`ctype.h`）：字符处理函数（头文件）
- `errno`（`errno.h`）：C 错误（头文件）
- `cfloat`（`float.h`）：浮点类型特性（头文件）
- `iso646`（`iso646.h`）：ISO 646 替代运算符写法（头文件）
- `limits`（`limits.h`）：整数类型大小（头文件）
- `locale`（`locale.h`）：C 本地化库（头文件）
- `cmath`（`math.h`）：数学库（头文件）
- `csetjmp`（`setjmp.h`）：非局部跳转（头文件）
- `csignal`（`signal.h`）：处理信号的 C 库（头文件）
- `stdarg`（`stdarg.h`）：可变参数处理（头文件）
- `stddef`（`stddef.h`）：C 标准定义（头文件）
- `stdio`（`stdio.h`）：执行输入输出操作的 C 库（头文件）
- `stdlib`（`stdlib.h`）：C 通用库（头文件）
- `string`（`string.h`）：C 字符串（头文件）
- `ctime`（`ctime.h`）：C 时间库（头文件）

## C++ 标准库：杂项库

### 语言支持库

## 参考 - C++ 参考

`http://www.cplplus.com/reference/`

| 元素 | 描述 |
| :--- | :--- |
| `limits` | 数值限制（头文件） |
| `new` | 动态内存（头文件） |
| `typeinfo` | 类型信息（头文件） |
| `exception` | 标准异常类（类） |

### 诊断库

| 元素 | 描述 |
| :--- | :--- |
| `stexcept` | 异常类（头文件） |
| `utility` | 通用组件（头文件） |
| `functional` | 函数对象（头文件） |

### 字符串库

| 元素 | 描述 |
| :--- | :--- |
| `string` | C++ 字符串库（库） |

### 本地化库

| 元素 | 描述 |
| :--- | :--- |
| `locale` | 本地化库（头文件） |

## C++ 标准库：标准模板库（STL）

### 容器库

| 元素 | 描述 |
| :--- | :--- |
| `bitset` | 位图集合（类模板） |
| `deque` | 双端队列（类模板） |
| `list` | 列表（类模板） |
| `map` | 映射（类模板） |
| `multimap` | 多键映射（类模板） |
| `multiset` | 多键集合（类模板） |
| `priority_queue` | 优先级队列（类模板） |
| `queue` | 队列（类模板） |
| `set` | 集合（类模板） |
| `stack` | 栈（类模板） |
| `vector` | 向量（类模板） |

### 迭代器库

| 元素 | 描述 |
| :--- | :--- |
| `iterator` | 迭代器定义（头文件） |

### 算法库

| 元素 | 描述 |
| :--- | :--- |
| `STL 算法` | 标准模板库：算法（库） |

### 数值库

| 元素 | 描述 |
| :--- | :--- |
| `complex` | 复数库（头文件） |
| `vararray` | 数值类型数组（头文件） |
| `numeric` | 通用数值操作（头文件） |

## C++ 标准库：输入/输出流库

提供了使用名为“流”的抽象的功能，专门设计用于对字符序列（如文件或字符串）执行输入和输出操作。

这些功能通过几个相关的类提供，如下所示关系图所示，上方是相应的头文件名称：

## 参考 - C++ 参考

| `<ios>` | `<iostream>` | `<iostream>` | `<fstream>` | `<sstream>` |
| :--- | :--- | :--- | :--- | :--- |
| `ios_base` | `istream` |  |  | `istream` |
| `ios` |  | `cin` | `fstream` | `stringstream` |
|  | `ostream` | `cout`、`cerr`、`clog` | `ofstream` | `ostringstream` |
|  |  | `streambuf` | `filebuf` | `stringbuf` |

如需更多信息，请参阅 C++ 输入/输出流库的参考页面。

首页 | 隐私政策

发现错误？联系我们
