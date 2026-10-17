
所有创建良好的脚本绑定都是需要某种程度手动调整的过程。尝试创建绑定的技术通常产生的 API 在脚本语言中听起来并不自然。例如，PyObjC 提供了用于 Python 中 Objective-C 对象的工具，这在 Python 中像 `setValue()` 这样的方法可能会很繁琐。

## 11.1.4 跨越语言屏垒

语言屏垒是指 C++ 与脚本语言相交边界。脚本绑定将处理从脚本语言到 C++ 的方法调用，这通常不会自动发生，除非专门设计为与脚本语言互操作而设计的 C++ API。

例如，考虑一个在 Python 中重写了虚拟方法的 C++ 类。这种做法是合理的，因为 C++ 变量是在编译时创建的，无法适应 Python 的动态能力。某些绑定技术提供了额外的功能来实现跨语言的多态性。

另一个问题是 C++ 代码是否使用内部事件或通知系统。如果是这样，则需要额外的机制来处理跨语言边界的 C++ 触发事件。例如，Qt 或 Boost 槽系统可以在 C++ 对象状态改变时发送通知，允许脚本编写代码来拦截 C++ 事件并将其跨越边界发送到脚本语言。

最后，异常是另一种 C++ 代码需要与脚本代码通信的情况。例如，未捕获的 C++ 异常必须在语言屏垒处被捕获，然后翻译成脚本语言的异常类型。

## 11.2 绑定技术

各种技术可用于生成封装器，允许脚本语言调用 C++ 代码。每种技术都有其优缺点。有些是支持许多脚本语言的语言无关技术（如 COM 或 CORBA），有些是特定于 C++ 但提供许多语言绑定的支持（如 SWIG），有些提供单一语言的绑定（如 Boost Python），而另一些专注于特定 API 的 C++ 绑定（如 Open Inventor 的 Python 绑定）。

我在这里列出其中几种，并在章的剩余部分详细介绍两种。我选择关注可移植的 C++ 解决方案，而不是考虑 COM 或 CORBA 等重量级通信模型。为了提供更大的实用性，我将查看一种通过编程定义脚本绑定的技术，另一种使用接口文件生成绑定代码的技术（SWIG）。

任何脚本绑定技术本质都基于适配器（Adapter）模式，即提供一个 API 到另一个 API 的一对一映射，同时将数据类型转换为相应的原生形式，并可能使用惯用命名法。认识这一事实意味着意识到代理（Proxy）和适配器等 API 封装模式所面临的问题。主要关注的是随着时间推移保持两个 API 同步的需求。正如你所看到的，Boost Python 和 SWIG 都要求你保留冗余文件：Boost 为 C++ 文件，SWIG 为独立的接口文件。事实是支持脚本 API 时最大的维护成本。

### 11.2.1 Boost Python

Boost Python（也称为 `boost::python` 或 Boost.Python）是一个让 C++ API 与 Python 互操作的 C++ 库。它是优秀的 Boost 库的一部分，可在 http://www.boost.org/ 获取。你可以在 C++ 代码中编程创建绑定，并链接 Python 与 Boost Python 之间的绑定。这产生了一个可以直接导入到 Python 的动态库。

Boost Python 在封装 C++ API 方面支持以下能力和功能：

- C++ 引用和指针
- C++ 异常到 Python
- C++ 默认参数和关键字参数
- 在 C++ 中操作 Python 对象
- 将 C++ 迭代器导出为 Python 迭代器
- Python 文档字符串
- 全局注册类型转换

### 11.2.2 SWIG

SWIG 是一个开源工具，可为各种高级语言创建 C 或 C++ 接口的绑定。支持的语言包括脚本语言如 Perl、PHP、Tcl 和 Ruby，以及非脚本语言如 C#、Common Lisp、Java、Lua、Mozilla-3、OCAML、Octave 和 R。

SWIG 的核心设计是接口文件，通常带有 `.i` 扩展名。此文件使用 C/C++ 语法为模块指定通用绑定。SWIG 接口文件的通用格式为：

```
// example.i

%module <module-name>

(

  // 编译生成的 C++ 绑定代码所需的声明

)

// 待封装的类、函数等的声明
```

SWIG 程序可以读取此接口文件并为特定语言生成绑定。这些绑定被编译为共享库，可以由脚本语言加载。。有关 SWIG 的更多信息，请参阅 http://www.swig.org/。

### 11.2.3 Python-SIP

SIP 是一个让你为 Python 创建 C 和 C++ 绑定的工具。它最初为 PyQt 包创建的，该包为 Nokia 的 Qt 工具包提供了 Python 绑定。因此，Python-SIP 有对 Qt 信号槽机制提供了特定支持。然而，该工具也可用于为任何 C++ API 创建绑定。

SIP 的工作方式与 SWIG 非常相似，尽管它不支持像 SWIG 那样广泛的语言。SIP 在其接口规范文件中支持大部分 C/C++ 语法，并在命令中使用了与 SWIG 相似的语法（即带有 `%` 符号的标记），尽管它支持一套不同的语言集和风格来定制绑定。这里是一个简单的 Python-SIP 接口规范文件示例。

