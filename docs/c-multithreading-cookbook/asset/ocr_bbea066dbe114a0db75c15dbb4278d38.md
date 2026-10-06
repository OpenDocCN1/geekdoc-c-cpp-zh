# Chapter 6

```
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
\    progress = gcnew ProgressBar();
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

297