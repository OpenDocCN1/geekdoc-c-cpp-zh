```
void InitializeComponent (void)
{
    this->groupBox = (gcnew
    System::Windows::Forms::GroupBox());
    this->status = (gcnew
    System::Windows::Forms::Label());
    this->progress = (gcnew
    System::Windows::Forms::ProgressBar());
    this->btnStart = (gcnew
    System::Windows::Forms::Button());
    this->canvas = (gcnew
    System::Windows::Forms::PictureBox());
    this->groupBox->SuspendLayout();
    (cli::System::ComponentModel::ISupportInitialize*)this->canvas)->BeginInit();
    this->ResumeLayout();
    /
    // groupBox
    /
    this->groupBox->Controls->Add(this->status);
    this->groupBox->Controls->Add(this->progress);
    this->groupBox->Controls->Add(this->btnStart);
    this->groupBox->Location =
    System::Drawing::Point(9, 615);
    this->groupBox->Name = "L"groupBox";
    this->groupBox->Size =
    System::Drawing::Size(800, 59);
    this->groupBox->TabIndex = 0;
    this->groupBox->TabStop = false;
    /
    // status
    this->status->Location =
    System::Drawing::Point(13, 20);
    this->status->Name = "L"status";
    this->status->Size =
    System::Drawing::Size(270, 27);
    this->status->TabIndex = 2;
    this->status->TextAlign =
    System::Drawing::ContentAlignment::MiddleLeft;
    /
    // progress
```