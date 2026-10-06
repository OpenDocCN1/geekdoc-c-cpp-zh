Application::SetCompatibleTextRenderingDefault(false);
Application::Run(gcnew MyForm());
return 0;


+   1. Open Solution Explorer and right-click on Header file. Under Visual C++, select UI.
Add a new Windows Form named MyForm. Open MyForm.h.

+   2. Add the following code:

```
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