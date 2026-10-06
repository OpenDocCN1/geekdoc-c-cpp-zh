
## Threads in the .NET Framework

Our following example will calculate the factorial of 25 and will then ask the user whether it should continue or not. In this way, we would need to use the Sleep method as the most primitive way of spinning with a 1-second sleep interval, in order to not wait too much processor time. In order to communicate between the main thread and the working thread, we will use the PostMessage API, as the most primitive way, but enough for now, because we will explain other communication techniques later.

## Getting ready

Make sure Visual Studio is up and running.

## How to do it...

Now, let's create our program and explain its structure. Perform the following steps:

- 1. Create a C++ CLR project application CLRAApplication3.
- 2. Open Solution Explorer and right-click on Source file. Add a new source file named main. Open main.cpp.

```cpp
#include <Windows.h>
#include <char.h>
#include "MyForm.h"

using namespace System::Windows::Forms;
using namespace System::Threading;
using namespace CLRAApplication3;

[STAThreadAttribute]
int _WinMain(HINSTANCE hThis, INSTANCE hPrev, LPTSTR commandLine, int iCmdShow)
{
    Application::EnableVisualStyles();
    Application::EnableCompatibleTextRenderingDefault(false);

    Application::Run(gcnew MyForm());

    return 0;
}
```

## 4. Add the following code:

```cpp
#pragma once

#include <Windows.h>
#pragma comment ( lib, "User32.lib" )
#define END_TASK WM_USER + 1

namespace CLRApplication3
{
    using namespace System;
    using namespace System::Windows::Forms;
    using namespace System::Drawing;
    using namespace System::Threading::Tasks;

    public ref class MyForm : public Form
    {
        public:
        MyForm(void) : bContinue(true)
        {
            InitializeComponent();
            this->Load += gcnew System::EventHandler(this,
            &MyForm::Form::OnLoad);
        }
        protected:
        ~MyForm()
        {
            if (components)
            {
                delete components;
            }
        }

        virtual void WndProc(Message& msg) override
        {
            switch (msg.Msg)
            {
                case END_TASK:
                    System::Windows::Forms::DialogResult* dlgResult =
                    MessageBox::Show(L"Do you want to calculate again?", L"Question",
                    MessageBoxButtons::YesNo, MessageBox::Question);
                    if (*dlgResult ==
                        System::Windows::Forms::DialogResult::Yes)
                    {
                        // logic to continue
                    }
                    else
                    {
                        PostMessage((HWND)this->Handle.ToPointer(), WM_CLOSE, 0, 0);
                        break;
                    }
                    break;
            }
            Form::WndProc(msg);
        }
    private:
        System::ComponentModel::Container^ components;
        Label* label;
        ProgressBar* progress;
        static const int N = 25;
        bool bContinue;

        System::Void Form_Load(System::Object^ sender,
        System::EventArgs^ e)
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

            Task^ task = gcnew Task(gcnew Action<Object^>
            (&MyForm::StartAddress), this);
            task->Start();
        }

        static ::Void StartAddress(Object^ parameter)
        {
            MyForm^ form = (MyForm*)parameter;

            GetFormHandleDelegate^ getHandle = gcnew
            GetFormHandleDelegate(form, &MyForm::GetFormHandle);
            IntPtr handle = (IntPtr)form->Invoke(getHandle);

            UpdateProgressBarDelegate^ action = gcnew
            UpdateProgressBarDelegate(form, &MyForm::UpdateProgressBar);
            UpdateLabelTextDelegate^ textArea = gcnew
            UpdateLabelTextDelegate(form, &MyForm::UpdateLabelText);

            Int64 iResult = 1;
            while (true)
            {
                if (!form->bContinue)
                {
                    System::Threading::Thread::Sleep(1000);
                    continue;
                }

                for (int iIndex = 1; iIndex <= MyForm::N; iIndex++)
                {
                    iResult *= iIndex;
                    form->BeginInvoke(action);
                    System::Threading::Thread::Sleep(100);
                }

                form->BeginInvoke(textArea, L"Result: " +
                Convert::ToString(iResult));
            }
        }
    }
};
```
