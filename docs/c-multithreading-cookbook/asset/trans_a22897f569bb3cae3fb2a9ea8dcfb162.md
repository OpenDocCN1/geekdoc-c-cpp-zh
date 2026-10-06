

# .NET Framework 中的线程

与我们之前的示例类似，需要注册一个事件，我们在这里使用 `AsyncDownloadDataCompleted` 方法来实现。当我们调用 `Client::DownloadDataAsync` 时，CLR 会创建一个新线程并行执行下载操作，并在完成后，它将触发一个事件并随后调用 `AsyncDownloadDataCompleted` 方法。

# 使用 BackgroundWorker 类

正如我们所说，EAP（异步事件模型）是一种非常好的机制，它允许程序员轻松地用更少的代码创建多线程应用程序。`BackgroundWorker` 对象是 EAP 的通用实现，具有许多优秀特性，例如实用的取消模型、安全更新另一个线程 UI 控件的能力、进度报告功能、异常转发、触发完成回调等。现在，我们将使用位于 `System::ComponentModel` 命名空间的 `BackgroundWorker` 类来实现我们的功能性示例。

# 准备工作

确保 Visual Studio 已启动并运行。

# 如何实现...

现在，让我们创建程序并解释其结构。执行以下步骤：

- 创建一个名为 `CLRAApplication7` 的新 C++ CLR 空项目应用程序。
- 打开解决方案管理器（Solution Explorer），右键点击源文件（Source file）。添加一个名为 `main` 的源文件。打开 `main.cpp`。

```cpp
#include <Windows.h>
#include <tchar.h>
#include "MyForm.h"

using namespace System::Windows::Forms;
using namespace System::Threading;
using namespace CLRAApplication7;

[STAThread]
int APIENTRY _tWinMain(HINSTANCE hThis, HINSTANCE hPrev, LPTSTR szCommandLine, int iCmdShow)
{
Application::EnableVisualStyles();
Application::SetCompatibleTextRenderingDefault(false);
Application::Run(gcnew MyForm());
return 0;
}
```

- 1. 打开解决方案管理器，右键点击头文件（Header file）。在 Visual C++ 下选择 UI。
添加一个名为 `MyForm` 的新 Windows Form（Windows Form）。打开 `MyForm.h`。

- 2. 添加以下代码：

```cpp
#pragma once
namespace CLRAApplication
{
    using namespace System;
    using namespace System::ComponentModel;
    using namespace System::Windows::Forms;
    using namespace System::Drawing;

    public ref class MyForm : public Form
    {
    public:
        MyForm()
        {
            InitializeComponent();
        }

        this->Load += gcnew EventHandler(this, &MyForm::OnLoad);
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
        Label* label;
        ProgressBar* progress;
    };
```

```cpp
static const int N = 25;

System::Void Form_OnLoad(System::Object^ sender, System::EventArgs^ e)
{
    InitializeApp();
}

System::Void InitializeApp(void)
{
    label = gcnew Label();
    label->Location = Point(2, 25);
    progress = gcnew ProgressBar();
    progress->Location = Point(2, 235);
    progress->Width = 280;
    progress->Height = 25;
    progress->Step = 1;
    progress->Maximum = MyForm::N;
    progress->Value = 0;
    this->Controls->Add(label);
    this->Controls->Add(progress);
    BackgroundWorker^ bckWorker = gcnew BackgroundWorker();
    bckWorker->WorkerReportsProgress = true;
    bckWorker->ProgressChanged += gcnew ProgressChangedEventHandler(this, MyForm::ProgressChanged);
    bckWorker->WorkerCompleted += gcnew WorkerCompletedEventHandler(this, MyForm::Running());
    bckWorker->DoWork += gcnew DoWorkEventHandler(this, MyForm::StartAddress);
    bckWorker->RunAsync(bckWorker);
}

System::Void StartAddress(Object^ sender, DoWorkEventArgs^ e)
{
    BackgroundWorker^ bckWorker = (BackgroundWorker^)e->Argument;
    Int64 iResult = 1;
    for (int iIndex = 1; iIndex <= MyForm::N; iIndex++)
    {
      iResult *= iIndex;
      bckWorker->ReportProgress(iIndex);
      System::Threading::Thread::Sleep(100);
      e->Result = iResult;
    }
}

System::Void ProgressChanged(Object^ sender, ProgressEventArgs^ e) 
{
  progress->Value = e->ProgressPercentage;
}

System::Void RunningCompleted(Object^ sender, RunWorkerCompletedEventArgs^ e) 
{
  label->AutoSize = false;
  label->Text = L"Result: * " + Convert::ToString(e->Result);
  label->AutoSize = true;
}
```

```cpp
#pragma region Windows Form Designer generated code
/// <summary>
/// Designer 所需的方法
/// 支持 - 不要修改
///  Use勿通过代码编辑器修改此方法的内容。
/// </summary>
void InitializeComponent(void) {
  this->components = gcnew System::ComponentModel::Container();
  this->Size = System::Drawing::Size(300, 300);
  this->Text = L"MyForm";
  this->Padding = System::Windows::Forms::Padding(0);
  this->AutoScale = System::Windows::Forms::AutoScale;
}
#pragma
```

*(注：后续文本中存在大量重复的段落，已根据要求保持核心逻辑翻译并不再进行重复输出。)*

