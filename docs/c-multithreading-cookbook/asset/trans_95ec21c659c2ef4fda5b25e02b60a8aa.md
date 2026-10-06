

# .NET Framework 中的线程

我们将遵循相似的步骤来设置标签文本。在完成类之后，我们需要指定应用程序的入口点。这在 `main.cpp` 文件中完成。就像在我们非托管代码中一样，我们将包含头文件以便使用预定义类型和 `_winMain` 方法。我们需要包含 `MyForm.h` 表单，以便使用我们的类以及框架运行所需的程序集。我们需要 `System::Windows` 来使用 `Application` 类。我们还需要 `System::Threading` 来设置线程套间状态，以及 `CLApplication` 命名空间以便将 `MyForm` 作为实例传递给 `Application::Run` 方法。我们将 `ApplicationState` 变量设置为单线程单元单元（STA）。这是为了让 COM 的正确初始化对 UI 友好是所必需的，例如，当我们在窗口 UI 上使用拖放功能时，以及用于托管 COM 控件。`Application::EnableVisualStyles` 方法用于丰富的 UI 样式，类似于我们的非托管示例。最后，我们将调用 `Application::Run`，它将启动应用程序窗口并进入其消息循环。

```cpp
#pragma comment {linker, ""} used in our unmanaged example
```

# 更多内容...

尽管我们已经解释了 .NET 应用程序的大部分，但仍然有大量的解释，这些内容不是本书的一部分。框架如此巨大，以至于我们需要几本书来处理所有内容。所有影响我们应用程序执行且对我们所关注的多线程概念至关重要的内容。还有一点非常重要，运算符。尽管我们正在使用托管 C++，但我们仍然可以使用非托管代码。由于这一出色的特性，`new` 运算符用于非托管内存的分配，它具有固定的地址；而 `gcnew` 运算符从 CLR 堆中分配地址，并由框架管理。这意味着地址不是固定的；它们在执行过程中可能会发生变化。这意味着程序员不需要担心它的重新分配。当它不再被需要时，CLR 将使用垃圾回收器（GC）删除其删除。这对应于 `^` 和 `+` 运算符，其中 `^` 表示托管，`+` 表示非托管；以及 `&` 运算符，它分别表示托管和非托管的引用。比较下表所示。

| 运算符 | 非托管 | 托管 |
|---|---|---|
| 间接（指针） | * | ^ |
| 引用 | & | % |

# 前台线程与后台线程的区别

在 .NET 中，有两种线程：前台线程和后台线程。线程默认被创建为后台线程。你可以显式地将线程状态设置为后台。区别在于，前台线程在运行时会保持应用程序存活；而后台线程则不会。换句话说，当你关闭应用程序时，所有后台线程都会自动终止。因此，当所有前台线程完成执行后，应用程序可以在后台线程返回之前退出。在所有前台线程停止或应用程序退出后，系统将停止所有后台线程。

我们之前的示例使用了 `Task` 对象，它默认在后台运行。我们接下来的示例将与之前相同，但重点是前台线程。这就是为什么我们使用使用 `Thread` 对象而不是 `Task`。

# 准备工作

确保 Visual Studio 已经启动并运行。

# 如何操作...

现在，让我们创建一个新项目并解释它的结构。执行以下步骤：

- 1. 创建一个名为 `CLApplication` 的新 C++ CLR 空项目应用程序。
- 2. 打开解决方案管理器，右键点击源文件。添加一个名为 `main` 的新源文件。打开 `main.cpp`。复制并粘贴以下代码：

```cpp
#include <Windows.h>
#include <tchar.h>
#include "MyForm.h"

using namespace System::Forms;
using namespace System::Threading;
using namespace CLApplication;

[STAThreadAttribute]
int APIENTRY _tWinMain(HINSTANCE hThis, HINSTANCE hPrev, LPTSTR szCommandLine, int iCmdShow)
{
    Application::EnableVisualStyles();
    Application::SetCompatibleTextRenderingDefault(false);

    Application::Run(gcnew MyForm());
    return 0;
}
```

- 3. 打开资源管理器，右键点击头文件。在 Visual C++ 下选择 UI。添加一个名为 `MyForm` 的新 Windows Forms。打开 `MyForm.h`。
- 4. 添加以下代码：

```cpp
#pragma once
namespace CLRApplication
{
    using namespace System;
    using namespace System::Windows::Forms;
    using namespace System::Drawing;
    using namespace System::Threading;

    public ref class MyForm : public Form
    {
        public:
        MyForm(void)
        {
            InitializeComponent();
            this->Load += gcnew System::EventHandler(this,MyForm::Load);
        }
        protected:
        ~MyForm()
        {
            if (components)
            {
                delete components;
            }
        }
        private:
            System::ComponentModel::Container^ components;
            Label^ label;
            ProgressBar^ progress;
            // ... 其他成员变量 ...
        };
    };
}
```

