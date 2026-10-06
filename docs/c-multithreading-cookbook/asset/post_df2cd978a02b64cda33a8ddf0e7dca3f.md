
## Threads in the .NET Framework

```cpp
}
  virtual void SetWait(void)
{
    Lock* lock = gcnew Lock(synHandle);
    Monitor::Wait(synHandle);
    delete lock;
}
  virtual void SetPulse(void)
{
    Lock* lock = gcnew Lock(synHandle);
    Monitor::Pulse(synHandle);
    delete lock;
}
```

private:
  System::ComponentModel::Container *components;
  Label* label;
  ProgressBar* progress;
  static unsigned N = 25;
  initially Object* synHandle;

```cpp
System::Void Form_OnLoad(Object^ sender, EventArgs^ e)
{
    InitializeApp();
}
```

```cpp
delegate void TaskCompletedDelegate(UInt64 uResult)
void TaskCompleted(UInt64 uResult)
{
    label->AutoSize = false;
    label->Text = L"Result: " + uResult;
    label->AutoSize = true;
}
```

```cpp
System::Windows::Forms::DialogResult^ dlgResult =
MessageBox::Show(L"Do you want to continue?", L"Question?",
MessageBoxButtons::YesNo, MessageBoxIcon::Question);
```

if (*dlgResult == System::Windows::Forms::DialogResult::Yes)
{
    this->SetPulse();
    progress->Value = 0;
    label->Text = L"Calculating...";
}
else
```

## Chapter 6

```cpp
{
    this->Close();
}
delegateate void UpdateProgressBarDelegate(void);
System::Void UpdateProgressBar(void)
{
    progress->PerformStep();
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
}
this->Controls->Add(label);
this->Controls->Add(progress);
Task* task = gcnew Task(gcnew Action<Object^>
(&MyForm::StartAddress, gcnew array<Object^>(2))
{ this, task });
task->Start();

static System::Void* StartAddress(Object** parameters = (array<Object^>*)parameters);
MyForm* form = (MyForm*)parameters[0];
Task* task = (Task*)parameters[1];

TaskCompletedDelegate taskCompleted = gcnew
TaskCompletedDelegate(form, &MyForm::TaskCompleted);
UpdateProgressBarDelegate updateProgressBar = gcnew
UpdateProgressBarDelegate(form, &MyForm::UpdateProgressBar);
UInt64 uResult = 1;
```

```cpp
while (true)
{
    uResult = 1;

    for (unsigned uIndex = 1; uIndex <= MyForm::uIndex++)
    {
        uResult *= uIndex;
        form->progress->BeginInvoke(updateProgressBar);
    }
    Thread::Sleep(100);
}

form->BeginInvoke(taskCompleted, uResult);

form->SetWait();
```

```cpp
#pragma region Windows Form Designer generated code
/// <summary>
/// Required method for Designer
/// support - do not modify
/// the contents of this method with the code editor.
/// </summary>
void InitializeComponent(void)
{
    this->SuspendLayout();
    this->AutoScaleDimensions = System::Drawing::SizeF(6, 13);
    this->AutoScaleMode = System::Windows::Forms::AutoScaleMode::Font;
    this->Size = System::Drawing::Size(284, 300);
    this->MaximizeBox = false;
    this->MinimizeBox = false;
    this->Name = L"MyForm";
    this->Text = L"MyForm";
    this->ResumeLayout(false);
}
#pragma endregion
```

## How it works...

Implementation of the Lock class remains the same, while the MyForm class introduces new methods: SetWait and SetPulse. These methods are declared protected in order to allow other programmers who may create a derivation from the MyForm class to expand its behavior. As we said before, a programmer must enclose the Wait and Pulse statements with locks. At a private scope, the MyForm class with the itHandle attribute. This attribute will be used as a synchronization object for the Monitor methods. The catch is that we've used the Control::BeginInvoke to asynchronously invoke the TaskCompleted routine. This is required for the following reason: if we had invoked (synchronously) the TaskCompleted method from the working thread, we would need to create delegates for all statements inside TaskCompleted that manipulates the UI created by the main thread. This would cause a exception by invoking TaskCompleted asynchronously, we are avoiding all coding and giving control to the main thread. In order to wait until the user provides an answer for task continuation, we will use the Monitor::Wait. The working thread then enters a suspended state, and no processor time is spent. So, the control has been given to the main thread; now it is to ask the user whether they want to continue; if the answer is "Yes", then we will call Monitor::Pulse in order to change the working thread's state to signaled. In this way, the working thread can continue execution and repeat the process.

## There's more...

Monitor::Wait and Pulse, in combination with locks. Our following example will calculate a mathematical formula, and plot its graph in order to show.

## Getting ready

Make sure Visual Studio is up and running.

## How to do it...

Now, let's create our program and explain its structure. Perform the following steps:

- 1. Create a new C++ CLR empty project named CLRBarrier.
- 2. Open Solution Explorer and right-click on Source file. Add a new source file named main. Open main.cpp. Copy and paste the following code:
- 3. Open Solution Explorer and right-click on Header file. Under Visual C++, select UI. Add a new Windows Form named MyForm. Open MyForm.h.
- 4. Adding the following code:

## Threads in the .NET Framework

![](img/4125b36adcce2d.png)

The Barrier class provides synchronization. The Barrier class returns the number of tasks. The Barrier class is enabled. The Barrier class is passed as argument.
