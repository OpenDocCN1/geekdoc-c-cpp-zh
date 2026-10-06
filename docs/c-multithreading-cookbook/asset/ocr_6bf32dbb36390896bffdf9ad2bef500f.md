```
progress->Value = 0;
this->Controls->Add(label);
this->Controls->Add(progress);

Task^ task = gcnew Task(gcnew Action<Object^>
(&MyForm::StartAddress), this);
task->Start();
```

```
static ::Void StartAddress(Object^ parameter)
MyForm^ form = (MyForm*)delegate;

GetFormHandleDelegate^ getHandle = gcnew
GetFormHandleDelegate(form, &MyForm::GetFormHandle);
IntPtr handle = (IntPtr)form->invoke(getHandle);
```

```
UpdateProgressBarDelegate^ action = gcnew
UpdateProgressBarDelegate(form, &MyForm::UpdateProgressBar);
UpdateLabelTextDelegate^ textArea = gcnew
UpdateLabelTextDelegate(form, &MyForm::UpdateLabelText);
```

```
Int64 iResult = 1;
while (true)
{
    if (!form->bContinue)
    {
        System::Threading::Thread::Sleep(1000);
        continue;
    }
```

```
iResult *= 1;
for (int iIndex = 1; iIndex <= MyForm::N; iIndex++)
{
    iResult *= iIndex;
    form->BeginInvoke(action);
```

```
System::Threading::Thread::Sleep(100);
```