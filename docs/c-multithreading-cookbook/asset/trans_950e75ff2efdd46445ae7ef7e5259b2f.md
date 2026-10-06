

## 如何终止线程？

在接下来的示例中，我们将展示如何使用 `Abort` 方法来终止线程。请确保 Visual Studio 已经运行。

执行以下步骤：

1. 创建一个名为 `RAApplication` 的新 CLR 空项目。
2. 打开解决方案管理器，右键点击“源文件”。添加一个名为 `main.cpp` 的新源文件。
3. 打开解决方案管理器，右键点击“头文件”。添加一个名为 `MyForm.h` 的新 Windows Form。
4. 添加以下代码：

```cpp
#pragma once
#include <Windows.h>

using namespace System;
using namespace System::Forms;
using namespace System::Threading;

[STAThread]
int main(HINSTANCE hInstance, HINSTANCE hPrev, LPTSTR szCommandLine, int iCmd)
{
    Application::EnableStyles();
    Application::CompatibleTextRendering(false);
    Application::Run(gcnew MyForm());
    return 0;
}
```

```cpp
#pragma once

namespace RAApplication
{
    using namespace System;
    using namespace System::Threading;
    using namespace System::Forms;
    using namespace System::Drawing;

    public ref class MyForm : Form
    {
    public:
        MyForm()
        {
            InitializeComponent();
            this->Load += gcnew System::EventHandler(this, &MyForm::Form_OnLoad);
            this->FormClosing += gcnew FormClosingEventHandler(this, &MyForm::FormClosingEvent);
        }

    protected:
        virtual ~MyForm()
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
        static const int N = 25;
        BackgroundWorker^ bckWorker;

        void Form_OnLoad(Object^ sender, EventArgs^ e)
        {
            InitializeApp();
        }

        void FormClosingEvent(Object^ sender, FormClosingEventArgs^ e)
        {
            System::Windows::Forms::DialogResult dlResult =
                MessageBox::Show("Do you want to abort execution?", "Question", MessageBoxButtons::YesNo, MessageBox::Question);

            if (dlResult == System::Windows::Forms::DialogResult::Yes)
            {
                bckWorker->CancelAsync();
            }
            else
            {
                e->Cancel = true;
            }
        }

        void InitializeApp()
        {
            label = gcnew Label();
            label->Location = Point(2, 25);

            progress = gcnew ProgressBar();
            progress->Location = Point(2, 235);
            progress->Width = 280;
            progress->Height = 25;
            progress->Step = 1;
            progress->Maximum = N;
            progress->Value = 0;

            this->Controls->Add(label);
            this->Controls->Add(progress);

            bckWorker = gcnew BackgroundWorker();
            bckWorker->WorkerReportsProgress = true;
            bckWorker->WorkerSupportsCancellation = true;
            bckWorker->ProgressChanged += gcnew ProgressChangedEventHandler(this, &MyForm::ProgressChanged);
            bckWorker->DoWork += gcnew DoWorkEventHandler(this, &MyForm::StartAddress);
            bckWorker->RunWorkerAsync();
        }

        void StartAddress(Object^ sender, DoWorkEventArgs^ e)
        {
            MyForm^ form = (MyForm^)e.Tag;
            Int64 iResult = 1;
            for (int iIndex = 1; iIndex <= N; iIndex++)
            {
                if (bckWorker->CancellationRequested)
                {
                    return;
                }
                iResult *= iIndex;
                bckWorker->ReportProgress(iIndex);
            }
            Thread::Sleep(100);
            form->label->Text = L"Result: " + Convert::ToString(iResult);
        }

        void ProgressChanged(Object^ sender, ProgressChangedEventArgs^ e)
        {
            progress->Value = e.ProgressPercentage;
            label->Text = L"Calculating... " + Convert::ToString(e.ProgressPercentage) + L"%";
        }

    #region Windows Form Designer code
    /// <summary>
    /// Designer 所需的方法
    /// 支持 - 请勿
    /// 使用代码编辑器修改此方法的的内容。
    /// </summary>
    void InitializeComponent(void)
    {
        this->SuspendLayout();
        this->AutoScaleDimensions = System::Drawing::Size(6, 13);
        this->AutoScaleMode = System::Forms::AutoScale::Font;
        this->Size = System::Size(284, 261);
        this->MaximizeBox = false;
        this->MinimizeBox = false;
        this->Name = L"MyForm";
        this->Text = L"MyForm";
        this->ResumeLayout(false);
    }
    #endregion
    };
}
```