```cpp
// 为示例库定义 SIP 包装器。

// 定义 Python 模块名称和生成版本号

%Module example 0

class Example {
// 在 SIP 生成的包装器中包含 example.h
%TypeHeader
#include <example.h>
%End
public:
    Example(const char *name);
    char *GetName() const;
;
```
### 11.2.4 COM 自动化

组件对象模型（COM）是一种二进制接口标准，允许对象通过连接进行相互作用。COM 对象指定了定义良好的接口，允许软件组件链接在一起以构建用户端应用程序。该技术由微软于 1993 年开发，至今仍在使用，主要用于 Windows 平台，尽管微软鼓励使用 .NET 和 SOAP。

COM 包含了一系列大型技术，但我将重点关注这里的 COM 自动化（COM Automation），也称为 OLE 自动化。这允许脚本语言中的自动化对象（也称为 ActiveX）执行重复任务或通过脚本控制应用程序。它支持大量的目标语言，例如 Visual Basic、JavaScript、Perl、Python、Ruby 以及一系列 Microsoft .NET 语言。

COM 对象通过全局唯一标识符（UUID）识别，并通过同样由 UUID 标识的接口暴露其功能。所有 COM 对象都支持 `AddRef()`、`Release()` 和 `QueryInterface()` 未方法。自动化对象额外实现了 `IDispatch` 接口，其中包含了对象中的 `Invoke()` 方法。

所暴露的接口模型使用接口描述语言（IDL）进行描述。IDL 是组件接口的与语言无关描述，通常存储在以 `.idl` 扩展名的文件中。这种 IDL 描述可以使用 Windows 上的 `MIDLEXE` 编译器翻译成各种形式。生成的文件包括 COM 对象的代理 DLL 代码和描述对象模型的类型库。以下示例显示了 Microsoft IDL 语法的示例：

```idl
// Example.idl

import "mydefs.h", "unknown.idl"

[
  object, uuid(d1420a03-d0ec-11b1-c04f-008c3ac31d2f),
]

interface ISomething : IUnknown
{
  HRESULT MethodA([in] Short Param1, [out] BFAST *pParam2);
  HRESULT MethodB([in], [out] BFAST *pParam1);
}

[
  object, uuid(1e1423d1-ba0c-d110-043a-00fc8cc31d2f),
  pointer_default(unique)
]

interface ISomethingElse : IUnknown
{
  HRESULT Method([in] long Max,
  [in, max_is(Max)] Param1;
  [out] long *pSize;
  [out, size_is(, *pSize)] BFAST **pParam2);
}
```

还有一个名为跨平台组件对象模型（或 XPCOM）的框架。这是一个由 Mozilla 开发的开源项目，用于它们的许多应用程序，包括 Firefox 浏览器。XPCOM 遵循与 COM 非常相似的设计，尽管它的组件不是可交互的或可交换的。

### 11.2.5 CORBA

通用对象请求架构 CORBA 是一种行业标准，允许软件组件独立于其位置和供应商进行相互通信。在这方面，它与 COM 非常相似；两种技术都解决了不同来源对象之间的通信问题，并且都使用语言无关的 IDL 格式来描述每个对象的接口。

CORBA 是跨平台的，具有多个开源实现，并对 UNIX 平台提供了强大的支持。它由对象管理组于 1991 年定义（即管理 UML 建模语言的组）。CORBA 提供了广泛的语言绑定，包括 Python、Perl、Smalltalk、JavaScript 和 CORBA 脚本语言（IDL-script）。与 COM 的单接口不同，它还支持多继承接口。

在脚本方面，CORBA 不需要 COM 那样的自动化接口。所有 CORBA 对象默认都可以通过动态调用接口（Dynamic Invocation Interface）进行脚本化，这允许语言动态确定对象的接口。一个从脚本语言访问 CORBA 对象的示例，这里是简单的 IDL 描述以及它如何映射到 Ruby 语言。

## 11.3 使用 Boost Python 添加 Python 绑定

```idl
// example.idl

interface myInterface
{
    struct MyStruct { short value; };
};
```

```ruby
// example.rb

require 'myinterface'

s = MyInterface::MyStruct.new

s.value = 42
```

本章的其余部分将致力于让你具体理解如何为你的 C++ API 创建脚本绑定。我将开始展示如何使用 Boost Python 库创建 Python 绑定。

Python 是一种由 Guido Rossum 设计的开源动态类型语言，首次出现于 1991 年。它带有一个庞且丰富的库，包括 os、sys、re、difflib、codecs、datetime、math、zip、socket、json 和 xml。Python 的一个较不寻常的方面是是使用缩进来定义作用域，而不是 C++ 中的大括号。有关 Python 的更多详细信息，请参考 http://www.python.org。

