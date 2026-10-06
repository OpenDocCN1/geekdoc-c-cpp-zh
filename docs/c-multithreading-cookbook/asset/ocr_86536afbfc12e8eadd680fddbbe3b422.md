```
static const int N = 25;

System::Void Form_OnLoad(System::Object^ sender,
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
BackgroundWorker^ bckWorker = gcnew BackgroundWorker();
bckWorker->WorkerReportsProgress = true;
bckWorker->ProgressChanged +=
    gcnew ProgressChangedEventHandler(this,
    MyForm::ProgressChanged);\nbckWorker->WorkerCompleted +=
    gcnew WorkerCompletedEventHandler(this,
    MyForm::Running());
bckWorker->DoWork += gcnew DoWorkEventHandler(this,
    MyForm::StartAddress);
bckWorker->RunAsync(bckWorker);
}

System::Void StartAddress(Object^ sender, DoWorkEventArgs^ e)
{
    BackgroundWorker^ bckWorker = (BackgroundWorker^)
    e->Argument;
    Int64 iResult = 1;
    for (int iIndex = 1; iIndex <= MyForm::N; iIndex++)

```