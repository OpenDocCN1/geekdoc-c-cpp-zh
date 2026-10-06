

# 第 6 章

3. 打开解决方案管理器（Solution Explorer）并右键头文件。在 Visual C++ 下选择 UI。
添加一个名为 MyForm 的新 Windows Form。打开 MyForm.h。

4. 添加以下代码：

```cpp
#pragma once

#include <Windows.h>
#pragma comment ( lib, "User32.lib" )

#define END_TASK WM_USER + 1

namespace CLRAApplication {
    using namespace System;
    using namespace System::Forms;
    using namespace System::Drawing;
    using namespace System::Threading;
    using namespace System::Threading::Tasks;
}
ref class Lock {
    Object* lockObject;
    public:
        Lock(Object* lock) : lockObject(lock) {
            Monitor::Enter(lockObject);
        }
    protected:
        ~Lock() {
            Monitor::Exit(lockObject);
        }
    };
    public ref class MyForm : public Form {
    public:
        MyForm(void) : bContinue(true) {
            lockObject = gcnew Object();
            InitializeComponent();
            this->Load += gcnew System::EventHandler(this,
            &MyForm::Form_OnLoad);
        }

protected:
        ~MyForm()
        {
            if (components)
            {
              delete components;
            }
        }

        virtual void WndProc(Message% msg) override
        {
            switch (msg.Msg) {
              case END_TASK:
                System::Windows::Forms::DialogResult^ dlgResult =
                MessageBox("Do you want to calculate again?", L"Question",
                MessageBoxButtons::YesNo, MessageBoxIcon::Question);

                if (*dlgResult ==
                  System::Windows::Forms::DialogResult::Yes)
                  {
                    SetState(true);
                    progress->Value = 0;
                    label->Text = L"Calculating...";
                  }
                else
                  {
                    PostMessage((HWND)this->Handle.ToPointer(), WM_CLOSE);
                  }
                break;
            }
        }

    private:
        System::ComponentModel::Container^components;
        Label^ label;
        ProgressBar^ progress;
        static const int N = 25;

        bool bContinue;
        Object^ lockObject;

    System::Void Form_OnLoad(System::Object^ sender,
    System::EventArgs^ e)
    {
        InitializeApp();
    }

    System::Void SetState(bool bState)
    {
        Lock* lock = gcnew Lock(this->lockObject);
        bContinue = bState;
        delete lock;
    }

    bool QueryState(void)
    {
        Lock* lock = gcnew Lock(this->lockObject);
        bContinue = bContinue;
        delete lock;

        return bContinue;
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
    }

    Task* task = gcnew Task(gcnew Action<Object*>(&MyForm::StartAddress), this);

    task->Start();
    }

    static System::Void StartAddress(Object^ parameter)
    {
        MyForm^ form = (MyForm*) parameter;

        GetFormHandleDelegate getHandle = gcnew
        GetFormHandleDelegate(form, &MyForm::GetFormHandle);
        IntPtr handle = (IntPtr)form->Invoke(getHandle);

        UpdateProgressBarDelegate action = gcnew
        UpdateProgressBar(form, &MyForm::UpdateProgressBar);
        UpdateLabelTextDelegate textAction = gcnew
        UpdateLabelTextDelegate(form, &MyForm::UpdateLabelText);

        Int64 iResult = 1;
        while (true)
        {
            if (!form->QueryState())
            {
                Thread::Sleep(1000);
                continue;
            }

            iResult = 1;
            for (int iIndex = 1; iIndex <= MyForm::N; iIndex++)
            {
                iResult *= iIndex;
                form->BeginInvoke(action);
            }

            Thread::Sleep(100);
        }

        form->BeginInvoke(textAction, L"Result: " +
        Convert::ToString(iResult));

        PostMessage((HWND)handle.ToPointer(), END_TASK, 0, 0);

        form->bContinue = false;

        Thread::Sleep(1000);
    }

    delegate void UpdateProgressBarDelegate(void);
    System::Void UpdateProgressBar(void)
    {
        progress->PerformStep();
    }

    delegate void UpdateLabelTextDelegate(String^ szText);

    System::Void UpdateLabelText(String^ szText)
    {
        label->AutoSize = false;
        label->Text = szText;
        label->AutoSize = true;
    }

    delegate IntPtr GetFormHandleDelegate(void);
    System::IntPtr GetFormHandle(void)
    {
        return this->Handle;
    }

    #pragma region Windows Form Designer generated code
    /// <summary>
    /// Required method for Designer
    /// support - do not modify
    /// the contents of this method with the code editor.
    /// </summary>
    void InitializeComponent(void)
    {
        this->components = nullptr;
        gcnew System::Windows::ComponentModel::ComponentContainer();
        this->Size = System::Drawing::Size(300, 300);
        this->Text = L"MyForm";
        this->Padding = System::Windows::Forms::Padding(0);
        this->AutoScaleMode = System::Windows::Forms::AutoScale::Font;
    }
    #pragma endregion
};
```