如前所述，Boost Python 用于通过编程方式定义 Python 程序。图 11.1 展示了这一基本工作流。

![Figure 11.1: 使用 Boost Python 创建 Python 绑定的工作流](img/170b14e5ba8f4b05aa823f929eb6333.png)

图 11.1：使用 Boost Python 创建 Python 绑定的工作流。白色框表示文件；阴影框表示命令。

### 11.3.1 构建 Boost Python

许多 Boost 包仅通过头文件实现（使用模板和内联函数），你只需要将 Boost 目录添加到编译包含路径。然而，Boost Python 需要你下载并链接 `boost_python` 库，因此你需要了解如何构建。

构建 Boost 的推荐使用 bjam，它是 Jam 构建系统的后代。大多数平台都可以从 http://www.boost.com/ 获取预编译的可执行文件。

在 UNIX 变体（如 Linux 或 Mac）上构建 涉及以下步骤：

```bash
cd <boost-root>
./bootstrap.sh -prefix=<install-dir>
./bjam toolset=install
```

`toolset` 字符串用于定义你想要构建的编译器，例如 `gcc`、`msvc` 或 `intel`。

如果你在机器上安装了多个版本的 Python，可以通过 bjam 配置（你应该在家目录下创建一个名为 `user-config.jam` 的文件）来指定要使用的版本。你可以在 Boost 手册找到更多关于配置 bjam 的详细信息，但基本上你可能想在 `user-config.jam` 文件中添加类似以下的内容：

```jam
using python @ version
: 2.6 @ executable Path
: /usr/local/bin/python2.6 @ include path
: /usr/local/include/python2.6 @ include path
: /usr/local/lib/python2.6 @ lib path
```

### 11.3.2 示例 API

```cpp
void SetName(const std::string& name);
std::string GetName() const;
void SetHomeName(const std::string& number) const;
std::string GetHomeNumber() const;
```

```cpp
class PhoneBook {
public:
    int GetSize() const;
    void AddPerson(Person* p);
    void RemovePerson(const std::string& name);
    Person* FindPerson(const std::string& name);
};
```

请注意，这将展示许多功能，包括包装多个类、使用 STL 容器以及构造函数。我将借此机会在将 C++ 成员函数直接映射到 Python 方法之外，演示如何创建 Python 属性。

`Person` 类本质上是一个数据容器：它只包含访问底层数据的 getter/setter 方法。这些是转换为 Python 属性（properties）的良好人选。Python 中的属性行为上像一个普通对象，但使用 getter/setter 方法来管理对该属性的访问（作为销毁对象的删除器）。这使得对于想要得像简单数据成员的类成员，可以进行直观的访问，同时允许你提供控制获取和设置值的逻辑。

现在我们已经展示了 C++ API，让我们来看看如何使用 `boost::python` 为其指定 Python 绑定。我们通常会创建一个单独的 .cpp 文件来为指定的模块指定绑定，按照惯例，使用与模块相同的基础文件名并添加 `_wrap` 后缀，即在我们的示例中使用了 `phonebook_wrap.cpp`。这个 wrap 文件就是你指定想要暴露的类以及想要提供的方法的地方：以下文件展示了包装我们的 `phonebook.h` API 所需的 boost::python 代码。

```cpp
// phonebook_wrap.cpp

#include "phonebook.h"
#include <boost/python.hpp>

BOOST_PYTHON_MODULE(phonebook)

class_<Person>("Person") 
    .add_property("name", &Person::GetName, &Person::SetName)
    .add_property("home_number", &Person::GetHomeNumber,
                  &Person::SetHomeNumber);

class_<PhoneBook>("PhoneBook")
    .def("size", &PhoneBook::GetSize)
    .def("add_person", &PhoneBook::AddPerson)
    .def("remove_person", &PhoneBook::RemovePerson)
    .def("find_person", &PhoneBook::FindPerson,
        return_value_policy<reference_existing_object>());
```

对于 `Person` 类，我定义了两个属性 `name` 和 `home_number`，并提供了 C++ getter/setter 函数来控制对这些属性的访问（如果我只提供 getter，则该方法将是只读的）。对于 `PhoneBook` 类，我分别定义了标准方法，命名为 `size()`、`add_person()`、`remove_person()` 和 `find_person()`。我还必须显式指定编译 `find_person()` 指针值的行为。

然后你可以将 `phonebook.cpp` 和 `phonebook_wrap.cpp` 的代码编译为动态库。这将涉及编译 Python 和 boost::python 的所有头文件，并链接你目标平台的库。结果在 Mac 和 Linux 上应该是 `phonebook.so` 库，在 Windows 上是 `phonebook.dll`。（注意：Python 不识别 Mac 上的 `.dylib` 扩展名）。例如，Linux：

```bash
g++ -c phonebook.cpp
g++ -c phonebook_wrap.cpp -I<boost_includes>-I<python_include>
g++ -shared -o phonebook.so phonebook_wrap.o -lboost_python -lpython
```
