# Chapter 6

3. Open Solution Explorer and right-click on Header file. Under Visual C++, select UI.
Add a new Windows Form named MyForm. Open MyForm.h.

4. Add the following code:

```
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
        -Lock() {
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
};
```

![](bbox=[0.765, 0.836, 0.811, 0.853])