![](img/412b0f5bbb36adcce2ddd2d5b7416516_269_0.png)

# .NET Framework 中的线程

# 它是如何工作的...

首先，我们将添加一个新的 Lock 类。Lock 对象的背后思想是防止共享对象被多个实例同时访问。为了实现这一目的，我们将使用位于 System::Threading 命名空间中的 Monitor 对象以及它的 Enter 和 Exit 方法。为了能够使用 Monitor::Enter 和 Monitor::Exit，你必须提供指向 System::Object 的指针，以防止共享对象被两个或多个线程同时访问。我们会在访问共享对象之前实例化 Lock 对象的指针，并在访问共享对象后立即删除该 Lock 对象。这是因为 Monitor::Exit 调用是在 Lock 的析构函数中执行的。通过这种方式，我们可以安全地设置或读取 bContinue 的值，而无需担心两个线程是否会同时访问并产生不可预测的结果。

# 还有更多...

让我们讨论死锁。死锁是指一个或多个线程等待另一个线程持有的某些独占资源的现象。当线程 A 等待线程 B 而线程 B 又在等待线程 A 时，所示：

img/412b0f5bbb36adcce2ddd2d5b7416516_274_0.png 死锁出现在许多存在独占访问的情况下。例如，如果主线程想要设置 bContinue 而工作线程想要读取它。有很多检测、避免和成功处理死锁的方法，但这并不是本文的主题。

# .NET 中的线程安全与类型

什么是线程安全？它是在不干扰独立线程的情况下执行独占访问的能力。当我们使用 .NET 时为什么这很重要？这是因为 .NET 对某些类型的内部实现是设计为线程安全的。良好的实践是以这种方式开发以避免设计问题。

在 .NET 中，所有静态成员都是线程安全的，而实例成员不是。例如，如果两个线程并发枚举某个 List 集合，它们将获得不同的迭代器。如果你不修改集合值，那是可以。但如果在枚举期间需要某些更改，我们必须使用锁。

让我们通过显示线程安全的代码来回顾：

```cpp
List<int> list = gcnew List<int>();

for (int iValue = 0; iValue < 5; iValue++)
{
    list->Add(iValue);
}
```

```cpp
array<Object^> _t1Params = gcnew array<Object^>(2)
{ list, List<Task^> _t1 };
Task^ _t1 = gcnew Task(Action<Object^>>(&EnumerableList), _t1Params );
t1->Start();
```

```cpp
array<Object^> _t2Params = gcnew array<Object^>(2)
{ list, List<Task^> _t2 };
Task^ _t2 = gcnew Task(Action<Object^>>(&EnumerableList), _t2Params );
t2->Start();
```

```cpp
static void EnumerableList(Object^ parameter)
{
    array<Object^>* _tParams = (array<Object>*)parameter;

    List<int>* lst = (List<int>*)_tParams[0];
}
```

![](img/412b0f5bbb36adcce2ddd2d5b7416516_275_0.png)

